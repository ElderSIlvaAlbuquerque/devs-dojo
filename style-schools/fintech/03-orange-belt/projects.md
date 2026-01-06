# 💰 Fintech: Orange Belt Projects

Choose **one** project as your capstone.

---

## Project 1: Simple Payment Processor

Build a basic payment processor that accepts payments via Stripe and stores them in a ledger.

**Requirements**:

- Accept credit card payments
- Store idempotently (prevent double-charges)
- Maintain double-entry ledger
- Support refunds
- Webhook integration with Stripe
- Basic fraud detection (rate limiting)

**Technical**:

- API: Flask/FastAPI or similar
- Database: PostgreSQL
- Payment: Stripe API
- Logging: Immutable audit log

**Deliverable**: Working payment processor with documentation

---

## Project 2: Fraud Detection Engine

Build a system that detects suspicious payment patterns in real-time.

**Requirements**:

- Rule-based detection (velocity, amount anomaly, geo anomaly)
- ML-based detection (train on historical fraud)
- Dashboard showing flagged transactions
- Adjustable thresholds
- Alert on suspected fraud

**Deliverable**: Fraud detection system with dashboard

---

## Project 3: Ledger & Reconciliation System

Build a complete ledger system with reconciliation.

**Requirements**:

- Double-entry bookkeeping for all transactions
- Account balance tracking and caching
- Fee accounting and reporting
- Daily reconciliation with external data
- Compliance-ready audit trail

**Deliverable**: Ledger system with working reconciliation

---

Choose one, build it, document it. You'll present to a peer engineer.
