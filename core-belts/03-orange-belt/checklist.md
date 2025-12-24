## 🥋 Promotion Requirements - Orange Belt 🧡

### Knowledge
- [ ] Can you explain the difference between concurrency and parallelism?
- [ ] Can you explain what a message queue is and why it's used?
- [ ] Can you explain what a race condition is?
- [ ] Can you explain what Prometheus is and the different types of metrics?

### Project
- [ ] Capstone project is complete.
- [ ] Handles concurrency without race conditions (verified with tests).
- [ ] Integrates with a message queue (producer + consumer).
- [ ] Exposes Prometheus metrics (latency, throughput, errors).
- [ ] Load tested: handles 10x expected traffic.
- [ ] README with performance considerations.
- [ ] Graceful shutdown + error recovery.

### Review
- [ ] Code has been reviewed by a senior engineer.
- [ ] Architecture has been reviewed and approved.
- [ ] Performance has been benchmarked.

### Success Metrics
- [ ] Load test shows p99 latency < 100ms.
- [ ] Prometheus dashboard shows metrics in real-time.
- [ ] Can handle 1 failure gracefully (message replay, retry).
- [ ] Can explain to a peer: "Why this concurrency pattern was chosen".
