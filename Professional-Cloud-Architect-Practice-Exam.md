# Professional Cloud Architect Practice Exam
---
1 - Because you do not know every possible future use for the data TerramEarth collects, you have decided to build a system that captures and stores all raw data in case you need it later. How can you most cost-effectively accomplish this goal?
- [ ] A. Have the vehicles in the field stream the data directly into BigQuery.
- [ ] B. Have the vehicles in the field pass the data to Cloud Pub/Sub and dump it into a Cloud Dataproc cluster that stores data in Apache Hadoop Distributed File System (HDFS) on persistent disks.
- [ ] C. Have the vehicles in the field continue to dump data via FTP, adjust the existing Linux machines, and use a collector to upload them into Cloud Dataproc HDFS for storage
- [ ] D. Have the vehicles in the field continue to dump data via FTP, and adjust the existing Linux machines to immediately upload it to Cloud Storage with gsutil.

#### Feedback
> A is not correct because TerramEarth has cellular service for 200,000 vehicles, and each vehicle sends at least one row (120 fields) per second. This exceeds BigQuery's maximum rows per second per project quota[1]. Additionally, there are 20 million total vehicles, most of which perform uploads when connected by a maintenance port, which drastically exceeds the streaming project quota further.

> B is not correct because although Cloud Pub/Sub is a fine choice for this application, Cloud Dataproc is probably not. The question posed asks us to optimize for cost. Because Cloud Dataproc is optimized for ephemeral, job-scoped clusters[2], a long-running cluster with large amounts of HDFS storage could be very expensive to build and maintain when compared to managed and specialized storage solutions like Cloud Storage[3].

> C is not correct because the question asks us to optimize for cost, and because Cloud Dataproc is optimized for ephemeral, job-scoped clusters[2], a long-running cluster with large amounts of HDFS storage could be very expensive to build and maintain when compared to managed and specialized storage solutions like Cloud Storage[3].

> D is correct because several load-balanced Compute Engine VMs would suffice to ingest 9 TB per day, and Cloud Storage is the cheapest per-byte storage offered by Google. Depending on the format, the data could be available via BigQuery immediately, or shortly after running through an ETL job. Thus, this solution meets business and technical requirements while optimizing for cost.

- https://cloud.google.com/bigquery/quotas#streaming_inserts
- https://cloud.google.com/blog/products/gcp/fastest-track-to-apache-hadoop-and-spark-success-using-job-scoped-clusters-on-cloud-native-architecture
- https://cloud.google.com/blog/products/data-analytics/10-tips-for-building-long-running-clusters-using-cloud-dataproc

---

2 - Today, TerramEarth maintenance workers receive interactive performance graphs for the last 24 hours (86,400 events) by plugging their maintenance tablets into the vehicle. The support group wants support technicians to view this data remotely to help troubleshoot problems. You want to minimize the latency of graph loads. How should you provide this functionality?
- [ ] A. Execute queries against data stored in a Cloud SQL.
- [ ] B. Execute queries against data indexed by vehicle_id.timestamp in Cloud Bigtable.
- [ ] C. Execute queries against data stored on daily partitioned BigQuery tables
- [ ] D. Execute queries against BigQuery with data stored in Cloud Storage via BigQuery federation.

#### Feedback
> A is not correct because Cloud SQL provides relational database services that are well-suited to OLTP workloads, but not storage and low-latency retrieval of time-series data.

> B is correct because Cloud Bigtable is optimized for time-series data. It is cost-efficient, highly available, and low-latency. It scales well. Best of all, it is a managed service that does not require significant operations work to keep running.

> C is not correct because BigQuery is fast for wide-range queries, but it is not as well-optimized for narrow-range queries as Cloud Bigtable is. Latency will be an order of magnitude shorter with Cloud Bigtable for this use.

> D is not correct because the objective is to minimize latency, and although BigQuery federation offers tremendous flexibility, it doesn't perform as well as native BigQuery storage[2], and will have longer latency than Cloud Bigtable for narrow-range queries.

- https://cloud.google.com/bigtable/docs/schema-design-time-series#time-series-cloud-bigtable
- https://cloud.google.com/bigquery/external-data-sources

---

3 - Your agricultural division is experimenting with fully autonomous vehicles. You want your architecture to promote strong security during vehicle operation. Which two architecture characteristics should you consider?
- [ ] A. Use multiple connectivity subsystems for redundancy.
- [ ] B. Require IPv6 for connectivity to ensure a secure address space.
- [ ] C. Enclose the vehicle’s drive electronics in a Faraday cage to isolate chips.
- [ ] D. Use a functional programming language to isolate code execution cycles.
- [ ] E. Treat every microservice call between modules on the vehicle as untrusted.
- [ ] F. Use a Trusted Platform Module (TPM) and verify firmware and binaries on boot.

#### Feedback
> A is not correct because this improves system durability, but it doesn't have any impact on the security during vehicle operation.

> B is not correct because IPv6 doesn't have any impact on the security during vehicle operation, although it improves system scalability and simplicity.

> C is not correct because it doesn't have any impact on the security during vehicle operation, although it improves system durability.

> D is not correct because merely using a functional programming language doesn't guarantee a more secure level of execution isolation. Any impact on security from this decision would be incidental at best.

> E is correct because this improves system security by making it more resistant to hacking, especially through man-in-the-middle attacks between modules.

> F is correct because this improves system security by making it more resistant to hacking, especially rootkits or other kinds of corruption by malicious actors.

---

4 - Which of TerramEarth’s legacy enterprise processes will experience significant change as a result of increased Google Cloud Platform adoption?
- [ ] A. OpEx/CapEx allocation, LAN change management, capacity planning
- [ ] B. Capacity planning, TCO calculations, OpEx/CapEx allocation
- [ ] C. Capacity planning, utilization measurement, data center expansion
- [ ] D. Data center expansion,TCO calculations, utilization measurement

#### Feedback
> A is not correct because LAN change management processes don't need to change significantly. TerramEarth can easily peer their on-premises LAN with their Google Cloud Platform VPCs, and as devices and subnets move to the cloud, the LAN team's implementation will change, but the change management process doesn't have to.

> B is correct because all of these tasks are big changes when moving to the cloud. Capacity planning for cloud is different than for on-premises data centers; TCO calculations are adjusted because TerramEarth is using services, not leasing/buying servers; OpEx/CapEx allocation is adjusted as services are consumed vs. using capital expenditures.

> C is not correct because measuring utilization can be done in the same way, often with the same tools (along with some new ones). Data center expansion is not a concern for cloud customers; it is part of the undifferentiated heavy lifting that is taken care of by the cloud provider.

> D is not correct because data center expansion is not a concern for cloud customers; it is part of the undifferentiated heavy lifting that is taken care of by the cloud provider. Measuring utilization can be done in the same way, often with the same tools (along with some new ones).

---

5 - You analyzed TerramEarth’s business requirement to reduce downtime and found that they can achieve a majority of time saving by reducing customers’ wait time for parts. You decided to focus on reduction of the 3 weeks’ aggregate reporting time. Which modifications to the company’s processes should you recommend?
- [ ] A. Migrate from CSV to binary format, migrate from FTP to SFTP transport, and develop machine learning analysis of metrics.
- [ ] B. Migrate from FTP to streaming transport, migrate from CSV to binary format, and develop machine learning analysis of metrics.
- [ ] C. Increase fleet cellular connectivity to 80%, migrate from FTP to streaming transport, and develop machine learning analysis of metrics.
- [ ] D. Migrate from FTP to SFTP transport, develop machine learning analysis of metrics, and increase dealer local inventory by a fixed factor.

#### Feedback
> A is not correct because machine learning analysis is a good means toward the end of reducing downtime, but shuffling formats and transport doesn't directly help at all.

> B is not correct because machine learning analysis is a good means toward the end of reducing downtime, and moving to streaming can improve the freshness of the information in that analysis, but changing the format doesn't directly help at all.

> C is correct because using cellular connectivity will greatly improve the freshness of data used for analysis from where it is now, collected when the machines are in for maintenance. Streaming transport instead of periodic FTP will tighten the feedback loop even more. Machine learning is ideal for predictive maintenance workloads.

> D is not correct because machine learning analysis is a good means toward the end of reducing downtime, but the rest of these changes don't directly help at all.

---

6 - Your company wants to deploy several microservices to help their system handle elastic loads. Each microservice uses a different version of software libraries. You want to enable their developers to keep their development environment in sync with the various production services. Which technology should you choose?
- [ ] A. RPM/DEB
- [ ] B. Containers
- [ ] C. Chef/Puppet
- [ ] D. Virtual machines

#### Feedback
> A is not correct because although OS packages are a convenient way to distribute and deploy libraries, they don't directly help with synchronizing. Even with a common repository, the development environments will probably deviate from production.

> B is correct because using containers for development, test, and production deployments abstracts away system OS environments, so that a single host OS image can be used for all environments. Changes that are made during development are captured using a copy-on-write filesystem, and teams can easily publish new versions of the microservices in a repository.

> C is not correct because although infrastructure configuration as code can help unify production and test environments, it is very difficult to make all changes during development this way.

> D is not correct because virtual machines run their own OS, which will eventually deviate in each environment, just as now.

---

7 - Your company wants to track whether someone is present in a meeting room reserved for a scheduled meeting. There are 1000 meeting rooms across 5 offices on 3 continents. Each room is equipped with a motion sensor that reports its status every second. You want to support the data upload and collection needs of this sensor network. The receiving infrastructure needs to account for the possibility that the devices may have inconsistent connectivity. Which solution should you design?
- [ ] A. Have each device create a persistent connection to a Compute Engine instance and write messages to a custom application.
- [ ] B. Have devices poll for connectivity to Cloud SQL and insert the latest messages on a regular interval to a device specific table.
- [ ] C. Have devices poll for connectivity to Cloud Pub/Sub and publish the latest messages on a regular interval to a shared topic for all devices.
- [ ] D. Have devices create a persistent connection to an App Engine application fronted by Cloud Endpoints, which ingest messages and write them to Cloud Datastore.

#### Feedback

> A is not correct because having a persistent connection does not handle the case where the device is disconnected.

> B is not correct because Cloud SQL is a relational database and not the best fit for sensor data. Additionally, the frequency of the writes has the potential to exceed the supported number of concurrent connections.

> C is correct because Cloud Pub/Sub can handle the frequency of this data, and consumers of the data can pull from the shared topic for further processing.

> D is not correct because having a persistent connection does not handle the case where the device is disconnected.

- https://cloud.google.com/sql/
- https://cloud.google.com/pubsub/

---

8 - Your company wants to try out the cloud with low risk. They want to archive approximately 100 TB of their log data to the cloud and test the analytics features available to them there, while also retaining that data as a long-term disaster recovery backup. Which two steps should they take?
- [ ] A. Load logs into BigQuery.
- [ ] B. Load logs into Cloud SQL.
- [ ] C. Import logs into Stackdriver.
- [ ] D. Insert logs into Cloud Bigtable.
- [ ] E. Upload log files into Cloud Storage.

#### Feedback
> A is correct because BigQuery is the fully managed cloud data warehouse for analytics and supports the analytics requirement.

> B is not correct because Cloud SQL does not support the expected 100 TB. Additionally, Cloud SQL is a relational database and not the best fit for time-series log data formats.

> C is not correct because Stackdriver is optimized for monitoring, error reporting, and debugging instead of analytics queries.

> D is not correct because Cloud Bigtable is optimized for read-write latency and analytics throughput, not analytics querying and reporting.

> E is correct because Cloud Storage provides the Coldline storage class to support long-term storage with infrequent access, which would support the long-term disaster recovery backup requirement.

- https://cloud.google.com/bigquery/
- https://cloud.google.com/stackdriver/
- https://cloud.google.com/storage/docs/storage-classes#coldline
- https://cloud.google.com/sql/
- https://cloud.google.com/bigtable/

---

9 - You set up an autoscaling instance group to serve web traffic for an upcoming launch. After configuring the instance group as a backend service to an HTTP(S) load balancer, you notice that virtual machine (VM) instances are being terminated and re-launched every minute. The instances do not have a public IP address. You have verified that the appropriate web response is coming from each instance using the curl command. You want to ensure that the backend is configured correctly. What should you do?
- [ ] A. Ensure that a firewall rule exists to allow source traffic on HTTP/HTTPS to reach the load balancer.
- [ ] B. Assign a public IP to each instance, and configure a firewall rule to allow the load balancer to reach the instance public IP.
- [ ] C. Ensure that a firewall rule exists to allow load balancer health checks to reach the instances in the instance group.
- [ ] D. Create a tag on each instance with the name of the load balancer. Configure a firewall rule with the name of the load balancer as the source and the instance tag as the destination.

#### Feedback
> A is not correct because the issue to resolve is the VMs being terminated, not access to the load balancer.

> B is not correct because this introduces a security vulnerability without addressing the primary concern of the VM termination.

> C is correct because health check failures lead to a VM being marked unhealthy and can result in termination if the health check continues to fail. Because you have already verified that the instances are functioning properly, the next step would be to determine why the health check is continuously failing.

> D is not correct because the source of the firewall rule that allows load balancer and health check access to instances is defined IP ranges, and not a named load balancer. Tagging the instances for the purpose of firewall rules is appropriate but would probably be a descriptor of the application, and not the load balancer.


- https://cloud.google.com/load-balancing/docs/health-check-concepts
- https://cloud.google.com/load-balancing/docs/https/

---
10 - Your organization has a 3-tier web application deployed in the same network on Google Cloud Platform. Each tier (web, API, and database) scales independently of the others. Network traffic should flow through the web to the API tier, and then on to the database tier. Traffic should not flow between the web and the database tier. How should you configure the network?
- [ ] A. Add each tier to a different subnetwork.
- [ ] B. Set up software-based firewalls on individual VMs.
- [ ] C. Add tags to each tier and set up routes to allow the desired traffic flow.
- [ ] D. Add tags to each tier and set up firewall rules to allow the desired traffic flow.

#### Feedback
> A is not correct because the subnetwork alone will not allow and restrict traffic as required without firewall rules.

> B is not correct because this adds complexity to the architecture and the instance configuration.

> C is not correct because routes still require firewall rules to allow traffic as requests. Additionally, the tags are used for defining the instances the route applies to, and not for identifying the next hop. The next hop is either an IP range or instance name, but in the proposed solution the tiers are only identified by tags.

> D is correct because as instances scale, they will all have the same tag to identify the tier. These tags can then be leveraged in firewall rules to allow and restrict traffic as required, because tags can be used for both the target and source.

- https://cloud.google.com/vpc/docs/using-vpc
- https://cloud.google.com/vpc/docs/add-remove-network-tags
- https://cloud.google.com/vpc/docs/routes

---

11 - Your organization has 5 TB of private data on premises. You need to migrate the data to Cloud Storage. You want to maximize the data transfer speed. How should you migrate the data?
- [ ] A. Use gsutil
- [ ] B. Use gcloud.
- [ ] C. Use GCS REST API.
- [ ] D. Use Storage Transfer Service.

#### Feedback
> A is correct because gsutil gives you access to write data to Cloud Storage.

> B is not correct because gcloud is the command-line interface for common platform tasks and does not include accessing Cloud Storage.

> C is not correct because the data size would require a resumable upload, and that does not meet the requirement of maximizing the data transfer speed.

> D is not correct because Storage Transfer Service is for importing online data, not on-premises. Your data source can be an Amazon Simple Storage Service (Amazon S3) bucket, an HTTP/HTTPS location, or a Cloud Storage bucket.

- https://cloud.google.com/storage/docs/gsutil
- https://cloud.google.com/storage/docs/json_api/v1/how-tos/upload
- https://cloud.google.com/storage-transfer/docs/overview
- https://cloud.google.com/sdk/gcloud/
- https://cloud.google.com/storage/docs/uploading-objects

--- 
12 - You are designing a mobile chat application. You want to ensure that people cannot spoof chat messages by proving that a message was sent by a specific user. What should you do? 
- [ ] A. Encrypt the message client-side using block-based encryption with a shared key.
- [ ] B. Tag messages client-side with the originating user identifier and the destination user.
- [ ] C. Use a trusted certificate authority to enable SSL connectivity between the client application and the server.
- [ ] D. Use public key infrastructure (PKI) to encrypt the message client-side using the originating user’s private key.

#### Feedback
> A is not correct because although this would encrypt the message, it does not validate either the client or the server.

> B is not correct because a malicious actor could spoof the user identifier and destination user information.

> C is not correct because SSL only requires the server to have a signed certificate and does not require validating the client.

> D is correct because PKI requires that both the server and the client have signed certificates, validating both the client and the server.

--- 
13 - You are designing a large distributed application with 30 microservices. Each of your distributed microservices needs to connect to a database backend. You want to store the credentials securely. Where should you store the credentials?
- [ ] A. In the source code
- [ ] B. In an environment variable
- [ ] C. In a key management system
- [ ] D. In a config file that has restricted access through ACLs

#### Feedback
> A is not correct because storing credentials in source code and source control is discoverable, in plain text, by anyone with access to the source code. This also introduces the requirement to update code and do a deployment each time the credentials are rotated.

> B is not correct because consistently populating environment variables would require the credentials to be available, in plain text, when the session is started.

> C is correct because key management systems generate, use, rotate, encrypt, and destroy cryptographic keys and manage permissions to those keys.

> D is not correct because instead of managing access to the config file and updating manually as keys are rotated, it would be better to leverage a key management system. Additionally, there is increased risk if the config file contains the credentials in plain text.

- https://cloud.google.com/kms/

---
14 - Mountkirk Games wants to set up a real-time analytics platform for their new game. The new platform must meet their technical requirements. Which combination of Google technologies will meet all of their requirements?
- [ ] A. Kubernetes Engine, Cloud Pub/Sub, and Cloud SQL
- [ ] B. Cloud Dataflow, Cloud Storage, Cloud Pub/Sub, and BigQuery
- [ ] C. Cloud SQL, Cloud Storage, Cloud Pub/Sub, and Cloud Dataflow
- [ ] D. Cloud Pub/Sub, Compute Engine, Cloud Storage, and Cloud Dataproc

#### Feedback
> A is not correct because Cloud SQL is the only storage listed, is limited to 10 TB of storage, and is better suited for transactional workloads. Mountkirk Games needs queries to access at least 10 TB of historical data for analytic purposes.

> B is correct because: 
> - Cloud Dataflow dynamically scales up or down, can process data in real time, and is ideal for processing data that arrives late using Beam windows and triggers.
> - Cloud Storage can be the landing space for files that are regularly uploaded by users’ mobile devices. 
> - Cloud Pub/Sub can ingest the streaming data from the mobile users.
> - BigQuery can query more than 10 TB of historical data.

> C is not correct because Cloud SQL is the only storage listed, is limited to 10TB of storage, and is better suited for transactional workloads. Mountkirk Games needs queries to access at least 10 TB of historical data for analytic purposes.

> D is not correct because Mountkirk Games needs the ability to query historical data. While this might be possible using workarounds, such as BigQuery federated queries for Cloud Storage or Hive queries for Cloud Dataproc, these approaches are more complex. BigQuery is a simpler and more flexible product that fulfills those requirements.

- https://cloud.google.com/sql/docs/quotas#fixed-limits
- https://beam.apache.org/documentation/programming-guide/#triggers
- https://cloud.google.com/solutions/using-apache-hive-on-cloud-dataproc
- https://beam.apache.org/documentation/programming-guide/#windowing
- https://cloud.google.com/bigquery/external-data-sources

---

15 - Mountkirk Games has deployed their new backend on Google Cloud Platform (GCP). You want to create a thorough testing process for new versions of the backend before they are released to the public. You want the testing environment to scale in an economical way. How should you design the process?
- [ ] A. Create a scalable environment in GCP for simulating production load.
- [ ] B. Use the existing infrastructure to test the GCP-based backend at scale.
- [ ] C. Build stress tests into each component of your application and use resources from the already deployed production backend to simulate load.
- [ ] D. Create a set of static environments in GCP to test different levels of load—for example, high, medium, and low.
#### Feedback
> A is correct because simulating production load in GCP can scale in an economical way.

> B is not correct because one of the pain points about the existing infrastructure was precisely that the environment did not scale well.

> C is not correct because it is a best practice to have a clear separation between test and production environments. Generating test load should not be done from a production environment.

> D is not correct because Mountkirk Games wants the testing environment to scale as needed. Defining several static environments for specific levels of load goes against this requirement.

- https://cloud.google.com/community/tutorials/load-testing-iot-using-gcp-and-locust
- https://github.com/GoogleCloudPlatform/distributed-load-testing-using-kubernetes

---
![](https://lh6.googleusercontent.com/Uu5noDQje_I5TjEBqrfCXflAm2zv4uGldV2NIACoSkkF5JMYaBSKKV8Jg90Co2Xqa6tHQ586gQ=w740)
- [ ] A. Cloud Storage, Cloud Dataflow, Compute Engine
- [ ] B. Cloud Storage, App Engine, Cloud Load Balancing
- [ ] C. Container Registry, Google Kubernetes Engine, Cloud Load Balancing
- [ ] D. Cloud Functions, Cloud Pub/Sub, Cloud Deployment Manager
#### Feedback
> A is not correct because Mountkirk Games wants to set up a continuous delivery pipeline, not a data processing pipeline. Cloud Dataflow is a fully managed service for creating data processing pipelines.

> B is not correct because a Cloud Load Balancer distributes traffic to Compute Engine instances. App Engine and Cloud Load Balancer are parts of different solutions.

> C is correct because: 
> - Google Kubernetes Engine is ideal for deploying small services that can be updated and rolled back quickly. It is a best practice to manage services using immutable containers.
> - Cloud Load Balancing supports globally distributed services across multiple regions. It provides a single global IP address that can be used in DNS records. Using URL Maps, the requests can be routed to only the services that Mountkirk wants to expose.
> - Container Registry is a single place for a team to manage Docker images for the services.

> D is not correct because you cannot reserve a single frontend IP for cloud functions. When deployed, an HTTP-triggered cloud function creates an endpoint with an automatically assigned IP.

- https://cloud.google.com/load-balancing/docs/https/
- https://cloud.google.com/load-balancing/docs/https/global-forwarding-rules#add_a_global_forwarding_rule
- https://cloud.google.com/solutions/best-practices-for-operating-containers#immutability
- https://cloud.google.com/dataflow/
- https://cloud.google.com/load-balancing/docs/load-balancing-overview
- https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address#reserve_new_static
- https://cloud.google.com/container-registry/
- https://cloud.google.com/functions/docs/calling/http

---

16 - Your customer is moving their corporate applications to Google Cloud Platform. The security team wants detailed visibility of all resources in the organization. You use Resource Manager to set yourself up as the org admin. What Cloud Identity and Access Management (Cloud IAM) roles should you give to the security team?
- [ ] A. Org viewer, Project owner
- [ ] B. Org viewer, Project viewer
- [ ] C. Org admin, Project browser
- [ ] D. Project owner, Network admin

#### Feedback
> A is not correct because Project owner is too broad. The security team does not need to be able to make changes to projects.

> B is correct because:
> - Org viewer grants the security team permissions to view the organization's display name.
> - Project viewer grants the security team permissions to see the resources within projects.

> C is not correct because Org admin is too broad. The security team does not need to be able to make changes to the organization.

> D is not correct because Project owner is too broad. The security team does not need to be able to make changes to projects.
- https://cloud.google.com/resource-manager/docs/access-control-org#using_predefined_roles

---
17 - To reduce costs, the Director of Engineering has required all developers to move their development infrastructure resources from on-premises virtual machines (VMs) to Google Cloud Platform. These resources go through multiple start/stop events during the day and require state to persist. You have been asked to design the process of running a development environment in Google Cloud while providing cost visibility to the finance department. Which two steps should you take?
- [ ] A. Use persistent disks to store the state. Start and stop the VM as needed.
- [ ] B. Use the --auto-delete flag on all persistent disks before stopping the VM.
- [ ] C. Apply VM CPU utilization label and include it in the BigQuery billing export.
- [ ] D. Use BigQuery billing export and labels to relate cost to groups.
- [ ] E. Store all state in local SSD, snapshot the persistent disks, and terminate the VM.
- [ ] F. Store all state in Cloud Storage, snapshot the persistent disks, and terminate the VM.
#### Feedback
> A is correct because persistent disks will not be deleted when an instance is stopped.

> B is not correct because the --auto-delete flag has no effect unless the instance is deleted. Stopping an instance does not delete the instance or the attached persistent disks.

> C is not correct because labels are used to organize instances, not to monitor metrics.

> D is correct because exporting daily usage and cost estimates automatically throughout the day to a BigQuery dataset is a good way of providing visibility to the finance department. Labels can then be used to group the costs based on team or cost center.

> E is not correct because the state stored in local SSDs will be lost when the instance is stopped.

> F is not correct because there is no need for persistent disks or snapshots if the state is to be stored in Cloud Storage.

- https://cloud.google.com/compute/docs/instances/instance-life-cycle
- https://cloud.google.com/sdk/gcloud/reference/compute/instances/create#--disk
- https://cloud.google.com/billing/docs/how-to/export-data-bigquery
- https://cloud.google.com/sdk/gcloud/reference/compute/instances/set-disk-auto-delete#--auto-delete
- https://cloud.google.com/compute/docs/disks/local-ssd#data_persistence
- https://cloud.google.com/resource-manager/docs/creating-managing-labels

---
18 - Your company has decided to make a major revision of their API in order to create better experiences for their developers. They need to keep the old version of the API available and deployable, while allowing new customers and testers to try out the new API. They want to keep the same SSL and DNS records in place to serve both APIs. What should they do?
- [ ] A. Configure a new load balancer for the new version of the API.
- [ ] B. Reconfigure old clients to use a new endpoint for the new API.
- [ ] C. Have the old API forward traffic to the new API based on the path.
- [ ] D. Use separate backend services for each API path behind the load balancer.
#### Feedback
> A is not correct because configuring a new load balancer would require a new or different SSL and DNS records which conflicts with the requirements to keep the same SSL and DNS records.

> B is not correct because it goes against the requirements. The company wants to keep the old API available while new customers and testers try the new API.

> C is not correct because it is not a requirement to decommission the implementation behind the old API. Moreover, it introduces unnecessary risk in case bugs or incompatibilities are discovered in the new API.

> D is correct because an HTTP(S) load balancer can direct traffic reaching a single IP to different backends based on the incoming URL.

- https://cloud.google.com/load-balancing/docs/https/url-map
- https://cloud.google.com/load-balancing/docs/https/global-forwarding-rules
- https://cloud.google.com/load-balancing/docs/backend-service

---
19 - The database administration team has asked you to help them improve the performance of their new database server running on Compute Engine. The database is used for importing and normalizing the company’s performance statistics. It is built with MySQL running on Debian Linux. They have an n1-standard-8 virtual machine with 80 GB of SSD zonal persistent disk. What should they change to get better performance from this system in a cost-effective manner?
- [ ] A. Increase the virtual machine’s memory to 64 GB.
- [ ] B. Create a new virtual machine running PostgreSQL.
- [ ] C. Dynamically resize the SSD persistent disk to 500 GB.
- [ ] D. Migrate their performance metrics warehouse to BigQuery.
#### Feedback
> A is not correct because increasing the memory size will not improve persistent disk throughput.

> B is not correct because the DB administration team is requesting help with their MySQL instance. Migration to a different product should not be the solution when other optimization techniques can still be applied first.

> C is correct because persistent disk performance is based on the total persistent disk capacity attached to an instance and the number of vCPUs that the instance has. Incrementing the persistent disk capacity will increment its throughput and IOPS, which in turn improve the performance of MySQL.

> D is not correct because the DB administration team is requesting help with their MySQL instance. Migration to a different product should not be the solution when other optimization techniques can still be applied first.

- https://cloud.google.com/compute/docs/disks/#pdspecs
- https://cloud.google.com/compute/docs/disks/performance