Стек  
Virtual Box 7.2.4  
Ubuntu Server 25.10  
Характеристики ВМ  
RAM: 16GB  
CPU: 8 cores  
VDI(SSD): 200GB  
PostgreSQL 17  

***Реализовать прямое соединение двух или более таблиц***  

Создаем БД join_homework и таблицы  customers, products, orders  
<img width="821" height="441" alt="image" src="https://github.com/user-attachments/assets/ba7bf787-05b2-456c-bdad-92bac683aa72" /> 

Добавляем данные в таблицы  
<img width="718" height="390" alt="image" src="https://github.com/user-attachments/assets/313d5176-d9e4-4a46-8619-655fcac387b8" />

Получаем заказы с данными клиентов и товаров с помощью прямого соединения  
*INNER JOIN возвращает только строки, где есть совпадения по условиям ON*    
<img width="849" height="385" alt="image" src="https://github.com/user-attachments/assets/18748360-d6ff-4936-881c-b68d67619974" />

***Реализовать левостороннее (или правостороннее) соединение двух или более таблиц***  

Получаем всех клиентов, даже если у них нет заказов, с помощью левостороннего соединения  
*LEFT JOIN гарантирует, что все строки из customers попадут в результат, для клиентов без заказов столбцы из orders и products будут NULL*  
<img width="1032" height="389" alt="image" src="https://github.com/user-attachments/assets/15829106-5410-4c96-8748-16cb81138a41" />

***Реализовать кросс соединение двух или более таблиц***

Получаем все возможные комбинации клиентов и товаров с помощью кросс соединения    
*CROSS JOIN, каждая строка из customers соединяется с каждой строкой из products*    
<img width="779" height="646" alt="image" src="https://github.com/user-attachments/assets/25a2519d-ae2d-4280-9069-a9a73e49a117" />

***Реализовать полное соединение двух или более таблиц*** 

Получаем всех клиентов и все товары, включая тех, у кого нет заказов с помощью полного соединения  
*FULL JOIN включает в себя всё, поля без совпадений заполняются NULL*  
<img width="879" height="389" alt="image" src="https://github.com/user-attachments/assets/767184fd-f3d6-4a29-b536-161804041729" />

***Реализовать запрос, в котором будут использованы разные типы соединений***  

Получаем полный список возможных комбинаций «клиент + товар» и отмечаем какие из этих комбинаций уже реализованы в реальных заказах с помощью cross join и left join 
*CROSS JOIN создаёт все возможные пары, каждый клиент связывается с каждым товаром* 
*LEFT JOIN пытается прикрепить к каждой паре реальный заказ* 
<img width="819" height="686" alt="image" src="https://github.com/user-attachments/assets/326a7e44-b1f2-45c8-afd4-6d30cd137475" /> 

***Сделать комментарии на каждый запрос
К работе приложить структуру таблиц, для которых
выполнялись соединения***

    CREATE TABLE customers (  
        customer_id SERIAL PRIMARY KEY,  
        first_name VARCHAR(50) NOT NULL,  
        lastname VARCHAR(50) NOT NULL,  
        email VARCHAR(100) UNIQUE  
    );  

INSERT INTO customers (first_name, lastname, email) VALUES  
    ('Анна', 'Иванова', 'anna.ivanova@example.com'),  
    ('Борис', 'Петров', 'boris.petrov@example.com'),  
    ('Светлана', 'Сидорова', 'svetlana.sidorova@example.com'),  
    ('Дмитрий', 'Кузнецов', 'dmitry.kuznetsov@example.com'),  
    ('Елена', 'Морозова', 'elena.morozova@example.com');  

CREATE TABLE products (  
    product_id SERIAL PRIMARY KEY,  
    product_name VARCHAR(100) NOT NULL,  
    price DECIMAL(10, 2) NOT NULL,  
    category VARCHAR(50)  
);   

INSERT INTO products (product_name, price, category) VALUES  
    ('Ноутбук Lenovo IdeaPad', 59999.99, 'Электроника'),  
    ('Смартфон Samsung Galaxy', 39999.99, 'Электроника'),  
    ('Кофеварка Bosch', 8999.99, 'Бытовая техника'),  
    ('Рюкзак городской', 2999.99, 'Аксессуары'),  
    ('Книга "PostgreSQL для начинающих"', 1499.99, 'Книги');  
    
CREATE TABLE orders (  
    order_id SERIAL PRIMARY KEY,  
    customer_id INT NOT NULL REFERENCES customers(customer_id) ON DELETE CASCADE,  
    product_id INT NOT NULL REFERENCES products(product_id) ON DELETE CASCADE,  
    order_date DATE NOT NULL,  
    quantity INT NOT NULL DEFAULT 1  
);

INSERT INTO orders (customer_id, product_id, order_date, quantity) VALUES    
    (1, 1, '2023-05-10', 1),      
    (1, 4, '2023-06-15', 2),      
    (2, 2, '2023-07-11', 1),       
    (3, 3, '2023-08-25', 1),          
    (4, 5, '2024-01-10', 3),      
    (5, 1, '2024-02-14', 1),    
    (2, 5, '2024-03-05', 1);  
