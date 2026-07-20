## Number Functions

- `ROUND` - округляет число

```sql
SELECT 
    3.568,           -- 3.568
    ROUND(3.568, 2), -- 3.570
    ROUND(3.568, 1), -- 3.600
    ROUND(3.568, 0)  -- 4.000
```

- `ABS` - модуль числа

```sql
SELECT
    2,      -- 2
    -2,     -- -2
    ABS(-2) -- 2
```
