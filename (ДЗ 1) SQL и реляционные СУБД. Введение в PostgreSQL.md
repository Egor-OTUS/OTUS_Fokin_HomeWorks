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
<img width="994" height="904" alt="image" src="https://github.com/user-attachments/assets/adb2ae36-b787-4d67-8032-1d723d3e9f42" />  
Проверяем работоспособность кластера  
<img width="1139" height="350" alt="image" src="https://github.com/user-attachments/assets/740d0e4e-0e59-49ea-9fe4-7ceaafe477da" />  

***зайти вторым ssh (вторая сессия)***  
**запустить везде psql из под пользователя postgres**  
**выключить auto commit**  
<img width="358" height="128" alt="image" src="https://github.com/user-attachments/assets/9b53aced-ba47-4b9a-814b-e7f127f634b5" />


***сделать в первой сессии новую таблицу и наполнить ее данными create table persons(id serial, first_name text, second_name text); insert into persons(first_name, second_name) values('ivan', 'ivanov'); insert into persons(first_name, second_name) values('petr', 'petrov'); commit;***    
<img width="682" height="228" alt="image" src="https://github.com/user-attachments/assets/98a08a45-7f6e-4430-82af-7ae11133a13a" />

***посмотреть текущий уровень изоляции: show transaction isolation level***  
<img width="370" height="93" alt="image" src="https://github.com/user-attachments/assets/3ff60cab-4437-49ef-bf1c-b5f3053eda3a" />

***начать новую транзакцию в обоих сессиях с дефолтным (не меняя) уровнем изоляции***  
<img width="359" height="71" alt="image" src="https://github.com/user-attachments/assets/0240ecef-df9b-4633-a013-d4f9dfd7202e" />

***в первой сессии добавить новую запись insert into persons(first_name, second_name) values('sergey', 'sergeev');***  
<img width="713" height="54" alt="image" src="https://github.com/user-attachments/assets/ead6fb98-592a-4851-ae32-6ccd88719b11" />

***сделать select from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**  
Новых записей не видно т.к. в первой транзакции мы ещё не завершили commit, а в READ COMMITTED вторая транзакция видит только зафиксированные данные
<img width="336" height="134" alt="image" src="https://github.com/user-attachments/assets/58c506aa-bfc0-4a50-b54a-31ecc901edba" />

**завершить первую транзакцию - commit;**    
<img width="724" height="84" alt="image" src="https://github.com/user-attachments/assets/347f1235-61af-4785-abcc-1b84548e53df" />

***сделать select from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**     
Теперь записи видны поскольку мы совершили COMMIT в первой транзакции  
<img width="397" height="264" alt="image" src="https://github.com/user-attachments/assets/a8d78df2-8b11-4f25-aa34-0960ba9b97b7" />

**завершите транзакцию во второй сессии**    
<img width="341" height="187" alt="image" src="https://github.com/user-attachments/assets/233d8837-d0cf-43e3-9e44-7d8ebb53bc86" />

***начать новые но уже repeatable read транзации - set transaction isolation level repeatable read;***  
<img width="400" height="51" alt="image" src="https://github.com/user-attachments/assets/a8ff97ec-a8b6-4b3d-b11a-a56e54fea208" />

***в первой сессии добавить новую запись insert into persons(first_name, second_name) values('sveta', 'svetova');***  
<img width="701" height="62" alt="image" src="https://github.com/user-attachments/assets/c72f5613-1efe-4203-84e2-05090fdc6e0f" />

***сделать select* from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**   
Не видно новую запись, т.к В REPEATABLE READ транзакция запоминает снимок данных на момент начала. Новые записи, добавленные другими транзакциями, не видны до перезапуска транзакции.  
<img width="404" height="201" alt="image" src="https://github.com/user-attachments/assets/c6046af6-ce49-492a-abed-e5410bdfb28d" />

**завершить первую транзакцию - commit;**  
<img width="755" height="97" alt="image" src="https://github.com/user-attachments/assets/6ae5f8a8-33a9-4c92-9fc1-5519c5ed492f" />

***сделать select from persons во второй сессии***   
**видите ли вы новую запись и если да то почему?**    
Все ещё нет, т.к В REPEATABLE READ транзакция запоминает снимок данных на момент начала. Новые записи, добавленные другими транзакциями, не видны до перезапуска транзакции.  
<img width="399" height="172" alt="image" src="https://github.com/user-attachments/assets/0cdfd50f-dac9-465e-b2f7-e61e669673c5" />

**завершить вторую транзакцию**  
<img width="342" height="201" alt="image" src="https://github.com/user-attachments/assets/c3fd87ce-18fd-4e50-811a-ea7c40b69421" />

***сделать select * from persons во второй сессии***  
**видите ли вы новую запись и если да то почему?**   
Теперь видно т.к. мы перезапустили транзакцию
<img width="367" height="183" alt="image" src="https://github.com/user-attachments/assets/21525fdb-48c3-47b5-8566-dabc9abcc6b7" />
