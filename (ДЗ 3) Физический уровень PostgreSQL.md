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
<img width="983" height="225" alt="image" src="https://github.com/user-attachments/assets/c0be7e82-fd61-4095-883f-4cddaafa0fe0" />

***проверьте что кластер запущен через sudo -u postgres pg_lsclusters***    
<img width="858" height="69" alt="image" src="https://github.com/user-attachments/assets/474bbaed-91ad-4289-9fb4-3774b7c6e061" />

***зайдите из под пользователя postgres в psql и сделайте произвольную таблицу с произвольным содержимым***  
<img width="444" height="197" alt="image" src="https://github.com/user-attachments/assets/f13b9705-2352-4203-92cd-1e332200e473" />

***остановите postgres например через sudo -u postgres pg_ctlcluster 15 main stop***  
<img width="968" height="185" alt="image" src="https://github.com/user-attachments/assets/a4fd2e51-c01d-4e6d-81d9-fcc2d4255147" />

***создайте новый диск к ВМ размером 10GB***  
<img width="887" height="361" alt="image" src="https://github.com/user-attachments/assets/11409546-e8a5-47be-a80e-239d6899f841" />

***добавьте свеже-созданный диск к виртуальной машине - надо зайти в режим ее редактирования и дальше выбрать пункт attach existing disk***  
Привет

***проинициализируйте диск согласно инструкции и подмонтировать файловую систему, только не забывайте менять имя диска на актуальное, в вашем случае это скорее всего будет /dev/sdb - https://www.digitalocean.com/community/tutorials/how-to-partition-and-format-storage-devices-in-linux***  
Привет

***перезагрузите инстанс и убедитесь, что диск остается примонтированным (если не так смотрим в сторону fstab)***  
Привет

***сделайте пользователя postgres владельцем /mnt/data - chown -R postgres:postgres /mnt/data/***  
Привет

***перенесите содержимое /var/lib/postgres/15 в /mnt/data - mv /var/lib/postgresql/15/mnt/data***  
Привет

***попытайтесь запустить кластер - sudo -u postgres pg_ctlcluster 15 main start***  
**напишите получилось или нет и почему**  
Привет

***задание: найти конфигурационный параметр в файлах раположенных в /etc/postgresql/15/main который надо поменять и поменяйте его***  
**напишите что и почему поменяли**   
Привет

***попытайтесь запустить кластер - sudo -u postgres pg_ctlcluster 15 main start***  
**напишите получилось или нет и почему**  
Привет

***зайдите через через psql и проверьте содержимое ранее созданной таблицы***  
Привет

***задание со звездочкой *: не удаляя существующий инстанс ВМ сделайте новый, поставьте на его PostgreSQL, удалите файлы с данными из /var/lib/postgres, перемонтируйте внешний диск который сделали ранее от первой виртуальной машины ко второй и запустите PostgreSQL на второй машине так чтобы он работал с данными на внешнем диске, расскажите как вы это сделали и что в итоге получилось.***  
Привет
