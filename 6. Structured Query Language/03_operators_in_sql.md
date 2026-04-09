# SQL Operators

SQL operators are symbols or keywords used to perform operations on values in queries — from basic math and comparisons to pattern matching, set operations, and logical conditions. They are the building blocks of filtering, joining, and transforming data. Below are some of the most common SQL operators, categorized by their function:

| Operator | Category | Description | Example |
| -------- | -------- | ----------- | ------- |
| `+` | Arithmetic | Addition | `salary + bonus` |
| `-` | Arithmetic | Subtraction | `price - discount` |
| `*` | Arithmetic | Multiplication | `quantity * unit_price` |
| `/` | Arithmetic | Division | `total / count` |
| `%` | Arithmetic | Modulo (remainder after division) | `17 % 5` → 2 |
| `=` | Comparison | Equal to | `WHERE age = 30` |
| `!=` / `<>` | Comparison | Not equal to | `WHERE status != 'inactive'` |
| `>` | Comparison | Greater than | `WHERE salary > 50000` |
| `<` | Comparison | Less than | `WHERE age < 18` |
| `>=` | Comparison | Greater than or equal to | `WHERE score >= 90` |
| `<=` | Comparison | Less than or equal to | `WHERE stock <= 10` |
| `AND` | Logical | Returns TRUE if both conditions are true | `WHERE age > 18 AND city = 'NYC'` |
| `OR` | Logical | Returns TRUE if at least one condition is true | `WHERE city = 'NYC' OR city = 'LA'` |
| `NOT` | Logical | Negates a condition | `WHERE NOT status = 'active'` |
| `IN` | Logical | TRUE if the value matches any value in a list | `WHERE country IN ('US', 'UK', 'CA')` |
| `NOT IN` | Logical | TRUE if the value does not match any value in a list | `WHERE country NOT IN ('US', 'UK')` |
| `BETWEEN` | Logical | TRUE if the value is within an inclusive range | `WHERE age BETWEEN 18 AND 65` |
| `LIKE` | Logical | TRUE if the value matches a pattern (`%` = any chars, `_` = one char) | `WHERE name LIKE 'J%'` |
| `IS NULL` | Logical | TRUE if the value is NULL | `WHERE email IS NULL` |
| `IS NOT NULL` | Logical | TRUE if the value is not NULL | `WHERE email IS NOT NULL` |
| `EXISTS` | Logical | TRUE if a subquery returns one or more rows | `WHERE EXISTS (SELECT 1 FROM orders WHERE orders.user_id = users.id)` |
| `ALL` | Logical | TRUE if the condition holds for all values returned by a subquery | `WHERE salary > ALL (SELECT salary FROM managers)` |
| `ANY` / `SOME` | Logical | TRUE if the condition holds for at least one value returned by a subquery | `WHERE salary > ANY (SELECT salary FROM managers)` |
| `&` | Bitwise | Bitwise AND | `5 & 3` → 1 |
| `\|` | Bitwise | Bitwise OR | `5 \| 3` → 7 |
| `^` | Bitwise | Bitwise XOR | `5 ^ 3` → 6 |
| `~` | Bitwise | Bitwise NOT (one's complement) | `~5` → -6 |
| `<<` | Bitwise | Left shift | `1 << 3` → 8 |
| `>>` | Bitwise | Right shift | `8 >> 2` → 2 |
| `\|\|` / `+` | String | Concatenation (syntax varies by database) | `first_name \|\| ' ' \|\| last_name` |
| `UNION` | Set | Combines results of two queries, removing duplicates | `SELECT ... UNION SELECT ...` |
| `UNION ALL` | Set | Combines results of two queries, keeping duplicates | `SELECT ... UNION ALL SELECT ...` |
| `INTERSECT` | Set | Returns only rows present in both queries | `SELECT ... INTERSECT SELECT ...` |
| `EXCEPT` / `MINUS` | Set | Returns rows from the first query not present in the second | `SELECT ... EXCEPT SELECT ...` |
