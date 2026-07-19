## ALTER

```sql
ALTER TABLE 
    persons
ADD COLUMN
    email VARCHAR(50) NOT NULL
```

- добавляет колонку `email` в таблицу `persons`

```sql
ALTER TABLE 
    persons
DROP COLUMN
    phone
```

- удаляет колонку `phone` из таблицы `persons`
