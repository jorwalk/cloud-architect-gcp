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

## [Continuous Delivery with Jenkins in Kubernetes Engine](https://google.qwiklabs.com/focuses/1104?parent=catalog)
In this lab, you will learn how to set up a continuous delivery pipeline with Jenkins on Kubernetes engine. Jenkins is the go-to automation server used by developers who frequently integrate their code in a shared repository.

### Overview

- What is Kubernetes Engine?   
- What is Jenkins?
- What is Continuous Delivery / Continuous Deployment?
- Setup
- Clone Repository
- Provisioning Jenkins
- Install Helm
- Configure and Install Jenkins
- Connect to Jenkins
- Understanding the Application
- Deploying the Application
- Creating the Jenkins Pipeline
- Creating the Development Environment
- Kick off Deployment
- Deploying a Canary Release
- Deploying to production

## [Networking 102](https://google.qwiklabs.com/focuses/556?parent=catalog)
In this lab you will allow and deny access to a network using firewall rules. You'll deploy the following lab environment of Projects, Networks, and Subnetworks to the Google Cloud Platform.
### What you will learn
- How default and user-created Networks are configured
- How to use the latest features of Firewalls for more precise and flexible control of connections
- How to use routes in Compute Engine
- How to identify and understand network-specific IAM roles

### Overview
- Create Virtual Private Cloud (VPC) Networks and Instances
- How Default and User-Created VPC Networks are Configured
- User-created networks
- Advanced firewall rules
- Using Cloud Routes
- Network-specific IAM roles

Run the following to create the network mynetwork with auto subnets:
```
gcloud compute networks create mynetwork --subnet-mode=auto
```
Run the following command to create the network privatenet with custom subnets:
```
gcloud compute networks create privatenet --subnet-mode=custom
```
Now run the following command to create the custom subnet in the privatenet network:
```
gcloud compute networks subnets create privatesubnet --network=privatenet \
--region=us-central1 --range=10.0.0.0/24 --enable-private-ip-google-access
```

Create some instances to use later for testing in all networks by running these commands:

```
gcloud compute instances create default-us-vm --zone=us-central1-a --network=default

gcloud compute instances create mynet-us-vm --zone=us-central1-a --network=mynetwork

gcloud compute instances create mynet-eu-vm --zone=europe-west1-b --network=mynetwork

gcloud compute instances create privatenet-bastion --zone=us-central1-c \
--subnet=privatesubnet --can-ip-forward

gcloud compute instances create privatenet-us-vm --zone=us-central1-f \
--subnet=privatesubnet
```

Now add some ingress firewall rules to allow us to SSH and ping the instances. Use the gcloud command line in Cloud Shell:
```
gcloud beta compute firewall-rules create mynetwork-allow-icmp --network mynetwork \
--action ALLOW --direction INGRESS --rules icmp

gcloud beta compute firewall-rules create mynetwork-allow-ssh --network mynetwork \
--action ALLOW --direction INGRESS --rules tcp:22

gcloud beta compute firewall-rules create mynetwork-allow-internal --network \
mynetwork --action ALLOW --direction INGRESS --rules all \
--source-ranges 10.128.0.0/9

gcloud beta compute firewall-rules list \
--filter="network:mynetwork"
```

First, create the same rules as before for the privatenet network. Enter the following commands in Cloud Shell:
```
gcloud beta compute firewall-rules create privatenet-allow-icmp \
--network privatenet --action ALLOW --direction INGRESS --rules icmp

gcloud beta compute firewall-rules create privatenet-allow-ssh \
--network privatenet --action ALLOW --direction INGRESS --rules tcp:22

gcloud beta compute firewall-rules create privatenet-allow-internal \
--network privatenet --action ALLOW --direction INGRESS --rules all \
--source-ranges 10.0.0.0/24
```

## [Site Reliability Troubleshooting with Stackdriver APM](https://google.qwiklabs.com/focuses/4186?parent=catalog)

### What you'll learn
- How to deploy a microservices application on an existing GKE cluster
- How to select appropriate SLIs/SLOs for an application
- How to implement SLIs using Stackdriver Monitoring features
- How to use Stackdriver Trace, Profiler, and Debugger to identify software issues





