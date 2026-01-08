Стек  
Virtual Box 7.2.4  
https://www.virtualbox.org/wiki/Downloads  
Ubuntu Server 25.10  
https://ubuntu.com/download/server#release-notes-tab-lts  
PostgreSQL 17    
Настраиваем NAT чтобы ВМ могли обращаться друг к другу   

Изменяем на всех ВМ параметр wal_level = logical в файле /etc/postgresql/17/main/postgresql.conf     
<img width="603" height="28" alt="image" src="https://github.com/user-attachments/assets/cc6be509-da67-4646-926d-7982269544d7" />

Также меняем параметр listen_addresses = '*' в файле /etc/postgresql/17/main/postgresql.conf  
<img width="559" height="27" alt="image" src="https://github.com/user-attachments/assets/9b861d32-8e54-41e2-8c05-ee3565175f75" />

Также даем на всех ВМ возможность подключаться ко всем БД со всех ip в файле /etc/postgresql/17/main/pg_hba.conf  
<img width="628" height="19" alt="image" src="https://github.com/user-attachments/assets/1996bd07-bece-4b1b-8c85-da25c3dc2bb6" />

После чего перезапускаем кластер на каждой ВМ для применения измений

***На 1 ВМ создаем таблицы test для записи, test2 для запросов на чтение.***  
Создаем таблицу на 1 ВМ  
<img width="343" height="163" alt="image" src="https://github.com/user-attachments/assets/030b8e29-47c4-41b2-b7da-376d9fdda40b" />

***Создаем публикацию таблицы test и подписываемся на публикацию таблицы test2 с ВМ №2.***  
Создаем публикацию  
<img width="438" height="33" alt="image" src="https://github.com/user-attachments/assets/81f46b8d-0d89-45aa-ac1d-00c1871f8775" />

Проверяем публикацию  
<img width="608" height="115" alt="image" src="https://github.com/user-attachments/assets/8c49b7a6-5324-4ef8-ac08-774580f72ccc" />


***На 2 ВМ создаем таблицы test2 для записи, test для запросов на чтение.***  
Создаем таблицу на ВМ 2  
<img width="254" height="99" alt="image" src="https://github.com/user-attachments/assets/beab11a0-ef2c-45ec-ac2b-acab762d2ff0" />


***Создаем публикацию таблицы test2 и подписываемся на публикацию таблицы test1 с ВМ №1.***  
Создаем публикацию  
<img width="452" height="36" alt="image" src="https://github.com/user-attachments/assets/ad5c1e5d-52af-4cdb-a645-ab9ca1215561" />

Проверяем публикацию  
<img width="616" height="121" alt="image" src="https://github.com/user-attachments/assets/de63921d-b9ab-443b-b93e-1a0ecdcc4f50" />


***3 ВМ использовать как реплику для чтения и бэкапов (подписаться на таблицы из ВМ №1 и №2 ).***  
Привет
