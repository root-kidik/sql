## JOINS

`JOIN` - объединяет колонки из разных таблиц

- объединение происходит на основе `колонки`

когда нужно использовать?:
- комбинировать данные (большая картинка)
    - `INNER`
    - `LEFT`
    - `FULL`
- обогащение данных (дополнительная информация)
    - `LEFT`
- проверка на существование (фильтрация)
    - `INNER`
    - `LEFT + WHERE`
    - `FULL + WHERE`

## INNER JOIN

- возвращает только те строки, которые есть в каждой таблице

```sql
SELECT
    *
FROM
    A
INNER JOIN
    B
ON 
    A.key = B.key
```

- возвращает только те строки, в которых `A.key = B.key`

```sql
SELECT
    *
FROM
    customers
INNER JOIN
    orders
ON
    customers.id = orders.customer_id
```

- возвращает только тех пользователей, у которых есть заказ, причём в ответ - включает как информацию о пользователе, так и информацию о заказе

## LEFT JOIN

- возвращает все строки из `левой` таблицы и только совпадающие из `правой` таблицы

```sql
SELECT
    *
FROM
    A
LEFT JOIN
    B
ON 
    A.key = B.key
```

- возвращает все строки из таблицы `A` и только те строки из таблицы `B`, в которых `A.key = B.key`

```sql
SELECT
    *
FROM
    customers
LEFT JOIN
    orders
ON
    customers.id = orders.customer_id
```

-  возвращает все пользователей, а также добавляет информацию о заказах, если она есть

## RIGHT JOIN

- возвращает все строки из `правой` таблицы и только совпадающие из `правой` таблицы

```sql
SELECT
    *
FROM
    A
RIGHT JOIN
    B
ON
    A.key = B.key
```
 
- возвращает все строки из таблицы `B` и только те строки из таблицы `A`, в которых `A.key = B.key`

```sql
SELECT
    *
FROM
    customers
RIGHT JOIN
    orders
ON 
    customers.id = orders.customer_id
```

- возвращает все заказы, даже те, которые не привязаны к пользователям

## FULL JOIN

- возвращает все строки из всех таблиц

```sql
SELECT
    *
FROM
    A
FULL JOIN
    B
ON
    A.key = B.key
```

- вернуть все строки из таблиц `A` и `B`

```sql
SELECT
    *
FROM
    customers
FULL JOIN
    orders
ON
    customers.id = orders.customer_id
```

- вернуть всех пользователей и все заказы

## LEFT ANTI JOIN

- возвращает строки из `левой` таблицы, которые не пересекаются со строками из `правой` таблицы

```sql
SELECT
    *
FROM
    A
LEFT JOIN
    B
ON
    A.key = B.key
WHERE
    B.key IS NULL
```

- вернуть строки из таблицы `A`, которые не пересекаются со строками по `B.key` с таблицей `B`

```sql
SELECT
    *
FROM
    customers
LEFT JOIN
    orders
ON
    customers.id = orders.customer_id
WHERE
    orders.customer_id IS NULL
```

- возвращает всех пользователей, которые не имеют заказов

## RIGHT ANTI JOIN

- возвращает строки из `правой` таблицы, которые не пересекаются со строками из `левой` таблицы

```sql
SELECT
    *
FROM
    A
LEFT JOIN
    B
ON
    A.key = B.key
WHERE
    A.key IS NULL
```

- вернуть строки из таблицы `B`, которые не пересекаются со строками по `A.key` с таблицей `A`

```sql
SELECT
    *
FROM
    customers
LEFT JOIN
    orders
ON
    customers.id = orders.customer_id
WHERE
    orders.customer_id IS NULL
```

- возвращает всех заказы, у которых нету пользователей

## FULL ANTI JOIN

- возвращает только те строки, которые не имеют совпадений

```sql
SELECT
    *
FROM
    A
FULL JOIN
    B
ON
    A.key = B.key
WHERE
    A.key IS NULL
    OR
    B.key IS NULL
```

- возвращает строки из `A` и `B`, которые не пересекаются между собой

```sql
SELECT
    *
FROM
    customers
FULL JOIN
    orders
ON
    customers.id = orders.customer_id
WHERE
    customer.id IS NULL
    OR
    orders.customer_id IS NULL
```

- возвращает пользователей, которые не имеют заказы + возвращает все заказы, которые не имеют пользователей

## CROSS JOIN

- объединяет каждую строку из `левой` таблицы с каждой строкой из `правой` таблицы
- декартово произведение

```sql
SELECT
    *
FROM
    A
CROSS JOIN
    B
```

- возвращает декартово произведение между `A` и `B`

```sql
SELECT
    *
FROM
    customers
CROSS JOIN
    orders
```

- возвращает декартово произведение между `customers` и `orders`

## Когда, какой `JOIN` использовать?

- только совпадение
    - `INNER JOIN`
-  все строки
    - с одной стороны
        - `LEFT JOIN`
    - с каждой стороны
        - `FULL JOIN`
- только не совпадения
    - с одной стороны
        - `ANTI LEFT JOIN`
    - с каждой стороны
        - `ANTI FULL JOIN`
