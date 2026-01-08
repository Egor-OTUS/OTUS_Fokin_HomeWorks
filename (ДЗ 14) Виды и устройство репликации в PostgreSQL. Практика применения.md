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
<img width="564" height="39" alt="image" src="https://github.com/user-attachments/assets/8cdef236-0934-42cd-b9cc-c91ca7ee9e33" />  

После чего перезапускаем кластер на каждой ВМ для применения измений

***На 1 ВМ создаем таблицы test для записи, test2 для запросов на чтение.***  
Создаем БД homework и таблицы test и test2 на ВМ 1  
<img width="518" height="278" alt="image" src="https://github.com/user-attachments/assets/c9713678-bcd5-40fe-a949-e0e96d9ee8fa" />






***Создаем публикацию таблицы test и подписываемся на публикацию таблицы test2 с ВМ №2.***  
Создаем публикацию  


Проверяем публикацию  


Подписываемся на публикацию ВМ2

Проверяем статус подписки


***На 2 ВМ создаем таблицы test2 для записи, test для запросов на чтение.***  
Создаем БД homework и таблицы test и test2 на ВМ 2  
<img width="514" height="355" alt="image" src="https://github.com/user-attachments/assets/ec60fd9c-3e0e-40fd-9613-d1f8591a5ccf" />



***Создаем публикацию таблицы test2 и подписываемся на публикацию таблицы test1 с ВМ №1.***  
Создаем публикацию  


Проверяем публикацию  


Подписываемся на публикацию ВМ 1


Проверяем статус подписки



***3 ВМ использовать как реплику для чтения и бэкапов (подписаться на таблицы из ВМ №1 и №2 ).***  
Создаем БД homework и таблицы test и test2 на ВМ 3  
<img width="855" height="502" alt="image" src="https://github.com/user-attachments/assets/57f89112-fc86-4812-b25c-d9a802325c92" />

Подписываемся

Проверяем подписки

Проверяем видны ли данные с таблиц

