# AI/ML - Green Belt Projects

Choose **ONE** project as your capstone.

---

## Project 1: Production MLOps Platform

**Time**: 4-5 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Training-to-serving automation, safety, and observability

### Requirements

**Platform Capabilities**:
- [ ] Reproducible training pipelines (feature store + artifacts)
- [ ] CI/CD that trains, validates, and promotes models
- [ ] Model registry with lineage, signatures, and approvals
- [ ] Canary + shadow deploys with automated rollback

**Operations**:
- [ ] Observability stack (logs/metrics/traces) for training and serving
- [ ] Drift detection (data + prediction) with alerts
- [ ] Cost dashboards and budget alerts
- [ ] Runbooks for incident response

**Performance**:
- [ ] Autoscaling on QPS and latency
- [ ] p99 latency SLO defined and met
- [ ] Load test results under peak traffic

### Deliverables
- [ ] Deployed platform (infra-as-code)
- [ ] Sample model onboarded end-to-end
- [ ] Dashboards + alerts + runbooks
- [ ] Architecture and operations docs

### Evaluation Criteria
- **Reliability (30%)**: Safe releases, rollbacks, resilience
- **Observability (25%)**: Depth of metrics, tracing, alerts
- **Automation (25%)**: CI/CD quality and policy gates
- **Performance (10%)**: Latency and scale
- **Docs (10%)**: Clear onboarding and operations

---

## Project 2: Real-Time Inference Service

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Low-latency serving, routing, and optimization

### Requirements

**Features**:
- [ ] Online feature store with cache warmup and TTL
- [ ] Multi-model routing (A/B, bandits, shadow)
- [ ] Request batching and dynamic batch sizing
- [ ] Adaptive rate limiting and load shedding

**Performance**:
- [ ] <50ms p99 latency target (adjust to model type)
- [ ] Throughput tests with step-load and soak
- [ ] GPU/CPU cost comparison with quantization or distillation

**Observability**:
- [ ] Per-model metrics (latency, QPS, errors)
- [ ] Trace propagation across ingress -> inference -> downstreams
- [ ] Drift monitoring with automated alerts

### Deliverables
- [ ] Deployed inference stack with IaC
- [ ] Benchmark + profiling report
- [ ] Routing policy documentation
- [ ] Runbook for hotfix and rollback

### Evaluation Criteria
- **Latency (30%)**: Meets SLO under load
- **Routing (25%)**: Correctness and flexibility
- **Efficiency (20%)**: Cost and resource usage
- **Reliability (15%)**: Load shedding, backpressure
- **Docs (10%)**: Clear playbooks

---

## Project 3: Drift-Aware Data and Monitoring System

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Data quality, drift detection, and governance

### Requirements

**Data Quality**:
- [ ] Data contracts with schema validation and freshness checks
- [ ] Great Expectations or similar tests in pipelines
- [ ] Lineage tracking from raw -> features -> model

**Monitoring**:
- [ ] Drift detection (PSI/KS) on key features and predictions
- [ ] Accuracy/precision proxies using delayed labels
- [ ] Alerting with burn-rate policies

**Governance**:
- [ ] Model versioning with approvals and audit trail
- [ ] PII handling plan and access controls
- [ ] Runbooks for bad data and rollback

### Deliverables
- [ ] Monitoring dashboards and alerts
- [ ] Incident simulations with MTTR reported
- [ ] Documentation of data contracts and lineage
- [ ] Postmortem template and example

### Evaluation Criteria
- **Detection (35%)**: Coverage and signal quality
- **Response (25%)**: Speed and clarity of playbooks
- **Governance (20%)**: Auditability and access control
- **Reliability (10%)**: Rollback and resilience
- **Docs (10%)**: Usability of runbooks

---

Choose one project that proves you can operate ML systems at production scale!
