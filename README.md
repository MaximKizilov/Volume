
# ДЗ по SQL запросам
---------------------------------------------------
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
