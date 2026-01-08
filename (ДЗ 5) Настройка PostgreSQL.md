***развернуть виртуальную машину любым удобным способом***  
*Стек*  
Virtual Box 7.2.4  
https://www.virtualbox.org/wiki/Downloads   
Ubuntu Server 25.10
https://ubuntu.com/download/server#release-notes-tab-lts 

Характеристики ВМ  
RAM: 16GB  
<img width="1632" height="334" alt="image" src="https://github.com/user-attachments/assets/e485eeb4-da53-4134-bec6-a7bde0645535" />
CPU: 8 cores
<img width="1629" height="347" alt="image" src="https://github.com/user-attachments/assets/553764b0-4c85-4a0b-ad24-78a814b8084d" />
VDI(SSD): 200GB
<img width="894" height="443" alt="image" src="https://github.com/user-attachments/assets/c0380803-eb86-4e0d-9a75-bc93e9fc2207" />

БД homework  (размер после инициализации БД с помощью pgbench)    
<img width="1537" height="54" alt="image" src="https://github.com/user-attachments/assets/c9e3d4ff-000b-4b03-9ed8-0e09c9ac5c1e" />

***поставить на неё PostgreSQL 15 любым способом***  
Использоваться будет PostgreSQL 17, т.к. версия новее и говорили, что можно её использовать  
<img width="858" height="69" alt="image" src="https://github.com/user-attachments/assets/474bbaed-91ad-4289-9fb4-3774b7c6e061" />

***нагрузить кластер через утилиту через утилиту pgbench (https://postgrespro.ru/docs/postgrespro/14/pgbench)***  

Иницилизируем БД homework чтобы можно было в дальнейшем её нагрузить  
pgbench -i -U postgres homework  
<img width="982" height="179" alt="image" src="https://github.com/user-attachments/assets/6bd3d2b0-2ab8-47d9-88d7-11ae26aef9d4" />

Нагружаем с помощью команды pgbench -c 50 -j 2 -P 10 -T 60 homework  
Нагрузка с базовыми параметрами tps = 1496  
<img width="555" height="356" alt="image" src="https://github.com/user-attachments/assets/28762241-7472-4873-9323-1179a2e98415" />

Нагрузка с измененными параметрами tps = 5443  
<img width="552" height="374" alt="image" src="https://github.com/user-attachments/assets/194596bc-99fe-4c13-96a2-3b870760329f" />

***настроить кластер PostgreSQL 15 на максимальную производительность не обращая внимание на возможные проблемы с надежностью в случае аварийной перезагрузки виртуальной машины***   
***написать какого значения tps удалось достичь, показать какие параметры в какие значения устанавливали и почему***

Нагрузка с базовыми параметрами tps = 1496   
Нагрузка с измененными параметрами  tps = 5443  
Производительность улучшилась в 3.6 раза  

**Параметры**  
**Отключаем гарантии записи на диск**   
synchronous_commit = off           # Параметр отвечает за запись на диск  
full_page_writes = off             # Параметр отвечает за запись на диск  
fsync = off                        # Параметр отвечает за запись на диск  

**Увеличиваем буферы и кэши**  
shared_buffers = 16GB              # 100% от RAM  
work_mem = 256MB                   # Значительно увеличаем, должно повысить производительность, но нет смысла ставить больше т.к. БД homework пустая  
maintenance_work_mem = 2GB         # Значительно увеличаем, должно повысить производительность, но нет смысла ставить больше т.к. БД homework пустая  
effective_cache_size = 16GB        # 100% от RAM  

**Настройки WAL**  
checkpoint_timeout = 1d            # реже чекпоинты - меньше нагрузка, данный параметр максимальный    
checkpoint_completion_target = 1.0 # реже чекпоинты - меньше нагрузка, данный параметр максимальный  
max_wal_size = 50GB                # Значительно увеличаем, должно повысить производительность, но нет смысла ставить больше т.к. БД homework пустая    
min_wal_size = 8GB                 # Значительно увеличаем, должно повысить производительность, но нет смысла ставить больше т.к. БД homework пустая    

**Оптимизация размеров страниц**    
random_page_cost = 1.1             # Стоит уменьшить размер параметра, т.к. диск на SSD - он будет и так быстро передавать страницы  

*Подробное описание каждого параметра есть в открытом доступе, информации много, добавлю информацию если потребуется*
