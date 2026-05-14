# AWS Certified Cloud Practitioner (CLF-C02)
## Complete Study Guide + Cheat Sheet

> **Exam Info:** 90 minutes | 65 questions | Passing score: 700/1000 | Cost: $100

---

# TABLE OF CONTENTS

1. [Cloud Concepts](#1-cloud-concepts)
2. [AWS Global Infrastructure](#2-aws-global-infrastructure)
3. [Core Compute Services](#3-core-compute-services)
4. [Storage Services](#4-storage-services)
5. [Database Services](#5-database-services)
6. [Networking & Content Delivery](#6-networking--content-delivery)
7. [Security & Compliance](#7-security--compliance)
8. [Monitoring & Management](#8-monitoring--management)
9. [Billing & Pricing](#9-billing--pricing)
10. [Support Plans](#10-support-plans)
11. [Migration & Innovation](#11-migration--innovation)
12. [Cheat Sheet](#-master-cheat-sheet)

---

# 1. Cloud Concepts

## What is Cloud Computing?
On-demand delivery of IT resources over the internet with pay-as-you-go pricing.

## Six Advantages of Cloud Computing
1. **Trade capital expense for variable expense** — Pay only for what you consume
2. **Benefit from massive economies of scale** — Lower pay-as-you-go prices
3. **Stop guessing capacity** — Scale up/down as needed
4. **Increase speed and agility** — Resources available in minutes
5. **Stop spending money on data centers** — Focus on customers, not infrastructure
6. **Go global in minutes** — Deploy in multiple regions instantly

## Three Cloud Deployment Models

| Model | Description | Example |
|-------|-------------|---------|
| **Public Cloud** | Fully on AWS | Startup hosted entirely on AWS |
| **Private Cloud** | On-premises, managed by org | Internal data center with VMware |
| **Hybrid Cloud** | Mix of public + private | AWS Direct Connect + on-prem |

## Three Cloud Service Models

| Model | You Manage | AWS Manages | Example |
|-------|-----------|-------------|---------|
| **IaaS** | OS, Apps, Data | Hardware, Networking | EC2 |
| **PaaS** | Data, Applications | OS, Runtime, Middleware | Elastic Beanstalk |
| **SaaS** | Nothing | Everything | Gmail, Salesforce |

## AWS Shared Responsibility Model

```
YOU (Customer) are responsible for:
  ✅ Security IN the cloud
  ✅ Customer data
  ✅ IAM / Access Management
  ✅ OS patching (on EC2)
  ✅ Network/firewall configuration
  ✅ Encryption of data (client-side)

AWS is responsible for:
  ✅ Security OF the cloud
  ✅ Physical hardware
  ✅ Global infrastructure
  ✅ Managed services (RDS patching, Lambda runtime)
  ✅ Edge locations
```

> **Memory Trick:** "IN the cloud = your job. OF the cloud = AWS's job."

---

# 2. AWS Global Infrastructure

## Key Components

### Regions
- Geographic area containing 2+ Availability Zones
- Currently **33+ regions** worldwide
- **Choose region based on:** compliance, latency, available services, pricing

### Availability Zones (AZs)
- One or more discrete data centers with redundant power/networking
- Each region has **3–6 AZs**
- AZs are connected with low-latency fiber
- Used for **high availability** and **fault tolerance**

### Edge Locations / Points of Presence
- Used by **CloudFront** (CDN) and **Route 53**
- **400+ edge locations** globally
- Cache content closer to end users = lower latency

### Local Zones
- Extensions of AWS Regions closer to large population centers
- Useful for latency-sensitive applications (gaming, media)

### Wavelength Zones
- Infrastructure embedded in telecom networks
- Ultra-low latency for **5G** applications

### AWS Outposts
- AWS-managed hardware installed **in your data center**
- Run AWS services on-premises

---

# 3. Core Compute Services

## Amazon EC2 (Elastic Compute Cloud)
Virtual servers in the cloud (IaaS).

### EC2 Instance Types

| Family | Use Case | Examples |
|--------|----------|----------|
| **General Purpose** | Balanced compute/memory | t3, m6i |
| **Compute Optimized** | High CPU workloads, gaming, HPC | c6i, c7g |
| **Memory Optimized** | Large in-memory DBs, caches | r6i, x2idn |
| **Storage Optimized** | High disk I/O, data warehousing | i3, d3 |
| **Accelerated Computing** | ML, GPU rendering | p4, g5, inf2 |

### EC2 Pricing Options

| Option | Description | Savings | Best For |
|--------|-------------|---------|----------|
| **On-Demand** | Pay by hour/second, no commitment | Baseline | Dev/test, unpredictable workloads |
| **Reserved Instances** | 1 or 3 year commitment | Up to 72% | Steady-state workloads |
| **Savings Plans** | Flexible commitment ($/hr) | Up to 72% | Flexible workloads |
| **Spot Instances** | Bid on unused capacity | Up to 90% | Fault-tolerant, batch jobs |
| **Dedicated Hosts** | Physical server for you | — | Compliance, licensing |
| **Dedicated Instances** | Your instances on your hardware | — | Compliance |
| **Capacity Reservations** | Reserve capacity without billing discount | — | Guaranteed capacity |

### Auto Scaling
- **Horizontal scaling** = adding more instances (preferred)
- **Vertical scaling** = making instance bigger (has limits)
- **Auto Scaling Group:** Min, Desired, Max instances
- Scale based on: CPU, memory, custom CloudWatch metrics, scheduled events

### EC2 Load Balancers (ELB)

| Type | Layer | Best For |
|------|-------|----------|
| **Application Load Balancer (ALB)** | Layer 7 (HTTP/HTTPS) | Web apps, microservices, routing |
| **Network Load Balancer (NLB)** | Layer 4 (TCP/UDP) | Ultra-high performance, low latency |
| **Gateway Load Balancer (GWLB)** | Layer 3 | Firewalls, intrusion detection |
| **Classic Load Balancer (CLB)** | Layer 4/7 | Legacy (avoid for new apps) |

---

## AWS Lambda
**Serverless** compute — run code without managing servers.

- Pay only for **compute time** (per 100ms)
- Max execution time: **15 minutes**
- Trigger via API Gateway, S3, DynamoDB, EventBridge, SQS, etc.
- Supports: Python, Node.js, Java, Go, Ruby, .NET

---

## Other Compute Services

| Service | What it Does |
|---------|-------------|
| **Elastic Beanstalk** | PaaS — deploy apps without managing infrastructure |
| **ECS (Elastic Container Service)** | Run Docker containers on AWS |
| **EKS (Elastic Kubernetes Service)** | Managed Kubernetes |
| **AWS Fargate** | Serverless containers (no EC2 management) |
| **AWS Batch** | Managed batch computing jobs |
| **Lightsail** | Simple VPS for beginners |
| **AWS Outposts** | AWS infrastructure on-premises |

---

# 4. Storage Services

## Amazon S3 (Simple Storage Service)
**Object storage** — store any file type, unlimited storage.

- Objects stored in **buckets**
- Globally unique bucket names
- Max object size: **5 TB**
- **11 nines (99.999999999%) durability**

### S3 Storage Classes

| Class | Use Case | Availability | Cost |
|-------|----------|-------------|------|
| **S3 Standard** | Frequently accessed | 99.99% | $$$ |
| **S3 Standard-IA** | Infrequently accessed, rapid retrieval | 99.9% | $$ |
| **S3 One Zone-IA** | Infrequent, non-critical | 99.5% | $ |
| **S3 Glacier Instant Retrieval** | Archives, ms retrieval | 99.9% | $ |
| **S3 Glacier Flexible Retrieval** | Archives, minutes-hours retrieval | 99.99% | $$ (low) |
| **S3 Glacier Deep Archive** | Long-term archive, 12hr retrieval | 99.99% | $  (lowest) |
| **S3 Intelligent-Tiering** | Unknown/changing access patterns | 99.9% | Auto |

### S3 Key Features
- **Versioning** — Keep multiple versions of objects
- **Lifecycle Policies** — Auto-transition to cheaper storage tiers
- **Replication** — Cross-region (CRR) or same-region (SRR)
- **S3 Transfer Acceleration** — Fast uploads using CloudFront edge locations
- **Multipart Upload** — Required for objects > 5 GB
- **Pre-signed URLs** — Temporary access to private objects
- **Static Website Hosting** — Host HTML/CSS/JS websites

---

## Other Storage Services

| Service | Type | Use Case |
|---------|------|----------|
| **EBS (Elastic Block Store)** | Block storage | Attached to single EC2, like a hard drive |
| **EFS (Elastic File System)** | File storage (NFS) | Shared across multiple EC2 instances, auto-scales |
| **FSx** | File storage | Windows File Server, Lustre (HPC) |
| **AWS Storage Gateway** | Hybrid storage | Connect on-prem to AWS storage |
| **AWS Snow Family** | Physical data transfer | Offline migration of massive data |

### Snow Family

| Device | Storage | Use Case |
|--------|---------|----------|
| **Snowcone** | 8 TB | Small, portable, edge computing |
| **Snowball Edge** | 80 TB | Petabyte-scale migration |
| **Snowmobile** | 100 PB | Exabyte-scale migration (literal truck) |

---

# 5. Database Services

## Relational Databases

### Amazon RDS (Relational Database Service)
Managed relational DB — AWS handles patching, backups, scaling.

**Supported engines:** MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora

### Amazon Aurora
- AWS-proprietary, MySQL/PostgreSQL compatible
- **5x faster** than MySQL, **3x faster** than PostgreSQL
- Auto-scales storage up to **128 TB**
- **Aurora Serverless** — auto starts/stops based on demand

---

## Non-Relational (NoSQL) Databases

| Service | Type | Best For |
|---------|------|----------|
| **DynamoDB** | Key-value / Document | Low-latency at any scale, serverless |
| **ElastiCache** | In-memory (Redis/Memcached) | Caching, session management |
| **DocumentDB** | Document (MongoDB-compatible) | JSON documents |
| **Neptune** | Graph DB | Social networks, recommendation engines |
| **Keyspaces** | Wide-column (Cassandra) | IoT, time-series |
| **Timestream** | Time-series | IoT telemetry, metrics |
| **QLDB** | Ledger DB | Immutable financial records |

---

## Data Warehousing & Analytics

| Service | Purpose |
|---------|---------|
| **Redshift** | Cloud data warehouse for BI/analytics (petabyte-scale) |
| **Athena** | Query S3 data with SQL (serverless) |
| **EMR** | Managed Hadoop/Spark for big data |
| **Glue** | Serverless ETL service |
| **QuickSight** | Business intelligence / dashboards |
| **Kinesis** | Real-time data streaming |
| **OpenSearch Service** | Search and log analytics (Elasticsearch) |

---

# 6. Networking & Content Delivery

## Amazon VPC (Virtual Private Cloud)
Your private, isolated section of the AWS cloud.

### VPC Components

| Component | Description |
|-----------|-------------|
| **Subnet** | Segment of IP addresses within a VPC (public or private) |
| **Internet Gateway (IGW)** | Allows VPC to communicate with the internet |
| **NAT Gateway** | Lets private subnets access the internet (outbound only) |
| **Route Table** | Rules directing traffic within VPC |
| **Security Group** | **Stateful** firewall for EC2 instances (allow rules only) |
| **NACL** | **Stateless** firewall at subnet level (allow + deny rules) |
| **VPC Peering** | Connect two VPCs privately |
| **VPC Endpoints** | Connect to AWS services without public internet |

### Security Groups vs NACLs

| Feature | Security Groups | NACLs |
|---------|----------------|-------|
| Level | Instance | Subnet |
| State | Stateful | Stateless |
| Rules | Allow only | Allow + Deny |
| Evaluation | All rules | In order (numbered) |

---

## Connectivity Services

| Service | Purpose |
|---------|---------|
| **Route 53** | DNS service + domain registration + health checks |
| **CloudFront** | CDN — cache content at 400+ edge locations |
| **API Gateway** | Create, publish, and manage REST/WebSocket APIs |
| **Direct Connect** | Dedicated private connection from on-prem to AWS |
| **VPN (Site-to-Site)** | Encrypted tunnel over internet to VPC |
| **Transit Gateway** | Hub-and-spoke to connect many VPCs/VPNs/Direct Connect |
| **Global Accelerator** | Route traffic to optimal AWS endpoint using Anycast |
| **PrivateLink** | Securely expose services to other VPCs without internet |

### Route 53 Routing Policies

| Policy | Use Case |
|--------|----------|
| **Simple** | Single resource |
| **Weighted** | A/B testing, traffic splitting |
| **Latency** | Route to lowest-latency region |
| **Failover** | Active-passive disaster recovery |
| **Geolocation** | Route based on user location |
| **Geoproximity** | Route based on geographic distance (requires Traffic Flow) |
| **Multi-value** | Return multiple healthy records |

---

# 7. Security & Compliance

## IAM (Identity and Access Management)

### Core IAM Concepts

| Concept | Description |
|---------|-------------|
| **User** | Individual with long-term credentials |
| **Group** | Collection of users with shared permissions |
| **Role** | Temporary credentials for AWS services or federated users |
| **Policy** | JSON document defining permissions |
| **MFA** | Multi-factor authentication — always enable on root! |

### IAM Best Practices
- ✅ Lock down **root account** (no access keys, enable MFA)
- ✅ **Least privilege** — grant only what's needed
- ✅ Use **roles** for EC2/Lambda, never embed credentials
- ✅ Use **groups** to assign permissions to users
- ✅ Rotate credentials regularly
- ✅ Enable **CloudTrail** to audit API calls

### Policy Types

| Type | Description |
|------|-------------|
| **Identity-based** | Attached to users, groups, roles |
| **Resource-based** | Attached to resources (e.g., S3 bucket policy) |
| **Permission Boundaries** | Max permissions an identity can have |
| **SCPs (Service Control Policies)** | AWS Organizations — restrict entire accounts |
| **Session Policies** | Used with temporary credentials |

---

## Key Security Services

| Service | Purpose |
|---------|---------|
| **AWS Shield** | DDoS protection (Standard: free, Advanced: paid) |
| **WAF (Web Application Firewall)** | Block SQL injection, XSS, Layer 7 attacks |
| **GuardDuty** | Threat detection using ML (monitors CloudTrail, VPC Flow Logs, DNS) |
| **Inspector** | Automated security assessments for EC2/Lambda/ECR |
| **Macie** | Discover and protect sensitive data in S3 (PII detection) |
| **Security Hub** | Central dashboard for security findings |
| **Detective** | Root cause analysis and security investigations |
| **Config** | Track resource configuration changes + compliance |
| **Secrets Manager** | Store and rotate secrets (DB passwords, API keys) |
| **Systems Manager Parameter Store** | Store config data and secrets (cheaper, less featured) |
| **KMS (Key Management Service)** | Create and control encryption keys |
| **CloudHSM** | Hardware Security Module — dedicated hardware, you control keys |
| **Certificate Manager (ACM)** | Provision SSL/TLS certificates (free for AWS services) |
| **Cognito** | User authentication for apps (sign-up/sign-in) |
| **IAM Identity Center (SSO)** | Single sign-on across AWS accounts and apps |

### KMS vs CloudHSM

| Feature | KMS | CloudHSM |
|---------|-----|---------|
| Key Management | AWS + you | You alone |
| Hardware | Shared HSM | Dedicated HSM |
| FIPS compliance | FIPS 140-2 Level 2 | FIPS 140-2 Level 3 |
| Price | Per API call | Hourly |

---

## Compliance & Governance

| Service | Purpose |
|---------|---------|
| **AWS Artifact** | Access compliance reports (SOC, PCI, ISO) |
| **AWS Audit Manager** | Continuous audit evidence collection |
| **Organizations** | Manage multiple AWS accounts centrally |
| **Control Tower** | Set up and govern multi-account environment |
| **Trusted Advisor** | Best practice recommendations (5 pillars) |

### AWS Organizations Features
- **Consolidated billing** — single payment for all accounts
- **SCPs (Service Control Policies)** — restrict services per account/OU
- **OU (Organizational Units)** — group accounts hierarchically

---

# 8. Monitoring & Management

## Monitoring Services

| Service | Purpose |
|---------|---------|
| **CloudWatch** | Metrics, logs, alarms, dashboards for AWS resources |
| **CloudTrail** | Log all API calls made in your account (who did what, when) |
| **X-Ray** | Distributed tracing for applications |
| **Health Dashboard** | AWS service health status |
| **Trusted Advisor** | Cost, performance, security, fault tolerance, limits |
| **Compute Optimizer** | Right-sizing recommendations for EC2, EBS, Lambda |

### CloudWatch Key Concepts
- **Metrics** — Time-series data (CPU utilization, network in/out)
- **Alarms** — Trigger actions based on metric thresholds
- **Logs** — Collect, monitor, analyze log files
- **Events/EventBridge** — React to changes in AWS resources
- **Dashboards** — Custom visualizations

---

## Management & Deployment Services

| Service | Purpose |
|---------|---------|
| **CloudFormation** | Infrastructure as Code (IaC) using JSON/YAML templates |
| **CDK (Cloud Development Kit)** | IaC using familiar programming languages |
| **Elastic Beanstalk** | PaaS — deploy apps without managing infra |
| **CodePipeline** | CI/CD pipeline automation |
| **CodeBuild** | Build and test code |
| **CodeDeploy** | Automate code deployment to EC2/Lambda/on-prem |
| **CodeCommit** | Git-based source control (being deprecated, use GitHub) |
| **Systems Manager** | Operational hub: patch, run commands, session manager |
| **OpsWorks** | Managed Chef and Puppet |
| **Service Catalog** | Create and manage approved product portfolios |

---

# 9. Billing & Pricing

## Pricing Fundamentals

### Three Fundamental Pricing Drivers
1. **Compute** — How long and how much (EC2 hours, Lambda GB-seconds)
2. **Storage** — How much data stored (S3 GB-months)
3. **Data Transfer** — Data leaving AWS (inbound is free!)

### Free Tier
- **Always Free:** Lambda (1M requests/mo), DynamoDB (25 GB), CloudWatch (10 metrics)
- **12 Months Free:** EC2 (750 hrs t2.micro), S3 (5 GB), RDS (750 hrs)
- **Trials:** Short-term free trials for specific services

---

## Cost Management Tools

| Tool | Purpose |
|------|---------|
| **AWS Pricing Calculator** | Estimate costs before you build |
| **Cost Explorer** | Visualize and analyze past spending |
| **Budgets** | Set spending limits and get alerts |
| **Cost Allocation Tags** | Tag resources to categorize costs |
| **Billing Dashboard** | Month-to-date costs and forecasts |
| **Savings Plans** | Flexible commitment pricing (EC2, Fargate, Lambda) |
| **Reserved Instances** | 1 or 3 year commitment for EC2, RDS, ElastiCache |
| **Spot Instances** | Up to 90% savings for interruptible workloads |

### Total Cost of Ownership (TCO)
**AWS TCO Calculator** (now part of Pricing Calculator) — Compare on-prem vs cloud costs.

Hidden on-prem costs include:
- Server hardware, racks, cooling
- Power and facilities
- IT staff for maintenance
- Software licensing
- Disaster recovery infrastructure

---

## AWS Support Plans

| Feature | Basic | Developer | Business | Enterprise On-Ramp | Enterprise |
|---------|-------|-----------|----------|--------------------|------------|
| **Price** | Free | $29/mo | $100/mo | $5,500/mo | $15,000/mo |
| **Tech Support** | None | Business hours | 24/7 | 24/7 | 24/7 |
| **Response (Critical)** | — | — | 1 hour | 30 min | 15 min |
| **Trusted Advisor** | 7 checks | 7 checks | All checks | All checks | All checks |
| **TAM** | No | No | No | Pool of TAMs | Dedicated TAM |
| **Concierge** | No | No | No | Yes | Yes |

> **TAM** = Technical Account Manager

---

# 10. Support Plans

## AWS Trusted Advisor — 5 Pillars
1. **Cost Optimization** — Underutilized resources, RI recommendations
2. **Performance** — CloudFront optimizations, EC2 right-sizing
3. **Security** — Open ports, MFA on root, public S3 buckets
4. **Fault Tolerance** — Multi-AZ, backups, Route 53 health checks
5. **Service Limits** — Warn before hitting AWS service quotas

> Basic + Developer plans: **7 core checks only**
> Business + Enterprise: **All checks** + API access

---

## Well-Architected Framework — 6 Pillars

| Pillar | Key Principle |
|--------|--------------|
| **Operational Excellence** | Run and monitor systems, continually improve |
| **Security** | Protect data, systems, and assets |
| **Reliability** | Recover from failures, meet demand |
| **Performance Efficiency** | Use resources efficiently |
| **Cost Optimization** | Eliminate unnecessary costs |
| **Sustainability** | Minimize environmental impact |

> **Memory trick:** "Operations Secure Reliable Performance Costs Sustainability" = **OS RPCS**

---

# 11. Migration & Innovation

## Cloud Adoption Framework (CAF)

### Six Perspectives
**Business Perspectives:**
- **Business** — Business value, strategy alignment
- **People** — Change management, culture
- **Governance** — Risk management, portfolio management

**Technical Perspectives:**
- **Platform** — Cloud architecture, design principles
- **Security** — Data protection, compliance
- **Operations** — Service management, monitoring

---

## Migration Strategies — The 7 Rs

| Strategy | Description |
|----------|-------------|
| **Retire** | Shut down apps no longer needed |
| **Retain** | Keep on-prem (not ready to migrate) |
| **Rehost** | Lift-and-shift to EC2 (no changes) |
| **Relocate** | Move to AWS with minimal changes (VMware → VMware Cloud on AWS) |
| **Repurchase** | Move to SaaS (e.g., CRM → Salesforce) |
| **Replatform** | Lift-tinker-and-shift (e.g., DB → RDS) |
| **Refactor/Re-architect** | Redesign for cloud-native (monolith → microservices) |

---

## AI & Machine Learning Services

| Service | Purpose |
|---------|---------|
| **SageMaker** | Build, train, deploy ML models |
| **Rekognition** | Image and video analysis |
| **Transcribe** | Speech to text |
| **Polly** | Text to speech |
| **Translate** | Language translation |
| **Comprehend** | NLP — sentiment analysis, entity detection |
| **Lex** | Build chatbots (powers Alexa) |
| **Kendra** | Intelligent enterprise search |
| **Personalize** | Recommendation engine |
| **Forecast** | Time-series forecasting |
| **Fraud Detector** | Detect online fraud |
| **Textract** | Extract text from documents |
| **Bedrock** | Access foundation models (Claude, Llama, etc.) |
| **CodeWhisperer / Q Developer** | AI coding assistant |

---

## Other Key Services Worth Knowing

| Service | Category | Purpose |
|---------|----------|---------|
| **SNS** | Messaging | Pub/Sub notifications (push) |
| **SQS** | Messaging | Message queue (pull), decouples services |
| **EventBridge** | Events | Serverless event bus |
| **Step Functions** | Orchestration | Coordinate Lambda functions as workflows |
| **SES** | Email | Send transactional/marketing emails |
| **AppSync** | API | Managed GraphQL service |
| **Amplify** | Frontend | Build full-stack web/mobile apps |
| **Device Farm** | Testing | Test apps on real mobile devices |
| **WorkSpaces** | Desktop | Virtual desktops (DaaS) |
| **AppStream 2.0** | Desktop | Stream applications to browsers |
| **Connect** | Contact Center | Cloud-based contact center |
| **Pinpoint** | Marketing | Customer engagement / analytics |

---

---

# ⚡ MASTER CHEAT SHEET

## Quick-Reference: Service → Category

```
COMPUTE
  EC2          → Virtual servers (IaaS)
  Lambda       → Serverless functions
  ECS/EKS      → Containers (ECS=Docker, EKS=Kubernetes)
  Fargate      → Serverless containers
  Beanstalk    → PaaS app deployment
  Lightsail    → Simple VPS

STORAGE
  S3           → Object storage (unlimited, any file)
  EBS          → Block storage (attached to 1 EC2)
  EFS          → File storage (shared, auto-scaling)
  Glacier      → Archive storage (S3 class)
  Snow Family  → Physical data transfer devices

DATABASE
  RDS          → Managed SQL (MySQL, Postgres, etc.)
  Aurora       → AWS SQL (5x faster than MySQL)
  DynamoDB     → NoSQL, serverless, any scale
  ElastiCache  → In-memory cache (Redis/Memcached)
  Redshift     → Data warehouse / analytics

NETWORKING
  VPC          → Private cloud network
  Route 53     → DNS + domain registration
  CloudFront   → CDN (edge caching)
  ELB          → Load balancing (ALB/NLB/GWLB)
  Direct Connect → Dedicated private line to AWS
  API Gateway  → Managed API endpoint

SECURITY
  IAM          → Users, roles, policies
  KMS          → Encryption key management
  Shield       → DDoS protection
  WAF          → Web application firewall
  GuardDuty    → Threat detection (ML)
  Inspector    → Vulnerability scanning
  Macie        → S3 sensitive data (PII)
  Cognito      → App user authentication
  Secrets Mgr  → Rotate & store secrets

MONITORING
  CloudWatch   → Metrics, logs, alarms
  CloudTrail   → API call logging (audit)
  X-Ray        → App distributed tracing
  Config       → Resource change tracking

MANAGEMENT
  CloudFormation → IaC (templates)
  Systems Mgr  → Patch, run commands
  Trusted Advisor → Best practice checks
  Organizations → Multi-account management
  Control Tower → Multi-account governance

AI/ML
  SageMaker    → Build/train/deploy ML
  Rekognition  → Image/video AI
  Bedrock      → Foundation models (Claude, etc.)
  Lex          → Chatbots
  Polly        → Text-to-speech
  Transcribe   → Speech-to-text

MESSAGING
  SNS          → Pub/Sub (push notifications)
  SQS          → Message queue (pull, decoupling)
  EventBridge  → Serverless event bus
```

---

## Key Numbers to Memorize

| Fact | Value |
|------|-------|
| S3 object max size | 5 TB |
| S3 durability | 11 nines (99.999999999%) |
| Lambda max timeout | 15 minutes |
| Regions (approx) | 33+ |
| Edge locations (approx) | 400+ |
| AZs per region | 3–6 |
| EC2 Reserved Instance terms | 1 or 3 years |
| Spot savings | Up to 90% |
| Reserved/Savings Plan savings | Up to 72% |
| Snowball Edge capacity | ~80 TB |
| Snowmobile capacity | 100 PB |
| Developer Support price | $29/mo |
| Business Support price | $100/mo |
| Enterprise Support price | $15,000/mo |

---

## Shared Responsibility Cheat Sheet

```
AWS MANAGES (Security OF the cloud):
  Physical data center security
  Network infrastructure
  Hypervisor
  Managed service OS patching (RDS, Lambda)

CUSTOMER MANAGES (Security IN the cloud):
  IAM users, roles, policies
  Data encryption
  OS patching on EC2
  Security groups and NACLs
  Application-level security
  Customer data
```

---

## Common Exam Traps

| Trap | Answer |
|------|--------|
| "Reduce costs for unpredictable workloads" | **Spot Instances** or **Auto Scaling** |
| "Long-term steady workload cheapest option" | **Reserved Instances** (1 or 3 yr) |
| "Serverless database" | **DynamoDB** or **Aurora Serverless** |
| "Global content delivery with low latency" | **CloudFront** |
| "DNS failover" | **Route 53 Failover routing** |
| "Share data across many EC2 instances" | **EFS** (not EBS — EBS = 1 EC2) |
| "Audit who called which API" | **CloudTrail** (not CloudWatch) |
| "Monitor CPU / set alarms" | **CloudWatch** (not CloudTrail) |
| "Detect threats automatically" | **GuardDuty** |
| "Scan EC2 for vulnerabilities" | **Inspector** |
| "Find PII in S3" | **Macie** |
| "Offline migration of 50 TB" | **Snowball Edge** |
| "Multi-account billing" | **AWS Organizations** |
| "Compliance reports" | **AWS Artifact** |
| "Temporary credentials for EC2" | **IAM Role** (not user) |
| "Decouple microservices" | **SQS** |
| "Fan out / pub-sub" | **SNS** |
| "DDoS protection, automatic" | **Shield Standard** (free) |
| "Store and auto-rotate secrets" | **Secrets Manager** |
| "Store config parameters cheaply" | **Parameter Store** |
| "Establish private AWS connection" | **Direct Connect** |

---

## Exam Domain Weights (CLF-C02)

| Domain | Weight |
|--------|--------|
| Cloud Concepts | 24% |
| Security & Compliance | 30% |
| Cloud Technology & Services | 34% |
| Billing, Pricing & Support | 12% |

> **Security & Services together = 64% of exam. Focus here!**

---

## Final Tips

- **Security is #1** — AWS loves least-privilege, MFA, and encryption
- **Know the difference:** CloudWatch (monitor) vs CloudTrail (audit)
- **Know the difference:** Security Groups (stateful, instance) vs NACLs (stateless, subnet)
- **Know the difference:** SNS (push/pub-sub) vs SQS (queue/pull)
- **Always choose Managed Services** when the question asks for "less operational overhead"
- **Serverless = Lambda, DynamoDB, Fargate, Aurora Serverless, S3, API Gateway**
- **High Availability = Multi-AZ | Disaster Recovery = Multi-Region**

---

*Good luck on your AWS CCP exam! ☁️*
