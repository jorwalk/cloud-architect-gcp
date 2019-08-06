# Google Cloud Certified
## Professional Cloud Architect
### Job Role Description
A Professional Cloud Architect enables organizations to leverage Google Cloud technologies. With a thorough understanding of cloud architecture and Google Cloud Platform, this individual can design, develop, and manage robust, secure, scalable, highly available, and dynamic solutions to drive business objectives.

The Google Cloud Certified - Professional Cloud Architect exam assesses your ability to:

- Design and plan a cloud solution architecture
- Manage and provision the cloud solution infrastructure
- Design for security and compliance
- Analyze and optimize technical and business processes
- Manage implementations of cloud architecture
- Ensure solution and operations reliability

### Study Material
- [Certification Exam Guide](Certification-Exam-Guide.md)


### Sample Case Studies
During the exam for the Cloud Architect Certification, some of the questions may refer you to a case study that describes a fictitious business and solution concept. These case studies are intended to provide additional context to help you choose your answer(s). Review some sample case studies that may be used in the exam.

- [Mountkirk Games](https://cloud.google.com/certification/guides/cloud-architect/casestudy-mountkirkgames-rev2/)
- [Dress4Win](https://cloud.google.com/certification/guides/cloud-architect/casestudy-dress4win-rev2/)
- [TerramEarth](https://cloud.google.com/certification/guides/cloud-architect/casestudy-terramearth-rev2/)

### Practice Exam
The Cloud Architect practice exam will familiarize you with types of questions you may encounter on the certification exam and help you determine your readiness or if you need more preparation and/or experience.
- [Launch The Exam](https://forms.gle/SHcLhSXckievBNBn6)

## Online Learning
### Coursera
- [Preparing for the Google Cloud Professional Cloud Architect Exam](https://www.coursera.org/learn/preparing-cloud-professional-cloud-architect-exam/home/welcome)

### QwikLabs
- [GCP Essentials](GCP-Essentials.md)

Cloud Architecture

This fundamental-level quest is unique amongst the other Qwiklabs offerings. The labs have been curated to give IT professionals hands-on practice with topics and services that appear in the Google Cloud Certified Associate Cloud Engineer Certification. From IAM, to networking, to Kubernetes engine deployment, this quest is composed of specific labs that will put your GCP knowledge to the test. Be aware that while practice with these labs will increase your skills and abilities, we recommend that you also review the exam guide and other available preparation resources.

#### [Orchestrating the Cloud with Kubernetes](https://google.qwiklabs.com/focuses/557?parent=catalog)
In this lab you will learn how to: Provision a complete Kubernetes cluster using Google Container Engine; Deploy and manage Docker containers using kubectl; and Break an application into microservices using Kubernetes’ Deployments and Services.
#### [Deployment Manager - Full Production](https://google.qwiklabs.com/focuses/981?parent=catalog)
In this lab you will launch a service using Deployment Manager, and monitor it using Stackdriver. You will set up basic black box monitoring with Stackdriver Dashboard and establish uptime check alert notification to trigger incident response.
#### [Continuous Delivery with Jenkins in Kubernetes Engine](https://google.qwiklabs.com/focuses/1104?parent=catalog)
In this lab you will deploy and completely configure a continuous delivery pipeline using Jenkins running on Kubernetes Engine and go through the dev - deploy process.
#### [Networking 102](https://google.qwiklabs.com/focuses/556?parent=catalog)
Properly secured networks control connections and access into, out of, and among your resources. In this lab, you will practice deploying Networks and Subnetworks in two different GCP projects and multiple instances within the Google Cloud.
#### [Site Reliability Troubleshooting with Stackdriver APM](https://google.qwiklabs.com/focuses/4186?parent=catalog)
The objective of this lab is to familiarize yourself with the specific capabilities of Stackdriver to monitor GKE cluster infrastructure, Istio, and applications deployed on this infrastructure.

### Documentation
Visit the [documentation page](https://cloud.google.com/docs/) with overviews and in-depth discussions on the concepts and critical components of GCP.

* [Shared VPC](https://cloud.google.com/vpc/docs/shared-vpc)
* [VPC Network Peering](https://cloud.google.com/vpc/docs/vpc-peering)


### Possible Exam Scenario's
#### Preemptible VM's
- Create and terminate machine to save costs, but preserve disk state.
    - --no-auto-delete --disk example-disk
- Managed instance group with PVM's keep recreating every minute.
    - Health check / firewall configuration
#### Backup and Disaster Recovery
- Rollback plan for managed instance group serving website - 100's of instances
    - Object versioning on static data in Cloud Storage
    - Rolling updates
    - NOT snapshots
- Backup critical database with zero downtime and minimal resource usage
    - Scheduled cron jobs
    - Backup database data to another location(persistent disk/Cloud Storage)
- App Engine - need to push risky update to live environment
    - Versioning/traffic splitting
    - Deploy update to small % of traffic as canary update
#### Network Design for Security and Isolation
- Instance group VM's keep restarting every minute
    - Failing health check
    - Configure firewall to allow proper access to instance group VM's (subnet, tag) from load balancer IP
- On-premises network access to proper network resources
    - Restrict ingress firewall access to on-premises network IP range
- Failover from on-premises load balancer hosted application to GCP hosted instance group (hot standby)
    - Consider security and compliance
    - Allow firewall access at instance group level (subnet/tag) from outside source
- External SSH access disabled, but operations team needs to remotely manage VM's
    - Give operations team access to Cloud Shell
    - Not same scenario as removing external IP's
#### Legal Compliance and Audits

            