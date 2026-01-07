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

***настроить кластер PostgreSQL 15 на максимальную производительность не обращая внимание на возможные проблемы с надежностью в случае аварийной перезагрузки виртуальной машины***  


***нагрузить кластер через утилиту через утилиту pgbench (https://postgrespro.ru/docs/postgrespro/14/pgbench)***  

Иницилизируем БД homework чтобы можно было в дальнейшем её нагрузить  
pgbench -i -U postgres homework  
<img width="982" height="179" alt="image" src="https://github.com/user-attachments/assets/6bd3d2b0-2ab8-47d9-88d7-11ae26aef9d4" />

Нагрузка будет осуществеляться с помощью команды pgbench -c 50 -j 2 -P 10 -T 60 homework  
Нагрузка с базовыми параметрами
<img width="847" height="387" alt="image" src="https://github.com/user-attachments/assets/d520f06b-721f-48b4-b5ae-ab42e45431e1" />

***написать какого значения tps удалось достичь, показать какие параметры в какие значения устанавливали и почему***  
Привет
