
# SQL: DQL-команди та вибірка даних
# SQL: DQL Commands and Data Querying

Домашнє завдання з теми 3 «Завантаження даних та основи SQL. DQL команди»: написання запитів `SELECT` до завантаженого датасету в MySQL Workbench.

Homework for Topic 3 "Data Loading and SQL Basics. DQL Commands": writing `SELECT` queries against the loaded dataset in MySQL Workbench.

## Зміст / Contents

- [Файли / Files](#файли--files)
- [Завдання 1 / Task 1](#завдання-1--task-1)
- [Завдання 2 / Task 2](#завдання-2--task-2)
- [Завдання 3 / Task 3](#завдання-3--task-3)
- [Завдання 4 / Task 4](#завдання-4--task-4)
- [Завдання 5 / Task 5](#завдання-5--task-5)
- [Запуск / Setup](#запуск--setup)

## Файли / Files

| Файл / File | Опис / Description |
|---|---|
| `p1_1.png` | Завдання 1: `SELECT *` з `products` / Task 1: `SELECT *` from `products` |
| `p1_2.png` | Завдання 1: `name`, `phone` з `shippers` / Task 1: `name`, `phone` from `shippers` |
| `p2.png` | Завдання 2: `AVG`, `MIN`, `MAX` по `price` / Task 2: `AVG`, `MIN`, `MAX` of `price` |
| `p3.png` | Завдання 3: `DISTINCT`, `ORDER BY`, `LIMIT` / Task 3: `DISTINCT`, `ORDER BY`, `LIMIT` |
| `p4.png` | Завдання 4: `COUNT` + `BETWEEN` / Task 4: `COUNT` + `BETWEEN` |
| `p5.png` | Завдання 5: `GROUP BY supplier_id` / Task 5: `GROUP BY supplier_id` |

## Завдання 1 / Task 1

Вибрати всі стовпчики з таблиці `products` (через wildcard `*`) та лише стовпчики `name`, `phone` з таблиці `shippers`.

Select all columns from `products` (using the `*` wildcard) and only the `name` and `phone` columns from `shippers`.

```sql
SELECT * FROM products;
```

```sql
SELECT name, phone FROM shippers;
```

Результат / Result:
- `products` — усі стовпчики / all columns: `id`, `name`, `supplier_id`, `category_id`, `unit`, `price`.
- `shippers` — 3 рядки / 3 rows: Speedy Express, United Package, Federal Shipping.

Скриншоти / Screenshots: `p1_1.png`, `p1_2.png`

## Завдання 2 / Task 2

Знайти середнє, мінімальне та максимальне значення стовпчика `price` таблиці `products`.

Find the average, minimum and maximum values of the `price` column in `products`.

```sql
SELECT AVG(price) AS average_price,
       MIN(price) AS min_price,
       MAX(price) AS max_price
FROM products;
```

Результат / Result:

| average_price | min_price | max_price |
|---|---|---|
| 28.866363636363637 | 2.5 | 263.5 |

Скриншот / Screenshot: `p2.png`

## Завдання 3 / Task 3

Обрати унікальні значення колонок `category_id` та `price`, відсортувати за спаданням `price` і вивести лише 10 рядків.

Select unique values of `category_id` and `price`, sort by `price` in descending order and return only 10 rows.

```sql
SELECT DISTINCT category_id, price
FROM products
ORDER BY price DESC
LIMIT 10;
```

Результат (топ-10 за ціною) / Result (top 10 by price):

| category_id | price |
|---|---|
| 1 | 263.5 |
| 6 | 123.79 |
| 6 | 97 |
| 3 | 81 |
| 8 | 62.5 |
| 4 | 55 |
| 7 | 53 |
| 3 | 49.3 |
| 1 | 46 |
| 7 | 45.6 |

`DISTINCT` застосовується до пари `(category_id, price)`, а не до кожної колонки окремо.

`DISTINCT` applies to the `(category_id, price)` pair, not to each column separately.

Скриншот / Screenshot: `p3.png`

## Завдання 4 / Task 4

Знайти кількість продуктів (рядків) з ціною від 20 до 100.

Count the products (rows) priced between 20 and 100.

```sql
SELECT COUNT(*) AS product_count
FROM products
WHERE price BETWEEN 20 AND 100;
```

Результат / Result: `36`

`BETWEEN` включає обидві межі (20 і 100).

`BETWEEN` is inclusive of both bounds (20 and 100).

Скриншот / Screenshot: `p4.png`

## Завдання 5 / Task 5

Знайти кількість продуктів (рядків) та середню ціну в розрізі кожного постачальника (`supplier_id`).

Find the number of products (rows) and the average price for each supplier (`supplier_id`).

```sql
SELECT supplier_id,
       COUNT(*) AS product_count,
       AVG(price) AS average_price
FROM products
GROUP BY supplier_id;
```

Результат: 29 рядків (по одному на кожного постачальника), разом 77 продуктів.

Result: 29 rows (one per supplier), 77 products in total.

| supplier_id | product_count | average_price |
|---|---|---|
| 1 | 3 | 15.666666666666666 |
| 2 | 4 | 20.35 |
| 3 | 3 | 31.666666666666668 |
| 4 | 3 | 46 |
| 5 | 2 | 29.5 |
| 6 | 3 | 14.916666666666666 |
| 7 | 5 | 35.57 |
| 8 | 4 | 28.175 |
| 9 | 2 | 15 |
| 10 | 1 | 4.5 |
| 11 | 3 | 29.709999999999997 |
| 12 | 5 | 44.678000000000004 |
| 13 | 1 | 25.89 |
| 14 | 3 | 26.433333333333334 |
| 15 | 3 | 20 |
| 16 | 3 | 15.333333333333334 |
| 17 | 3 | 20 |
| 18 | 2 | 140.75 |
| 19 | 2 | 14.024999999999999 |
| 20 | 3 | 26.483333333333334 |
| 21 | 2 | 10.75 |
| 22 | 2 | 11.125 |
| 23 | 3 | 18.083333333333332 |
| 24 | 3 | 30.933333333333334 |
| 25 | 2 | 15.725 |
| 26 | 2 | 28.75 |
| 27 | 1 | 13.25 |
| 28 | 2 | 44.5 |
| 29 | 2 | 38.9 |

Скриншот / Screenshot: `p5.png`

## Запуск / Setup

1. Завантажити датасет у MySQL (схема `mydb`) згідно з конспектом до теми 3.
2. Відкрити MySQL Workbench, підключитися до `Local instance 3306`.
3. Виконати `USE mydb;` і запустити запити з цього файлу.

1. Load the dataset into MySQL (schema `mydb`) following the Topic 3 notes.
2. Open MySQL Workbench and connect to `Local instance 3306`.
3. Run `USE mydb;` and execute the queries from this file.

```sql
USE mydb;
```
