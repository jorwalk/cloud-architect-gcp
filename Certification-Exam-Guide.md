# Professional Cloud Architect

## Certification Exam Guide

### Section 1: Designing and planning a cloud solution architecture
1.1 Designing a solution infrastructure that meets business requirements. Considerations include:
- business use cases and product strategy
    * > What does success look like qualitatively
- cost optimization
    * > A separate step after business logic criteria are met
- supporting the application design
    * > What procedures and processes will be needed?
- integration
    * > Working with existing systems in parallel at first? Are there parts that must remain on premises?
- movement of data
    * > How and when will the data migrate to the new solutions? 
- tradeoffs
    * > Priorities. Timing can be critical to value.
- build, buy or modify
    * > Control vs. overhead vs. time
- success measurements (e.g., Key Performance Indicators (KPI), Return on Investment (ROI), metrics)
    * > What does success look like quantitatively?
- Compliance and observability

1.2 Designing a solution infrastructure that meets technical requirements. Considerations include:
- high availability and failover design
    * > What are the real criteria?
    * > What are the measurable goals?
- elasticity of cloud resources
    * > How do you want the solution to behave when busy? How will the system behave when under attack? How will it behave when traffic diminishes?
- scalability to meet growth requirements
    * > Scaling for growth is different from autoscaling to cover temporary demand non-linearities. When is it time to add a node, upgrade a service, or switch services?

1.3 Designing network, storage, and compute resources. Considerations include:
- integration with on premises/multi-cloud environments
    * > When to use gsutil, gsutil rsync, and Storage Transfer Service
- Cloud native networking (VPC, peering, firewalls, container networking)
    * > Understand all the networking services and how to connect for throughput, security, billing, and so forth.
- identification of data processing pipeline
- matching data characteristics to storage systems
    * > Velocity(how frequent), Volume(how much), Variety(format, structure), Volatility(how often does it change) -- which services match?
- data flow diagrams
    * > Very helpful to know where the data will travel through the solution and to look for bottlenecks and flow monitoring and control 
- storage system structure (e.g., Object, File, RDBMS, NoSQL, NewSQL)
    * > ACID(Atomicity, Consistency, Isolation, Durability) - What is eventual consistency? BASE(Basically Available, soft state, eventual consistency). Structure requirements?
- mapping compute needs to platform products
    * > Scale, capacity, control/overhead?

1.4 Creating a migration plan (i.e., documents and architectural diagrams). Considerations include:
- integrating solution with existing systems
    * > Parallel?
- migrating systems and data to support the solution
    * > How much, how to synchronize in both directions? Where is the source of data truth? 
- licensing mapping
    * > Data center license to cloud license -- may have different license or requirements for licensed software. 
- network and management planning
    * > How will on premises connect to the cloud solution? 
- testing and proof-of-concept
    * > Different ways to divide a test audience: random, group, phased, test. 

1.5 Envisioning future solution improvements. Considerations include:
- cloud and technology improvements
    * > When the technology improves, how will the solution embrace the improvements?
- business needs evolution
    * > When the business changes, how will the solution change? Most solutions don't just need to work once, they need to become self-sustaining.
- evangelism and advocacy
    * > Who are the gatekeepers and what do they need to know to effectively do their jobs?
    
### Section 2: Managing and provisioning solution Infrastructure
2.1 Configuring network topologies. Considerations include:

- extending to on-premise (hybrid networking)
    * > VPN. Interconnect.
- extending to a multi-cloud environment which may include GCP to GCP communication
    * > Interoperation interface. Stackdriver(GCP + AWS)
- security
- data protection
    * > Encryption, access, CSEK, KMS

2.2 Configuring individual storage systems. Considerations include:
- data storage allocation
    * > Where will the data be located? Resiliency? Change?
- data processing/compute provisioning
    * > Which Platform? What capacity?
- security and access management
    * > CSEK and Cloud Storage, for example. 
- network configuration for data transfer and latency
    * > Location makes a difference in egress charges and round-trip time.
- data retention and data lifecycle management
    * > What is the Nearline and Coldline policy? When to delete data?
- data growth management
    * > When do you need a different way to organize the data? How much/how big will the current design support?

2.3 Configuring compute systems. Considerations include:

- compute system provisioning
    * > Speed, throughput, capacity, burstiness? Turn off when not in use?
- compute volatility configuration (preemptible vs. standard)
    * > Stateful vs. Stateless. Tolerance for lost data/state
- network configuration for compute nodes
    * > Firewall rules, load balancing, NAT, VPN
- infrastructure provisioning technology configuration (e.g. Chef/Puppet/Ansible/Terraform)
    * > Deployment Manager...others. The value of self-documenting and automated orchestration of infrastructure.
- container orchestration (e.g. Kubernetes)
    * > The value of container-based development: portability, scalability, fault isolation, platform agnostic deployment, CI/CD development methods

### Section 3: Designing for security and compliance
3.1 Designing for security. Considerations include:

- Identity and Access Management (IAM)
- Resource hierarchy (organizations, folders, projects)
- data security (key management, encryption)
- penetration testing
- Separation of Duties (SoD)
- security controls
- Managing customer-supplied encryption keys with Cloud KMS

3.2 Designing for legal compliance. Considerations include:

- legislation (e.g., Health Insurance Portability and Accountability Act (HIPAA), Children’s Online Privacy Protection Act (COPPA), etc.)
- audits (including logs)
- certification (e.g., Information Technology Infrastructure Library (ITIL) framework)

### Section 4: Analyzing and optimizing technical and business processes

4.1 Analyzing and defining technical processes. Considerations include:

- Software Development Lifecycle Plan (SDLC)
- continuous integration / continuous deployment
- troubleshooting / post mortem analysis culture
- testing and validation
- IT enterprise process (e.g. ITIL)
- business continuity and disaster recovery

4.2 Analyzing and defining business processes. Considerations include:

- stakeholder management (e.g. Influencing and facilitation)
- change management
- team assessment / skills readiness
- decision making process
- customer success management
- cost optimization / resource optimization (Capex / Opex)

4.3 Developing procedures to test resilience of solution in production (e.g., DiRT and Simian Army)

### Section 5: Managing implementation

5.1 Advising development/operation team(s) to ensure successful deployment of the solution. Considerations include:
- application development
- API best practices
- testing frameworks (load/unit/integration)
- data and system migration tooling

5.2 Interacting with Google Cloud using GCP SDK (gcloud, gsutil and bq). Considerations include:
- local installation
- Google Cloud Shell

### Section 6: Ensuring solution and operations reliability

6.1 Monitoring/Logging/Alerting solution

6.2 Deployment and release management

6.3 Supporting operational troubleshooting

6.4 Evaluating quality control measures
