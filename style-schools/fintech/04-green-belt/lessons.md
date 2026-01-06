````markdown
# Fintech - Green Belt Lessons

## Lesson 1: Payment Orchestration and Idempotency

### Core Concepts
- Auth/capture/refund flows and state machines
- Idempotency keys, deduplication windows, and sequencing
- Retry strategies (idempotent vs non-idempotent operations)

### Implementation (TypeScript)
```ts
import { randomUUID } from "crypto";

async function handlePayment(req, res) {
  const idempotencyKey = req.headers["idempotency-key"] ?? randomUUID();
  const existing = await repo.findByKey(idempotencyKey);
  if (existing) return res.json(existing.result);

  const result = await processor.authorize(req.body);
  await repo.save({ key: idempotencyKey, result });
  return res.json(result);
}
```

---

## Lesson 2: Ledgers and Reconciliation

### Core Concepts
- Double-entry accounting, balanced debits/credits
- Ledger sequencing and immutability
- Reconciliation: expected vs actual settlements

### Ledger Entry Example (SQL)
```sql
INSERT INTO ledger_entries (id, account_id, amount, direction, currency, sequence)
VALUES (:id, :account, :amount, 'debit', :currency, nextval('ledger_seq'));
```

### Reconciliation Checklist
- Daily reports with cuts at T+N windows
- FX handling and rounding rules
- Exception queues for breaks and manual review

---

## Lesson 3: Webhooks and Security

### Core Concepts
- HMAC signing, timestamp tolerance, and replay defense
- Signature rotation and key management
- Idempotent webhook handlers

### Verification Snippet (Node.js)
```ts
import crypto from "crypto";

function verifySignature(payload: string, signature: string, secret: string, timestamp: number): boolean {
  const message = `${timestamp}.${payload}`;
  const expected = crypto.createHmac("sha256", secret).update(message).digest("hex");
  return crypto.timingSafeEqual(Buffer.from(expected), Buffer.from(signature));
}
```

---

## Lesson 4: Fraud Detection and Disputes

### Core Concepts
- Rules engines (velocity, device, geo) and ML scores
- Feature logging and explainability
- Dispute lifecycle states and SLAs

### Rules Engine Outline (Python)
```python
rules = [
    lambda ctx: ctx["amount"] > 5000,
    lambda ctx: ctx["country"] not in ctx["allowed_countries"],
    lambda ctx: ctx["velocity_hour"] > 5,
]

def evaluate(ctx):
    return any(rule(ctx) for rule in rules)
```

---

## Lesson 5: Observability and SLOs

### Core Concepts
- SLOs for auth/capture latency and success rate
- Decline code taxonomy and alerting
- Synthetic monitoring for PSP health

### Metrics to Track
- Auth/capture/refund p50/p95/p99 latency
- Success vs decline rates by code and provider
- Queue depth and retry counts
- Ledger imbalance and reconciliation breaks

---

These lessons prepare you to operate payments systems safely and reliably at scale.
````