## String Functions

### Manipulation

- `CONCAT` - комбинирует множество строк - в одну

```sql
SELECT
    first_name,
    country,
    CONCAT(first_name, ' ', country) as name_country
FROM
    customers
```

- `UPPER` - переводит все символы в верхний регистр

```sql
SELECT
    first_name,
    UPPER(first_name) AS low_name
FROM
    customers
```

- `LOWER`  - переводит все символы в верхний регистр

```sql
SELECT
    first_name,
    LOWER(first_name) AS low_name
FROM
    customers
```

- `TRIM` - удаляем ведущие и конечные проблемы

```sql
SELECT
    first_name
FROM
    customers
WHERE
    first_name != TRIM(first_name)
```

- `REPLACE` - заменяет один символ на другой

```sql
SELECT
    REPLACE('123-456-7890', '-', '') as phone
```

### Calculation

- `LENGTH` - возвращает длину строки

```sql
SELECT
    LENGTH(first_name) as len_name
FROM
    customers
```

### String Extraction

- `LEFT` - возвращает определённое количество символов начиная с левой стороны строки

```sql
SELECT
    LEFT(first_name, 2)
FROM
    customers
```

- `RIGHT`  - возвращает определённое количество символов начиная с правой стороны строки

```sql
SELECT
    RIGHT(first_name, 2)
FROM
    customers
```

- `SUBSTRING` - возвращает подстроку, начиная с определённой позиции

```sql
SELECT
    SUBSTRING(first_name, 2, LEN(first_name))
FROM
    customers
```
