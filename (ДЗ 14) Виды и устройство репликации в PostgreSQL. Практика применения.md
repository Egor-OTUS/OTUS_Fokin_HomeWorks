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

После чего перезапускаем кластер на каждой ВМ для применения изменений

***На 1 ВМ создаем таблицы test для записи, test2 для запросов на чтение.***  
Создаем БД homework и таблицы test и test2 на ВМ1  
<img width="518" height="278" alt="image" src="https://github.com/user-attachments/assets/c9713678-bcd5-40fe-a949-e0e96d9ee8fa" />

***Создаем публикацию таблицы test и подписываемся на публикацию таблицы test2 с ВМ №2.***  
Создаем публикацию на ВМ1  
<img width="440" height="37" alt="image" src="https://github.com/user-attachments/assets/e827efab-5358-4ba5-84ae-05852e75d656" />

Проверяем публикацию  
<img width="610" height="123" alt="image" src="https://github.com/user-attachments/assets/4a1b7c2c-23f0-4b41-bc03-62939b83a41c" />

Подписываемся на публикацию ВМ2  
<img width="734" height="84" alt="image" src="https://github.com/user-attachments/assets/6eeac057-feb7-4eac-b29f-c53d48d15134" />

Проверяем статус подписки  
<img width="889" height="157" alt="image" src="https://github.com/user-attachments/assets/5e0948bb-48c0-4cd9-bab0-23e274d1c7e5" />

Проверяем появились ли данные в test2  
<img width="260" height="230" alt="image" src="https://github.com/user-attachments/assets/89eac045-de52-4fc6-a5fc-9937d40ae2f8" />



***На 2 ВМ создаем таблицы test2 для записи, test для запросов на чтение.***  
Создаем БД homework и таблицы test и test2 на ВМ2  
<img width="514" height="355" alt="image" src="https://github.com/user-attachments/assets/ec60fd9c-3e0e-40fd-9613-d1f8591a5ccf" />



***Создаем публикацию таблицы test2 и подписываемся на публикацию таблицы test1 с ВМ №1.***  
Создаем публикацию на ВМ2  
<img width="463" height="36" alt="image" src="https://github.com/user-attachments/assets/886f0de6-1074-41d3-922a-b4256e4228f0" />

Проверяем публикацию  
<img width="610" height="119" alt="image" src="https://github.com/user-attachments/assets/25ec8127-5bca-4af2-b98c-ecc00c02dd5e" />


Подписываемся на публикацию ВМ1  
<img width="738" height="81" alt="image" src="https://github.com/user-attachments/assets/44d7a086-7089-4beb-8dbf-0404162c06df" />


Проверяем статус подписки  
<img width="769" height="156" alt="image" src="https://github.com/user-attachments/assets/3b993670-8005-4091-b54e-ac875827d714" />

Проверяем содержимое таблиццы test  
<img width="248" height="239" alt="image" src="https://github.com/user-attachments/assets/101c815e-2fe5-4fe9-b9e6-8780dfa68e02" />

***3 ВМ использовать как реплику для чтения и бэкапов (подписаться на таблицы из ВМ №1 и №2 ).***  
Создаем БД homework и таблицы test и test2 на ВМ 3  
<img width="855" height="502" alt="image" src="https://github.com/user-attachments/assets/57f89112-fc86-4812-b25c-d9a802325c92" />

Подписываемся на ВМ1 и ВМ2  
<img width="667" height="162" alt="image" src="https://github.com/user-attachments/assets/3ee22576-d335-44e7-bfdb-a6285dc18e4b" />

Проверяем подписки     
<img width="915" height="189" alt="image" src="https://github.com/user-attachments/assets/90e27ca0-389b-4718-a689-aa7d8cd9ea0a" />

Проверяем видны ли данные с таблиц  
<img width="255" height="481" alt="image" src="https://github.com/user-attachments/assets/ff49b0d3-6850-4f09-9224-d399570201f8" />

