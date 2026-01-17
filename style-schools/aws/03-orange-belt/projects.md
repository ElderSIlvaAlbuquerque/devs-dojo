# AWS - Orange Belt Projects

Choose **ONE** project as your capstone.

---

## Project 1: Highly Available Web Application

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐ Intermediate  
**Focus**: Multi-tier architecture with HA and auto-scaling

### Description

Build a production-ready, highly available web application using AWS best practices.

### Requirements

**Architecture**:

- [ ] Multi-AZ deployment across at least 2 availability zones
- [ ] VPC with public and private subnets
- [ ] Application Load Balancer for traffic distribution
- [ ] Auto Scaling Group (min: 2, max: 6)
- [ ] RDS database with Multi-AZ enabled
- [ ] S3 for static assets
- [ ] CloudFront CDN for content delivery
- [ ] Route 53 for DNS management

**Application**:

- [ ] Web tier: EC2 instances running your application
- [ ] Database tier: RDS (PostgreSQL or MySQL)
- [ ] Session management using ElastiCache or DynamoDB
- [ ] Health check endpoint for load balancer
- [ ] Logging to CloudWatch

**Security**:

- [ ] Security groups with least privilege
- [ ] Database only accessible from application tier
- [ ] SSL/TLS certificate (ACM)
- [ ] IAM roles for EC2 instances (no hardcoded credentials)
- [ ] Encrypted RDS database

**Monitoring & Operations**:

- [ ] CloudWatch alarms for CPU, memory, disk
- [ ] Auto Scaling policies based on metrics
- [ ] SNS notifications for critical alerts
- [ ] Automated backups configured
- [ ] CloudWatch Logs for application logs

**Infrastructure as Code**:

- [ ] Complete CloudFormation or Terraform template
- [ ] Parameterized for different environments
- [ ] Documentation for deployment

### Deliverables

- [ ] Working application accessible via custom domain
- [ ] Architecture diagram
- [ ] CloudFormation/Terraform code
- [ ] Deployment guide
- [ ] Load testing results showing auto-scaling
- [ ] Cost analysis report

### Evaluation Criteria

- **Architecture (30%)**: Well-designed, highly available
- **Functionality (25%)**: Application works reliably
- **Security (20%)**: Follows security best practices
- **Automation (15%)**: IaC implementation
- **Documentation (10%)**: Clear documentation

---

## Project 2: Serverless Data Processing Pipeline

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐ Intermediate  
**Focus**: Event-driven serverless architecture

### Description

Build a serverless data processing pipeline that ingests, processes, and analyzes data.

### Requirements

**Data Ingestion**:

- [ ] API Gateway endpoint for data submission
- [ ] Lambda function to validate incoming data
- [ ] Store raw data in S3
- [ ] Publish event to SNS topic

**Processing Pipeline**:

- [ ] S3 event triggers Lambda for processing
- [ ] Process data (transform, enrich, aggregate)
- [ ] Store processed data in DynamoDB
- [ ] Error handling with DLQ

**Data Analysis**:

- [ ] Lambda function to query and analyze data
- [ ] API Gateway endpoints for retrieving results
- [ ] CloudWatch metrics for pipeline monitoring
- [ ] Athena queries for ad-hoc analysis

**Advanced Features**:

- [ ] Step Functions for complex workflows
- [ ] SQS for buffering during high load
- [ ] EventBridge for scheduled processing
- [ ] Lambda layers for shared code

**Monitoring**:

- [ ] X-Ray for distributed tracing
- [ ] CloudWatch Logs Insights queries
- [ ] Custom CloudWatch metrics
- [ ] Dashboard showing pipeline health

### Deliverables

- [ ] Working pipeline processing real data
- [ ] API documentation
- [ ] CloudFormation/SAM template
- [ ] Architecture diagram
- [ ] Performance metrics and costs
- [ ] Sample queries and results

### Evaluation Criteria

- **Architecture (30%)**: Well-designed serverless pipeline
- **Reliability (25%)**: Error handling and resilience
- **Performance (20%)**: Efficient processing
- **Monitoring (15%)**: Comprehensive observability
- **Documentation (10%)**: Clear architecture docs

---

## Project 3: Containerized Microservices Platform

**Time**: 3-4 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: ECS with microservices architecture

### Description

Deploy a microservices application using Amazon ECS with supporting AWS services.

### Requirements

**Container Platform**:

- [ ] ECS cluster with Fargate or EC2 launch type
- [ ] ECR repositories for container images
- [ ] At least 3 microservices (e.g., API, auth, worker)
- [ ] Application Load Balancer with path-based routing
- [ ] Service discovery using Cloud Map

**Services**:

- [ ] API service: REST API (Express, Flask, etc.)
- [ ] Auth service: Authentication/authorization
- [ ] Worker service: Background job processing
- [ ] Database: RDS or DynamoDB
- [ ] Cache: ElastiCache (Redis)
- [ ] Queue: SQS for async communication

**DevOps**:

- [ ] CI/CD pipeline (CodePipeline or GitHub Actions)
- [ ] Automated Docker builds and pushes to ECR
- [ ] Blue-green or rolling deployments
- [ ] Automated testing in pipeline
- [ ] Infrastructure as Code

**Monitoring & Logging**:

- [ ] Centralized logging with CloudWatch Logs
- [ ] Container Insights for ECS metrics
- [ ] X-Ray for distributed tracing
- [ ] Health checks for all services
- [ ] Alerting via SNS

### Deliverables

- [ ] Running microservices platform
- [ ] CI/CD pipeline working
- [ ] Architecture diagram
- [ ] IaC templates
- [ ] API documentation
- [ ] Runbook for operations

### Evaluation Criteria

- **Architecture (30%)**: Well-designed microservices
- **Automation (25%)**: CI/CD and IaC
- **Reliability (20%)**: Resilient, fault-tolerant
- **Monitoring (15%)**: Comprehensive observability
- **Documentation (10%)**: Complete documentation

---

## Project 4: Disaster Recovery Implementation

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐ Intermediate  
**Focus**: Business continuity and disaster recovery

### Description

Implement a complete disaster recovery solution for a web application with documented RTO and RPO.

### Requirements

**Primary Region Setup**:

- [ ] Multi-tier web application
- [ ] RDS database with automated backups
- [ ] S3 for user-generated content
- [ ] Comprehensive monitoring

**DR Region Setup**:

- [ ] Pilot light or warm standby in different region
- [ ] Cross-region RDS replication
- [ ] S3 cross-region replication
- [ ] CloudFormation templates for rapid recovery

**Recovery Procedures**:

- [ ] Automated failover scripts
- [ ] Step-by-step recovery runbook
- [ ] DNS failover with Route 53
- [ ] Data consistency validation

**Testing**:

- [ ] Conduct failover test
- [ ] Measure actual RTO and RPO
- [ ] Document lessons learned
- [ ] Cost analysis of DR setup

**Scenarios to Handle**:

- [ ] Complete region failure
- [ ] Database corruption
- [ ] Accidental data deletion
- [ ] Application failure

### Deliverables

- [ ] Working primary and DR environments
- [ ] Automated failover scripts
- [ ] Detailed runbook
- [ ] Test results with RTO/RPO metrics
- [ ] Cost-benefit analysis
- [ ] Architecture diagrams for both regions

### Evaluation Criteria

- **Completeness (30%)**: All scenarios covered
- **Automation (25%)**: Automated recovery procedures
- **Testing (20%)**: Thorough DR testing conducted
- **Documentation (15%)**: Clear runbooks
- **Cost Efficiency (10%)**: Optimized DR costs

---

Choose one project that aligns with your interests and career goals. Document thoroughly and present your work!
