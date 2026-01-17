# 🥋 Purple Belt: Promotion Checklist

This checklist confirms your readiness for promotion to the **Blue Belt** (Staff Engineer level).

**Promotion Requirements**: Complete **ALL** items marked `[ ]`.

---

## Lessons & Concepts (Understanding)

- [ ] **Scalability**: Explain vertical vs horizontal scaling with examples
- [ ] **Load Balancing**: Describe 3 load balancing algorithms and when to use each
- [ ] **Caching**: Explain cache invalidation strategies (TTL, event-based, write-through)
- [ ] **Databases at Scale**: Design a simple schema and explain how to shard it
- [ ] **CAP Theorem**: State the theorem and explain CP vs AP trade-offs
- [ ] **Consistency Models**: Explain strong, eventual, and causal consistency
- [ ] **Distributed Transactions**: Compare 2PC vs Saga pattern with pros/cons
- [ ] **Idempotency**: Explain idempotency and design an idempotent API endpoint
- [ ] **Message Queues**: Name 3 message queue systems and their use cases
- [ ] **Pub/Sub**: Explain publish-subscribe pattern and fan-out strategies
- [ ] **Event-Driven Architecture**: Design a simple event-driven system
- [ ] **Rate Limiting**: Implement or explain token bucket algorithm
- [ ] **Observability**: Define logs, metrics, traces and their purposes
- [ ] **Monitoring**: Identify key metrics for a system and design alert thresholds
- [ ] **Distributed Tracing**: Explain how to trace requests across services
- [ ] **Resilience Patterns**: Explain circuit breaker, bulkhead, timeout, graceful degradation
- [ ] **Microservices**: Explain benefits and challenges vs monolith
- [ ] **Data Consistency in Microservices**: Design approach to keep services in sync
- [ ] **Search at Scale**: Explain full-text search and inverted indexes
- [ ] **Stream Processing**: Explain windowing, ordering, exactly-once semantics
- [ ] **Cost Optimization**: Identify cost levers (auto-scaling, instance types, regions)
- [ ] **Batch Processing**: Design a simple ETL pipeline
- [ ] **Deployment**: Explain blue-green and canary deployments
- [ ] **Disaster Recovery**: Define RTO, RPO and design a recovery plan

---

## Daily Exercises (Practice)

- [ ] **Completed 25 daily exercises** (at least 4 per week)
  - [ ] Week 1: URL Shortener, Social Feed, Cache Invalidation, Leaderboard, Replicas (5 exercises)
  - [ ] Week 2: Idempotency, Distributed Transactions, Event Sourcing, CAP Trade-offs, Rollback (5 exercises)
  - [ ] Week 3: Pub/Sub, Message Ordering, Rate Limiting, Event-Driven, Backpressure (5 exercises)
  - [ ] Week 4: Monitoring, Alerting, Distributed Tracing, Circuit Breaker, Graceful Degradation (5 exercises)
  - [ ] Week 5+: Advanced Patterns - Notifications, API Gateway, Search, Real-Time Analytics (5 exercises)

- [ ] **Exercise Quality**:
  - [ ] Diagrams included (hand-drawn or digital)
  - [ ] Assumptions stated clearly
  - [ ] Trade-offs analyzed
  - [ ] Scaling strategy explained

---

## Capstone Project

Choose **one** system design project (Twitter, Uber, E-commerce, Messaging, Video Streaming, Trading, CDN):

### Document Requirements

- [ ] **Architecture Document** (10-15 pages minimum)
  - [ ] Executive summary (1 page): Problem statement, scale, key challenges
  - [ ] High-level architecture (2-3 pages with diagrams)
  - [ ] Database design (schema, indexing, partitioning strategy)
  - [ ] API design (endpoints, request/response formats)
  - [ ] Caching strategy (what to cache, invalidation, CDN)
  - [ ] Real-time systems (if applicable: WebSocket, Kafka, streaming)
  - [ ] Scalability analysis (how to handle 10x, 100x load)
  - [ ] High availability (redundancy, failover, monitoring)
  - [ ] Data consistency model (strong vs eventual)
  - [ ] Cost analysis (infrastructure, operational)
  - [ ] Deployment strategy (rolling updates, rollback)
  - [ ] Known limitations and trade-offs

### Completeness

- [ ] **Architecture covers all major components**:
  - [ ] API/Gateway layer
  - [ ] Application/Business logic layer
  - [ ] Data layer (databases, caches, search)
  - [ ] Real-time layer (if needed: WebSocket, message queues)
  - [ ] Analytics/Monitoring layer

- [ ] **Database design is production-ready**:
  - [ ] Schema designed with normalization/denormalization trade-offs noted
  - [ ] Indexes identified for critical queries
  - [ ] Partitioning/sharding strategy explained
  - [ ] Replication strategy for high availability

- [ ] **Scalability is well-thought-out**:
  - [ ] Identified all major bottlenecks
  - [ ] Proposed solutions for each bottleneck
  - [ ] Explained how system would scale 10x, 100x, 1000x
  - [ ] Cost implications of scaling

- [ ] **Reliability and disaster recovery**:
  - [ ] High availability strategy (multiple zones, regions)
  - [ ] Failover mechanisms
  - [ ] Backup and recovery procedures
  - [ ] Monitoring and alerting strategy
  - [ ] RTO and RPO defined

- [ ] **Real-world pragmatism**:
  - [ ] Balanced over-engineering (don't use bleeding-edge tech for simple problems)
  - [ ] Operational complexity considered
  - [ ] Trade-offs explained (don't just list pros and cons, make decisions)
  - [ ] Cost-benefit analysis where relevant

### Presentation & Code Review

- [ ] **Presentation (30 minutes)**:
  - [ ] Clear explanation of problem and scale
  - [ ] High-level architecture with good visuals
  - [ ] Deep dive into 2-3 most complex components
  - [ ] Confidence in answering follow-up questions
  - [ ] Honest about trade-offs and limitations

- [ ] **Peer/Mentor Review**:
  - [ ] Another engineer reviewed your design
  - [ ] You incorporated feedback
  - [ ] Design document updated based on review
  - [ ] Follow-up questions answered

---

## Code & Implementation (Optional but Recommended)

- [ ] **Implemented critical components** (choose 2-3):
  - [ ] Prototype of the API (basic endpoints)
  - [ ] Database schema and migrations
  - [ ] Caching layer (Redis, in-memory)
  - [ ] Message queue producer/consumer
  - [ ] Simple rate limiter
  - [ ] Distributed tracing instrumentation

- [ ] **Code is tested**:
  - [ ] Unit tests for business logic
  - [ ] Integration tests for critical flows
  - [ ] Load testing (how many requests/second?)

---

## Communication & Documentation

- [ ] **Architecture is well-documented**:
  - [ ] Diagrams are clear and labeled
  - [ ] Assumptions stated explicitly
  - [ ] Trade-offs documented
  - [ ] Decisions explained (not just "I chose X")

- [ ] **Can explain decisions to others**:
  - [ ] Defended database choice
  - [ ] Explained caching strategy
  - [ ] Justified trade-offs (consistency vs availability, cost vs performance)
  - [ ] Answered "what if" questions (what if this service fails?)

---

## Advanced Topics (Choose at least 2)

Choose 2+ advanced topics to demonstrate deep knowledge:

- [ ] **Advanced Consistency**:
  - [ ] Implemented or explained CQRS (Command Query Responsibility Segregation)
  - [ ] Designed event sourcing for a component
  - [ ] Explained causal or session consistency

- [ ] **Advanced Caching**:
  - [ ] Designed multi-level caching (L1: app, L2: Redis, L3: CDN)
  - [ ] Explained cache stampede and thundering herd problems
  - [ ] Designed cache warming strategy

- [ ] **Advanced Queuing**:
  - [ ] Designed dead-letter queues for failed messages
  - [ ] Explained exactly-once semantics and how to achieve it
  - [ ] Designed backpressure mechanism

- [ ] **Advanced Monitoring**:
  - [ ] Designed custom metrics beyond standard (latency, throughput, errors)
  - [ ] Explained correlation and causality in observability
  - [ ] Designed alert tuning to reduce false positives

- [ ] **Security & Compliance**:
  - [ ] Designed authentication/authorization flow
  - [ ] Explained how to protect data in transit and at rest
  - [ ] Designed audit logging for compliance

- [ ] **Cost Optimization**:
  - [ ] Calculated TCO (total cost of ownership)
  - [ ] Identified 3+ cost optimization opportunities
  - [ ] Trade-off analysis: cost vs performance/reliability

---

## Reflection & Growth

- [ ] **Written reflection** (1-2 pages):
  - [ ] What was hardest about this design?
  - [ ] What would you do differently if starting over?
  - [ ] How would you approach this differently with infinite resources?
  - [ ] How would you approach this differently with minimal resources?
  - [ ] What's one system design principle you'll apply in future work?

- [ ] **Ready for next belt**:
  - [ ] Confident in designing systems at scale
  - [ ] Can identify trade-offs and make decisions
  - [ ] Can handle ambiguity and make reasonable assumptions
  - [ ] Understand that "it depends" is a valid answer (context matters)

---

## Promotion Criteria Summary

**To promote from System Design (05) to Blue Belt (06), you must**:

1. ✅ Complete all lessons and concepts section (demonstrate understanding)
2. ✅ Complete 25+ daily exercises (demonstrate practice)
3. ✅ Choose and complete ONE capstone project (demonstrate application)
4. ✅ Present capstone to peer or mentor (demonstrate communication)
5. ✅ Choose 2+ advanced topics (demonstrate depth)
6. ✅ Write reflection (demonstrate metacognition)

---

## Sign-Off

- [ ] **Self-Assessment**: I am ready for promotion
  - Date: _________
  
- [ ] **Peer/Mentor Review**: This engineer is ready for promotion
  - Name: _________
  - Date: _________
  - Comments: ___________________________________________

---

## Next Steps

Once promoted to **Blue Belt** (06-blue-belt), you'll study:
- Staff Engineer-level topics
- Technical leadership and mentoring
- Architecture authority and tech strategy
- Moving toward Principal Engineer track
