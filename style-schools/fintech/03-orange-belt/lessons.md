# 💰 Fintech: Orange Belt Lessons

## Module 1: Payment Processing Fundamentals

### 1.1 How Payments Work

Payment processing involves multiple parties:

- **Cardholder**: The person making the payment (customer)
- **Merchant**: The business receiving the payment
- **Payment Processor**: Handles transactions (Stripe, PayPal)
- **Acquiring Bank**: Merchant's bank
- **Issuing Bank**: Cardholder's bank
- **Card Network**: VISA, Mastercard (routes the transaction)
- **Payment Gateway**: API interface (usually part of processor)

**The Flow**:

```
Customer → Merchant (you) → Payment Processor → Card Network → Issuing Bank
     ↓         ↓              ↓                 ↓              ↓
  Visa     Charge User   Validate Card   Route Payment    Check Funds
Card       via API       Check Fraud     Authorization    Approve/Decline
```

### 1.2 Types of Payments

- **Card Payments**: Credit/Debit card (VISA, Mastercard, Amex)
  - Synchronous: Response in seconds
  - Chargeback risk: Customer can dispute up to 180 days later
  
- **ACH Transfers**: Automated Clearing House (US domestic)
  - Asynchronous: 1-3 business days
  - Cheaper but slower
  - No chargeback risk (harder to reverse)

- **Wire Transfers**: International (SWIFT, SEPA)
  - Fast (hours to days)
  - Expensive
  - Irreversible

- **Cryptocurrencies**: Bitcoin, Ethereum, Stablecoins
  - Decentralized, immutable
  - Volatile (except stablecoins)
  - Complex regulatory status

### 1.3 Payment Intent & Authorization

**Authorization** ≠ **Settlement**

- **Authorization**: "Do you have the funds?" (tentative hold, no money transfers)
- **Capture**: Actually taking the money (happens after authorization)
- **Settlement**: Moving money to merchant's bank account (1-2 business days later)

Example timeline:

```
Day 1, 2:30 PM: Customer clicks "Buy" → Authorization (card has funds? ✓)
Day 1, 2:35 PM: Merchant ships order → Capture (take the money now)
Day 2, 6:00 AM: Batch processing → Settlement (fund merchant account)
Day 2, 10:00 AM: Money appears in merchant bank account
```

### 1.4 Idempotency in Payments

**Critical**: Networks fail. A payment request might:
- Succeed but customer doesn't see response (timeout)
- Fail but customer retries anyway
- Timeout and customer double-clicks "Pay"

**Solution**: Idempotency Keys

Every payment request includes a unique key. If same key retried:

```json
POST /payments
{
  "amount": 2000,
  "currency": "usd",
  "idempotency_key": "user_123_order_456_timestamp_2024010512345"
}

// Response: Payment created
// If customer retries with same key:
// Response: Same payment (not created again)
```

---

## Module 2: Transaction Atomicity & Safety

### 2.1 Race Conditions in Payment Systems

**Scenario**: Two concurrent transactions on same account:

Thread 1: Withdraw $100 (balance was $200)
Thread 2: Withdraw $50 (balance was $200)

Without locking:
- Thread 1 reads: balance = 200
- Thread 2 reads: balance = 200
- Thread 1 subtracts: 200 - 100 = 100, writes balance = 100
- Thread 2 subtracts: 200 - 50 = 150, writes balance = 150
- **Result**: Balance = 150, but $150 was withdrawn!

**Solution**: Database Transactions

```sql
BEGIN TRANSACTION;
  SELECT balance FROM accounts WHERE id = 123 FOR UPDATE; -- Lock the row
  UPDATE accounts SET balance = balance - 100 WHERE id = 123;
COMMIT;
```

### 2.2 ACID Guarantees

- **Atomicity**: Transaction completes fully or not at all
- **Consistency**: Database rules enforced (no invalid states)
- **Isolation**: Transactions don't interfere with each other
- **Durability**: Committed data survives system failure

Modern databases (PostgreSQL, MySQL InnoDB) provide ACID for single databases. Multi-database transactions are harder.

### 2.3 Two-Phase Commit (2PC)

For transactions spanning multiple databases (rare in modern systems):

```
Coordinator: "Will you commit T123?"
Database A: "Yes, I can" (Phase 1: Prepare)
Database B: "Yes, I can" (Phase 1: Prepare)

Coordinator: "Commit T123"
Database A: Commits (Phase 2: Commit)
Database B: Commits (Phase 2: Commit)
```

**Problem**: If Database B crashes after saying "yes" but before committing, data is inconsistent.

**Modern Alternative**: Event Sourcing or Sagas (we'll cover these in Green Belt)

### 2.4 Settlement Issues

**Problem**: Authorization doesn't guarantee settlement.

Scenario:
- 1:00 PM: Charge $100, authorization succeeds
- 1:05 PM: Merchant cancels order, void the charge
- 2:00 PM: Card issuer crashes during settlement
- 3:00 PM: Payment processor retries settlement
- Result: Money taken despite void!

**Solution**: Reconciliation (matching batch settlements with your records)

---

## Module 3: Fraud Detection Basics

### 3.1 Common Fraud Patterns

- **Card Testing**: Small transactions to test stolen card validity
- **Velocity Abuse**: Many transactions in short time (same card, different merchants)
- **Geographical Anomalies**: Transaction in Tokyo followed by transaction in New York 5 minutes later
- **Amount Anomalies**: Customer normally buys $50 items, suddenly buys $5000
- **New Card Fraud**: Stolen card used immediately
- **Chargeback Fraud**: Customer buys, receives, then claims they didn't

### 3.2 Fraud Detection Approaches

**Rules-Based**:
- If amount > $1000, require 3D Secure authentication
- If transaction count > 10 per hour, block and alert

**Machine Learning**:
- Learn patterns from historical fraud/legitimate
- Score new transactions (0-100, higher = more suspicious)
- Threshold: Block if score > 80

**Real-Time vs Batch**:
- Real-time: Approve/decline instantly (rules or low-latency ML)
- Batch: Detect fraud after-the-fact (more data, better ML)

### 3.3 3D Secure (3DS)

When fraud risk is high, require additional authentication:

```
User clicks "Pay" 
→ 3D Secure challenge (user's bank password)
→ User authenticates with bank
→ Payment completes with bank proof
```

Benefit: Bank liability shifts to the bank (not merchant).

---

## Module 4: Regulatory Compliance Introduction

### 4.1 PCI-DSS (Payment Card Industry Data Security Standard)

If you store, process, or transmit credit card data, you must comply with PCI-DSS.

**Level 1** (Highest risk):
- 6+ million transactions per year
- Full PCI-DSS compliance required
- Annual external audits
- Quarterly penetration testing

**Levels 2-4** (Lower volume):
- Self-assessment questionnaire
- Less stringent requirements

**Key Rules**:
- Don't store full card data (store only last 4 digits + metadata)
- Don't transmit card data unencrypted
- Strong access controls (who can see card data?)
- Network segmentation (isolate payment systems)
- Regular security testing

**Best Practice**: Use tokenization (payment processor stores card, gives you token instead)

### 4.2 GDPR (General Data Protection Regulation)

If processing data of EU residents:

- **Right to be Forgotten**: Users can request deletion of their data
- **Data Minimization**: Collect only what you need
- **Consent**: Must ask before using data
- **Data Breach Notification**: Report breaches within 72 hours

### 4.3 AML/KYC (Anti-Money Laundering / Know Your Customer)

- **KYC**: Verify identity of users (government ID, address)
- **AML**: Detect suspicious patterns (sudden large transfers, frequent transfers)
- **CTF**: Counter-Terrorist Financing (block transactions with sanctioned entities)

---

## Module 5: Ledger Systems & Accounting

### 5.1 Double-Entry Bookkeeping

Every transaction affects two accounts:

```
Debit: User's Balance Account -$100
Credit: Merchant's Balance Account +$100
```

This ensures: Total Debits = Total Credits (system is always balanced)

### 5.2 Account Types

- **Assets**: Money the system holds (user balances, merchant payouts)
- **Liabilities**: Money owed by the system (pending payouts, chargebacks)
- **Revenue**: Money earned (transaction fees)
- **Expenses**: Money spent (fraud losses, processing costs)

### 5.3 Transaction Ledger Design

```sql
CREATE TABLE ledger_entries (
  id BIGINT PRIMARY KEY,
  transaction_id VARCHAR(255),  -- Link to original transaction
  account_id INT,               -- Which account
  amount DECIMAL(15, 2),        -- Signed (positive = credit, negative = debit)
  entry_type VARCHAR(50),       -- "payment", "refund", "fee", etc.
  created_at TIMESTAMP,
  description VARCHAR(500),
  
  FOREIGN KEY (account_id) REFERENCES accounts(id),
  UNIQUE (transaction_id, account_id, entry_type)  -- Idempotency
);

-- Verify double-entry: Should be 0 for each transaction
SELECT transaction_id, SUM(amount) FROM ledger_entries
GROUP BY transaction_id
HAVING SUM(amount) != 0;  -- Should return nothing
```

### 5.4 Reconciliation

End of day, compare:
- **Internal ledger**: What your system recorded
- **External data**: What payment processor/bank recorded

Discrepancies indicate bugs or fraud.

```python
internal_total = db.query("SELECT SUM(amount) FROM ledger_entries")
external_total = stripe.balance.retrieve()

if internal_total != external_total:
    alert("Reconciliation mismatch: {internal_total} vs {external_total}")
```

---

## Module 6: Settlement & Payout

### 6.1 How Money Gets to Merchants

1. **Batch Settlement** (daily or weekly):
   - Payment processor aggregates transactions
   - Deducts fees and chargebacks
   - Transfers net amount to merchant's bank

2. **Timing**:
   - T+0: Same day (premium, rare)
   - T+1: Next business day
   - T+3: 3 business days (standard)

3. **Calculation**:
```
Settlement = ∑(Transactions) - ∑(Chargebacks) - Fees - Reserves
```

Example:
- Total transactions: $100,000
- Chargebacks: -$500
- Processing fee (2%): -$2,000
- Reserve (5% held for chargebacks): -$5,000
- **Settlement**: $92,500
```

### 6.2 Reserves & Rolling Reserves

Stripe (and others) hold back a percentage to cover potential chargebacks:

- **Amount**: 10-25% of daily settlement
- **Duration**: 90-180 days
- **Release**: Money returned after chargeback window closes
- **Downside**: Your cash flow is delayed

---

## Key Principles

1. **Correctness First**: A crash is better than invalid state
2. **Idempotency Everywhere**: Networks fail; design for retries
3. **Audit Trail**: Every transaction must be logged immutably
4. **Reconciliation**: Verify internal and external records match
5. **Fail Safely**: On error, don't charge the customer (better to lose money than overcharge)

---

## Further Reading

- "Payment Systems in the U.S." by Benson & Loftesness (excellent overview)
- Stripe documentation (best for practical integration)
- OWASP Payment Card Industry Data Security Standard guides
