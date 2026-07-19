## DELETE

```sql
DELETE FROM
    customers
```

- удалить все строки из таблицы `customers` (лучше использовать `TRUNCATE TABLE customers`)

```sql
DELETE FROM
    customers
WHERE
    id > 5
```

- удалить все строки из таблицы `customers`, в который `id > 5`

```sql
TRUNCATE TABLE
    customers
```

- удалить все строки из таблицы `customers`
