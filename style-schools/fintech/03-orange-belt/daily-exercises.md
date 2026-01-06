# 💰 Fintech: Orange Belt Daily Exercises

Duration: **40-60 minutes per exercise**

These exercises build practical payment system skills.

---

## Week 1: Payment Processing

### Day 1: Integrate Stripe Payment

Build a simple API endpoint that processes a payment through Stripe.

**Task**:
1. Create a `/charge` endpoint that accepts amount and card token
2. Call Stripe API to create and confirm a payment intent
3. Return success/failure response
4. Handle errors (invalid card, insufficient funds, etc.)

**Deliverable**: Working endpoint with error handling

---

### Day 2: Implement Idempotency

Add idempotency to the payment endpoint using idempotency keys.

**Task**:
1. Add idempotency_key to request
2. Store key + result in database
3. Return cached result if key already processed
4. Test by submitting same request twice

**Deliverable**: Idempotent payment API

---

### Day 3: Webhook Processing

Handle Stripe webhooks (events like payment success, failure).

**Task**:
1. Create endpoint to receive Stripe webhooks
2. Verify webhook signature (prevent spoofing)
3. Update order status based on event
4. Log events for audit trail

**Deliverable**: Webhook handler with verification

---

### Day 4: Card Tokenization

Don't store full card data; use tokenization instead.

**Task**:
1. Generate a Stripe token from card data
2. Store token (not card data)
3. Charge using token instead of card
4. Verify you can't decrypt the token (it's secure)

**Deliverable**: Tokenization implementation

---

### Day 5: Multiple Payment Methods

Support credit card, ACH, and Apple Pay.

**Task**:
1. Create payment method selector
2. Handle each payment type differently
3. Store which method was used
4. Enable retry with different payment method if first fails

**Deliverable**: Multi-method payment processor

---

## Week 2: Fraud & Safety

### Day 6: Rate Limiting for Payments

Prevent card testing (rapid small charges).

**Task**:
1. Implement rate limiting (max 5 charges per hour per card)
2. Implement velocity check (max 10 charges per day per user)
3. Block and alert on violations
4. Log all blocked attempts

**Deliverable**: Rate limiting system

---

### Day 7: 3D Secure Flow

Implement 3D Secure for high-risk transactions.

**Task**:
1. Detect high-risk transactions (new card, large amount, etc.)
2. Initiate 3D Secure challenge
3. Handle user auth callback
4. Complete payment after successful auth

**Deliverable**: 3D Secure integration

---

### Day 8: Fraud Pattern Detection

Build simple fraud detection.

**Task**:
1. Implement rules: amount > $10k, block
2. Geographic anomaly: TX → NY in 5 min, flag
3. Card testing: $1 charge, block until verified
4. Dashboard showing flagged transactions

**Deliverable**: Fraud detection rules

---

### Day 9: Transaction Logging

Log every payment attempt immutably.

**Task**:
1. Create audit log table
2. Log: timestamp, user, card (last 4), amount, status
3. No updates allowed (immutable log)
4. Query tool to search logs

**Deliverable**: Immutable audit log system

---

### Day 10: Refund Processing

Allow refunds and handle edge cases.

**Task**:
1. Implement refund endpoint
2. Only allow refund within 90 days
3. Prevent double refunds (idempotency)
4. Update ledger (debit merchant, credit user)

**Deliverable**: Refund system with safeguards

---

## Week 3: Ledger & Accounting

### Day 11: Double-Entry Ledger

Implement basic double-entry bookkeeping.

**Task**:
1. Create ledger_entries table
2. For each payment, create two entries (debit + credit)
3. Verify balance equation: sum(debits) == sum(credits)
4. Query sample transactions

**Deliverable**: Ledger system with verification

---

### Day 12: Account Balances

Calculate and cache account balances.

**Task**:
1. Calculate balance from ledger (sum all entries)
2. Cache in accounts table (for performance)
3. Verify cached matches ledger periodically
4. Implement balance transfer (atomic operation)

**Deliverable**: Balance tracking system

---

### Day 13: Fee Accounting

Track fees separately in ledger.

**Task**:
1. On payment, add fee entry
2. Fee goes to revenue account, not user account
3. Dashboard showing total fees collected
4. Calculate actual payout: payment - fee

**Deliverable**: Fee accounting

---

### Day 14: Multi-Currency Ledger

Support multiple currencies in ledger.

**Task**:
1. Add currency field to ledger entries
2. Separate balance by currency
3. Implement currency conversion (using exchange rate)
4. Convert to base currency for reporting

**Deliverable**: Multi-currency ledger

---

### Day 15: Reconciliation

Match internal ledger with external payment processor.

**Task**:
1. Download settlement data from Stripe
2. Compare with internal ledger
3. Identify discrepancies
4. Alert if mismatch > $0.01

**Deliverable**: Reconciliation tool

---

## Reflection

After completing these exercises:

1. How would you handle a failed refund?
2. What if reconciliation shows a $1000 mismatch?
3. How would you prevent double-charging?
4. What other fraud patterns should be detected?
5. If Stripe API is down, how do you queue payments?
