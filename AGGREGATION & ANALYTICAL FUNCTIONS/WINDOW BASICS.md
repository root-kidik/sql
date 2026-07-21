## WINDOW BASICS

### WINDOW FUNCTIONS

#### AGGREGATE

- `COUNT(expr)` - количество
- `SUM(expr)` - сумма
- `AVG(expr)` - среднее
- `MAX(expr)` - максимальное
- `MIN(expr)` - минимальное

#### RANK

- `ROW_NUMBER()` - возвращает уникальный порядковый номер. даже при одинаковых значениях - номера не повторяются
- `RANK()` - присваивает ранг каждой строке с пропусками. при совпадении значений - даёт одинаковый ранг, а следующий номер перепрыгивает на количество совпадений
- `DENSE_RANK()` - присваивает ранг каждой строке без пропусков. при совпадении значений - даёт одинаковый ранг, но следующий идёт строго по порядку
- `CUME_DIST()` - кумулятивное распределение. показывает долю строк, у которых значение меньше или равно текущему (от >0 до 1)
- `PERCENT_RANK()` - показывает относительный ранг строки в диапозоне от 0 до 1. формула `(RANK - 1) / (ВСЕГО_СТРОК - 1)`
- `NTILE(n)` - делит отсортированный набор данных на `n` групп (корзин). и возвращает номер группы (от 1 до `n`) для каждой строки

#### VALUE

- `LEAD(expr,offset,default)` - возвращает значение из строки, которая находится на `offset строк вперёд` (по умолчанию `offset = 1`). если такой строки нет, возвращает `default` (или `NULL`)
- `LAG(expr,offset,default)` - возвращает значение из строки, которая находится на `offset строк назад` (по умолчанию `offset = 1`). если такой строки нет, возвращает `default` (или `NULL`)
- `FIRST_VALUE(expr)` - возвращает значение из первой строки в границах окна
- `LAST_VALUE(expr)` - возвращает значение из последней строки в границах окна

### WINDOW SYNTAX

```sql
AVG(sales) OVER(PARTITION BY category ORDER BY order_date ROWS UNBOUNDED PRECEDING)
```

- `AVG(sales)` - оконная функция
- `sales` - выражение
- `OVER(PARTITION BY category ORDER BY order_date ROWS UNBOUNDED PRECEDING)` - конструкция `OVER` превращает любую агрегационную функцию - в оконную. строки не схлопываются в отличие от `GROUP BY`
- `PARTITION BY category` - разделяет строки на группы (окна)
- `ORDER BY order_date` - сортирует строки внутри группы (окна)
- `ROWS UNBOUNDED PRECEDING` - конструкция `FRAME` определяет подгруппы внутри окна

### `OVER`

```sql
SELECT
    SUM(sales) OVER()
FROM
    orders
```

### `PARTITION`

- возвращает в каждой строке - общее количество продаж

```sql
SELECT
    SUM(sales) OVER(PARTITION BY product_id)
FROM
    orders
```

- возвращает сумму отдельно по каждой категории товаров, но оставляет детализацию по заказам

```sql
SELECT
    order_id,
    order_date,
    product_id,
    SUM(sales) OVER(PARTITION BY product_id)
FROM
    orders
```

- возвращает сумму отдельно по каждой категории товаров, но оставляет детализацию по заказам

### `ORDER BY`

```sql
SELECT
    RANK() OVER(PARTITION BY product_id ORDER BY order_date DESC)
FROM
    orders
```

- берём все строки
- делим на окна по `product_id`
- сортируем внутри окон по `order_date` в порядке убывания
- расчитываем `ранк` для каждой строки в каждом окне
- вовзращаем результат

### `FRAME` clause

- правила:
    - обязан также быть `ORDER BY`
    - минимальная граница должна быть перед максимальной границей

- тип фрейма:
    - `ROWS`
    - `RANGE`

- минимальная граница фрейма
    - `CURRENT ROW`
    - `N PRECEDING`
    - `UNBOUNDED PRECEDING` 

- максимальная граница фрейма
    - `CURRENT ROW`
    - `N FOLLOWING`
    - `UNBOUNDED FOLLOWING`

```sql
SUM(sales)
OVER(ORDER BY order_date
ROWS BETWEEN CURRENT ROW AND 2 FOLLOWING)
```

- вычисляет количество продаж с помощью скользяще окна размером `3`

### RULES

- оконные функции можно использовать только внутри `SELECT` или `ORDER BY`
- вложенные оконные функции - не разрешены
- оконные функции исполняются после `WHERE`
- оконные функции можно использовать вместе с `GROUP BY`, только если использованы одинаковые колонки
