# 🥋 Engineer Dojo: A Language-Agnostic Software Engineering Career Path

This repository contains a structured framework for progressing in a software engineering career, from Junior to Principal Engineer. It's designed to be language-agnostic, focusing on universal software engineering concepts.

## ⛩️ The Dojo Structure

The dojo is divided into three main sections:

- **Core Belts**: These represent the universal software engineering knowledge that applies to any programming language. The belts range from White Belt (fundamentals) to Black Belt (Staff Engineer level), plus a dedicated **Purple Belt** (Staff level) covering distributed systems and large-scale architecture.
- **Dans**: These are post-Black Belt specializations for those on the Principal Engineer track.
- **Style Schools**:
  - **Technology-Specific** (Go, React, PostgreSQL, AWS, Git, Ruby on Rails)
  - **Domain-Specific** (Fintech, AI/ML Systems, Blockchain) - specialized systems engineering for niche problems

The philosophy: As AI generates more code, engineering becomes about **architectural thinking and system design**. Our niche schools teach you to architect complex systems in high-stakes domains.

## 🥋 Your Learning Path

### Phase 1: Foundation (Belts 01-04)

- **White Belt**: Programming fundamentals
- **Yellow Belt**: Software design patterns
- **Orange Belt**: Web development and databases
- **Green Belt**: Microservices and scalability

**Duration**: ~18-24 months | **Output**: Junior Engineer

### Phase 2: Architecture (Purple Belt - 05)

- **Purple Belt**: Distributed systems, scalability, consistency, resilience
- **Level**: Staff Engineer | **Duration**: 8-12 weeks

After completing this belt, you can design systems at scale:

- Twitter/X (500M users)
- Uber (real-time location tracking)
- Trading platforms (1M events/sec)
- Streaming services (2B users)
- E-commerce (100M products)
- Messaging (1B users)
- CDN (petabyte-scale caching)

27 real-world design scenarios + 7 capstone projects

### Phase 3: Specialization (Pick ONE after Purple Belt)

After completing the Purple Belt, choose your specialty:

#### 💰 Fintech Engineering School

- Path: Purple Belt → Orange Belt (Fintech) → Green Belt (Fintech)
- Topics: Payment processing, fraud detection, compliance, ledgers
- For: Engineers building payment systems, trading platforms, financial apps
- Real skills: PCI-DSS, idempotency, double-entry accounting, settlement

#### 🤖 AI/ML Systems Engineering School

- Path: Purple Belt → Orange Belt (AI/ML) → Green Belt (AI/ML)
- Topics: Model serving, feature stores, monitoring, inference optimization
- For: Engineers deploying ML models in production
- Real skills: Feature pipelines, model monitoring, drift detection, optimization

#### ⛓️ Blockchain Systems Engineering School

- Path: Purple Belt → Orange Belt (Blockchain) → Green Belt (Blockchain)
- Topics: Smart contracts, consensus, DeFi, cryptography
- For: Engineers building blockchain applications and protocols
- Real skills: Solidity, consensus mechanisms, cryptographic proofs, security

## 📊 Belt Summary

| Belt | Topic | Weeks | Target Level |
| --- | --- | --- | --- |
| 01 White | Programming fundamentals | 6-8 | Junior |
| 02 Yellow | Design patterns, testing | 4-6 | Junior |
| 03 Orange | Web, databases, APIs | 6-8 | Mid-level |
| 04 Green | Microservices, scaling | 8-10 | Senior |
| **05 Purple** | **Distributed systems, architecture** | **8-12** | **Staff** |
| 06 Blue | Advanced reliability | 6-8 | Staff |
| 07 Brown | Technical leadership | 8-10 | Principal |
| 08 Black | Organizational systems | 10-12 | Principal |

## 🎯 Getting Started

**Choose your starting point:**

- **New to software engineering?** → Start with 01-white-belt
- **Already a junior engineer?** → Check your skills against 03-orange-belt
- **Senior engineer wanting architecture depth?** → Start with 05-purple-belt
- **Want to specialize in a domain?** → Complete Purple Belt first, then choose fintech/AI-ML/blockchain

## 🚀 How to Use the Dojo

### For Individual Learning

1. Clone or fork this repository.
2. Start at `core-belts/01-white-belt/`.
3. Work your way through the `lessons.md`, `daily-exercises.md`, and choose a capstone project from `projects.md`.
4. Use the `checklist.md` to self-assess your progress.
5. Once you've completed a belt, move on to the next one.

### With an AI Assistant (like Copilot or Claude)

You can use an AI assistant to help you on your journey. For example, you can ask it to:

- **Review your progress**: "I'm on the white belt and I've completed the CRUD API project. Can you review my code against the promotion requirements?"
- **Suggest exercises**: "I have 20 minutes. What's a good orange-belt exercise?"
- **Help you choose a project**: "Which capstone project should I pick for the purple belt? I know Go and React."

### For Teams

1. Each engineer forks the repository.
2. Each engineer tracks their progress in `examples/[username]/progress.md`.
3. The team reviews capstone projects together.
4. A senior engineer confirms when a promotion to the next belt is earned.

## ⚡ Setup Instructions

1. **Clone the repository**:

    ```bash
    git clone https://github.com/[username]/engineer-dojo.git
    cd engineer-dojo
    ```

2. **Create your progress directory**:

    ```bash
    mkdir -p examples/[your-github]
    touch examples/[your-github]/progress.md
    ```

3. **Start with the White Belt**:

    ```bash
    cd core-belts/01-white-belt
    ```

    - Follow `lessons.md` and `daily-exercises.md`.
    - Pick one project from `projects.md`.

4. **Track your progress**:

    ```bash
    echo "## Week 1: White Belt" >> examples/[your-github]/progress.md
    git add .
    git commit -m "🥋 Week 1: Started White Belt"
    git push
    ```

5. **Graduate to the next belt**:
    - Complete all the items in the `checklist.md`.
    - Get a code review from a peer or senior.
    - Move on to the next belt.
    - For Purple Belt, make sure you've completed 04-green-belt first.
