# Blockchain Green Belt - Daily Exercises

**Duration**: 30-45 minutes per exercise  
**Goal**: Build secure, scalable, production-ready blockchain systems

---

## Week 1: Smart Contract Safety

### Monday-Tuesday - Upgradeability
- [ ] Implement transparent proxy or UUPS pattern
- [ ] Add initializer guards and versioned storage layout
- [ ] Write migration script and test storage compatibility

### Wednesday - Access Control
- [ ] Add role-based permissions (admin, operator, guardian)
- [ ] Implement circuit breaker/pause
- [ ] Verify role revocation works on-chain

### Thursday-Friday - Testing
- [ ] Add fuzz and invariant tests with Echidna/Foundry
- [ ] Cover reentrancy, overflow/underflow, access control
- [ ] Add gas snapshot tests to catch regressions

---

## Week 2: DeFi and MEV

### Monday-Tuesday - AMM/Lending
- [ ] Implement swap function with fee and slippage checks
- [ ] Add liquidation logic and health factor math
- [ ] Simulate oracle drift and verify protections

### Wednesday - MEV Mitigation
- [ ] Analyze transaction ordering and sandwich risk
- [ ] Add commit-reveal or off-chain signing to reduce MEV
- [ ] Test against forked mainnet scenarios

### Thursday-Friday - Observability
- [ ] Emit structured events for critical actions
- [ ] Build alerting on failed tx, high gas, or reorgs
- [ ] Add dashboards for liquidity, utilization, and risk

---

## Week 3: Scalability and Bridges

### Monday-Tuesday - Layer 2
- [ ] Deploy to an L2 (Optimism/Arbitrum/zkSync/Scroll)
- [ ] Measure cost and latency vs L1
- [ ] Add retry/backoff for RPC instability

### Wednesday-Thursday - Cross-Chain
- [ ] Prototype message passing with a bridge SDK
- [ ] Add replay protection and nonce management
- [ ] Validate proofs/attestations in tests

### Friday - Audit Prep
- [ ] Write threat model and checklist
- [ ] Run Slither/Foundry audit scripts
- [ ] Document known limitations and assumptions

---

Stay disciplined with testing and monitoring to ship secure protocols!
