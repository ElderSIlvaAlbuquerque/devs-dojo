# 🥋 Purple Belt: Daily Exercises

Duration: **30-45 minutes per exercise** (these are more involved than previous belts)

These exercises are designed to build intuition for distributed systems thinking. Each exercise asks you to design a simplified version of a real system.

---

## Week 1: Fundamentals

### Day 1: Design a URL Shortener (Basic)

**Task**: Design the system for a service like bit.ly or TinyURL.

**Requirements**:
- 100 million URLs shortened per day
- 10 billion redirects per month
- URLs should last for years

**Think about**:
1. How do you generate unique short codes (randomly or sequentially)?
2. How do you map short codes → long URLs?
3. What database schema would you use?
4. How would you handle 10 billion reads per month?

**Deliverable**: Draw or write out:
- Database schema (at least 1 table)
- Basic request/response flow
- One scaling bottleneck and how to solve it

---

### Day 2: Design a Social Feed (Database Layer)

**Task**: Design the database for a social media feed (like Twitter).

**Requirements**:
- 1 million active users
- Each user follows 100-1000 people
- Each user reads 100-500 posts per day
- Posts should appear in chronological order

**Think about**:
1. How do you store posts and follows?
2. How do you efficiently fetch a user's feed?
3. Where's the read bottleneck?
4. Denormalization: store a copy of the feed for each user, or compute on-read?

**Deliverable**:
- Database schema (users, posts, follows tables minimum)
- The query to fetch a user's feed
- Analysis: Is this normalized or denormalized? Why?

---

### Day 3: Cache Invalidation Problem

**Task**: Implement a caching strategy for an API.

**Scenario**: You have a product catalog API. Products have prices that change occasionally. You want to cache responses but need to ensure stale data isn't served too long.

**Think about**:
1. TTL-based expiration: How long should you cache (seconds, minutes, hours)?
2. Event-based invalidation: When a price changes, invalidate the cache
3. Cache-aside vs write-through: Which makes more sense here?

**Deliverable**:
- Decide on a strategy (TTL, event-based, or hybrid)
- Pseudocode showing how cache is checked, updated, and invalidated
- Trade-offs: Stale data risk vs computation cost

---

### Day 4: Design a Leaderboard System

**Task**: Design a real-time leaderboard for an online game.

**Requirements**:
- 1 million concurrent players
- Leaderboard updated every second
- Users want to see: global top 100, friends' positions, their own rank

**Think about**:
1. How do you rank users efficiently (sorting 1M records is expensive)?
2. What data structure is best? (Sorted set in Redis, database with indexes?)
3. How do you handle concurrent updates (multiple players scoring simultaneously)?
4. Can you use denormalization?

**Deliverable**:
- Choice of data structure and why
- How you'd update scores (transaction or eventual consistency?)
- API design (what endpoint returns the leaderboard?)

---

### Day 5: Design a Database with Read Replicas

**Task**: Scale a read-heavy application using database replication.

**Scenario**: You have a MySQL master with 80% read traffic and 20% write traffic. Queries are slow.

**Think about**:
1. How does replication work (master → replicas)?
2. How do you route reads to replicas and writes to master?
3. What if a replica lags behind the master?
4. What if a replica fails?

**Deliverable**:
- Architecture diagram: Master + 3 replicas
- Logic for choosing which replica to read from
- How you'd handle replica lag (eventual consistency)

---

## Week 2: Consistency & Transactions

### Day 6: Implement an Idempotent API Endpoint

**Task**: Design an API endpoint that is safe to retry.

**Scenario**: A payment API where network failures are common. Clients might accidentally retry payments.

**Think about**:
1. How do you prevent duplicate transactions?
2. Use an idempotency key (unique per request)
3. Store the key and result, return cached result on retry

**Deliverable**:
- Database schema for storing idempotency keys
- Pseudocode for the payment endpoint that checks for existing keys
- What if a retry comes in while the original request is still processing?

---

### Day 7: Distributed Transaction Problem

**Task**: Transfer money between two banks (two separate databases).

**Requirements**:
- Atomicity: Both debits and credits happen, or neither
- Two databases are in different regions (network latency)

**Think about**:
1. Two-phase commit: Pros and cons
2. Saga pattern: Compensating transactions
3. Why eventual consistency might be okay here

**Deliverable**:
- Compare 2PC vs Saga approach
- Pseudocode for the Saga (debit account A, then credit account B, with rollback logic)

---

### Day 8: Event Sourcing for a Bank Account

**Task**: Design an event log for a bank account instead of storing balance directly.

**Requirements**:
- Trace all account changes
- Rebuild account state at any point in time
- Audit trail for compliance

**Think about**:
1. What events would you log? (Deposit, Withdrawal, Fee, Interest)
2. How do you compute current balance? (Replay all events)
3. How do you handle out-of-order events?

**Deliverable**:
- Event schema (event type, amount, timestamp, user)
- Algorithm to compute balance from event log
- How to optimize (snapshots vs replaying 1000 events every time?)

---

### Day 9: CAP Theorem Trade-offs

**Task**: Analyze three real systems and identify which CAP property they sacrifice.

**Systems to analyze**:
1. Banking system (what consistency do you need?)
2. Social media feed (does everyone see the same posts immediately?)
3. Email system (eventual delivery vs immediate delivery?)

**Deliverable**:
- For each system: Is it CP (consistent, partition-tolerant) or AP (available, partition-tolerant)?
- Justify your choice
- What would be the consequence of choosing differently?

---

### Day 10: Design Transaction Rollback

**Task**: You're processing a batch of 1000 orders. One fails halfway through.

**Requirements**:
- Atomicity: Either all orders process or none
- Partial failure: One fails, but 500 succeeded before it
- Failure handling: Rollback all 500

**Think about**:
1. Could you use a distributed transaction?
2. How about event sourcing with compensating actions?
3. Write a state machine for order processing

**Deliverable**:
- Pseudocode for batch order processor with rollback
- State machine diagram showing success and failure paths

---

## Week 3: Asynchronous Systems

### Day 11: Publish-Subscribe System Design

**Task**: Design a pub/sub system for user notifications.

**Scenario**: When a user posts, notify all their followers. 10M posts/day, 1M followers per popular user.

**Think about**:
1. Push model: Immediately send to all followers (scalability issue)
2. Pull model: Followers check for new posts (less real-time)
3. Hybrid: Use a message queue

**Deliverable**:
- Architecture: User posts → Topic → Message Queue → Notification service
- What message queue? (Kafka for high throughput, RabbitMQ for reliability)
- How to handle slow consumers (followers with poor network)?

---

### Day 12: Message Queue Ordering

**Task**: Ensure messages are processed in order (important for financial transactions).

**Scenario**: Account transactions: Deposit $100, Withdraw $50, Check balance. Must happen in order.

**Think about**:
1. Single queue = ordered but not scalable
2. Partitioned queue: Partition by account ID (transactions for same account go to same partition)

**Deliverable**:
- Explain partitioning strategy
- Why this ensures ordering
- How many partitions do you need?

---

### Day 13: Rate Limiting Implementation

**Task**: Implement rate limiting for an API (100 requests per minute per user).

**Think about**:
1. Token bucket algorithm
2. Sliding window
3. Where to store state? (Redis for distributed)

**Deliverable**:
- Pseudocode for token bucket
- API response when rate limit exceeded (429 Too Many Requests)
- How to handle distributed rate limiting (multiple API servers)?

---

### Day 14: Event-Driven Inventory System

**Task**: Design inventory updates using events (not direct database updates).

**Scenario**: E-commerce: When order placed, inventory decrements. When order cancelled, it increments.

**Think about**:
1. Events: OrderPlaced, OrderCancelled, InventoryAdjusted
2. Event ordering and idempotency
3. Eventual consistency: Inventory might be slightly stale

**Deliverable**:
- Event schema
- Consumer logic for updating inventory
- How to handle double-processing (same event processed twice)?

---

### Day 15: Backpressure in a Pipeline

**Task**: Design a data pipeline where each stage can be slower or faster than others.

**Scenario**: Extract → Transform → Load (ETL). Extract is fast (1000 items/sec), but Transform is slow (100 items/sec).

**Think about**:
1. Without backpressure: Extract fills up memory, system crashes
2. With backpressure: Extract waits for Transform to catch up

**Deliverable**:
- Diagram showing queue sizes and backpressure
- How to implement (queue size limits, blocking?)

---

## Week 4: Monitoring & Reliability

### Day 16: Design a Monitoring Dashboard

**Task**: What metrics should you monitor for a web service?

**System**: E-commerce API (checkout, product search, user accounts)

**Think about**:
1. Business metrics: Conversion rate, revenue
2. System metrics: Latency (p50, p95, p99), throughput, error rate
3. Infrastructure metrics: CPU, memory, disk, network

**Deliverable**:
- List of 10-15 key metrics
- Which are most important for alerting?
- Sketch a dashboard layout

---

### Day 17: Alerting Strategy

**Task**: Set up alerts without alert fatigue.

**Scenario**: You have 20 services, each with 50 metrics. If you alert on all, you'll get paged 100 times/day.

**Think about**:
1. Which alerts are truly critical? (Page on-call)
2. Which are warnings? (Sent to Slack, not paging)
3. How to correlate alerts (one problem, many symptoms)?

**Deliverable**:
- Alert rules for: API latency spike, database down, out-of-memory
- Severity levels: Critical, Warning, Info
- Runbook (steps to diagnose and fix)

---

### Day 18: Distributed Tracing Architecture

**Task**: Trace a request through 5 microservices.

**Scenario**: User checkout request flows through: API Gateway → Order Service → Payment Service → Inventory Service → Notification Service.

**Think about**:
1. Correlation ID: Unique ID for the entire request
2. Span: Each service adds a span to trace
3. Latency attribution: Which service is slow?

**Deliverable**:
- Trace ID and Span IDs
- How each service adds its span
- Latency breakdown (which service took longest?)

---

### Day 19: Circuit Breaker Pattern

**Task**: Prevent cascading failures using circuit breaker.

**Scenario**: Payment service is down. Your checkout service keeps calling it, adding to the failure pile.

**Think about**:
1. States: Closed (working), Open (failing, don't call), Half-Open (testing recovery)
2. When to open: After 5 failures
3. When to close: After successful test

**Deliverable**:
- State machine diagram
- Pseudocode for circuit breaker
- What to return when circuit is open?

---

### Day 20: Graceful Degradation

**Task**: Keep the system partially functional when a critical service fails.

**Scenario**: Recommendation service fails, but users should still be able to shop.

**Think about**:
1. Fallback: Show generic/cached recommendations
2. Downgrade: Show fewer but more relevant items
3. Timeout: Don't wait forever for slow services

**Deliverable**:
- Fallback strategies for 3 different services
- Which features work degraded vs which fail entirely?

---

## Week 5: Advanced Patterns

### Day 21: Design a Notification System

**Task**: Send notifications (email, SMS, push) to millions of users.

**Requirements**:
- 100 million notifications/day
- Multiple channels (email, SMS, push notification)
- Retry failed notifications
- Deduplication (don't send same notification twice)

**Think about**:
1. Message queue: Kafka or RabbitMQ?
2. Channel selection: Which channel for which user?
3. Rate limiting: Don't overwhelm users

**Deliverable**:
- Architecture diagram
- Database schema for notification log
- How to deduplicate?

---

### Day 22: API Gateway Design

**Task**: Design an API gateway that sits in front of multiple microservices.

**Requirements**:
- Route requests to correct service
- Authentication & authorization
- Rate limiting
- Request/response transformation

**Think about**:
1. Is it a single point of failure?
2. How do you make it highly available?
3. Performance: Does it add significant latency?

**Deliverable**:
- Routing rules (e.g., /users/* → User Service)
- Authentication flow
- High availability setup (multiple gateways, load balancer)

---

### Day 23: Design a Search System

**Task**: Full-text search for an e-commerce site (search 100 million products).

**Requirements**:
- Fast search (< 100ms)
- Relevant results (matching title, description, tags)
- Handle typos (did you mean "socks"?)

**Think about**:
1. Elasticsearch or similar
2. Inverted index: Fast searching
3. Reindexing: When products change
4. Read model vs write model (search is read-optimized)

**Deliverable**:
- How you'd index a product
- Query execution (find products matching "red shirt")
- How often to reindex?

---

### Day 24: Design a Real-Time Analytics System

**Task**: Aggregate metrics in real-time (like page view counts, user online status).

**Requirements**:
- 1 million events per second
- Aggregate over 5-min windows
- Support multiple dimensions (page, user, region)

**Think about**:
1. Stream processing (Kafka Streams, Flink)
2. Windowing: Aggregate over time buckets
3. Late arrivals: Events that come in out of order
4. Exactly-once semantics: Don't double-count

**Deliverable**:
- Data pipeline: Events → Stream Processor → Aggregator → Storage
- Window definition (5-minute tumbling window)
- How to handle events arriving 1 hour late?

---

## Week 6: Production Readiness

### Day 25: Design a Batch Processing System

**Task**: Process 1 billion records overnight (ETL pipeline).

**Requirements**:
- Read from database, transform, write to warehouse
- Fault tolerance: If fails partway, resume
- Cost-effective: Use spot instances if possible

**Think about**:
1. Orchestration: Airflow, dbt
2. Partitioning: Split 1B records into 100 workers
3. Checkpointing: Save progress, resume from last checkpoint

**Deliverable**:
- DAG (Directed Acyclic Graph) of the pipeline
- Failure recovery strategy
- Cost estimation (how many machines needed?)

---

### Day 26: Blue-Green Deployment

**Task**: Deploy a new version with zero downtime.

**Requirements**:
- Two identical environments (Blue and Green)
- Switch traffic instantly if new version fails
- Rollback must be instantaneous

**Think about**:
1. Database migrations: How do you handle schema changes?
2. Backward compatibility: Old and new versions must coexist
3. Testing: Full tests before switching traffic

**Deliverable**:
- Step-by-step deployment procedure
- Database migration strategy
- Rollback procedure (how long to keep Blue environment?)

---

### Day 27: Disaster Recovery Plan

**Task**: Design recovery from a major outage (region-wide failure).

**Requirements**:
- RTO (Recovery Time Objective): 1 hour
- RPO (Recovery Point Objective): 15 minutes of data loss acceptable
- Failover to another region

**Think about**:
1. Backups: Daily snapshots, continuous replication
2. Failover: Automatic or manual?
3. Data loss: 15 min = 900 transaction might be lost
4. Testing: Regular disaster recovery drills

**Deliverable**:
- Backup strategy (snapshots, continuous replication)
- Failover procedure (automatic vs manual?)
- Recovery testing schedule

---

### Day 28: Design for Cost

**Task**: Reduce costs by 30% without sacrificing performance or reliability.

**Scenario**: Your current system: 10 servers × $1000/month = $10k/month.

**Think about**:
1. Auto-scaling: Turn off unused servers at night
2. Instance types: Are you using the right machine sizes?
3. Reserved instances: Commit to 1-year terms for discounts
4. Regional optimization: Cheaper regions for non-critical workloads

**Deliverable**:
- Cost breakdown by service
- 5 cost optimization ideas with estimated savings
- Risk analysis: Could optimizations cause issues?

---

## Reflection Questions

After completing these exercises, answer:

1. Which distributed systems problem felt hardest to reason about?
2. Where did you make consistency vs availability trade-offs?
3. What's one system you designed that wouldn't actually work in production? Why?
4. How would you test your designs? (Load testing, chaos engineering?)
5. What would change if scale increased 10x?
