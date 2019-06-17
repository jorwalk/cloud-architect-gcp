# Professional Cloud Architect

## Certification Exam Guide

### Section 1: Designing and planning a cloud solution architecture
1.1 Designing a solution infrastructure that meets business requirements. Considerations include:
- business use cases and product strategy
- cost optimization
- supporting the application design
- integration
- movement of data
- tradeoffs
- build, buy or modify
- success measurements (e.g., Key Performance Indicators (KPI), Return on Investment (ROI), metrics)
- Compliance and observability

1.2 Designing a solution infrastructure that meets technical requirements. Considerations include:
- high availability and failover design
- elasticity of cloud resources
- scalability to meet growth requirements

1.3 Designing network, storage, and compute resources. Considerations include:
- integration with on premises/multi-cloud environments
- Cloud native networking (VPC, peering, firewalls, container networking)
- identification of data processing pipeline
- matching data characteristics to storage systems
- data flow diagrams
- storage system structure (e.g., Object, File, RDBMS, NoSQL, NewSQL)
- mapping compute needs to platform products

1.4 Creating a migration plan (i.e., documents and architectural diagrams). Considerations include:
- integrating solution with existing systems
- migrating systems and data to support the solution
- licensing mapping
- network and management planning
- testing and proof-of-concept

1.5 Envisioning future solution improvements. Considerations include:
- cloud and technology improvements
- business needs evolution
- evangelism and advocacy

### Section 2: Managing and provisioning solution Infrastructure
2.1 Configuring network topologies. Considerations include:

- extending to on-premise (hybrid networking)
- extending to a multi-cloud environment which may include GCP to GCP communication
- security
- data protection

2.2 Configuring individual storage systems. Considerations include:
- data storage allocation
- data processing/compute provisioning
- security and access management
- network configuration for data transfer and latency
- data retention and data lifecycle management
- data growth management

2.3 Configuring compute systems. Considerations include:

- compute system provisioning
- compute volatility configuration (preemptible vs. standard)
- network configuration for compute nodes
- infrastructure provisioning technology configuration (e.g. Chef/Puppet/Ansible/Terraform)
- container orchestration (e.g. Kubernetes)

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
