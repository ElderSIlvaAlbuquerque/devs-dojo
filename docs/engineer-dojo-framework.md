# 🥋 Engineer Dojo: Belt Progression Framework

**Language-Agnostic Software Engineering Career Path**  
**Junior → Senior → Staff → Principal Engineer**

---

## Project Structure

This is a simplified, modular framework for tracking software engineering skill progression. It focuses on **universal software engineering concepts** (language-agnostic), with optional **style schools** for language-specific mastery.

### Core Concept

- **Core Belts**: Universal software engineering knowledge (applies to ANY language)
- **Style Schools**: Language/tech-specific implementation
- **Dans**: Post-Black Belt specializations (Principal Engineer level)

---

## Directory Structure

``` bash
engineer-dojo/
├── README.md                           # Main documentation
├── STRUCTURE.md                        # This file - guide for generators
├── LICENSE                             # MIT
│
├── core-belts/                         # UNIVERSAL (Language-agnostic)
│   ├── 01-white-belt/
│   │   ├── README.md                  # Belt overview
│   │   ├── lessons.md                 # What to learn
│   │   ├── projects.md                # Capstone ideas
│   │   ├── daily-exercises.md         # Daily tasks (15-25 min each)
│   │   └── checklist.md               # Promotion requirements
│   │
│   ├── 02-yellow-belt/
│   ├── 03-orange-belt/
│   ├── 04-green-belt/
│   ├── 05-blue-belt/
│   ├── 06-brown-belt/
│   └── 07-black-belt/
│
├── dans/                               # POST-BLACK BELT (Specializations)
│   ├── 01-first-dan/                  # Senior → Principal transition
│   ├── 02-second-dan/
│   └── 03-third-dan/                  # Principal Engineer level
│
├── style-schools/                      # LANGUAGE/TECH SPECIFIC
│   ├── ruby-on-rails/
│   │   ├── README.md
│   │   ├── belt-progression.md        # Which belt to apply Rails concepts
│   │   ├── 02-yellow-belt/            # Rails Yellow-specific
│   │   ├── 03-orange-belt/
│   │   └── projects/
│   │
│   ├── golang/
│   ├── react/
│   ├── postgresql/
│   └── aws/
│
├── examples/                           # YOUR JOURNEY
│   └── [your-github]/
│       ├── progress.md
│       └── completed-projects/
│
└── docs/
    ├── getting-started.md
    ├── how-to-use-with-ai.md
    └── faq.md
```

---

## Belt Progression (8 Core Belts + 3 Dans)

**New in 2026**: Added **05-Purple Belt** (Staff Engineer level) covering distributed systems, which opens the door to **Domain-Specific Niche Schools** (Fintech, AI/ML, Blockchain).

### **01-White-Belt 🕊️ (Week 1-2)**

**Level**: Junior Developer (Year 0-1)

#### Lessons to Learn

- Fundamentals of HTTP/REST (status codes, verbs, headers)
- Version control (Git, branches, commits, PRs)
- Unit testing basics (what, why, structure)
- Docker containers (images, compose, basic networking)
- Database basics (CRUD, relational concepts, SQL SELECT)

#### Daily Exercises (15-25 min each)

- [ ] Read 1 HTTP concept article (2x/week)
- [ ] Git workflow: create branch → commit → PR (3x/week)
- [ ] Write 1 unit test (daily) - start simple (assert x == y)
- [ ] Run local service in Docker (2x/week)
- [ ] Write 1 SQL SELECT query (daily)

#### Capstone Projects (Pick ONE)

- CRUD API with unit tests (Ruby/Go/Node/Python)
- Local Docker environment with API + database
- Simple web page (React) connecting to API

#### Promotion Requirements

- [ ] CRUD API working locally (all 4 operations)
- [ ] ≥5 unit tests with >80% coverage
- [ ] Docker compose file for local development
- [ ] README with setup instructions
- [ ] 1 clean git history (meaningful commits)

#### Success Metrics

- Deploy to free tier (Render, Heroku, Railway)
- Share live URL on LinkedIn
- Pass code review from peer/senior

---

### **02-Yellow-Belt 💛 (Week 3-4)**

**Level**: Junior Developer (Year 1-2)

#### Lessons to Learn

- API design best practices (error handling, validation, contracts)
- Database migrations and schema design
- Integration testing (with database, external APIs)
- CI/CD basics (GitHub Actions, automated tests)
- Logging and debugging (structured logs, tracing IDs)

#### Daily Exercises (15-25 min each)

- [ ] Design 1 API endpoint with validation (3x/week)
- [ ] Write 1 database migration (2x/week)
- [ ] Write 1 integration test (daily)
- [ ] Set up GitHub Actions workflow (1x/week)
- [ ] Add structured logging to a function (2x/week)

#### Capstone Projects (Pick ONE)

- Rate-limiting API gateway
- User authentication system (signup, login, JWT)
- Todo API with complete CRUD + validation
- Real-time chat backend (WebSocket basics)

#### Promotion Requirements

- [ ] API with input validation + error handling
- [ ] Database migrations (create + update operations)
- [ ] ≥10 integration tests (testing with real DB)
- [ ] CI/CD pipeline that runs tests on push
- [ ] Structured logging throughout code
- [ ] README documenting API contracts

#### Success Metrics

- Deploy with CI/CD (tests run automatically)
- Call your own API from frontend/CLI
- Explain to peer: "Why this validation matters"

---

### **03-Orange-Belt 🧡 (Week 5-7)**

**Level**: Junior → Mid-level (Year 2-3)

#### Lessons to Learn

- Concurrency patterns (threads, async/await, goroutines, race conditions)
- Message queues and async processing (Kafka, RabbitMQ, job queues)
- Prometheus metrics (counters, gauges, histograms, SLIs)
- Performance profiling (identifying bottlenecks)
- Load testing (simulating realistic traffic)

#### Daily Exercises (15-25 min each)

- [ ] Solve 2 concurrency problems (3x/week) - LeetCode-style
- [ ] Add metrics to existing code (2x/week)
- [ ] Implement exponential backoff retry logic (1x/week)
- [ ] Run load test on local service (1x/week)
- [ ] Read 1 distributed systems concept (2x/week)

#### Capstone Projects (Pick ONE)

- Event processor (consume Kafka → process → store, 10k events/sec)
- Job queue system (async task processing)
- Rate limiter with metrics dashboard
- Real-time data pipeline (collect → transform → store)

#### Promotion Requirements

- [ ] Handles concurrency without race conditions (verified with tests)
- [ ] Integrates with message queue (producer + consumer)
- [ ] Exposes Prometheus metrics (latency, throughput, errors)
- [ ] Load tested: handles 10x expected traffic
- [ ] README with performance considerations
- [ ] Graceful shutdown + error recovery

#### Success Metrics

- Load test shows p99 latency < 100ms
- Prometheus dashboard shows metrics in real-time
- Can handle 1 failure gracefully (message replay, retry)
- Explain to peer: "Why this concurrency pattern was chosen"

---

### **04-Green-Belt 💚 (Week 8-10)**

**Level**: Mid-level (Year 2-4)

#### Lessons to Learn

- Microservices architecture (service boundaries, communication)
- Database design at scale (indexing, query optimization, connection pooling)
- Distributed tracing (OpenTelemetry, Jaeger, correlation IDs)
- Domain-Driven Design basics (bounded contexts, aggregates)
- API gateway patterns and service discovery

#### Daily Exercises (15-25 min each)

- [ ] Design 1 bounded context (1x/week)
- [ ] Add database index + explain query plan (2x/week)
- [ ] Add distributed trace span to function (2x/week)
- [ ] Solve 2 SQL performance problems (2x/week)
- [ ] Read 1 microservices pattern (2x/week)

#### Capstone Projects (Pick ONE)

- 3-service microservices system (e.g., user + order + inventory)
- API gateway routing to 2+ backend services
- Event-sourcing proof of concept
- Database sharding for 1M+ records

#### Promotion Requirements

- [ ] 2-3 independent services with clear boundaries
- [ ] Services communicate via async (Kafka) or sync (REST/gRPC)
- [ ] Distributed tracing works: can trace request across services
- [ ] Database optimized (indexes, queries explain-planned)
- [ ] Service discovery working (hardcoded OK for now)
- [ ] README with architecture diagram

#### Success Metrics

- Trace a request through all 3 services in Jaeger
- Each service has different database (microservices pattern)
- Query latency < 50ms even with 1M+ records
- 1 database index prevents full table scan
- Can deploy 1 service independently without others

---

### **05-Blue-Belt 💙 (Month 3-4) → **First Job Transition**

**Level**: Mid-level → Senior (Year 3-5)

#### Lessons to Learn

- System design and trade-offs (scalability, availability, consistency)
- Caching strategies (cache-aside, write-through, cache invalidation)
- Security fundamentals (auth, CORS, SQL injection, secrets management)
- Monitoring and alerting (SLOs, on-call, incident response)
- Infrastructure as Code basics (Terraform, CloudFormation)

#### Daily Exercises (15-25 min each)

- [ ] System design challenge (2x/week) - design TinyURL, chat, etc.
- [ ] Add caching to slow query (1x/week)
- [ ] Design infrastructure for 100x growth (1x/week)
- [ ] Write SLO for critical path (1x/week)
- [ ] Solve 2 security problems (2x/week)

#### Capstone Projects (Pick ONE)

- Payment processing system (idempotency, webhook handling)
- Real-time analytics dashboard (high-throughput writes)
- Content delivery system (caching, CDN patterns)
- Rate limiting at scale (distributed rate limiter)

#### Promotion Requirements

- [ ] Designed for scale: explain how it handles 10x traffic
- [ ] Implements caching (Redis or similar) with clear strategy
- [ ] Security: secrets not in code, auth working, basic CORS
- [ ] Monitoring: meaningful alerts, SLO defined, dashboards
- [ ] IaC: infrastructure defined in code (can deploy from scratch)
- [ ] README with trade-offs: why this approach over others

#### Success Metrics

- System design interview: pass mock with peer/senior
- Load tested at intended scale (explain results)
- Can explain every design decision (why Redis not Memcached?)
- Infrastructure reproducible: 1 command deploys everything
- 1 SLO defined + monitored (e.g., 99.9% availability)

---

### **06-Brown-Belt 🤎 (Month 5-7)**

**Level**: Senior (Year 4-6)

#### Lessons to Learn

- Advanced database patterns (sharding, replication, multi-region)
- Distributed systems fundamentals (CAP theorem, consensus, eventual consistency)
- API design at scale (versioning, deprecation, backwards compatibility)
- Team leadership skills (code reviews, mentoring, design docs)
- Resilience patterns (circuit breakers, bulkheads, retry strategies)

#### Daily Exercises (15-25 min each)

- [ ] Read 1 distributed systems paper/blog (2x/week)
- [ ] Shard a dataset (1x/week) - design, not implementation
- [ ] Write design doc for new feature (1x/week)
- [ ] Mentor 1 junior on architecture (1x/week)
- [ ] Add 1 resilience pattern (circuit breaker, bulkhead, etc.) (1x/week)

#### Capstone Projects (Pick ONE)

- Sharded user service (100M+ users, hash-based sharding)
- Multi-region architecture (active-active or active-passive)
- Consensus system (Raft, Paxos, or simplified blockchain)
- Event-sourcing system with CQRS

#### Promotion Requirements

- [ ] Handles sharding transparently (shard routing works)
- [ ] Replication + failover: 1 node down doesn't break system
- [ ] Distributed tracing shows all services involved
- [ ] Resilience: system degrades gracefully under load
- [ ] Design doc explains: why sharding over other approaches
- [ ] Mentored 1 junior on the architecture
- [ ] README with lessons learned

#### Success Metrics

- Explain sharding strategy to peer: hash function, hot spots, scaling
- System survives 1 node failure (verified with test)
- Design doc answers: "What if 10x more traffic?"
- Code review feedback from peer: "This pattern is solid"
- 1 junior understands your architecture (pair program)

---

### **07-Black-Belt ⚫ (Month 8-13)**

**Level**: Senior → Staff (Year 5-8)

#### Lessons to Learn

- Staff engineer responsibilities (tech roadmaps, architecture authority)
- System design at organizational scale (multiple teams, platforms)
- Technical communication (architecture decision records, RFCs)
- Performance optimization (profiling, benchmarking, complex trade-offs)
- Building for operations (observability, deployment strategies, SRE mindset)

#### Daily Exercises (15-25 min each)

- [ ] Write 1 architecture decision record (1x/week)
- [ ] Design system for different constraint (2x/week)
- [ ] Review 2 junior's architecture decisions (2x/week)
- [ ] Performance optimization task (1x/week)
- [ ] Plan technology migration (1x/week)

#### Capstone Projects (Pick ONE)

- Distributed ledger system (blockchain, consensus, Byzantine fault tolerance)
- Real-time platform (chat, notifications, feeds - millions of users)
- Highly available system (99.99%+ uptime, multiple regions)
- Complex data processing system (streaming, batch, CQRS)

#### Promotion Requirements

- [ ] System design at massive scale (1M+ concurrent users)
- [ ] Handles Byzantine failures (1+ malicious/broken nodes)
- [ ] Multiple deployment strategies documented (blue-green, canary, etc.)
- [ ] Built for observability (every critical path is traceable)
- [ ] Architecture RFC explaining design to team
- [ ] Mentored 2+ juniors/mid-levels
- [ ] Published 1 technical blog post or design doc
- [ ] README with performance benchmarks and trade-offs

#### Success Metrics

- Staff engineer interview: pass 1-2 with senior engineers
- System survives chaos engineering test (intentional failures)
- Architecture RFC approved by 2+ senior engineers
- Performance: p99 latency, throughput, cost explained
- Team understands your architecture (1+ junior can extend it)

---

## Dans: Post-Black Belt (Principal Engineer Track)

### **01-First-Dan (Shodan) 🎖️ (Month 13-18)**

**Level**: Staff Engineer → Principal (Year 7-10)

**Focus**: Technical Leadership at Organizational Level

#### Key Responsibilities

- Define technical strategy across multiple teams
- Make infrastructure investment decisions
- Establish architecture principles and patterns
- Lead major platform initiatives

#### Learning Areas

- Technology strategy and roadmaps
- Organizational design and scaling teams
- Cost optimization at scale
- Platform thinking (enabling other teams)

#### Capstone

- Design + lead implementation of 1 major platform (internal or customer-facing)
- Write technology strategy document for 3-year period

---

### **02-Second-Dan (Nidan) 🎖️🎖️ (Month 18-24)**

**Level**: Principal Engineer (Year 8-12)

**Focus**: Industry and Community Leadership

#### Key Responsibilities

- Public speaking (conferences, company)
- Open-source project leadership
- Industry influence (standards, best practices)
- Mentoring multiple teams across organization

#### Learning Areas

- Public speaking and communication
- Building communities
- Industry standards and RFCs
- Organizational scaling

#### Capstone

- Publish 1 significant open-source project or 5+ technical articles
- Speak at 1+ industry conference

---

### **03-Third-Dan (Sandan) 🎖️🎖️🎖️ (Month 24+)**

**Level**: Principal Engineer / Distinguished Engineer (Year 10+)

**Focus**: Industry Thought Leadership

#### Key Responsibilities

- Shape industry direction
- Executive advisory on technical decisions
- Talent attraction through reputation
- Company's technical representative

---

## Style Schools: Language/Tech-Specific

These are **optional** and organized by belt level. Each style teaches:

- How to apply belt concepts in THIS language/framework
- Language-specific patterns and idioms
- Tool ecosystem

### Structure for Each Style School

```
style-schools/[language]/
├── README.md                         # Overview
├── getting-started.md                # Setup guide
├── 02-yellow-belt/
│   ├── lessons.md
│   ├── exercises.md
│   └── projects.md
├── 03-orange-belt/
├── 04-green-belt/
└── examples/
    └── capstone-implementations/
```

### Initial Style Schools (Examples)

#### **Ruby on Rails**

- White: HTTP basics, REST conventions, MVC
- Yellow: Migrations, validation, Active Record
- Orange: Background jobs (Sidekiq), caching
- Green: Rails engines, service objects, N+1 queries
- Blue: Scaling Rails (sharding, multi-database)
- Brown: Rails internals, metaprogramming, performance

#### **Go**

- White: goroutines, channels, HTTP package
- Yellow: error handling, testing, interfaces
- Orange: concurrency patterns, sync package
- Green: gRPC, protobuf, service design
- Blue: profiling (pprof), memory management
- Brown: unsafe, runtime internals, performance tuning

#### **React**

- White: components, JSX, state
- Yellow: hooks, testing (React Testing Library)
- Orange: performance (memoization, lazy loading)
- Green: state management (Redux, Context)
- Blue: server-side rendering, static generation
- Brown: advanced patterns, library internals

#### **PostgreSQL**

- White: CRUD, SELECT, basic schema
- Yellow: indexes, constraints, foreign keys
- Orange: query optimization (EXPLAIN), transactions
- Green: window functions, recursive queries
- Blue: partitioning, replication, failover
- Brown: internals, MVCC, tuning parameters

#### **AWS**

- White: EC2, S3, RDS basics
- Yellow: IAM, security groups, CloudWatch
- Orange: Lambda, SQS, auto-scaling
- Green: ECS, multi-region, disaster recovery
- Blue: cost optimization, advanced networking
- Brown: organizational design, cross-account

---

## Daily Exercise Template

Each belt has a **daily-exercises.md** with:

```markdown
## Daily Exercises - [Belt Name]

Duration: 15-25 min per exercise (pick 1-2 daily)

### Monday
- [ ] **Core Concept**: Read about [concept] (15 min)
- [ ] **Code**: Implement [small task] (20 min)

### Tuesday  
- [ ] **Problem**: Solve [LeetCode/System Design] (25 min)
- [ ] **Review**: Read peer's code (10 min)

... and so on for the week
```

---

## Promotion Checklist Template

Each belt has a **checklist.md**:

```markdown
## Promotion Requirements - [Belt Name]

### Knowledge
- [ ] Can explain [concept 1] to peer
- [ ] Can explain [concept 2] to peer
- [ ] Understand trade-offs in [pattern]

### Project
- [ ] Capstone project complete
- [ ] Code has >80% test coverage
- [ ] README documents approach
- [ ] Deployed to live environment

### Review
- [ ] Code reviewed by 1 senior engineer
- [ ] Architecture reviewed and approved
- [ ] Performance benchmarked

### Presentation
- [ ] Can present project to group
- [ ] Can answer "Why this approach?"
- [ ] Can discuss learnings

**Promotion**: ✓ All items checked
```

---

## How to Use This Framework

### For Individual Learning

1. Clone/fork this repo
2. Start at 01-white-belt/
3. Complete lessons → daily exercises → capstone
4. Self-assess using checklist
5. Move to next belt

### With AI Assistant (Copilot/Gemini)

```bash
# Ask Copilot/Gemini to review your progress
"I'm on white-belt. I completed the CRUD API.
Can you review this [code link] against promotion requirements?"

# Ask for daily exercise ideas
"I have 20 minutes. What's a good orange-belt exercise?"

# Ask for project ideas
"Which capstone project should I pick for yellow-belt?
I know Ruby and Go."
```

### For Teams

1. Each engineer forks repo
2. Tracks progress in `examples/[username]/progress.md`
3. Team reviews capstone projects
4. Senior engineer confirms promotion
5. Engineer advances to next belt

---

## File Templates

### lesson.md Template

```markdown
# [Belt Name] - Lesson: [Topic]

## What You'll Learn
- [ ] Concept A
- [ ] Concept B

## Core Ideas
1. Idea 1 with example
2. Idea 2 with example

## Why This Matters
Real-world scenario where this is critical

## Common Mistakes
- Mistake 1 and how to avoid
- Mistake 2 and how to avoid

## Further Reading
- Link 1
- Link 2
```

### projects.md Template

```markdown
# [Belt Name] - Capstone Projects

Pick ONE project to graduate to next belt.

## Project 1: [Name]
**Time**: 2-4 weeks  
**Tech Stack**: [Flexible - pick your language]  
**Concepts**: What this teaches  
**Requirements**:
- Requirement 1
- Requirement 2

## Project 2: [Name]
...

## Project 3: [Name]
...

## Submission
- [ ] Code on GitHub
- [ ] README with approach
- [ ] Live deployment
- [ ] Pass promotion checklist
```

---

## Purple Belt (05-purple-belt) - NEW

**Level**: Staff Engineer (Year 5-6)  
**Focus**: Distributed systems, large-scale architecture, foundational for niche schools

This belt bridges from single-service architecture (Green Belt) to complex distributed systems. Required before specializing in Fintech, AI/ML, or Blockchain.

### Coverage

- Load balancing, caching, databases at scale
- CAP theorem, consistency models, distributed transactions
- Message queues, pub/sub, event-driven architecture
- Monitoring, observability, reliability patterns
- Microservices, search, real-time systems
- Cost optimization, batch processing, deployment strategies

### Projects (Pick ONE)

1. **Design Twitter/X**: Scale to 500M users, 100M daily active
2. **Design Uber/Lyft**: Real-time location tracking, matching algorithm
3. **Design E-Commerce Platform**: Inventory, catalog search, checkout at scale
4. **Design Messaging Platform**: Real-time delivery, offline queuing, encryption
5. **Design Video Streaming**: Encoding pipelines, CDN strategy, recommendations
6. **Design Trading Platform**: Order matching, real-time data, compliance
7. **Design Content Delivery Network (CDN)**: Global edge servers, DDoS mitigation

---

## Niche Style Schools (NEW)

With system design fundamentals mastered, specialize in high-value domains:

### 💰 Fintech Engineering School

**When to Start**: After 04-green-belt or concurrent with 05-purple-belt

**Belts Offered**:
- 03-orange-belt: Payment processing, fraud detection, regulatory basics
- 04-green-belt: Settlement, reconciliation, compliance, high-volume transactions

**Topics Covered**:
- Payment processing (credit cards, ACH, wire, crypto)
- Transaction atomicity and safety
- Fraud detection and 3D Secure
- PCI-DSS and regulatory compliance
- Ledger systems and reconciliation
- Settlement and payout operations

**Why This Matters**: 
Fintech is where correctness and compliance are non-negotiable. Building fintech systems develops the architectural thinking needed for all high-stakes systems.

---

### 🤖 AI/ML Systems Engineering School

**When to Start**: After 04-green-belt or concurrent with 05-purple-belt

**Belts Offered**:
- 03-orange-belt: Model serving, feature engineering, experiment tracking
- 04-green-belt: Real-time + batch inference, data pipelines, model monitoring

**Topics Covered**:
- Model serving and inference optimization
- Feature engineering and feature stores
- Experiment tracking and hyperparameter optimization
- Real-time and batch prediction systems
- Data pipelines and retraining automation
- Model monitoring and drift detection

**Why This Matters**: 
With AI models handling increasingly critical decisions, the engineering infrastructure is more important than the models themselves. Learn to build systems that scale inference, keep models fresh, detect failures, and optimize costs.

---

### ⛓️ Blockchain Systems Engineering School

**When to Start**: After 04-green-belt or concurrent with 05-purple-belt

**Belts Offered**:
- 03-orange-belt: Smart contracts, consensus basics, transaction models
- 04-green-belt: Advanced smart contracts, DeFi protocols, cross-chain systems

**Topics Covered**:
- Blockchain fundamentals and consensus mechanisms
- Smart contract development and security
- UTXO vs Account transaction models
- DeFi protocols (lending, AMM, staking)
- Cross-chain bridges and interoperability
- Privacy-preserving techniques (zero-knowledge proofs)

**Why This Matters**: 
Blockchain solves distributed systems problems differently than traditional systems. Learning both perspectives (trusted operator vs trustless) is crucial for the future of systems engineering.

---

## Quick Start

```bash
# 1. Clone repo
git clone https://github.com/[username]/engineer-dojo.git
cd engineer-dojo

# 2. Create your progress directory
mkdir -p examples/[your-github]
touch examples/[your-github]/progress.md

# 3. Start white-belt
cd core-belts/01-white-belt
# Follow lessons.md, daily-exercises.md, pick 1 project

# 4. Track progress
echo "## Week 1: White Belt" >> examples/[your-github]/progress.md
git add .
git commit -m "🥋 Week 1: Started White Belt"
git push

# 5. When ready to graduate
# Complete all checklist items
# Push final project code
git commit -m "🥋 White Belt: Ready for promotion"
# Get code review from peer/senior
# Move to 02-yellow-belt/

# After 04-green-belt, choose your specialization:
# - cd core-belts/05-purple-belt (required foundation)
# - Then pick niche school:
#   - style-schools/fintech
#   - style-schools/ai-ml
#   - style-schools/blockchain
```

---

## Next Steps to Build This

1. **Core belts 01-07** are language-agnostic foundations
2. **Purple belt (05)** bridges to specialization
3. **Niche schools** (fintech, ai-ml, blockchain) for domain expertise
4. **Technology schools** (Go, React, etc.) for language mastery
5. **Dans** for post-black-belt principal engineer track

This structure reflects the future of engineering: **AI generates code, engineers design systems**. Our niche schools teach the architectural thinking needed for high-stakes domains.

````

---

**License**: MIT  
**Created**: Dec 24, 2025  
**For**: Any developer wanting to track career progression from Junior → Staff → Principal Engineer
