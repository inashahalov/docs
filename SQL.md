````markdown
## Задача

Таблица `Sales(sale_id, region, salesperson, amount, sale_date)`.  
Для каждого региона найди продавца с наибольшей суммой продаж за январь 2024.  
Если суммы равны — выбери того, у кого `salesperson` идёт первым по алфавиту.

---

## Решение

```sql
WITH totals AS (
    SELECT
        region,
        salesperson,
        SUM(amount) AS total
    FROM Sales
    WHERE sale_date >= '2024-01-01'
      AND sale_date <  '2024-02-01'
    GROUP BY region, salesperson
),
ranked AS (
    SELECT *,
        ROW_NUMBER() OVER (
            PARTITION BY region
            ORDER BY total DESC, salesperson ASC
        ) AS rn
    FROM totals
)
SELECT region, salesperson, total
FROM ranked
WHERE rn = 1;
```

---

## Как работает запрос

| CTE | Что делает |
|--------|--------------------------------------------------|
| `totals` | Фильтрует январь 2024 и суммирует продажи по каждому продавцу внутри региона |
| `ranked` | Нумерует строки внутри каждого региона: сначала по сумме ↓, затем по алфавиту ↑ |
| `WHERE rn = 1` | Оставляет только победителя в каждом регионе |

---

## Логика сортировки в `ROW_NUMBER`

```sql
ORDER BY total DESC,     -- сначала максимальная сумма
         salesperson ASC -- при равенстве — первый по алфавиту
```
````
