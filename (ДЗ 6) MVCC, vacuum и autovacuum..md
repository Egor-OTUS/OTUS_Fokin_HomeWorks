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
<img width="656" height="148" alt="image" src="https://github.com/user-attachments/assets/b7a5c335-53e4-4140-8781-12f4b68c755a" />


***Посмотреть размер файла с таблицей***  
 <img width="534" height="83" alt="image" src="https://github.com/user-attachments/assets/6c2e2161-b752-4315-9aad-db820c0247d3" />


***5 раз обновить все строчки и добавить к каждой строчке любой символ***   
<img width="318" height="160" alt="image" src="https://github.com/user-attachments/assets/4f08d641-93af-4dfc-ba5c-79c87d4afa46" />

***Посмотреть количество мертвых строчек в таблице и когда последний раз приходил автовакуум***  
<img width="464" height="200" alt="image" src="https://github.com/user-attachments/assets/1d10345c-d58c-441c-998a-9d2c7fed9af4" />

***Подождать некоторое время, проверяя, пришел ли автовакуум***  
Не пришел  
<img width="468" height="260" alt="image" src="https://github.com/user-attachments/assets/ed8bfa77-d12c-442d-9fed-e859506d8698" />

Проверяем активен ли автовакуум  
<img width="303" height="116" alt="image" src="https://github.com/user-attachments/assets/9c406301-cb13-44aa-83af-2d90b8f72891" />

***5 раз обновить все строчки и добавить к каждой строчке любой символ***  
<img width="308" height="165" alt="image" src="https://github.com/user-attachments/assets/3bb91d40-dbb2-4deb-b195-a4ba902e6c96" />

***Посмотреть размер файла с таблицей***  
<img width="530" height="80" alt="image" src="https://github.com/user-attachments/assets/2c967b2f-a5f2-48ff-9328-cfdca00f895f" />

<img width="465" height="166" alt="image" src="https://github.com/user-attachments/assets/7d46459c-ee64-4599-8ae1-64d7657c9f79" />


***Отключить Автовакуум на конкретной таблице***  
<img width="484" height="37" alt="image" src="https://github.com/user-attachments/assets/152ade88-0303-4732-a353-1f7caef8632e" />

Убедимся, что автовакуум для таблицы отключен
<img width="525" height="88" alt="image" src="https://github.com/user-attachments/assets/a85c3f16-bad7-4a69-8eca-c84caedd7699" />

***10 раз обновить все строчки и добавить к каждой строчке любой символ***  
<img width="317" height="346" alt="image" src="https://github.com/user-attachments/assets/733de5f5-c764-489b-8fef-628d27543cf4" />


***Посмотреть размер файла с таблицей***  
**Объясните полученный результат**
**Не забудьте включить автовакуум)**  
Размер не изменился, с ним 10 записей занимали 673MB, без него дополнительные 10 занимают 674MB  
Делалось несколько раз все с 0 по порядку, возможно, изменился механизм работы вакуума в PostgreSQL17 или требуется выполение ещё каких-либо условий, из материалов к ДЗ я их не нашёл
<img width="540" height="90" alt="image" src="https://github.com/user-attachments/assets/87c06dcb-6756-4905-a97f-1f0fca1dc9d3" />





