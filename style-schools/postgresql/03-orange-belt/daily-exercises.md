# PostgreSQL Orange Belt - Daily Exercises

**Duration**: 20-30 minutes per exercise  
**Goal**: Master intermediate PostgreSQL features

---

## Week 1: Complex Queries

### Monday - JOINs

- [ ] **Exercise** (25 min): Practice all JOIN types
  - INNER JOIN
  - LEFT/RIGHT/FULL OUTER JOIN
  - CROSS JOIN
  - SELF JOIN

### Tuesday - Subqueries

- [ ] **Exercise** (20 min): Write correlated and non-correlated subqueries
  - WHERE clause subqueries
  - SELECT clause subqueries
  - FROM clause subqueries

### Wednesday - CTEs

- [ ] **Exercise** (25 min): Common Table Expressions

  ```sql
  WITH sales_summary AS (
      SELECT 
          product_id,
          SUM(amount) as total_sales,
          COUNT(*) as order_count
      FROM orders
      GROUP BY product_id
  )
  SELECT 
      p.name,
      s.total_sales,
      s.order_count
  FROM products p
  JOIN sales_summary s ON p.id = s.product_id
  ORDER BY s.total_sales DESC;
  ```

### Thursday - Window Functions

- [ ] **Exercise** (30 min): ROW_NUMBER, RANK, DENSE_RANK

### Friday - Aggregations

- [ ] **Exercise** (25 min): GROUP BY with HAVING, ROLLUP, CUBE

---

## Week 2: Performance & Indexing

### Monday - EXPLAIN ANALYZE

- [ ] **Exercise** (30 min): Analyze query performance
  - Run EXPLAIN ANALYZE
  - Identify sequential scans
  - Find slow operations

### Tuesday-Wednesday - Indexing

- [ ] **Exercise** (45 min): Create and test indexes
  - B-tree indexes
  - Partial indexes
  - Multi-column indexes
  - Test query performance before/after

### Thursday - Query Optimization

- [ ] **Exercise** (30 min): Optimize slow queries
  - Rewrite subqueries as JOINs
  - Add appropriate indexes
  - Avoid SELECT *

### Friday - Transactions

- [ ] **Exercise** (25 min): Practice transaction isolation levels

---

## Week 3: Advanced Features

### Monday-Tuesday - PL/pgSQL Functions

- [ ] **Exercise** (45 min): Create stored procedures

### Wednesday - Triggers

- [ ] **Exercise** (30 min): Implement audit logging trigger

### Thursday - JSON Operations

- [ ] **Exercise** (30 min): Work with JSONB data

### Friday - Full-Text Search

- [ ] **Exercise** (30 min): Implement search with tsvector

---

Practice daily to build strong PostgreSQL skills!
