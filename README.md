
# ДЗ по SQL запросам

### Cкрипт создания таблицы с параметрами
```sql
CREATE SCHEMA TESTSCHEMA AUTHORIZATION postgres;
CREATE TABLE TESTSCHEMA.Persons(
     name VARCHAR(20) NOT NULL,
     surname TEXT DEFAULT 0,
     age INT CHECK (age >= 0),
     phone_number text UNIQUE,
     city_of_living text,
     PRIMARY KEY (name, surname, age)
    );
```
### Добавление в таблицу и пробное удаление 
```sql
INSERT INTO TESTSCHEMA.Persons (name,surname, age, phone_number , city_of_living)
VALUES ('Иван', 'Иванов', 18, '+79998886655', 'Москва'),
('Петр', 'Петров', 19, '+79998886656', 'Уфа'),
('Яков', 'Яковлев', 17, '+79998886654', 'Пермь'),
('Николай', 'Николаев', 27, '+79998886658', 'Тула');
```

```sql
DELETE FROM TESTSCHEMA.Persons
WHERE name = 'Николай';
```
### Cкрипт, который будет ищет в таблице PERSONS поля name и surname москвичей
```sql
SELECT name, surname FROM TESTSCHEMA.Persons
WHERE city_of_living = 'Москва';
```
### Скрипт, который ищет в таблице PERSONS все поля, у которых поле age меньше 27 лет, и сортирует по убыванию возраста
```sql
SELECT * FROM TESTSCHEMA.Persons
WHERE age < 27
ORDER BY age DESC;
```
### Скрипт создания таблицы CUSTOMERS:
```sql
CREATE TABLE CUSTOMERS(
    id int UNIQUE,
    name VARCHAR(20) NOT NULL,
    surname TEXT DEFAULT 0,
    age INT CHECK (age >= 0),
    phone_number text UNIQUE,
    PRIMARY KEY (id)
);
```
### Скрипт создания таблицы ORDERS:
```sql
CREATE TABLE ORDERS(
    id int UNIQUE not null,
    date DATE DEFAULT CURRENT_DATE,
    customer_id int,
    product_name VARCHAR(30) NOT NULL,
    amount INT CHECK (amount >= 0),
    PRIMARY KEY (id),
    FOREIGN KEY (customer_id) REFERENCES customers (id)
);
```
###  Скрипт, который будет возвращать из таблиц поля product_name для пользователей с именем alexey независимо от регистра ввода имени.:
```sql
SELECT product_name
FROM ORDERS JOIN CUSTOMERS ON ORDERS.customer_id = CUSTOMERS.id
WHERE LOWER(CUSTOMERS.name) = 'алексей';
```
###  Скрипт, который меняет тип данных поля id c int на serial.:
```sql
ALTER TABLE CUSTOMERS DROP CONSTRAINT customers_pkey cascade ;
ALTER TABLE customers ALTER COLUMN id SET DATA TYPE BIGINT;
CREATE SEQUENCE id START WITH 1 INCREMENT BY 1;
ALTER TABLE customers ALTER COLUMN id SET DEFAULT nextval('id'::regclass);
ALTER TABLE CUSTOMERS ADD CONSTRAINT customers_pkey PRIMARY KEY (id);
```
###  Чистка и удаление таблицы:
```sql
TRUNCATE TABLE ORDERS;
DROP TABLE ORDERS;
```
