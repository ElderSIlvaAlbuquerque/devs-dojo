# PostgreSQL - Orange Belt Lessons

## Lesson 1: Window Functions

### What You'll Learn

- [ ] ROW_NUMBER, RANK, DENSE_RANK
- [ ] LAG and LEAD functions
- [ ] Moving averages and cumulative sums
- [ ] PARTITION BY and ORDER BY

### Core Ideas

#### 1. Ranking Functions

```sql
SELECT 
    name,
    salary,
    department,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as row_num,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank,
    DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) as dense_rank
FROM employees;
```

### Why This Matters

Window functions enable complex analytics without self-joins.

---

## Lesson 2: Indexing Strategies

### What You'll Learn

- [ ] Index types (B-tree, Hash, GiST, GIN)
- [ ] When to use which index
- [ ] Multi-column indexes
- [ ] Partial indexes

### Core Ideas

#### 1. B-tree Indexes (Default)

```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_created ON orders(created_at DESC);
```

#### 2. Partial Indexes

```sql
CREATE INDEX idx_active_users ON users(email) WHERE active = true;
```

### Why This Matters

Proper indexing is crucial for query performance.

---

## Lesson 3: Query Optimization

### What You'll Learn

- [ ] EXPLAIN and EXPLAIN ANALYZE
- [ ] Reading query plans
- [ ] Identifying bottlenecks
- [ ] Optimization techniques

### Core Ideas

#### 1. EXPLAIN ANALYZE

```sql
EXPLAIN ANALYZE
SELECT * FROM orders 
WHERE user_id = 123 
AND created_at > '2024-01-01';
```

### Why This Matters

Understanding query plans enables effective optimization.

---

More lessons covering transactions, PL/pgSQL, triggers, and JSON operations...
