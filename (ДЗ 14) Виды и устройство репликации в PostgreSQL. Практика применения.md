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
Создаем таблицу на 1 ВМ  
<img width="520" height="127" alt="image" src="https://github.com/user-attachments/assets/3a4f0c10-e73c-4d40-90cb-6054dc5a217d" />




***Создаем публикацию таблицы test и подписываемся на публикацию таблицы test2 с ВМ №2.***  
Создаем публикацию  
<img width="444" height="37" alt="image" src="https://github.com/user-attachments/assets/baa12b87-3efb-48c1-9841-36841d507ed5" />

Проверяем публикацию  
<img width="612" height="115" alt="image" src="https://github.com/user-attachments/assets/76381bac-0f00-406a-a955-0e78f871c94c" />


***На 2 ВМ создаем таблицы test2 для записи, test для запросов на чтение.***  
Создаем таблицу на ВМ 2  



***Создаем публикацию таблицы test2 и подписываемся на публикацию таблицы test1 с ВМ №1.***  
Создаем публикацию  


Проверяем публикацию  



***3 ВМ использовать как реплику для чтения и бэкапов (подписаться на таблицы из ВМ №1 и №2 ).***  
Привет
