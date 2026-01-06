# AWS - Orange Belt Lessons

## Lesson 1: VPC and Networking Fundamentals

### What You'll Learn

- [ ] How VPCs provide isolated network environments
- [ ] Subnets, route tables, and internet gateways
- [ ] NAT gateways for private subnet internet access
- [ ] Security groups vs Network ACLs

### Core Ideas

#### 1. VPC Architecture

```
VPC (10.0.0.0/16)
├── Public Subnet (10.0.1.0/24) - AZ-1
│   ├── Internet Gateway
│   └── Web Servers
├── Private Subnet (10.0.2.0/24) - AZ-1
│   ├── Application Servers
│   └── NAT Gateway
└── Private Subnet (10.0.3.0/24) - AZ-1
    └── Databases (RDS)
```

#### 2. Security Layers

**Security Groups** (Stateful):
- Applied at instance level
- Allow rules only (implicit deny)
- Return traffic automatically allowed

**Network ACLs** (Stateless):
- Applied at subnet level
- Allow and deny rules
- Must explicitly allow return traffic

#### 3. Internet Access Patterns

```bash
# Public subnet: Internet Gateway
Internet <-> IGW <-> Public Subnet <-> EC2

# Private subnet: NAT Gateway
Private Subnet <-> NAT GW (in public subnet) <-> IGW <-> Internet
```

### Why This Matters

VPCs are fundamental to AWS architecture, providing network isolation and security for your applications.

### Common Mistakes

- Not planning CIDR ranges carefully (can't change later)
- Forgetting to enable auto-assign public IP for public subnets
- Using Network ACLs when Security Groups are sufficient
- Not using multiple Availability Zones for high availability

---

## Lesson 2: Load Balancing and High Availability

### What You'll Learn

- [ ] Types of load balancers (ALB, NLB, CLB)
- [ ] Health checks and target groups
- [ ] Cross-zone load balancing
- [ ] SSL/TLS termination

### Core Ideas

#### 1. Load Balancer Types

**Application Load Balancer (ALB)** - Layer 7 (HTTP/HTTPS):
- Content-based routing
- Host-based and path-based routing
- WebSocket support
- Best for web applications

**Network Load Balancer (NLB)** - Layer 4 (TCP/UDP):
- Extreme performance (millions of requests/sec)
- Static IP addresses
- Preserve source IP
- Best for low-latency requirements

**Classic Load Balancer (CLB)** - Legacy:
- Both Layer 4 and 7
- Being phased out
- Use ALB or NLB instead

#### 2. Target Groups

```
ALB
├── Listener (Port 80)
│   └── Forward to Target Group A
├── Listener (Port 443)
│   ├── Rule: /api/* -> Target Group B
│   └── Default -> Target Group A
```

#### 3. Health Checks

```yaml
Health Check:
  Protocol: HTTP
  Path: /health
  Interval: 30 seconds
  Timeout: 5 seconds
  Healthy Threshold: 2
  Unhealthy Threshold: 3
```

### Why This Matters

Load balancers distribute traffic, provide high availability, and enable zero-downtime deployments.

---

## Lesson 3: Auto Scaling

### What You'll Learn

- [ ] Launch templates vs launch configurations
- [ ] Scaling policies (target tracking, step scaling)
- [ ] Desired capacity, min, and max
- [ ] Integration with load balancers

### Core Ideas

#### 1. Auto Scaling Components

```
Launch Template (what to launch)
    ↓
Auto Scaling Group (when and how many)
    ↓
Load Balancer (distribute traffic)
```

#### 2. Scaling Policies

**Target Tracking**:
```json
{
  "TargetValue": 70.0,
  "PredefinedMetricSpecification": {
    "PredefinedMetricType": "ASGAverageCPUUtilization"
  }
}
```

**Step Scaling**:
```
CPU > 80%: Add 2 instances
CPU > 90%: Add 4 instances
CPU < 30%: Remove 1 instance
```

#### 3. Best Practices

- Start with target tracking (simpler)
- Use health checks to replace unhealthy instances
- Set appropriate cooldown periods
- Monitor scaling activities

### Why This Matters

Auto Scaling ensures your application handles traffic spikes while minimizing costs during low usage.

---

## Lesson 4: RDS and Managed Databases

### What You'll Learn

- [ ] RDS engines (PostgreSQL, MySQL, MariaDB, Oracle, SQL Server)
- [ ] Multi-AZ deployments for high availability
- [ ] Read replicas for performance
- [ ] Automated backups and snapshots

### Core Ideas

#### 1. Multi-AZ vs Read Replicas

**Multi-AZ** (High Availability):
- Synchronous replication
- Automatic failover
- Same endpoint
- For disaster recovery

**Read Replicas** (Performance):
- Asynchronous replication
- Separate endpoint
- Read-only
- For scaling reads

#### 2. Backup Strategy

```
Automated Backups:
  - Retention: 7-35 days
  - Automatic, daily
  - Point-in-time recovery
  - Performance impact during backup window

Manual Snapshots:
  - Retained until manually deleted
  - Can copy across regions
  - No performance impact
  - Use for major changes
```

#### 3. Connection Management

```python
# Use connection pooling
import psycopg2
from psycopg2 import pool

connection_pool = pool.SimpleConnectionPool(
    minconn=1,
    maxconn=10,
    host="mydb.xxxxx.us-east-1.rds.amazonaws.com",
    database="myapp",
    user="admin",
    password="password"
)

conn = connection_pool.getconn()
# Use connection
connection_pool.putconn(conn)
```

### Why This Matters

RDS eliminates database management overhead while providing enterprise-grade reliability and performance.

---

## Lesson 5: Serverless with Lambda and API Gateway

### What You'll Learn

- [ ] Lambda function basics and execution model
- [ ] API Gateway REST vs HTTP APIs
- [ ] Event-driven architectures
- [ ] Cold starts and optimization

### Core Ideas

#### 1. Lambda Function Structure

```python
import json

def lambda_handler(event, context):
    # event: input data (API request, S3 event, etc.)
    # context: runtime information
    
    body = json.loads(event['body'])
    
    # Your business logic
    result = process_data(body)
    
    return {
        'statusCode': 200,
        'headers': {'Content-Type': 'application/json'},
        'body': json.dumps(result)
    }
```

#### 2. API Gateway Integration

```
Client -> API Gateway -> Lambda -> Database
         (HTTPS)        (invoke)   (query)
```

#### 3. Lambda Best Practices

- Keep functions small and focused
- Use environment variables for configuration
- Initialize connections outside handler
- Use Lambda layers for dependencies
- Monitor with CloudWatch Logs

```python
# Initialize outside handler (reused across invocations)
import boto3
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('MyTable')

def lambda_handler(event, context):
    # Handler code - runs on each invocation
    result = table.get_item(Key={'id': event['id']})
    return result['Item']
```

### Why This Matters

Serverless architectures eliminate server management and scale automatically, paying only for actual usage.

---

## Lesson 6: Infrastructure as Code with CloudFormation

### What You'll Learn

- [ ] CloudFormation template structure
- [ ] Resources, parameters, and outputs
- [ ] Stack operations (create, update, delete)
- [ ] Change sets for safe updates

### Core Ideas

#### 1. Template Structure

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'Simple web application infrastructure'

Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
    AllowedValues: [t2.micro, t2.small, t2.medium]

Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
      ImageId: ami-0c55b159cbfafe1f0
      SecurityGroups:
        - !Ref MySecurityGroup
  
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow HTTP
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

Outputs:
  InstanceId:
    Description: Instance ID
    Value: !Ref MyEC2Instance
  PublicIP:
    Description: Public IP
    Value: !GetAtt MyEC2Instance.PublicIp
```

#### 2. Intrinsic Functions

```yaml
# Ref - reference parameter or resource
!Ref ParameterName

# GetAtt - get attribute of resource
!GetAtt ResourceName.AttributeName

# Join - concatenate strings
!Join [':', [a, b, c]]  # "a:b:c"

# Sub - substitute variables
!Sub 'Hello ${AWS::StackName}'
```

#### 3. Stack Management

```bash
# Create stack
aws cloudformation create-stack \
  --stack-name my-stack \
  --template-body file://template.yaml \
  --parameters ParameterKey=InstanceType,ParameterValue=t2.small

# Update stack (with change set for safety)
aws cloudformation create-change-set \
  --stack-name my-stack \
  --change-set-name my-changes \
  --template-body file://template-v2.yaml

aws cloudformation describe-change-set \
  --stack-name my-stack \
  --change-set-name my-changes

aws cloudformation execute-change-set \
  --stack-name my-stack \
  --change-set-name my-changes

# Delete stack
aws cloudformation delete-stack --stack-name my-stack
```

### Why This Matters

Infrastructure as Code enables version control, repeatability, and automation of infrastructure provisioning.

---

## Lesson 7: Messaging with SNS and SQS

### What You'll Learn

- [ ] SNS for pub/sub messaging
- [ ] SQS for queuing and decoupling
- [ ] Dead letter queues
- [ ] Fan-out patterns

### Core Ideas

#### 1. SNS (Simple Notification Service)

Pub/Sub pattern:

```
SNS Topic
├── Subscriber 1 (Email)
├── Subscriber 2 (SMS)
├── Subscriber 3 (Lambda)
└── Subscriber 4 (SQS Queue)
```

#### 2. SQS (Simple Queue Service)

Message queue pattern:

```
Producer -> SQS Queue -> Consumer
            (buffer)     (processes at own pace)
```

**Standard Queue**:
- At-least-once delivery
- Best-effort ordering
- Unlimited throughput

**FIFO Queue**:
- Exactly-once processing
- Strict ordering
- Up to 3,000 messages/sec

#### 3. Fan-out Pattern

```
Application -> SNS Topic -> SQS Queue 1 -> Service A
                         -> SQS Queue 2 -> Service B
                         -> SQS Queue 3 -> Service C
```

Each service processes messages independently.

#### 4. Dead Letter Queues

```python
# Configure DLQ for failed messages
{
    "RedrivePolicy": {
        "deadLetterTargetArn": "arn:aws:sqs:us-east-1:123456789012:my-dlq",
        "maxReceiveCount": "3"
    }
}
```

### Why This Matters

SNS and SQS enable building decoupled, scalable, and resilient architectures.

---

## Lesson 8: Cost Optimization

### What You'll Learn

- [ ] Cost allocation tags
- [ ] Reserved instances and savings plans
- [ ] Spot instances for cost savings
- [ ] Cost monitoring and alerts

### Core Ideas

#### 1. Cost Optimization Strategies

**Compute**:
- Right-size instances (don't over-provision)
- Use Auto Scaling to match demand
- Reserved Instances (1-3 year commitment)
- Spot Instances (up to 90% savings)

**Storage**:
- S3 lifecycle policies (move to cheaper tiers)
- Delete unused EBS volumes
- Use EBS snapshots efficiently
- Compress data before storage

**Database**:
- Use read replicas instead of larger instances
- Schedule non-production databases
- Use Aurora Serverless for variable workloads

#### 2. Cost Monitoring

```bash
# Enable Cost Explorer
# Set up billing alerts
aws cloudwatch put-metric-alarm \
  --alarm-name "HighBilling" \
  --alarm-description "Alert when billing exceeds $100" \
  --metric-name EstimatedCharges \
  --namespace AWS/Billing \
  --statistic Maximum \
  --period 21600 \
  --threshold 100 \
  --comparison-operator GreaterThanThreshold

# Use cost allocation tags
aws ec2 create-tags \
  --resources i-1234567890abcdef0 \
  --tags Key=Project,Value=WebApp Key=Environment,Value=Production
```

#### 3. AWS Cost Optimization Tools

- **Cost Explorer**: Visualize and analyze costs
- **Trusted Advisor**: Get cost optimization recommendations
- **Compute Optimizer**: Right-sizing recommendations
- **S3 Storage Lens**: Storage usage insights

### Why This Matters

Unmanaged AWS costs can quickly spiral. Optimization is essential for sustainable cloud operations.

---

Remember: Always follow the principle of least privilege for security and clean up unused resources to avoid unnecessary costs.
