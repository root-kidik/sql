# SELECT

Делает выборку данных

___

```sql
SELECT 
    * 
FROM 
    table
```

- селекция: выбрать все строки
- проекция: вывести все столбцы

___


```sql
SELECT 
    col1, 
    col2 
FROM 
    table
```

- селекция: выбрать все строки
- проекция: вывести столбцы `col1`, `col2`

___

## WHERE

Фильтрует строки по условию

___

```sql
SELECT 
    *
FROM 
    table
WHERE 
    condition
```

- выбрать строки по условию `condition`
- вывести все столбцы

___

## ORDER BY

Сортирует выбранные данные по определённому столбцу


`Default` - `ASC`

`ASC` - в порядке возрастания
`DESC` - в порядке убывания

___

```sql
SELECT 
    *
FROM 
    table
ORDER BY 
    score
```

- выбрать все строки
- отсорировать по возрастанию столбца `score`
- вывести все столбцы

___

```sql
SELECT 
    *
FROM 
    table
ORDER BY
    country ASC,
    score DESC
```

- выбрать все строки
- отсортировать по столбцу `country` в порядке возрастания (лексиграфически)
- отсортировать те строки, в которых `country` одинаковая по столбцу `score` в порядке убывания 
- вывести все столбцы

___

## GROUP BY

Объеденяет строки с одинаковым значением в столбце - в одну группу

- если в `SELECT`, есть столбец, который не указан в `GROUP BY`, на этот столбец обязана применится функция агрегации

___

```sql
SELECT
    country,
    SUM(score) as total_score
FROM
    table
GROUP BY
    country
```

- выбрать все строки
- объеденить строки с одинаковым `country` в одну группу
- вывести столбцы `country` и `total_score`, выполнив агрегацию `SUM(score)` по строкам из групп

___

```sql
SELECT
    country,
    first_name,
    SUM(score) as total_score
FROM 
    table
GROUP BY
    country,
    first_name
```

- выбрать все строки
- объеденить все строки по уникальному сочетанию значений `country` + `first_name` в группы
- вывести столбцы `country`, `first_name`, `total_score`, выполнив агрегацию `SUM(score)` по строкам из групп

___

```sql
SELECT
    country,
    SUM(score) as total_score,
    COUNT(id) as total_customers
FROM
    customers
GROUP BY
    country
```

- выбрать все строки
- сгруппировать строки по `country`
- вывести столбцы `country`, `total_score` (аккумулируя `score` в группе), `total_customers` (подсчитывая количество `id != NULL` в группе)

## HAVING

Фильтрует данные, строго после агрегации - `GROUP BY`

- можно фильтровать только по колонкам на которые была примена `SUM`, `AVG`, `COUNT`, либо по той колонке на которую сделали `GROUP BY`

___

```sql
SELECT
    country,
    SUM(score) as total_score
FROM
    table
GROUP BY
    country
HAVING
    SUM(score) > 800
```

- выбрать все строки
- сгруппировать по `country`
- отфильтровать те группы, в которых аккумулированный `score <= 800`
- вывести столбцы `country`, `total_score` (аккумулируя `score`)

___

```sql
SELECT
    country,
    SUM(score) as total_score
FROM
    table
WHERE
    score > 400
GROUP BY
    country
HAVING
    SUM(score) > 800
```

- выбрать все строки
- отфильтровать строки по `score > 400` 
- сгруппировать по `country`
- отфильтровать те группы, в которых аккумулированный `score <= 800`
- вывести столбцы `country`, `total_score` (аккумулируя `score`)

___

```sql
SELECT
    country,
    AVG(score) AS avg_score
FROM 
    table
WHERE 
    score != 0
GROUP BY
    country
HAVING
    AVG(score) > 430
```

- выбрать все строки 
- отфильтрова строки по `score != 0`
- сгрупировать по `country`
- отфильтровать те группы, в которых агрегированное среднее значение `score <= 430`
- вывести столбцы `country`, `avg_score` (агрегируя столбец `score` как среднее значение)

## DISTINCT

Удаляет дубликаты

___

```sql
SELECT DISTINCT
    country
FROM 
    table
```

- выбрать все строки
- отфильтровать строки с одинаковым `country`
- вывести столбцы `country`

___

```sql
SELECT DISTINCT
    country,
    city
FROM 
    table
```

- выбрать все строки
- отфильтровать строки по уникальм сочетаниям `country` + `city` (дубликаты таких пар удаляются)
- вывести столбцы `country`, `city`


## TOP

Ограничивает количество получаемых строк

___

```sql
SELECT TOP 3
    *
FROM
    table
```

- выбрать все строки
- отфильтровать, выбрав только первые `3`
- вывести все столбцы

___

```sql
SELECT TOP 3
    *
FROM
    table
ORDER BY
    score DESC
```

- выбрать все строки
- отсортировать строки по убыванию `score`
- отфильтровать, выбрав только первые `3`
- вывести все столбцы

## LIMIT

Ограничивает количество получаемых строк

___

```sql
SELECT
    *
FROM
    table
LIMIT 3
```

- выбрать все строки
- отфильтровать, выбрав только первые `3`
- вывести все столбцы

___

```sql
SELECT
    *
FROM
    table
ORDER BY
    score DESC
LIMIT 3
```

- выбрать все строки
- отсортировать строки по убыванию `score`
- отфильтровать, выбрав только первые `3`
- вывести все столбцы

## OFFSET

Пропускает первые `N` строк

___

```sql
SELECT
    *
FROM
    table
OFFSET
    5
```

- выбрать все строки
- пропустить первые `5` строк
- вернуть все столбцы

___

```sql
SELECT
    *
FROM
    table
LIMIT
    10
OFFSET
    5
```

- выбрать все строки
- пропустить первые `5` строк
- выбрать `10` строк
- вернуть все столбцы


## ORDER

```sql
SELECT DISTINCT
    col1,
    SUM(col2) as col2_total_sum
FROM
    table
WHERE
    condition
GROUP BY
    col1
HAVING
    SUM(col2) > 30
ORDER BY
    col1 ASC
LIMIT 
    2
OFFSET
    10
```

- `FROM` выбираем все строки из таблицы
- `WHERE` фильтруем строки по `condition`
- `GROUP BY` группируем строки по `col1`
- `HAVING` фильтруем по `SUM(col2) > 30`
- `SELECT col1, SUM(col2) as col2_total_sum` формируем финальную таблицу, со столбцами `col1` `col2_tatol_sum` (аккумулируя `col2`)
- `DISTINCT` фильтруем одинаковые строки
- `ORDER BY` сортируем по возрастанию `col1`
- `OFFSET` пропускаем первые `10` строк
- `LIMIT 2` - берём только первые `2`

## Fixed Values

Можно включать в вывод - фиксированные значения

___

```sql
SELECT 1
```

`1`

___

```sql
SELECT 123 as static_number
```

| static_number |
| ------------- |
| 123           |

___

```sql
SELECT 'Hello' AS static_string
```

| static_string |
| ------------- |
| Hello         |

___

```sql
SELECT
    id,
    first_name,
    'New Customer' as customer_type
FROM 
    customers
```

| id | first_name | customer_type |
| -- | ---------- | ------------- |
| 1  | Marta      | New Customer  |
| 2  | Nikita     | New Customer  |
