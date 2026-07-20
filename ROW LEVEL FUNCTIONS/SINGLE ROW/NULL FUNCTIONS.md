## Null Functions

- `ISNULL` - возвращает либо значение, либо замену, если значение `NULL`

```sql
ISNULL(value, replacement)
```

```sql
ISNULL(ShippingAddress, BillingAddress)
```

- `COALESCE` - возвращает первый `NOT IS NULL` значение, которое встретилось в списке

```sql
COALESCE(value1, value2, value3, ...)
```

```sql
COALESCE(ShippingAddress, BillingAddress, 'unknown')
```

- `NULLIF` - возвращает `NULL`, если значения одинаковые, иначе - первое значение

```sql
NULLIF(value1, value2)
```
