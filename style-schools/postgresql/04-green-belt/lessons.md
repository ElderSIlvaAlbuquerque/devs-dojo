# PostgreSQL - Green Belt Lessons

## Lesson 1: Replication and High Availability

### Core Concepts
- Streaming replication (physical)
- Logical replication
- Synchronous vs asynchronous
- Failover and switchover
- Split-brain prevention

### Implementation
```sql
-- Configure primary
ALTER SYSTEM SET wal_level = 'replica';
ALTER SYSTEM SET max_wal_senders = 10;

-- On replica
pg_basebackup -h primary -D /var/lib/postgresql/data -U replication -v -P
```

---

## Lesson 2: Table Partitioning

### Core Concepts
- Range partitioning
- List partitioning
- Hash partitioning
- Partition pruning
- Partition maintenance

### Implementation
```sql
CREATE TABLE orders (
    id SERIAL,
    order_date DATE NOT NULL,
    amount NUMERIC
) PARTITION BY RANGE (order_date);

CREATE TABLE orders_2024_01 
    PARTITION OF orders
    FOR VALUES FROM ('2024-01-01') TO ('2024-02-01');
```

---

## Lesson 3: Performance Tuning

### Key Parameters
- shared_buffers (25% of RAM)
- effective_cache_size (50-75% of RAM)
- work_mem (per operation)
- maintenance_work_mem
- checkpoint settings

### Vacuum and Analyze
```sql
-- Configure autovacuum
ALTER SYSTEM SET autovacuum = on;
ALTER SYSTEM SET autovacuum_naptime = '1min';

-- Manual maintenance
VACUUM ANALYZE orders;
REINDEX TABLE orders;
```

---

## Lesson 4: Backup and Recovery

### Backup Strategies
- Physical backups (pg_basebackup)
- Logical backups (pg_dump)
- Continuous archiving (WAL)
- Point-in-time recovery

### Implementation
```bash
# Base backup
pg_basebackup -D /backup -Ft -z -P

# WAL archiving
archive_command = 'cp %p /archive/%f'

# Recovery
restore_command = 'cp /archive/%f %p'
recovery_target_time = '2024-01-15 12:00:00'
```

---

## Lesson 5: Security Best Practices

### Authentication
- SSL/TLS encryption
- SCRAM-SHA-256 authentication
- Certificate authentication
- Connection limits

### Authorization
- Role-based access control
- Row Level Security (RLS)
- Column-level privileges
- Audit logging

```sql
-- Row Level Security
CREATE POLICY tenant_isolation ON orders
    FOR ALL
    TO app_user
    USING (tenant_id = current_setting('app.current_tenant')::int);
    
ALTER TABLE orders ENABLE ROW LEVEL SECURITY;
```

---

## Lesson 6: Monitoring and Diagnostics

### Key Metrics
- Connection count
- Transaction rate
- Cache hit ratio
- Replication lag
- Lock waits
- Slow queries

### Tools
- pg_stat_statements
- pg_stat_activity
- pgBadger for log analysis
- Prometheus + Grafana

```sql
-- Enable pg_stat_statements
CREATE EXTENSION pg_stat_statements;

-- Find slow queries
SELECT query, calls, mean_exec_time
FROM pg_stat_statements
ORDER BY mean_exec_time DESC
LIMIT 10;
```

---

These lessons prepare you for running PostgreSQL in production!
