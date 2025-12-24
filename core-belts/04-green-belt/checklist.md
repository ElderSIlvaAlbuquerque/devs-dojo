## 🥋 Promotion Requirements - Green Belt 💚

### Knowledge
- [ ] Can you explain the concept of a microservice and its trade-offs?
- [ ] Can you explain what distributed tracing is and why it's important in a microservices architecture?
- [ ] Can you explain the basics of Domain-Driven Design?
- [ ] Can you explain what an API gateway is and what it's used for?

### Project
- [ ] Capstone project is complete.
- [ ] 2-3 independent services with clear boundaries.
- [ ] Services communicate via async (Kafka) or sync (REST/gRPC).
- [ ] Distributed tracing works: can trace request across services.
- [ ] Database optimized (indexes, queries explain-planned).
- [ ] Service discovery working (hardcoded OK for now).
- [ ] README with architecture diagram.

### Review
- [ ] Code has been reviewed by a senior engineer.
- [ ] Architecture has been reviewed and approved.

### Success Metrics
- [ ] Trace a request through all 3 services in Jaeger.
- [ ] Each service has a different database (microservices pattern).
- [ ] Query latency < 50ms even with 1M+ records.
- [ ] 1 database index prevents a full table scan.
- [ ] Can deploy 1 service independently without others.
