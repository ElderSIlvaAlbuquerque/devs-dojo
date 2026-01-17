# Fintech Green Belt - Daily Exercises

**Duration**: 30-45 minutes per exercise  
**Goal**: Build resilient, compliant payment systems at scale

---

## Week 1: Payments and Idempotency

### Monday-Tuesday - Payment API
- [ ] Design auth/capture/refund endpoints
- [ ] Add idempotency keys with safe retries
- [ ] Simulate duplicate requests and verify single effect

### Wednesday - Webhooks
- [ ] Implement HMAC-signed webhooks with timestamp tolerance
- [ ] Add replay protection and signature rotation
- [ ] Write verifier tests for tampered payloads

### Thursday-Friday - Routing
- [ ] Build payment router with primary/secondary PSPs
- [ ] Add circuit breaker and exponential backoff
- [ ] Track decline codes and route on failure patterns

---

## Week 2: Ledger and Settlement

### Monday-Tuesday - Ledger
- [ ] Implement double-entry ledger entries for auth/capture/refund
- [ ] Add constraints: balanced entries, sequence numbers
- [ ] Build daily reconciliation report (expected vs actual)

### Wednesday - Settlement
- [ ] Model settlement windows and cutoffs
- [ ] Handle FX with locked conversion rates
- [ ] Simulate delayed settlement and fund availability

### Thursday-Friday - Disputes
- [ ] Implement dispute lifecycle states and SLAs
- [ ] Add evidence collection and deadlines
- [ ] Alert on approaching SLA breaches

---

## Week 3: Fraud and Observability

### Monday-Tuesday - Fraud Signals
- [ ] Implement rules engine (velocity, geo, device fingerprint)
- [ ] Log features for ML scoring (butterfly tests with real data anonymized)
- [ ] Build allow/deny lists with expiry

### Wednesday-Thursday - Monitoring
- [ ] Define SLOs for auth and capture latency/success
- [ ] Create dashboards for success rates and decline reasons
- [ ] Add synthetic probes to detect PSP outages

### Friday - Resilience
- [ ] Run chaos test: PSP outage and network partition
- [ ] Validate circuit breaker, reroute, and message retries
- [ ] Document incident findings and action items

---

Master these to keep money movement reliable, compliant, and observable.
