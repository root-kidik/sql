## WHERE operators

### Comparision

- =
- <> !=
- >
- >=
- <
- <=

### Logical

- AND
- OR
- NOT

### Range

- BETWEEN

```sql
SELECT 
    *
FROM
    customers
WHERE
    score BETWEEN 100 AND 500
```

- выбрать все строки
- оставить только те, которые находятся в пределах [100; 500] (всё включительно)

### Membership

- IN
- NOT IN

```sql
SELECT
    *
FROM
    customers
WHERE
    country IN ('UK', 'USA')
```

- выбрать все строки
- оставить только те, в которых колонка `country` равна `UK` или `USA`

### Search

- LIKE

- `%` - хоть что
- `_` - ровно один символ

```sql
SELECT
    *
FROM
    customers
WHERE
    first_name LIKE 'M%'
```

- найти все строки, в которых `first_name` начинается с первой буквы `M`
