## CREATE

```sql
CREATE TABLE persons (
    id INT NOT NULL,
    person_name VARCHAR(255) NOT NULL,
    birth_date DATE,
    phone VARCHAR(255) NOT NULL,
    CONSTRAINT pk_id PRIMARY KEY (id)
)
```

- создаёт таблицу с колонками
