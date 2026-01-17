# AWS Orange Belt - Daily Exercises

**Duration**: 20-30 minutes per exercise  
**Goal**: Build practical AWS skills through hands-on practice

---

## Week 1: Networking & VPC

### Monday

**Focus**: VPC Setup

- [ ] **Exercise** (25 min): Create custom VPC

  ```bash
  # Using AWS CLI
  aws ec2 create-vpc --cidr-block 10.0.0.0/16 --tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=MyVPC}]'
  
  # Create public subnet
  aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block 10.0.1.0/24 --availability-zone us-east-1a
  
  # Create private subnet
  aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block 10.0.2.0/24 --availability-zone us-east-1a
  
  # Create Internet Gateway
  aws ec2 create-internet-gateway
  aws ec2 attach-internet-gateway --vpc-id <vpc-id> --internet-gateway-id <igw-id>
  ```

### Tuesday

**Focus**: Load Balancing

- [ ] **Exercise** (30 min): Set up Application Load Balancer
  - Create target group
  - Launch 2 EC2 instances
  - Register instances with target group
  - Create ALB and configure listener
  - Test load distribution

### Wednesday

**Focus**: Auto Scaling

- [ ] **Exercise** (25 min): Configure Auto Scaling Group
  - Create launch template
  - Set up Auto Scaling Group (min: 2, max: 5)
  - Configure scaling policies (CPU > 70%)
  - Test scaling by generating load

### Thursday

**Focus**: Route 53

- [ ] **Exercise** (20 min): DNS configuration
  - Register a domain or use existing
  - Create hosted zone
  - Add A record pointing to ALB
  - Test DNS resolution

### Friday

**Focus**: Review & Architecture

- [ ] **Exercise** (30 min): Design HA architecture
  - Sketch multi-AZ deployment
  - Document security groups
  - Plan disaster recovery
  - Calculate costs

---

## Week 2: Databases & Storage

### Monday

**Focus**: RDS Setup

- [ ] **Exercise** (30 min): Deploy PostgreSQL RDS
  - Create DB subnet group
  - Launch RDS instance
  - Configure security groups
  - Connect from EC2 instance
  - Create database and tables

### Tuesday

**Focus**: S3 Advanced

- [ ] **Exercise** (25 min): S3 lifecycle and versioning
  - Create S3 bucket with versioning
  - Upload multiple versions of files
  - Configure lifecycle policy (move to Glacier after 30 days)
  - Set up cross-region replication
  - Test bucket policies

### Wednesday

**Focus**: DynamoDB

- [ ] **Exercise** (25 min): NoSQL database operations
  - Create DynamoDB table
  - Define partition key and sort key
  - Add items using CLI
  - Query with filters
  - Set up auto-scaling

### Thursday

**Focus**: Backup & Recovery

- [ ] **Exercise** (20 min): Snapshot management
  - Create RDS snapshot
  - Create EBS volume snapshot
  - Restore from snapshot
  - Automate snapshots with Lambda

### Friday

**Focus**: Storage Classes

- [ ] **Exercise** (20 min): S3 storage optimization
  - Analyze S3 usage patterns
  - Implement intelligent tiering
  - Calculate cost savings
  - Set up S3 analytics

---

## Week 3: Serverless & Containers

### Monday-Tuesday

**Focus**: Lambda Functions

- [ ] **Exercise** (45 min): Build serverless API
  - Create Lambda function (Python/Node.js)
  - Set up API Gateway
  - Configure Lambda triggers
  - Add environment variables
  - Test with Postman

### Wednesday

**Focus**: ECS Deployment

- [ ] **Exercise** (30 min): Containerize application
  - Create Dockerfile
  - Build and push to ECR
  - Create ECS cluster
  - Define task definition
  - Deploy service

### Thursday-Friday

**Focus**: Infrastructure as Code

- [ ] **Exercise** (45 min): CloudFormation template
  - Write template for VPC + EC2
  - Use parameters and outputs
  - Create stack
  - Update stack
  - Delete and clean up

---

Remember to clean up resources after each exercise to avoid unnecessary charges!
