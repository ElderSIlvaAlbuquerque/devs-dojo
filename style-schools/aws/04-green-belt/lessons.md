# AWS - Green Belt Lessons

## Lesson 1: Multi-Account Strategy with AWS Organizations

### What You'll Learn

- [ ] AWS Organizations structure and best practices
- [ ] Service Control Policies (SCPs)
- [ ] Consolidated billing and cost allocation
- [ ] Cross-account access patterns

### Core Ideas

#### 1. Organization Structure

```
Root
├── Core OU
│   ├── Security Account
│   ├── Log Archive Account
│   └── Shared Services Account
├── Production OU
│   ├── Prod App 1 Account
│   └── Prod App 2 Account
└── Development OU
    ├── Dev Account
    └── Test Account
```

#### 2. Service Control Policies

SCPs define maximum permissions:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "ec2:InstanceType": ["t2.micro", "t2.small"]
        }
      }
    }
  ]
}
```

### Why This Matters

Multi-account strategy provides security isolation, cost tracking, and governance at scale.

---

## Lesson 2: EKS and Kubernetes on AWS

### What You'll Learn

- [ ] EKS architecture and components
- [ ] Node groups vs Fargate
- [ ] Kubernetes networking on AWS
- [ ] IAM roles for service accounts (IRSA)

### Core Ideas

#### 1. EKS Control Plane

```
AWS Managed
├── API Server
├── etcd
├── Controller Manager
└── Scheduler

Your Responsibility
├── Worker Nodes (EC2 or Fargate)
├── Applications
└── Cluster Configuration
```

#### 2. IRSA (IAM Roles for Service Accounts)

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-app
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::ACCOUNT:role/my-app-role
---
apiVersion: apps/v1
kind: Deployment
spec:
  template:
    spec:
      serviceAccountName: my-app
```

### Why This Matters

EKS provides managed Kubernetes with AWS integration, essential for containerized workloads.

---

## Lesson 3: Step Functions for Workflow Orchestration

### What You'll Learn

- [ ] State machine patterns
- [ ] Error handling and retries
- [ ] Parallel and map states
- [ ] Integration with AWS services

### Core Ideas

#### 1. State Types

- Task: Execute work (Lambda, ECS, etc.)
- Choice: Branch based on conditions
- Parallel: Execute branches simultaneously
- Map: Iterate over array
- Wait: Delay execution
- Succeed/Fail: End states

#### 2. Error Handling

```json
{
  "Retry": [
    {
      "ErrorEquals": ["ServiceException"],
      "IntervalSeconds": 2,
      "MaxAttempts": 3,
      "BackoffRate": 2.0
    }
  ],
  "Catch": [
    {
      "ErrorEquals": ["States.ALL"],
      "Next": "HandleError"
    }
  ]
}
```

### Why This Matters

Step Functions enables complex workflows without managing orchestration infrastructure.

---

## Lesson 4: EventBridge for Event-Driven Architecture

### What You'll Learn

- [ ] Event buses and event patterns
- [ ] Schema registry
- [ ] Cross-account event routing
- [ ] Integration patterns

### Core Ideas

#### 1. Event Pattern Matching

```json
{
  "source": ["myapp.orders"],
  "detail-type": ["Order Placed"],
  "detail": {
    "amount": [{"numeric": [">", 100]}]
  }
}
```

#### 2. Architecture Pattern

```
Event Source -> EventBridge -> Multiple Targets
                              ├── Lambda
                              ├── Step Functions
                              ├── SQS
                              └── SNS
```

### Why This Matters

EventBridge enables loosely coupled, event-driven architectures at scale.

---

## Lesson 5: Advanced Security and Compliance

### What You'll Learn

- [ ] GuardDuty for threat detection
- [ ] Security Hub for compliance
- [ ] Secrets Manager rotation
- [ ] Config rules for compliance

### Core Ideas

#### 1. Defense in Depth

```
Network Layer: Security Groups, NACLs
Identity Layer: IAM, Cognito
Application Layer: WAF, Shield
Data Layer: KMS, encryption
Monitoring Layer: GuardDuty, CloudTrail
```

#### 2. Automated Compliance

AWS Config Rules check for:
- Unencrypted S3 buckets
- Overly permissive security groups
- Missing tags
- Non-compliant instance types

### Why This Matters

Comprehensive security is essential for enterprise AWS deployments.

---

## Lesson 6: Advanced Cost Optimization

### What You'll Learn

- [ ] Cost Anomaly Detection
- [ ] Savings Plans strategies
- [ ] Resource tagging for cost allocation
- [ ] Cost optimization tools

### Core Ideas

#### 1. Cost Allocation Strategy

```
Tags for every resource:
- Environment (prod/dev/test)
- Project
- Owner
- CostCenter
```

#### 2. Optimization Techniques

- Compute Optimizer recommendations
- Trusted Advisor checks
- Cost Explorer analysis
- Scheduled scaling for non-prod

### Why This Matters

Cost management at scale requires automation and continuous optimization.

---

These advanced lessons prepare you for enterprise-scale AWS deployments.
