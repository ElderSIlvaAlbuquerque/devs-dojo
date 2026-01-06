# 🥋 Purple Belt: Core Lessons

## Overview

The Purple Belt covers the art and science of building large-scale distributed systems that are scalable, reliable, and maintainable. As AI increasingly handles code generation, the ability to think architecturally and design robust systems becomes a critical differentiator for senior engineers.

This belt focuses on **foundational distributed systems concepts** that apply across all domains (web services, fintech, AI/ML, blockchain, etc.).

---

## Week 1: Fundamentals & Core Concepts

### 1. The Scalability Problem

- **Vertical Scaling**: Adding more resources to a single machine (CPU, RAM, disk)
- **Horizontal Scaling**: Distributing load across multiple machines
- **Why it matters**: As systems grow, single machines become bottlenecks
- **Trade-offs**: Horizontal scaling adds complexity but provides flexibility

### 2. Load Balancing

- **Purpose**: Distribute incoming requests across multiple servers
- **Algorithms**: Round-robin, least connections, IP hash, weighted routing
- **Sticky Sessions**: Keeping a user's requests on the same server
- **Health Checks**: Detecting and removing failed servers from rotation

### 3. Caching Strategies

- **In-Memory Caching**: Redis, Memcached for sub-millisecond latency
- **Cache Invalidation**: "There are only two hard things in Computer Science: cache invalidation and naming things"
- **Cache Patterns**: Cache-aside, write-through, write-behind
- **Cache Eviction**: LRU, LFU, TTL-based expiration

### 4. Databases at Scale

- **Replication**: Master-slave, master-master (eventual consistency tradeoffs)
- **Sharding**: Horizontal partitioning of data (hash-based, range-based, geo-based)
- **Read Replicas**: Scaling read operations
- **Write Bottlenecks**: When master becomes the limiting factor

---

## Week 2: Consistency & Distributed Transactions

### 5. The CAP Theorem

- **Consistency**: All nodes see the same data at the same time
- **Availability**: System responds to requests even if some nodes fail
- **Partition Tolerance**: System continues when network partitions occur
- **The Trade-off**: You can guarantee at most 2 of 3. Most systems choose AP over C (eventual consistency)
- **Real-world**: Network partitions WILL happen; design for it

### 6. Consistency Models

- **Strong Consistency**: All reads see latest writes (like SQL transactions)
- **Eventual Consistency**: Reads may see stale data temporarily (like DNS)
- **Causal Consistency**: Causally related operations stay ordered
- **When to use each**: Trade latency for consistency guarantees

### 7. Distributed Transactions

- **Two-Phase Commit (2PC)**: Atomic commits across databases (slow, blocking)
- **Saga Pattern**: Long-running transactions with compensating actions
- **Event Sourcing**: Store sequence of events rather than current state
- **CQRS**: Separate read and write models for performance

### 8. Idempotency & Retries

- **Idempotent Operations**: Same operation applied multiple times = same result
- **Why it matters**: Networks fail; retries are essential
- **Idempotency Keys**: Deduplication tokens to prevent duplicate processing
- **Retry Strategies**: Exponential backoff, jitter, circuit breakers

---

## Week 3: Asynchronous Systems & Message Queues

### 9. Pub/Sub & Message Queues

- **Synchronous**: Direct request-response (fast, tightly coupled)
- **Asynchronous**: Producers and consumers are decoupled (slower, more resilient)
- **Use Cases**: Event notifications, batch processing, rate limiting
- **Trade-offs**: Easier to scale but harder to reason about ordering

### 10. Message Queue Systems

- **RabbitMQ**: Traditional message broker (AMQP)
- **Apache Kafka**: High-throughput distributed log (event streaming)
- **AWS SQS**: Managed queue service (simpler, less control)
- **Design Decisions**: At-least-once vs exactly-once delivery semantics

### 11. Event-Driven Architecture

- **Events as the Source of Truth**: Immutable log of what happened
- **Event Ordering**: Global order vs per-partition order
- **Replay-ability**: Rebuild state from event log
- **Consumer Groups**: Scaling event consumption

### 12. Rate Limiting & Backpressure

- **Token Bucket**: Smooth rate limiting (allow bursts)
- **Leaky Bucket**: Strict rate limiting
- **Backpressure**: Upstream systems slow down when downstream is overwhelmed
- **Importance**: Preventing cascading failures

---

## Week 4: Monitoring, Observability & Reliability

### 13. Observability (Logs, Metrics, Traces)

- **Logs**: Discrete events (what happened), but unstructured and expensive to query at scale
- **Metrics**: Time-series data (CPU, latency, QPS), aggregated and cheap
- **Traces**: Request paths through microservices (showing dependencies and latency)
- **Log Aggregation**: ELK stack, Loki, CloudWatch for centralized search
- **Structured Logging**: JSON logs for better querying and filtering

### 14. Metrics & Alerting

- **Key Metrics**: Latency (p50, p99), throughput (QPS), error rate, saturation
- **Monitoring Tools**: Prometheus, Grafana, DataDog
- **Dashboards**: Real-time visibility into system health
- **Alerting**: Page on-call only for severe issues (alert fatigue is real)

### 15. Distributed Tracing

- **Correlation IDs**: Track requests across services
- **Span Relationships**: Understanding call stacks in microservices
- **Tools**: Jaeger, Zipkin, Lightstep
- **Latency Attribution**: Finding where time is spent in complex systems

### 16. Resilience Patterns

- **Circuit Breaker**: Fail fast when downstream is failing
- **Bulkhead Pattern**: Isolate failure (don't let one bad service take down everything)
- **Timeout & Deadline**: Never wait forever for responses
- **Graceful Degradation**: Degrade service quality rather than failing completely

---

## Week 5: Advanced Patterns & Real-World Complexity

### 17. Microservices Architecture

- **Monolith vs Microservices**: Tradeoff between simplicity and scalability
- **Service Boundaries**: Organizing around business capabilities, not technology
- **API Gateway**: Single entry point, routing, authentication, rate limiting
- **Service Discovery**: Dynamic registration and discovery of services

### 18. Data Consistency in Microservices

- **Shared Databases**: Simple but violates service boundaries
- **Database per Service**: Isolated but complicates transactions
- **Event-Driven Consistency**: Use events to keep services in sync
- **Eventual Consistency Everywhere**: Design for it

### 19. Search & Indexing at Scale

- **Full-Text Search**: Elasticsearch, Solr (separate read-optimized copies)
- **Inverted Indexes**: Fast searching but requires reindexing
- **Search-as-You-Type**: Trie-based autocomplete
- **Faceted Search**: Filtering and drilling down

### 20. Real-Time Data Processing

- **Stream Processing**: Kafka Streams, Apache Flink
- **Windowing**: Aggregating data over time windows
- **Late Arrivals**: Data that arrives out of order
- **Exactly-Once Semantics**: Hard problem in distributed systems

---

## Week 6: Cost Optimization & Production Readiness

### 21. Resource Utilization & Cost

- **CPU-bound vs I/O-bound**: Different scaling strategies
- **Auto-scaling**: Based on metrics (CPU, memory, custom metrics)
- **Spot Instances & Preemptible VMs**: Cheaper but can be interrupted
- **Cost Attribution**: Measuring unit economics (cost per request, per user)

### 22. Batch Processing

- **MapReduce & Hadoop**: The original batch processing framework
- **Data Warehousing**: OLAP systems (Snowflake, BigQuery, Redshift)
- **ETL Pipelines**: Extract-Transform-Load for data integration
- **Scheduling**: Airflow, dbt for orchestrating workflows

### 23. Deployment Strategies

- **Blue-Green Deployments**: Two identical environments for zero-downtime deploys
- **Canary Deployments**: Roll out to small % of users first
- **Feature Flags**: Decouple deployment from release
- **Rollback Plans**: Fast recovery when things go wrong

### 24. Disaster Recovery & High Availability

- **RTO (Recovery Time Objective)**: How quickly to recover
- **RPO (Recovery Point Objective)**: How much data loss is acceptable
- **Backups**: Regular snapshots, tested recovery procedures
- **Geographic Redundancy**: Resilient to regional outages

---

## Key Principles

1. **Measure & Monitor Everything**: You can't optimize what you don't measure
2. **Embrace Failure**: Distributed systems fail; design for graceful degradation
3. **Simplicity is Expensive**: Fight complexity, but don't oversimplify
4. **Eventually Consistent**: Accept that strong consistency is often not worth the cost
5. **Automation Over Manual Processes**: Reduce human error in operations
6. **Think in Terms of Patterns**: Don't reinvent; apply proven distributed systems patterns

---

## Further Reading & Resources

- "Designing Data-Intensive Applications" by Martin Kleppmann (essential reading)
- "System Design Interview" by Alex Xu (practical problems)
- DDIA Papers & Blog Posts
- High Scalability blog (case studies of real systems)
