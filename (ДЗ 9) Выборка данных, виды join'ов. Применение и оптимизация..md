Стек  
Virtual Box 7.2.4  
Ubuntu Server 25.10  
Характеристики ВМ  
RAM: 16GB  
CPU: 8 cores  
VDI(SSD): 200GB  
PostgreSQL 17  

***Реализовать прямое соединение двух или более таблиц***  
Создаем БД и таблицы

***Реализовать левостороннее (или правостороннее) соединение двух или более таблиц***  
Привет

***Реализовать кросс соединение двух или более таблиц***  
Привет

***Реализовать полное соединение двух или более таблиц***  
Привет

***Реализовать запрос, в котором будут использованы разные типы соединений***  
Привет

***Сделать комментарии на каждый запрос
К работе приложить структуру таблиц, для которых
выполнялись соединения***

CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    lastname VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);

CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    category VARCHAR(50)
);

CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT NOT NULL REFERENCES customers(customer_id) ON DELETE CASCADE,
    product_id INT NOT NULL REFERENCES products(product_id) ON DELETE CASCADE,
    order_date DATE NOT NULL,
    quantity INT NOT NULL DEFAULT 1
);
