
# ДЗ по SQL запросам
---------------------------------------------------
create SCHEMA TESTSCHEMA AUTHORIZATION postgres;
create TABLE TESTSCHEMA.Persons(
     name VARCHAR(20) NOT NULL,
     surname TEXT DEFAULT 0,
     age INT CHECK (age >= 0),
     phone_number text UNIQUE,
     city_of_living text,
     PRIMARY KEY (name, surname, age)
    );
---------------------------------------------------
INSERT INTO TESTSCHEMA.Persons (name,surname, age, phone_number , city_of_living)
VALUES ('Иван', 'Иванов', 18, '+79998886655', 'Москва'),
('Петр', 'Петров', 19, '+79998886656', 'Уфа'),
('Яков', 'Яковлев', 17, '+79998886654', 'Пермь'),
('Николай', 'Николаев', 27, '+79998886658', 'Тула');

---------------------------------------------------
DELETE FROM TESTSCHEMA.Persons
WHERE name = 'Николай';
---------------------------------------------------
SELECT * FROM TESTSCHEMA.Persons
WHERE city_of_living = 'Москва';
---------------------------------------------------
SELECT * FROM TESTSCHEMA.Persons
WHERE age < 27
ORDER BY age DESC;
