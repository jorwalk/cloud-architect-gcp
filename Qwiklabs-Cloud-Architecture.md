# Cloud Architecture
This fundamental-level quest is unique amongst the other Qwiklabs offerings. The labs have been curated to give IT professionals hands-on practice with topics and services that appear in the Google Cloud Certified Associate Cloud Engineer Certification. From IAM, to networking, to Kubernetes engine deployment, this quest is composed of specific labs that will put your GCP knowledge to the test. Be aware that while practice with these labs will increase your skills and abilities, we recommend that you also review the exam guide and other available preparation resources.

## [Orchestrating the Cloud with Kubernetes](https://google.qwiklabs.com/focuses/557?parent=catalog)
In this lab you will learn how to: Provision a complete Kubernetes cluster using Google Container Engine; Deploy and manage Docker containers using kubectl; and Break an application into microservices using Kubernetes’ Deployments and Services.

In the cloud shell environment type the following command to set the zone:
```
gcloud config set compute/zone us-central1-b
```
After you set the zone, start up a cluster for use in this lab:

```
gcloud container clusters create io
```

## [Deployment Manager - Full Production](https://google.qwiklabs.com/focuses/981?parent=catalog)
In this lab, you will launch a service using an infrastructure orchestration tool called Deployment Manager and monitor the service using Stackdriver. In Stackdriver, you will set up basic black box monitoring with a Stackdriver dashboard and establish an Uptime Check (alert notification) to trigger incident response.

### Objectives
In this lab, you will learn to:

- Launch a cloud service from a collection of templates.
- Configure basic black box monitoring of an application.
- Create an uptime check to recognize a loss of service.
- Establish an alerting policy to trigger incident response procedures.
- Create and configure a dashboard with dynamically updated charts.
- Test the monitoring and alerting regimen by applying a load to the service.
- Test the monitoring and alerting regimen by simulating a service outage.