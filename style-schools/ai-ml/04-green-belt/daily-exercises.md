# AI/ML Green Belt - Daily Exercises

**Duration**: 30-45 minutes per exercise  
**Goal**: Master production-grade MLOps, scalability, and monitoring

---

## Week 1: Deployment and Release Safety

### Monday-Tuesday - Deployment Patterns
- [ ] Containerize a model server (FastAPI/TensorFlow Serving/Triton)
- [ ] Implement blue/green and canary rollouts
- [ ] Add shadow testing against production traffic
- [ ] Capture latency and error-rate metrics per model version

### Wednesday-Thursday - Feature Store
- [ ] Define data contracts and validation rules
- [ ] Materialize batch features to offline store
- [ ] Serve online features with low-latency cache
- [ ] Add point-in-time correctness tests

### Friday - Promotion Workflow
- [ ] Automate training -> validation -> registry promotion
- [ ] Gate releases on evaluation metrics and p99 latency SLO
- [ ] Build rollback playbook and test it

---

## Week 2: Observability and Drift

### Monday-Tuesday - Monitoring
- [ ] Emit structured logs, metrics, and traces from inference
- [ ] Track request/response schemas and payload sizes
- [ ] Build dashboards for throughput, latency, and errors
- [ ] Alert on SLO burn rate and saturation

### Wednesday - Drift Detection
- [ ] Implement population stability index or KS test
- [ ] Monitor feature/data drift and model quality proxies
- [ ] Route drifted traffic to shadow model for comparison

### Thursday-Friday - Incident Response
- [ ] Simulate bad deployment; validate rollback speed
- [ ] Write runbook for data pipeline outage
- [ ] Add synthetic canary checks for feature freshness

---

## Week 3: Performance and Cost

### Monday-Tuesday - Inference Efficiency
- [ ] Profile CPU vs GPU throughput for the same model
- [ ] Apply quantization or distillation and compare metrics
- [ ] Benchmark batch vs real-time inference strategies

### Wednesday-Thursday - Scaling
- [ ] Configure autoscaling on QPS and latency signals
- [ ] Add load shedding and circuit breaker for upstreams
- [ ] Validate multi-region failover plan

### Friday - Cost Controls
- [ ] Build cost dashboard (compute, storage, egress)
- [ ] Set budgets/alerts; identify biggest cost drivers
- [ ] Document savings from optimizations

---

Master these production skills to operate ML systems reliably at scale!
