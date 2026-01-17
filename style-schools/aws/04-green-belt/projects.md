# AWS - Green Belt Projects

Choose **ONE** project as your capstone.

---

## Project 1: AWS Landing Zone Implementation

**Time**: 4-5 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Enterprise-grade multi-account setup

### Description

Implement a complete AWS Landing Zone following best practices for an enterprise organization.

### Requirements

**Organization Structure**:

- [ ] AWS Organizations with multi-OU structure
- [ ] Account vending machine for automated provisioning
- [ ] Service Control Policies for governance
- [ ] Consolidated billing and cost allocation

**Security Baseline**:

- [ ] Centralized logging (CloudTrail, Config)
- [ ] GuardDuty across all accounts
- [ ] Security Hub with compliance standards
- [ ] Centralized secrets management
- [ ] Cross-account IAM roles

**Network Architecture**:

- [ ] Transit Gateway for connectivity
- [ ] Shared services VPC
- [ ] Network segmentation strategy
- [ ] VPC endpoints for AWS services

**Governance**:

- [ ] Service Catalog for approved services
- [ ] Tagging policies
- [ ] Backup policies
- [ ] Budget alerts and cost controls

### Deliverables

- [ ] Complete Landing Zone deployed
- [ ] Documentation and runbooks
- [ ] Architecture diagrams
- [ ] Compliance report
- [ ] Cost projection

### Evaluation Criteria

- **Architecture (35%)**: Well-designed, scalable
- **Security (30%)**: Comprehensive security controls
- **Governance (20%)**: Effective policies
- **Documentation (15%)**: Complete documentation

---

## Project 2: Production-Grade EKS Platform

**Time**: 4-5 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Enterprise Kubernetes on AWS

### Description

Build a production-ready Kubernetes platform on EKS with all supporting services.

### Requirements

**EKS Cluster**:

- [ ] Multi-AZ EKS cluster
- [ ] Managed node groups and Fargate profiles
- [ ] Cluster autoscaler
- [ ] IAM roles for service accounts (IRSA)

**Networking**:

- [ ] ALB Ingress Controller
- [ ] Service mesh (Istio or App Mesh)
- [ ] Network policies
- [ ] External DNS

**Observability**:

- [ ] Container Insights
- [ ] Prometheus and Grafana
- [ ] Fluent Bit for logging
- [ ] X-Ray for tracing

**Security**:

- [ ] Pod security policies
- [ ] Secrets encryption with KMS
- [ ] Network policies
- [ ] OPA for policy enforcement

**CI/CD**:

- [ ] Automated deployments
- [ ] GitOps with Flux or ArgoCD
- [ ] Image scanning
- [ ] Progressive delivery

### Deliverables

- [ ] Running EKS platform
- [ ] Sample applications deployed
- [ ] Monitoring dashboards
- [ ] CI/CD pipelines
- [ ] Operations runbook

### Evaluation Criteria

- **Architecture (30%)**: Production-ready design
- **Security (25%)**: Comprehensive security
- **Automation (25%)**: Full CI/CD pipeline
- **Observability (20%)**: Complete monitoring

---

## Project 3: Event-Driven Microservices Platform

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Serverless event-driven architecture

### Description

Build a complete event-driven microservices platform using EventBridge, Step Functions, and Lambda.

### Requirements

**Event Architecture**:

- [ ] Custom EventBridge bus
- [ ] Event schemas with schema registry
- [ ] Cross-account event routing
- [ ] Event replay capability

**Microservices**:

- [ ] At least 5 services communicating via events
- [ ] Step Functions for orchestration
- [ ] Lambda functions with proper error handling
- [ ] DynamoDB with streams

**Integration**:

- [ ] API Gateway for external access
- [ ] AppSync GraphQL API
- [ ] SQS for buffering
- [ ] SNS for notifications

**Observability**:

- [ ] X-Ray distributed tracing
- [ ] CloudWatch Logs Insights
- [ ] Custom metrics and dashboards
- [ ] Alarm-based alerting

**Testing**:

- [ ] Event-driven testing strategy
- [ ] Chaos engineering tests
- [ ] Load testing
- [ ] Security testing

### Deliverables

- [ ] Working platform
- [ ] Event catalog documentation
- [ ] Architecture diagrams
- [ ] Testing results
- [ ] Performance analysis

### Evaluation Criteria

- **Architecture (35%)**: Well-designed event-driven system
- **Reliability (25%)**: Resilient and fault-tolerant
- **Observability (20%)**: Comprehensive monitoring
- **Testing (20%)**: Thorough testing strategy

---

Choose one project that demonstrates your mastery of advanced AWS concepts!
