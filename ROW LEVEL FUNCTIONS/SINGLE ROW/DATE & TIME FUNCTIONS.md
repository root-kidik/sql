## Date & Time Functions

- `Date`

`2025-08-20`

- Year
- Month
- Day

- `GETDATE` - возвращает таймстамп на момент исполнения запроса в базе данных

```sql
SELECT
    GETDATE() as now
```

- `Time`

`18:55:45`

- Hours
- Minutes
- Seconds

- `Datetime`

`Date` + `Time` = `Timestamp`

### Part Extraction

- `DAY` - возвращает день даты

```sql
SELECT
    DAY(GETDATE()) AS day
```

- `MONTH` - возвращает месяц даты

```sql
SELECT
    MONTH(GETDATE()) AS day
```

- `YEAR` - возвращает год даты

```sql
SELECT
    YEAR(GETDATE()) AS day
```

- `DATEPART` - возвращает определённую часть даты - как число

```sql
SELECT
    DATEPART(year, GETDATE()),
    DATEPART(quarter, GETDATE()),
    DATEPART(month, GETDATE()),
    DATEPART(week, GETDATE()),
    DATEPART(weekday, GETDATE()),
    DATEPART(day, GETDATE()),
    DATEPART(hour, GETDATE()),
    DATEPART(minute, GETDATE()),
    DATEPART(seconds, GETDATE())
```

- `DATENAME` - возвращает имя определнной части даты

```sql
SELECT
    DATENAME(year, GETDATE()),
    DATENAME(quarter, GETDATE()),
    DATENAME(month, GETDATE()),
    DATENAME(week, GETDATE()),
    DATENAME(weekday, GETDATE()),
    DATENAME(day, GETDATE()),
    DATENAME(hour, GETDATE()),
    DATENAME(minute, GETDATE()),
    DATENAME(seconds, GETDATE())
```

- `DATETRUNC` - обрезает дату до определенной части

```sql
SELECT
    DATETRUNC(year, GETDATE()),
    DATETRUNC(quarter, GETDATE()),
    DATETRUNC(month, GETDATE()),
    DATETRUNC(week, GETDATE()),
    DATETRUNC(weekday, GETDATE()),
    DATETRUNC(day, GETDATE()),
    DATETRUNC(hour, GETDATE()),
    DATETRUNC(minute, GETDATE()),
    DATETRUNC(seconds, GETDATE())
```

- `EOMONTH` - возвращает дату, где в дне - указан последний день месяца

```sql
SELECT
    EOMONTH(GETDATE()),                         -- конец месяца
    CAST(DATETRUNC(month, GETDATE()) AS Date)   -- начало месяца
```

### Format & Casting

- `FORMAT` - изменяет формат даты

```sql
SELECT
    FORMAT(GETDATE(), 'yyyy-MM-dd'),
    FORMAT(GETDATE(), 'dd-MM-yyyy'),
    FORMAT(GETDATE(), 'dd-MM-yy'),
    FORMAT(GETDATE(), 'dd'),
    FORMAT(GETDATE(), 'ddd'),
    FORMAT(GETDATE(), 'dddd'),
    FORMAT(GETDATE(), 'MM'),
    FORMAT(GETDATE(), 'MMM'),
    FORMAT(GETDATE(), 'MMMM'),
    'DAY ' +  FORMAT(GETDATE(), 'ddd MMM') + ' Q'  + DATENAME(quarter, GETDATE()) + ' ' + FORMAT(GETDATE(), 'yyyy hh:mm:ss tt')
```

```sql
SELECT
    FORMAT(1234.56, 'N'),  -- 1,234.56
    FORMAT(1234.56, 'P'),  -- 123,456.00 %
    FORMAT(1234.56, 'C'),  -- $1,234.56
    FORMAT(1234.56, 'E'),  -- 1,23E+09
    FORMAT(1234.56, 'F'),  -- 1234.56
    FORMAT(1234.56, 'N0'), -- 1,235
    FORMAT(1234.56, 'N1'), -- 1,234.6
    FORMAT(1234.56, 'N2'), -- 1,234.56
    FORMAT(1234.56, 'N,de_DE'),  -- 1.234,56
    FORMAT(1234.56, 'N,en_US'),  -- 1,234.56
```

- `CONVERT` - превращает один тип данных в другой, можно указать формат

```sql
SELECT
    CONVERT(INT, '123') AS [String to Int Convert],
    CONVERT(DATE, '2025-08-20'),
    CONVERT(DATE, GETDATE()),
    CONVERT(VARCHAR, GETDATE())
```

- `CAST` - превращает один тип данных в другой, нельзя указать формат

```sql
SELECT
    CAST('123' AS INT) AS [String to Int],
    CAST(123 AS VARCHAR) AS [Int to String],
    CAST('2025-08-20' AS DATE) AS [String to Date],
    CAST('2025-08-20' AS DATETIME2) AS [String to Datetime]
```

### Calculations

- `DATEADD` - позволяет добавить/убавить определенный интервал к дате

```sql
SELECT
    DATEADD(year, 2, GETDATE()),
    DATEADD(month, 3, GETDATE()),
    DATEADD(day, -10, GETDATE())
```

- `DATEDIFF` - позволяет найти разницу между двумя датами

```sql
SELECT
    DATEDIFF(year, '2026-07-20', GETDATE())
```

### Validation

- `ISDATE` - проверяет если это дата

```sql
SELECT
    order_date,
    CASE WHEN ISDATE(order_date) = 1 THEN CAST(order_date AS DATE)
        ELSE '9999-01-01'
    END new_order_date
FROM 
(
    SELECT '2025-08-20' AS order_date
    UNION
    SELECT '2025-08-21'
    UNION
    SELECT '2025-08-23'
    UNION
    SELECT '2025-08'
)
```
