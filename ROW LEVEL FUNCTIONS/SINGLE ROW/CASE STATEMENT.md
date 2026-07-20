
## CASE STATEMENT

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result
END
```

- если нету `ELSE` - и не один `WHEN` не подошёл - то результатом будет `NULL`
- результат после `THEN` обязан иметь одинаковый тип данных на все `THEN`
