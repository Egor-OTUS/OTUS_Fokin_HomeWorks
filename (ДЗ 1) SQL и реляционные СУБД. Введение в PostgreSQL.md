***создать новый проект в Яндекс облако или на любых ВМ, докере***  
*Стек*  
Virtual Box 7.2.4  
https://www.virtualbox.org/wiki/Downloads   
Ubuntu Server 25.10, т.к. версия новее требующейся  
https://ubuntu.com/download/server#release-notes-tab-lts 

Характеристики ВМ  
RAM: 16GB  
<img width="1632" height="334" alt="image" src="https://github.com/user-attachments/assets/e485eeb4-da53-4134-bec6-a7bde0645535" />
CPU: 8 cores
<img width="1629" height="347" alt="image" src="https://github.com/user-attachments/assets/553764b0-4c85-4a0b-ad24-78a814b8084d" />
VDI(SSD): 200GB
<img width="894" height="443" alt="image" src="https://github.com/user-attachments/assets/c0380803-eb86-4e0d-9a75-bc93e9fc2207" />

***далее создать инстанс виртуальной машины с дефолтными параметрами***  
<img width="699" height="504" alt="image" src="https://github.com/user-attachments/assets/cd636082-89e2-4c14-a0c8-acc64ee452b3" />

***добавить свой ssh ключ в metadata ВМ***  
Генерирурем открытый ключ на своей машине  
<img width="533" height="294" alt="image" src="https://github.com/user-attachments/assets/f474fc70-984a-40d0-b8f5-7780c8af96e2" />  
Копируем ключ на ВМ  
<img width="818" height="56" alt="image" src="https://github.com/user-attachments/assets/34d8b0ad-e51d-4cae-affe-151673e90f80" />  
Перекидываем в /.ssh/authorized.keys и проверяем содержимое файла  
<img width="998" height="128" alt="image" src="https://github.com/user-attachments/assets/0ff33404-fba8-4128-b2ef-598815825784" />

***зайти удаленным ssh (первая сессия), не забывайте про ssh-add, поставить PostgreSQL***    
Привет

***зайти вторым ssh (вторая сессия)***
**запустить везде psql из под пользователя postgres**
**выключить auto commit**  
Привет

***сделать в первой сессии новую таблицу и наполнить ее данными create table persons(id serial, first_name text, second_name text); insert into persons(first_name, second_name) values('ivan', 'ivanov'); insert into persons(first_name, second_name) values('petr', 'petrov'); commit;***  
Привет

***посмотреть текущий уровень изоляции: show transaction isolation level***  
Привет

***начать новую транзакцию в обоих сессиях с дефолтным (не меняя) уровнем изоляции***  
Привет

***в первой сессии добавить новую запись insert into persons(first_name, second_name) values('sergey', 'sergeev');***  
Привет

***сделать select from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**
**завершить первую транзакцию - commit;**  
Привет

***сделать select from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**    
**завершите транзакцию во второй сессии**   
Привет

***начать новые но уже repeatable read транзации - set transaction isolation level repeatable read;***  
Привет

***в первой сессии добавить новую запись insert into persons(first_name, second_name) values('sveta', 'svetova');***  
Привет

***сделать select* from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**  
**завершить первую транзакцию - commit;**  
Привет

***сделать select from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**  
**завершить вторую транзакцию**  
Привет

***сделать select * from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**  
Привет
