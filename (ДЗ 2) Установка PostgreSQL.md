***создать ВМ с Ubuntu 20.04/22.04 или развернуть докер любым удобным способом***\
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


***поставить на нем Docker Engine***\
curl -fsSL https://get.docker.com -o get-docker.sh  
bash get-docker.sh   
 <img width="974" height="133" alt="image" src="https://github.com/user-attachments/assets/7165829d-35d3-4678-acf1-fe4daf8be440" />

***сделать каталог /var/lib/postgres***\
<img width="396" height="50" alt="image" src="https://github.com/user-attachments/assets/8417904e-2c32-470e-9a21-76b8cb4722ff" />

***развернуть контейнер с PostgreSQL 15 смонтировав в него /var/lib/postgresql***\  
Создаем docker-сеть  
<img width="803" height="73" alt="image" src="https://github.com/user-attachments/assets/8872e8f9-efcf-414e-9fea-93d2c33d79d2" />     
Разворачиваем контейнер  
<img width="1275" height="115" alt="image" src="https://github.com/user-attachments/assets/09c92722-94d2-4ede-bd4c-59fe053af37a" />  
Проверяем появились ли содержимое в папке   
<img width="959" height="66" alt="image" src="https://github.com/user-attachments/assets/e911a1aa-b1da-4d3d-883e-b49622de539c" />    
Создаем БД work  
<img width="1174" height="391" alt="image" src="https://github.com/user-attachments/assets/30b27251-232a-40f6-856b-c0125853792f" />  

***развернуть контейнер с клиентом postgres, подключится из контейнера с клиентом к контейнеру с сервером и сделать таблицу с парой строк***\
<img width="1045" height="100" alt="image" src="https://github.com/user-attachments/assets/5f51e39c-fe21-40c1-bdab-223896687d92" />  
Создаем таблицу и строки  
<img width="447" height="184" alt="image" src="https://github.com/user-attachments/assets/66c3589d-236b-4a9e-8d7f-1aa8d70b77fa" />  
Проверяем данные  
<img width="367" height="106" alt="image" src="https://github.com/user-attachments/assets/aa5b3320-2982-472a-bc52-03ea19f34dea" />  

***подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов ЯО/места установки докера***\
Подключаемся через pgAdmin4 от своего компьютера к БД на ВМ  
<img width="409" height="948" alt="image" src="https://github.com/user-attachments/assets/d19ba4fa-69e3-468a-9553-b99560869c86" />

***удалить контейнер с сервером***\
<img width="597" height="114" alt="image" src="https://github.com/user-attachments/assets/3f932eb0-88f7-48ad-a75a-25333e0cd10d" />

***создать его заново***\
<img width="1274" height="111" alt="image" src="https://github.com/user-attachments/assets/f0ae0b1d-1e51-47b7-9f7f-c8881a1f1c5b" />

***подключится снова из контейнера с клиентом к контейнеру с сервером***\
<img width="1014" height="83" alt="image" src="https://github.com/user-attachments/assets/b7c01f4e-9bd0-4391-b687-1a08e490f722" />

***проверить, что данные остались на месте***\
Данные остались на месте
<img width="322" height="132" alt="image" src="https://github.com/user-attachments/assets/2139b07e-da11-45e4-a9cf-eef73766b109" />

***оставляйте в ЛК ДЗ комментарии что и как вы делали и как боролись с проблемами***\
Привет
