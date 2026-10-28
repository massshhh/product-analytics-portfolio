# SQL-практика

Учебный датасет маркетплейса: таблицы `orders` (96 заказов) и `users` (25 пользователей).
Файлы для импорта в любой онлайн-редактор (SQLite Online, DB Fiddle): `orders.sql`, `users.sql` из основного репозитория стажировки.

## Освоенные темы
- [x] SELECT, FROM, WHERE (сравнения, AND/OR)
- [x] IN, BETWEEN, LIKE
- [x] ORDER BY, LIMIT
- [x] JOIN (INNER / LEFT) — освоено 18.10.2026
- [x] GROUP BY + HAVING — освоено 18.10.2026 (агрегаты COUNT/SUM/AVG, группировка с JOIN, фильтр по группам)
- [x] Оконные функции — освоено: ROW_NUMBER + обёртка-подзапрос («первый/последний заказ пользователя»)
- [x] CTE (WITH) и подзапросы — освоено: именованные промежуточные таблицы, «выручка выше средней»

## Примеры решённых задач

**Заказы дороже 5000 ₽:**
```sql
SELECT order_id
FROM orders
WHERE amount > 5000;
```

**Заказы пользователя, от новых к старым:**
```sql
SELECT order_id
FROM orders
WHERE user_id = 7
ORDER BY order_date DESC;
```

**Топ-10 самых дорогих заказов:**
```sql
SELECT order_id
FROM orders
ORDER BY amount DESC
LIMIT 10;
```

**Заказы за сентябрь 2026 (через LIKE по ISO-дате):**
```sql
SELECT order_id
FROM orders
WHERE order_date LIKE '2026-09%'
ORDER BY amount ASC;
```

**Заказы и выручка по каждому пользователю (GROUP BY):**
```sql
SELECT user_id,
       COUNT(order_id) AS order_count,
       SUM(amount)     AS tot
FROM orders
GROUP BY user_id;
```

**Клиенты с суммарной выручкой больше 50 000 (HAVING):**
```sql
SELECT user_id,
       SUM(amount) AS total_rev
FROM orders
GROUP BY user_id
HAVING SUM(amount) > 50000;
```
