## DELETE

```sql
DELETE FROM
    customers
```

- удалить все строки из таблицы `customers` (лучше использовать `TRUNCATE TABLE customers`)

___

```sql
DELETE FROM
    customers
WHERE
    id > 5
```

- удалить все строки из таблицы `customers`, в который `id > 5`

___

```sql
TRUNCATE TABLE
    customers
```

- удалить все строки из таблицы `customers`
