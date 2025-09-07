# Cloud Computing 

## CC Fundamentals

### What is Cloud Computing?
*Definition*: On-demand delivery of computing services (servers, storage, databases, networking, software) over the internet with pay-as-you-go pricing.

### Characteristics 
1. *On-demand self-service*: Provision resources automatically
2. *Broad network access*: Available over network from various devices
3. *Resource pooling*: Multi-tenant model with dynamic assignment
4. *Rapid elasticity*: Scale up/down quickly
5. *Measured service*: Pay for what you use

### Cloud Service Models

#### 1. IaaS (Infrastructure as a Service)
- Virtual machines, storage, networks
- *Examples*: AWS EC2, Azure VMs, Google Compute Engine
- *User Control*: OS, middleware, runtime, applications
- *Provider Control*: Virtualization, servers, storage, networking

#### 2. PaaS (Platform as a Service)
- Development platform and tools
- *Examples*: AWS Lambda, Google App Engine, Azure App Service
- *User Control*: Applications and data
- *Provider Control*: Runtime, middleware, OS, infrastructure

#### 3. SaaS (Software as a Service)
- Complete applications
- *Examples*: Salesforce, Gmail, Office 365
- *User Control*: User configuration
- *Provider Control*: Everything else

### Cloud Deployment Models

#### 1. Public Cloud
- *Owned by*: Third-party provider (AWS, Azure, GCP)
- *Access*: Over public internet
- *Benefits*: Cost-effective, scalable, no maintenance
- *Drawbacks*: Less control, security concerns

#### 2. Private Cloud
- *Owned by*: Single organization
- *Location*: On-premises or hosted
- *Benefits*: Full control, enhanced security, compliance
- *Drawbacks*: Higher cost, maintenance overhead

#### 3. Hybrid Cloud
- *Definition*: Combination of public and private clouds
- *Use case*: Keep sensitive data private, burst to public cloud
- *Benefits*: Flexibility, cost optimization, gradual migration

#### 4. Multi-Cloud
- *Definition*: Using multiple cloud providers
- *Benefits*: Avoid vendor lock-in, best-of-breed services
- *Challenges*: Complexity, integration, cost management

##  Core Cloud Services

### Compute Services

#### Virtual Machines

Traditional Server → Hypervisor → Multiple VMs

- *Benefits*: Isolation, multiple OS, resource sharing
- *Use cases*: Legacy applications, full OS control needed
- AWS: EC2, Azure: Virtual Machines, GCP: Compute Engine

#### Containers

Host OS → Container Runtime → Multiple Containers

- *Benefits*: Lightweight, portable, consistent environments
- *Docker*: Container packaging standard
- *Kubernetes*: Container orchestration platform
- AWS: ECS/EKS, Azure: AKS, GCP: GKE

#### Serverless/Functions
- *Concept*: Code runs without managing servers
- *Billing*: Pay per execution time
- *Benefits*: Auto-scaling, no server management, cost-effective
- AWS: Lambda, Azure: Functions, GCP: Cloud Functions

### Storage Services

#### Object Storage
- *Structure*: Flat namespace with unique keys
- *Use cases*: Web assets, backups, data lakes
- *Features*: Unlimited scalability, REST APIs, metadata
- AWS: S3, Azure: Blob Storage, GCP: Cloud Storage

#### Block Storage
- *Structure*: Raw block-level storage
- *Use cases*: Database storage, file systems, boot volumes
- *Features*: High IOPS, consistent performance
- AWS: EBS, Azure: Managed Disks, GCP: Persistent Disks

#### File Storage
- *Structure*: Hierarchical file system
- *Use cases*: Shared storage across multiple instances
- *Features*: POSIX compliance, concurrent access
- AWS: EFS, Azure: Files, GCP: Filestore

### Database Services

#### Relational Databases (SQL)
- *Managed Services*: Automated backups, patching, scaling
- *AWS*: RDS (MySQL, PostgreSQL, Oracle, SQL Server)
- *Azure*: SQL Database, Database for MySQL/PostgreSQL
- *GCP*: Cloud SQL, Cloud Spanner

#### NoSQL Databases
- *Document*: MongoDB-like (AWS DocumentDB, Azure Cosmos DB)
- *Key-Value*: High performance (AWS DynamoDB, Azure Cosmos DB)
- *Graph*: Relationship-focused (AWS Neptune, Azure Cosmos DB)
- *Column-family*: Big data analytics (AWS Keyspaces, GCP Bigtable)

## Networking in Cloud

### Virtual Private Cloud (VPC)
- *Purpose*: Isolated network environment in cloud
- *Components*: Subnets, route tables, internet gateways
- *Benefits*: Security, control, connectivity to on-premises

### Load Balancing
#### Application Load Balancer (Layer 7)
- *Features*: HTTP/HTTPS routing, path-based routing
- *Use cases*: Web applications, microservices

#### Network Load Balancer (Layer 4)
- *Features*: TCP/UDP traffic, ultra-high performance
- *Use cases*: Gaming, IoT, real-time applications

### Content Delivery Network (CDN)
- *Purpose*: Cache content globally for low latency
- *Benefits*: Faster load times, reduced origin server load
- *AWS: CloudFront, **Azure: CDN, **GCP*: Cloud CDN

### API Gateway
- *Purpose*: Manage, secure, and analyze APIs
- *Features*: Authentication, rate limiting, monitoring
- *Use cases*: Microservices architecture, third-party integrations

##  Security in Cloud

### Shared Responsibility Model

Customer Responsibility:
- Data encryption
- Network traffic protection
- Operating system updates
- Application security

Provider Responsibility:
- Physical security
- Infrastructure
- Hypervisor
- Network controls


### Identity and Access Management (IAM)
- *Principle of Least Privilege*: Minimum necessary permissions
- *Role-Based Access Control (RBAC)*: Assign permissions to roles
- *Multi-Factor Authentication (MFA)*: Additional security layer
- *Service Accounts*: For application-to-service authentication

### Data Security
#### Encryption at Rest
- *Purpose*: Protect stored data
- *Methods*: AES-256, customer-managed keys
- *Services*: Database encryption, storage encryption

#### Encryption in Transit
- *Purpose*: Protect data during transmission
- *Methods*: TLS/SSL, VPN tunnels
- *Implementation*: HTTPS, encrypted database connections

### Network Security
- *Security Groups*: Virtual firewalls for instances
- *Network ACLs*: Subnet-level security
- *WAF (Web Application Firewall)*: Protect web applications
- *DDoS Protection*: Absorb and mitigate attacks

## Scalability and Availability

### Horizontal vs Vertical Scaling
#### Horizontal Scaling (Scale Out)
- *Method*: Add more instances/servers
- *Benefits*: Better fault tolerance, unlimited scaling potential
- *Challenges*: Application complexity, data consistency

#### Vertical Scaling (Scale Up)
- *Method*: Increase instance size (CPU, RAM)
- *Benefits*: Simple, no application changes
- *Limits*: Hardware limitations, single point of failure

### Auto Scaling

CloudWatch Metrics → Auto Scaling Policy → Launch/Terminate Instances

- *Triggers*: CPU utilization, memory, custom metrics
- *Policies*: Target tracking, step scaling, predictive
- *Benefits*: Cost optimization, automatic capacity management

### High Availability Patterns

#### Multi-AZ Deployment
- *Concept*: Deploy across multiple availability zones
- *Benefits*: Fault tolerance, disaster recovery
- *Implementation*: Load balancers distribute traffic

#### Active-Passive Failover
- *Setup*: Primary active, secondary standby
- *Failover*: Manual or automatic switchover
- *Use case*: Database master-slave replication

#### Active-Active Setup
- *Setup*: Multiple active instances
- *Benefits*: Better resource utilization, load distribution
- *Challenges*: Data synchronization complexity

## Monitoring and DevOps

### Cloud Monitoring
- *Metrics*: CPU, memory, network, custom business metrics
- *Logs*: Application logs, system logs, audit logs
- *Alerts*: Threshold-based, anomaly detection
- *Services*: AWS CloudWatch, Azure Monitor, GCP Operations

### Infrastructure as Code (IaC)
- *Purpose*: Manage infrastructure using code
- *Benefits*: Version control, repeatability, consistency
- *Tools*: Terraform, AWS CloudFormation, Azure ARM Templates

### CI/CD in Cloud

Code Commit → Build → Test → Deploy to Staging → Deploy to Production

- *CI Tools*: AWS CodeBuild, Azure DevOps, GCP Cloud Build
- *CD Tools*: AWS CodeDeploy, Azure Pipelines, GCP Cloud Deploy
- *Benefits*: Faster deployments, reduced errors, automation

## Cost Optimization

### Pricing Models
#### On-Demand
- *Payment*: Pay per hour/second of usage
- *Use case*: Unpredictable workloads, short-term projects

#### Reserved Instances
- *Payment*: Upfront payment, commitment upto some years
- *Use case*: Steady-state workloads

#### Spot Instances
- *Payment*: Bid for unused capacity
- *Risk*: Can be terminated with short notice
- *Use case*: Fault-tolerant, batch processing

### Cost Optimization Strategies
1. *Right-sizing*: Match instance size to actual needs
2. *Auto-scaling*: Scale down during low usage
3. *Storage optimization*: Use appropriate storage tiers
4. *Reserved capacity*: Commit to long-term usage
5. *Monitoring*: Track and analyze spending patterns

##

### Microservices architecture in cloud context
Microservices break applications into small, independent services that communicate via APIs. In cloud, each service can be deployed as containers on Kubernetes, with API Gateway managing external access, service mesh for inter-service communication, and separate databases per service. This enables independent scaling and deployment.

## Cloud Migration Strategies (6 R's)

1. *Rehost* (Lift and Shift): Move as-is to cloud
2. *Replatform*: Minor optimizations during migration
3. *Repurchase*: Replace with SaaS solutions
4. *Refactor*: Redesign using cloud-native features
5. *Retire*: Eliminate unnecessary applications
6. *Retain*: Keep on-premises for now

## Emerging Cloud Trends

### Edge Computing
- *Purpose*: Process data closer to users/devices
- *Benefits*: Lower latency, reduced bandwidth
- *Use cases*: IoT, autonomous vehicles, AR/VR

### Serverless Architecture
- *Evolution*: From containers to functions to serverless databases
- *Benefits*: No server management, automatic scaling, pay-per-use
- *Services*: Lambda, API Gateway, DynamoDB, S3

### Cloud-Native Technologies
- *Containers*: Docker, Kubernetes
- *Service Mesh*: Istio, Linkerd
- *Observability*: Prometheus, Grafana, Jaeger
- *GitOps*: Infrastructure and applications managed via Git


## Common Terms

**Elasticity:** Automatically scale resources up/down based on demand

**Scalability:** Ability to handle increased load by adding resources

**Fault Tolerance:** System continues operating even when components fail

**High Availability:** System remains operational most of the time

**Disaster Recovery:** Plans and procedures to restore systems after major failures

**Multi-tenancy:** Multiple customers sharing same infrastructure securely


