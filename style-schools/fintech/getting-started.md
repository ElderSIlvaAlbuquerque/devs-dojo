# 💰 Fintech: Getting Started

This guide will get you set up to start learning fintech engineering.

## Prerequisites

Before diving into fintech, you should have:

1. ✅ Completed **04-green-belt** from core belts (understanding of microservices, distributed systems)
2. ✅ Completed or be taking **05-purple-belt** (understanding of transactions, consistency)
3. ✅ Basic knowledge of: databases (SQL), APIs (REST), concurrency concepts
4. ✅ Interest in financial systems or payments

## Concepts You Should Know

Before starting, ensure you understand:

- **ACID Transactions**: Atomicity, Consistency, Isolation, Durability
- **Eventual Consistency**: When distributed systems can't have strong consistency
- **Idempotency**: Operations safe to retry without side effects
- **Message Queues**: Kafka, RabbitMQ for event logging
- **Database Indexes & Optimization**: For transaction-heavy systems
- **API Design**: REST, error handling, retry logic

If you're unfamiliar with any of these, review the relevant core belt section first.

## What You'll Build

### Orange Belt Projects

1. **Simple Payment Processor**: Process credit card payments (using Stripe API or similar)
2. **Fraud Detection Engine**: Real-time pattern matching for suspicious transactions
3. **Ledger System**: Implement double-entry bookkeeping

### Green Belt Projects

1. **Multi-Currency Payment System**: Handle currency conversion, settlement delays
2. **Settlement & Reconciliation**: Match transactions with bank statements
3. **PCI-DSS Compliant System**: Build with security and compliance in mind

## Tech Stack Suggestions

You can use any tech you're comfortable with. Popular choices for fintech:

**Languages**: Python, Go, Java, C++ (performance)
**Databases**: PostgreSQL (strong ACID guarantees), CockroachDB (distributed)
**Message Queues**: Kafka (immutable log for compliance), RabbitMQ (reliability)
**Payment APIs**: Stripe (most developer-friendly), PayPal (enterprise)
**Monitoring**: Datadog, New Relic (fintech-specialized monitoring)

## Getting Started

### Step 1: Pick a Payment Provider

You'll likely integrate with one in your projects. Options:

- **Stripe** (recommended): Simple API, great docs, test mode
- **Square**: Good for brick-and-mortar + online
- **PayPal**: Enterprise, widely trusted
- **Wise (formerly TransferWise)**: Multi-currency specialist

Create a test account (free tier available).

### Step 2: Understand One Payment Method Deeply

Pick **one** and learn it thoroughly:

- **Credit Cards**: VISA, Mastercard, American Express (Stripe handles this)
- **ACH Transfers**: Clearing House Automated Clearing House (slower, cheaper)
- **Wire Transfers**: Fast, expensive, international
- **Cryptocurrencies**: Bitcoin, Ethereum (decentralized)

Start with credit cards (most common, well-documented).

### Step 3: Set Up Your Environment

Create a simple project:

```bash
# Python example
python3 -m venv venv
source venv/bin/activate
pip install stripe flask sqlalchemy psycopg2

# Or Go
go mod init github.com/yourname/fintech-dojo
```

### Step 4: Build a Test Transaction

Your first project: Process a payment through Stripe test mode.

```python
import stripe

stripe.api_key = "sk_test_..."  # Get from Stripe dashboard

# Create a payment intent
intent = stripe.PaymentIntent.create(
    amount=2000,  # $20.00
    currency="usd",
    payment_method="pm_card_visa",  # Test card
    confirm=True,
)

print(f"Payment status: {intent.status}")  # "succeeded"
```

### Step 5: Start the Orange Belt

Begin with [03-orange-belt/lessons.md](03-orange-belt/lessons.md).

You now have:
- [ ] A test Stripe account
- [ ] A development environment
- [ ] A simple payment integration
- [ ] Ready to learn payment processing deeply

Good luck, and remember: **in fintech, correctness first, optimization second!**
