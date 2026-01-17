# Blockchain - Green Belt Projects

Choose **ONE** project as your capstone.

---

## Project 1: Secure DeFi Protocol

**Time**: 4-5 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Lending/AMM mechanics, security, and monitoring

### Requirements

**Protocol**:
- [ ] Core contracts (pool, token, risk module)
- [ ] Accurate accounting and health factor logic
- [ ] Oracle integration with fallback and staleness checks
- [ ] Upgradeable proxy with role-based controls

**Security**:
- [ ] Reentrancy guards and access control
- [ ] Fuzz + invariant tests (liquidity conservation, solvency)
- [ ] Static analysis (Slither/Foundry) reports
- [ ] Pause/guardian controls and emergency withdraw flow

**Operations**:
- [ ] Event schema for monitoring and analytics
- [ ] Dashboards for TVL, utilization, liquidation events
- [ ] Alerting on reorgs, price divergence, and failed tx

### Deliverables
- [ ] Deployed contracts (testnet/mainnet fork)
- [ ] Full test suite with coverage
- [ ] Audit-style report and threat model
- [ ] Runbooks for incident response

### Evaluation Criteria
- **Security (35%)**: Tests, guards, and audit depth
- **Mechanics (25%)**: Correct math and risk controls
- **Operations (20%)**: Monitoring and runbooks
- **Performance (10%)**: Gas and throughput
- **Docs (10%)**: Clarity of specs and assumptions

---

## Project 2: Cross-Chain Bridge/Messaging

**Time**: 4-5 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Interoperability, safety, and replay protection

### Requirements

**Bridge Core**:
- [ ] Message format with nonce/replay protection
- [ ] Proof or attestation verification
- [ ] Retry and idempotency handling
- [ ] Rate limiting and circuit breaker

**Security**:
- [ ] Slashable validator/relayer set or third-party attestation
- [ ] Timeouts and challenge periods (if optimistic)
- [ ] Double-spend and duplicate message prevention

**Operations**:
- [ ] Monitoring for failed or delayed messages
- [ ] Cross-chain dashboards and alerts
- [ ] Runbooks for stuck messages and rollbacks

### Deliverables
- [ ] Deployed on two networks (testnets acceptable)
- [ ] End-to-end tests across chains
- [ ] Security notes and assumptions
- [ ] Operational docs and dashboards

### Evaluation Criteria
- **Safety (35%)**: Replay protection, validation, fail-safes
- **Reliability (25%)**: Handling delays and reorgs
- **Performance (20%)**: Latency and cost
- **Observability (10%)**: Monitoring depth
- **Docs (10%)**: Clarity of flows

---

## Project 3: L2-Optimized dApp with MEV Mitigation

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Cost-efficiency, MEV-aware design, and UX

### Requirements

**dApp**:
- [ ] Deploy to an L2 rollup
- [ ] Gas-optimized calldata and storage patterns
- [ ] Commit-reveal or off-chain signing to reduce MEV
- [ ] Robust access control and pausability

**Infrastructure**:
- [ ] RPC reliability strategy (retries/backoff)
- [ ] Frontend with transaction simulation and fee estimates
- [ ] Monitoring for dropped/replaced transactions

**Security/Testing**:
- [ ] Fuzz/invariant tests for core flows
- [ ] Gas snapshot and regression tests
- [ ] Static analysis and audit checklist

### Deliverables
- [ ] Live L2 deployment
- [ ] Test suite and gas reports
- [ ] MEV mitigation rationale
- [ ] Operations dashboard and runbooks

### Evaluation Criteria
- **Efficiency (30%)**: Gas and calldata optimizations
- **Security (25%)**: Testing and mitigation quality
- **Reliability (20%)**: Handling RPC/network issues
- **UX (15%)**: User guidance on fees and status
- **Docs (10%)**: Clarity of design choices

---

Choose one project to demonstrate secure, scalable blockchain engineering!
