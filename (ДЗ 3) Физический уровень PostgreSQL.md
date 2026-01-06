***создайте виртуальную машину c Ubuntu 20.04/22.04 LTS в ЯО/Virtual Box/докере***     
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


***поставьте на нее PostgreSQL 15 через sudo apt*** 
Устанавливается версия PostgreSQL 17 через apt т.к. она новее
<img width="982" height="223" alt="image" src="https://github.com/user-attachments/assets/4a9310ea-deda-476b-9403-d74b81677ce8" />

***проверьте что кластер запущен через sudo -u postgres pg_lsclusters***    
<img width="858" height="69" alt="image" src="https://github.com/user-attachments/assets/474bbaed-91ad-4289-9fb4-3774b7c6e061" />

***зайдите из под пользователя postgres в psql и сделайте произвольную таблицу с произвольным содержимым***  
<img width="444" height="197" alt="image" src="https://github.com/user-attachments/assets/f13b9705-2352-4203-92cd-1e332200e473" />

***остановите postgres например через sudo -u postgres pg_ctlcluster 15 main stop***  
<img width="968" height="185" alt="image" src="https://github.com/user-attachments/assets/a4fd2e51-c01d-4e6d-81d9-fcc2d4255147" />

***создайте новый диск к ВМ размером 10GB,добавьте свеже-созданный диск к виртуальной машине - надо зайти в режим ее редактирования и дальше выбрать пункт attach existing disk***  
<img width="887" height="361" alt="image" src="https://github.com/user-attachments/assets/11409546-e8a5-47be-a80e-239d6899f841" />

***проинициализируйте диск согласно инструкции и подмонтировать файловую систему, только не забывайте менять имя диска на актуальное, в вашем случае это скорее всего будет /dev/sdb - https://www.digitalocean.com/community/tutorials/how-to-partition-and-format-storage-devices-in-linux***  
Сайт не прогружается, поэтому опишу как делал я  
После добавление диска находим его с помощью команды lsblk, узнаю его название, а именно /dev/sdb  
Теперь нужно создать новый раздел с помощью команды fdisk /dev/sdb, создаю раздел /dev/sdb1    
После чего можем создать файловую систему с помощью mkfs.ext4 /dev/sdb1    
Получаем следующее  
<img width="586" height="261" alt="image" src="https://github.com/user-attachments/assets/a440d4c9-11cf-4072-9f53-633537c3c9b7" />  

Осталось создать точку монтирования для диска и добавить запись в fstab чтобы диск был примонтирован даже после перезагрузки машины   
Создаем каталог для монтирования mkdir /mnt/new_disk  
Узнаем UUID диска blkid /dev/sdb1  
Добавляем запись в /etc/fstab по самому последнему примеру  
<img width="909" height="273" alt="image" src="https://github.com/user-attachments/assets/4d341de0-6f20-4caf-b0b5-53ae97484e92" />  
По итогу получаем диск готовый к работе


***перезагрузите инстанс и убедитесь, что диск остается примонтированным (если не так смотрим в сторону fstab)***  
Диск примонтирован корректно  
<img width="413" height="72" alt="image" src="https://github.com/user-attachments/assets/a46b6eab-d4d3-4db7-a8b4-885d22668528" />

***сделайте пользователя postgres владельцем /mnt/data - chown -R postgres:postgres /mnt/data/***  
<img width="542" height="147" alt="image" src="https://github.com/user-attachments/assets/7299ca3a-b133-41eb-83d2-8fbd079d3a00" />

***перенесите содержимое /var/lib/postgres/15 в /mnt/data - mv /var/lib/postgresql/15/mnt/data***  
<img width="519" height="68" alt="image" src="https://github.com/user-attachments/assets/6ca3f518-735b-4005-ba95-b5b1d84dd49a" />

***попытайтесь запустить кластер - sudo -u postgres pg_ctlcluster 15 main start***  
**напишите получилось или нет и почему**   
Не получилось поскольку пытается запуститься по пути /var/lib/postgresql/17/main, а там уже ничего нет
<img width="583" height="52" alt="image" src="https://github.com/user-attachments/assets/04e7bd2e-faa3-4607-9d23-67c9c14523b1" />


***задание: найти конфигурационный параметр в файлах раположенных в /etc/postgresql/15/main который надо поменять и поменяйте его***  
**напишите что и почему поменяли** 
Необходимо изменить значение параметра data_directory в postgresql.conf на тот путь, куда мы переместили содержимое 
<img width="725" height="130" alt="image" src="https://github.com/user-attachments/assets/752e6435-7acd-417f-ba65-2dec7831b91c" />


***попытайтесь запустить кластер - sudo -u postgres pg_ctlcluster 15 main start***  
**напишите получилось или нет и почему**    
Получилось т.к. мы изменили путь data_directory в postgresql.conf    
<img width="733" height="68" alt="image" src="https://github.com/user-attachments/assets/50d9d84c-48d7-4a5d-a371-e6fc02877c44" />

***зайдите через через psql и проверьте содержимое ранее созданной таблицы***  
Данные остались на месте  
<img width="286" height="138" alt="image" src="https://github.com/user-attachments/assets/8ee71fe2-12bc-4a0d-b6c3-2a4cccbf1c26" />
<img width="286" height="138" alt="image" src="https://github.com/user-attachments/assets/8ee71fe2-12bc-4a0d-b6c3-2a4cccbf1c26" />

