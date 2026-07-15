## INSERT

```sql
INSERT INTO
    customers (id, first_name, country, score)
VALUES
    (6, 'Marta', 'Russia', 100),
    (7, 'Nikita', 'Russia', NULL)
```

- добавить две строки в таблицу `customers`
- колонки, которые не указаны в `INSERT INTO` - во вставленной строку - будут `NULL`

___

```sql
INSERT INTO
    customers
VALUES
    (6, 'Marta', 'Russia', 100),

```

- можно опускать перечисление колонок, если вставляются данные для каждой колонки

___

```sql
INSERT INTO 
    persons (id, person_name, birth_date, phone)
SELECT
    id, 
    first_name, 
    NULL, 
    'Unknow'
FROM
    customers
```

- выбрать все строки из таблицы `customers`
- выбрать только столбцы `id`, `first_name` + добавить колонки со статическим значением `NULL`, `Unknow`
- вставить получившиеся строки в таблицу `persons`
