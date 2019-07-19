https://aws.amazon.com/architecture/well-architected/

What are the questions that need to be asked in order to consult for a Google Cloud Platform architecture?
- Do you have image, movie or pdf documents that need to be accessed by uses?
    - [ ] Yes 
        - Use Google Cloud CDN to cache and retreve those assets on Edge networks. 
        - Use a Google Storage Bucket -  multi-regional
- Micro-services or Monolith
- [ ]  Micro-services
    - Kubernetes 
- [ ]  Monolith
    - Compute Engine Instance Groups
    - advise on cloud functions
    - advise on micro-services
       
        

- Networking
    - create a custom vpc network and subnet in chosen region
    - create an ephemeral ip address
    - create a firewall
    - for production a static ip address is required and needs to be reserved.

Analysis separate from recommendations    
    
# Google Cloud Platform
## Management
### Marketplace
### Billing

### APIs & Services
#### Library
#### Credentials

### Support 
#### Cases
#### Chat Support
#### Phone Support

### IAM & admin
#### IAM
#### Identity & Organization
#### Organization policies
#### Quotas
#### Service Accounts
#### Labels
#### Settings
#### Privacy & Security
#### Cryptographic Keys
#### Identity-Aware Proxy
#### Roles
#### Audit Logs

### Getting started

### Security
#### Security Container Center
#### Identity-Aware Proxy
#### Access Context Manager
#### VPC Service Controls
#### Binary Authorization
#### Data Loss Prevention
#### Cryptographic Keys
#### Access Approval
#### Web Security Scanner


## Compute
### App Engine
#### Dashboard
#### Services
#### Versions
#### Instances
#### Task Queues
#### Cron jobs
#### Security scans
#### Firewall rules
#### Quotas
#### Memcache
#### Search
#### Settings 

### Compute Engine
#### VM instances
#### Instance groups
#### Instance templates
#### Sole tenant nodes
#### Disk
#### Snapshots
#### Images
#### TPUs
#### Committed use discounts
#### Metadata
#### Health checks
#### Zones
#### Network endpoint groups
#### Operations
#### Security scans
#### Settings

### Kubernetes Engine
#### Clusters
#### Workloads
#### Service & Ingress
#### Applications
#### Configuration
#### Storage 


### Cloud Functions
### Cloud Run

## Storage
### Bigtable
### Datastore
#### Entities
#### Dashboard
#### Indexes
#### Admin

### Firestore
#### 

### Filestore
### Storage
#### Browser
#### Transfer
#### Transfer Appliance
#### Settings

### SQL
### Spanner
Cloud Spanner is a fully managed relational database service that offers transactional consistency 
and high availability at global scale. To use Cloud Spanner, create a Cloud Spanner instance within your project, 
then set up your development environment to access Cloud Spanner so that you can add data.
### Memorystore
Cloud Memorystore for Redis provides a fully-managed in-memory store with high availability, 
seamless capacity scaling, and compliance with open-source protocol. 

Use Cloud Memorystore for Redis to easily deploy, manage, and monitor your in-memory stores. 
 

## Networking
### VPC networking
- You cannot switch from custom to automatic subnetting mode.
#### VPC networks
- How would you best connect your on-premises network to Google Cloud while keeping traffic private?
    - Use a VPN connection that is tied to your VPC network.

#### External IP addresses

- External IP's are either ephemeral or static
    - Ephemeral by default, and change when instance is restarted
    - Static IPs can be reserved and attached to an instance, used for production systems.
    - The static IP must be in the same region as an instance
     
#### Firewall rules
- Every VPC network has a managed firewall
- Manages both inbound(ingress) and outbound(egress) traffic
- Can be applied to entire VPC network or individual instances
#### Routes
- Roadmap of how to get from Point A to point B
- Mapping of an IP range to a destination
- Tell a VPC network what route to take to send packets to an IP address
- Can either use default routing table, or create custom rules
#### VPC network peering
#### Shared VPC
#### Serverless VPC access

### Network services
#### Load balancing
- Distributes user requests among sets of instances
- Works with instance groups
- Used for auto-scaling, batch processing, and distributed traffic, and fault tolerance.
#### Cloud DNS
- DNS translates a computer domain names (like google.com) into IP addresses
- Google Cloud DNS is a high-performance, resilient, global Domain Name System service that publishes
your domain names to the global DNS in a cost-effective way.
#### Cloud CDN
#### Cloud NAT
#### Traffic Director

### Hybrid Connectivity
#### VPN
#### Interconnect
#### Cloud Routers

### Network Service Tiers
Network Service Tiers enable you to optimize network quality and performance vs. cost for your resources and projects.
### Network Security
#### Cloud Armor
#### SSL policies


## Stackdriver
- Provides powerful monitoring, logging, and diagnostics for cloud operations.
- Natively monitor GCP, Amazon Web Services (AWS), or a hybrid of both environments.
    - Combine metrics, logs, and metadata from both platforms into a single viewing environment
- Robust partner ecosystem to make working
    - PagerDuty, BMC, Splunk, and others.
### Monitoring
- Full-stack monitoring for Google Cloud Platform and Amazon Web Services
### Debug
- Investigate your code's behavior in production
### Trace
- Find performance bottlenecks in production
### Logging
- Real-time log management and analysis
### Error Reporting
- Identify and understand your application errors
### Profiler
- CPU and Heap profiling

## Tools
### Cloud Build
### Cloud Scheduler
### Cloud Tasks
### Container Registry
### Identity Platform
### Source Repositories
- Git repository hosted on GCP
- Built in Source code editor
- Integrates with Stackdriver debugger
- Connect to GitHub or Bitbucket

### Deployment Manager
- Specify resources needed for your application in a declarative format using yaml
- Repeatable deployment process
- Declarative language, focus on application
- Template driven

### Private Catalog
### Endpoints

## Big Data
### Composer
### Dataflow
### BigQuery
### Pub/Sub
### Dataproc
### IoT Core
### Data Catalog
### Data Fusion
### Genomics
### Healthcare
### Dataprep

## Artificial Intelligence
### Data Labeling
### AI Platform
### Natural Language
### Tables
### Talent Solutions
### Translation
### Vision
### Video Intelligence 

## Other Google Solutions
### Google Maps