# AI/ML Green Belt Checklist

## Core Concepts

- [ ] Production ML system design (offline/online separation)
- [ ] Feature stores and data contracts
- [ ] Model deployment patterns (batch, online, streaming)
- [ ] CI/CD for models (training and serving)
- [ ] Model registry, versioning, and lineage
- [ ] Experiment tracking and reproducibility
- [ ] Inference optimization (quantization, distillation, GPUs)
- [ ] Scalability (autoscaling, multi-region, cost control)
- [ ] Observability (drift, data quality, performance SLOs)
- [ ] Safety and rollback strategies (canary, shadow, A/B)
- [ ] Monitoring and alerting (latency, accuracy, stability)
- [ ] Compliance (PII handling, privacy, auditability)

## Practical Tasks

- [ ] Design data contracts and schema validation for features
- [ ] Implement a feature store with batch and online materialization
- [ ] Build CI/CD that trains, validates, and promotes models
- [ ] Ship an online model with canary + shadow deployment
- [ ] Add model registry integration with automated rollbacks
- [ ] Implement drift detection and alerting (covariate/label)
- [ ] Optimize inference with quantization or distillation
- [ ] Add autoscaling policies based on QPS and latency SLOs
- [ ] Instrument tracing/metrics/logs for training and serving
- [ ] Produce runbooks for incident response and rollback

## Projects

- [ ] End-to-end MLOps platform for a real product use case
- [ ] Real-time inference service with drift-aware routing
- [ ] Cost-optimized batch + streaming pipeline with SLAs

Once you can confidently check off these items, you are ready for the Blue Belt!
