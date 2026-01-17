# Fintech - Green Belt Projects

Choose **ONE** project as your capstone.

---

## Project 1: Payment Orchestration Engine

**Time**: 4-5 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Multi-PSP routing, resilience, and compliance

### Requirements

**Core**:
- [ ] Auth/capture/refund/void APIs with idempotency keys
- [ ] Routing across multiple PSPs with fallback and weighting
- [ ] Circuit breakers, retries with backoff, and dead-letter queue
- [ ] Webhook verification and replay protection

**Observability**:
- [ ] SLOs for success rate and p99 latency
- [ ] Dashboards for decline reasons and provider health
- [ ] Synthetic probes per PSP

**Compliance**:
- [ ] PCI scope assessment and data handling plan
- [ ] Audit logs for money movement
- [ ] Runbooks for outages and disputes

### Deliverables
- [ ] Deployed service with IaC
- [ ] Automated tests (unit, integration, contract)
- [ ] Load and failover test results
- [ ] Architecture and compliance docs

### Evaluation Criteria
- **Reliability (30%)**: Routing, retries, failover quality
- **Compliance (25%)**: Data handling and auditability
- **Performance (20%)**: SLO adherence under load
- **Observability (15%)**: Metrics, logs, alerts
- **Docs (10%)**: Clarity and completeness

---

## Project 2: Ledger-Backed Wallet System

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Accounting correctness and reconciliation

### Requirements

**Ledger**:
- [ ] Double-entry with sequence numbers and immutability
- [ ] Balance snapshots and consistency checks
- [ ] Reconciliation jobs with exception handling

**Features**:
- [ ] Wallet operations: credit, debit, hold, release
- [ ] Idempotent operations with idempotency keys
- [ ] Settlement scheduling with cutoffs and FX

**Observability/Compliance**:
- [ ] Audit trails and access controls
- [ ] Metrics for ledger imbalance and delays
- [ ] Runbooks for breaks and manual adjustments

### Deliverables
- [ ] API + ledger schema + migrations
- [ ] Test suite with property/invariant tests
- [ ] Reconciliation reports and dashboards
- [ ] Operations and compliance docs

### Evaluation Criteria
- **Correctness (35%)**: Balanced entries and invariants
- **Reliability (25%)**: Idempotency and sequencing
- **Operations (20%)**: Reconciliation and monitoring
- **Compliance (10%)**: Auditability
- **Docs (10%)**: Clear processes

---

## Project 3: Fraud Detection and Dispute Management

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Risk controls, explainability, and dispute workflows

### Requirements

**Fraud**:
- [ ] Rules engine with velocity/device/geo checks
- [ ] ML scoring integration with feature logging
- [ ] Allow/deny lists with expiry and audit

**Disputes**:
- [ ] Dispute lifecycle with timers and SLAs
- [ ] Evidence collection and secure storage
- [ ] Notification flows for merchants and customers

**Observability**:
- [ ] Dashboards for fraud rates and false positives
- [ ] Alerts on SLA breaches and spike anomalies
- [ ] Postmortem template and example

### Deliverables
- [ ] Risk service APIs and worker jobs
- [ ] Test suite with synthetic attack scenarios
- [ ] Runbooks for fraud spikes and disputes
- [ ] Documentation of controls and data handling

### Evaluation Criteria
- **Risk Coverage (35%)**: Signal depth and accuracy
- **Reliability (20%)**: SLA adherence and routing
- **Explainability (20%)**: Logged features and audit trails
- **Operations (15%)**: Monitoring and playbooks
- **Docs (10%)**: Clarity and completeness

---

Choose one project that demonstrates you can build compliant, resilient fintech systems!
