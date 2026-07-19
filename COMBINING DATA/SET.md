## SET operators

`SET operators` - объединяют строки из разных таблиц

- в каждой таблице - должны быть одинаковые колонки

- может использоваться почти везде
    - `WHERE`
    - `JOIN`
    - `GROUP BY`
    - `HAVING`
    - `ORDER BY` - только единожды в конце запроса
- количество колонок - должны быть одинаково в каждом запросе
- типы данных в каждой запросе - должны быть совместимы
- последовательность колонк в каждом запросе - должна быть одна и та же
- имя колонки в результате - будет именем колонки из первого запроса

```sql
SELECT
    first_name,
    second_name
FROM
    customers
JOIN
    clause
WHERE
    clause
GROUP BY
    clause

UNION

SELECT
    first_name,
    second_name
FROM
    Employees
JOIN
    clause
WHERE
    clause
GROUP BY
    clause

ORDER BY
    first_name
```

## UNION

- вовзращает все строки из каждого запроса
- удаляет одинаковые строки из результата

```sql
SELECT
    first_name
FROM
    customers

UNION

SELECT
    first_name
FROM
    employees
```

- возвращает результат где указаны уникальные имена работников и клиентов

## UNION ALL

- возвращает все строки из каждого запроса
- сохраняет дубликаты

```sql
SELECT
    first_name
FROM
    customers

UNION ALL

SELECT
    first_name
FROM
    employees
```

- возвращает результат где указаны имена работников м клиентов

## EXCEPT

- возвращает все строки из `первого` запроса, которых нету во `втором` запросе

```sql
SELECT
    first_name
FROM
    customers

EXCEPT

SELECT
    first_name
FROM
    employees
```

- возвращает имена всех клиентов, которые не являются работниками

## INTERSECT

- возвращает все строки, которые есть и в `первом` запросе и во `втором` запросе

```sql
SELECT
    first_name
FROM
    customers

INTERSECT

SELECT
    first_name
FROM
    employees
```

- возвращает имена всех клиентов, которые также являются работниками

## Когда нужно использовать?

- объеденить похожие данные перед анализом
    - `UNION`
    - `UNION ALL`
- нужно найти разницу между двумя наборами данных
    - `EXCEPT`
