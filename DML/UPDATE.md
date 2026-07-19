## UPDATE

```sql
UPDATE 
    customers
SET
    score = 0
WHERE
    id = 6
```

- обновить в таблице `customers` все строки, у которых `id = 6`, сделав `score = 0`

```sql
UPDATE 
    customers
SET
    score = 0
    country = 'Russia'
WHERE
    id = 10
```

- обновить в таблице `customers` все строки, у которых `id = 10`, сделав `score = 0` и `country = 'Russia'`

```sql
UPDATE
    customers
SET
    score = 0
WHERE
    score IS NULL
```

- обновить в таблице `customers` все строки, у которых `score IS NULL`, сделав `score = 0`
