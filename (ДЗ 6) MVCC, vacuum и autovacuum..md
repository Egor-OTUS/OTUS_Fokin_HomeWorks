***Создать инстанс ВМ с 2 ядрами и 4 Гб ОЗУ и SSD 10GB***  
Virtual Box 7.2.4   
Ubuntu Server 25.10  
<img width="546" height="61" alt="image" src="https://github.com/user-attachments/assets/8ec159a2-e973-43ef-bbd3-b9ab9586e53d" />  
<img width="613" height="117" alt="image" src="https://github.com/user-attachments/assets/31f956c5-0fa9-40d8-bce0-c3efe913f3dd" /> 
<img width="631" height="286" alt="image" src="https://github.com/user-attachments/assets/34c0e431-99cc-4b19-a4be-dca119c528b5" />

***Установить на него PostgreSQL 15 с дефолтными настройками***  
Устанавливается будет PostgreSQL 17, т.к. версия новее и говорили, что можно работать с ней  
<img width="829" height="36" alt="image" src="https://github.com/user-attachments/assets/2302f397-02fa-4c49-a4dd-8b9cb1b90a17" />

***Создать БД для тестов: выполнить pgbench -i postgres***  
<img width="560" height="179" alt="image" src="https://github.com/user-attachments/assets/76e657d6-0139-44f7-9647-bd96a451f539" />


***Запустить pgbench -c8 -P 6 -T 60 -U postgres postgres***  
<img width="583" height="419" alt="image" src="https://github.com/user-attachments/assets/cd4914fc-2e2d-41dd-b6be-0353f5c8dff6" />

***Применить параметры настройки PostgreSQL из прикрепленного к материалам занятия файла***  
**Протестировать заново  
Что изменилось и почему?**  
Добавляем параметры в /etc/postgresql/17/main/postgresql.conf и перезапускаем кластер  
<img width="443" height="343" alt="image" src="https://github.com/user-attachments/assets/08617c6c-95b5-4496-aa43-7c5d62aeb514" />

Увеличилось кол-во транзакций в секунду (tps) и также снизилась средняя задержка  
<img width="582" height="422" alt="image" src="https://github.com/user-attachments/assets/241a9377-b164-474a-8c37-af133841ae8e" />

Транзакции увеличили благодаря shared_buffers, effective_cache_size, max_wal_size     
Задержку снизили благодаря work_mem   

Разница в результате не слишком заметна т.к. у нас достаточно слабая ВМ

***Создать таблицу с текстовым полем и заполнить случайными или сгенерированными данным в размере 1млн строк***  
<img width="494" height="337" alt="image" src="https://github.com/user-attachments/assets/afde1278-e5bf-46a5-b7a7-9d5e1d10188d" />

***Посмотреть размер файла с таблицей***  
<img width="546" height="81" alt="image" src="https://github.com/user-attachments/assets/ca64f202-66e8-46b7-a6a1-7faf3b2a7854" />  

***5 раз обновить все строчки и добавить к каждой строчке любой символ***   
<img width="408" height="163" alt="image" src="https://github.com/user-attachments/assets/700a7d62-30b9-4faf-b8c3-b24f454f14eb" />  

***Посмотреть количество мертвых строчек в таблице и когда последний раз приходил автовакуум***  
Привет

***Подождать некоторое время, проверяя, пришел ли автовакуум***  
Привет

***5 раз обновить все строчки и добавить к каждой строчке любой символ***  
Привет

***Посмотреть размер файла с таблицей***  
Привет

***Отключить Автовакуум на конкретной таблице***  
Привет

***10 раз обновить все строчки и добавить к каждой строчке любой символ***  
Привет

***Посмотреть размер файла с таблицей***  
**Объясните полученный результат**
**Не забудьте включить автовакуум)**  
Привет

***Задание со *:
Написать анонимную процедуру, в которой в цикле 10 раз обновятся все строчки в искомой таблице.
Не забыть вывести номер шага цикла.***  
Привет
