# AWS Green Belt - Daily Exercises

**Duration**: 30-45 minutes per exercise  
**Goal**: Master advanced AWS architectures and enterprise patterns

---

## Week 1: Multi-Account & Organizations

### Monday

**Focus**: AWS Organizations setup

- [ ] **Exercise** (30 min): Create organization structure
  - Create AWS Organization
  - Create OUs (Prod, Dev, Shared)
  - Apply SCPs to OUs
  - Enable CloudTrail across organization

### Tuesday

**Focus**: Account vending

- [ ] **Exercise** (40 min): Automated account creation
  - Create account using Organizations API
  - Configure baseline security
  - Set up cross-account roles
  - Implement tagging strategy

### Wednesday-Friday

**Focus**: Landing Zone implementation

- [ ] **Exercise** (multiple days): Deploy Control Tower
  - Set up Control Tower
  - Configure guardrails
  - Create account factory
  - Test account provisioning

---

## Week 2: Kubernetes & EKS

### Monday-Wednesday

**Focus**: EKS cluster setup

- [ ] **Exercise** (90 min total): Deploy EKS cluster
  - Create EKS cluster with eksctl
  - Configure node groups
  - Set up kubectl access
  - Deploy sample application
  - Configure ALB Ingress Controller

### Thursday-Friday

**Focus**: EKS operations

- [ ] **Exercise** (60 min): Advanced EKS features
  - Set up cluster autoscaler
  - Configure Fargate profiles
  - Implement pod security policies
  - Set up monitoring with Container Insights

---

## Week 3: Advanced Serverless & Event-Driven

### Monday-Tuesday

**Focus**: Step Functions

- [ ] **Exercise** (60 min): Build workflow
  - Create Step Functions state machine
  - Implement error handling
  - Add retry logic and timeouts
  - Integrate with Lambda and SNS

### Wednesday-Thursday

**Focus**: EventBridge

- [ ] **Exercise** (60 min): Event-driven architecture
  - Create custom event bus
  - Define event patterns
  - Route events to targets
  - Test cross-account events

### Friday

**Focus**: Advanced Lambda

- [ ] **Exercise** (30 min): Lambda optimization
  - Implement Lambda layers
  - Configure provisioned concurrency
  - Set up destinations
  - Optimize cold starts

---

Remember to document architectures and clean up resources!
