# GCP Essentials
In this introductory-level quest, you will get hands-on practice with the Google Cloud Platform’s fundamental tools and services. GCP Essentials is the recommended first Quest for the Google Cloud learner—you will come in with little or no prior cloud knowledge, and come out with practical experience that you can apply to your first GCP project. From writing Cloud Shell commands and deploying your first virtual machine, to running applications on Kubernetes Engine or with load balancing, GCP Essentials is a prime introduction to the platform’s basic features.

### [A Tour of Qwiklabs and the Google Cloud Platform](https://google.qwiklabs.com/focuses/2794?parent=catalog)
In this first hands-on lab you will access Qwiklabs and the Google Cloud Platform Console and use the basic GCP features: Projects, Resources, IAM Users, Roles, Permissions, APIs, and Cloud Shell.

### [Creating a Virtual Machine](https://google.qwiklabs.com/focuses/3563?parent=catalog)
In this hands-on lab, you’ll learn how to create a Google Compute Engine virtual machine and understand zones, regions, and machine types.
```
gcloud compute instances create gcelab2 --machine-type n1-standard-2  
--zone [your_zone]
```

### [Getting Started with Cloud Shell & gcloud](https://google.qwiklabs.com/focuses/563?parent=catalog)
In this hands-on lab, you will learn how to connect to computing resources hosted on Google Cloud Platform via the web. You will also learn how to use Cloud Shell and the Cloud SDK gcloud command.

Create a Storage Bucket
```
gsutil mb gs://unique-name
```

Upload some data to a bucket you created
```
gsutil cp test.dat gs://unique-name
```

### [Kubernetes Engine: Qwik Start](https://google.qwiklabs.com/focuses/878?parent=catalog)
Google Kubernetes Engine provides a managed environment for deploying, managing, and scaling your containerized applications using Google infrastructure. This hands-on lab shows you how deploy a containerized application with Kubernetes Engine.

Set a default compute zone
```
gcloud config set compute/zone us-central1-a
```

Create a Kubernetes Engine Cluster
```
gcloud container clusters create [CLUSTER-NAME]
``` 

Get authentication credentials for the cluster
```
gcloud container clusters get-credentials [CLUSTER-NAME]
```

Deploying an application to the cluster
```
kubectl run hello-server --image=gcr.io/google-samples/hello-app:1.0 --port 8080
```

Create a Kubernetes Service
```
kubectl expose deployment hello-server --type="LoadBalancer"
```

### [Set Up Network and HTTP Load Balancers](https://google.qwiklabs.com/focuses/558?parent=catalog)

Set the default region and zone for all resources
```
gcloud config set compute/zone us-central1-a
gcloud config set compute/region us-central1
```

#### Create multiple web server instances

startup script to be used by every virtual machine 
```
cat << EOF > startup.sh
#! /bin/bash
apt-get update
apt-get install -y nginx
service nginx start
sed -i -- 's/nginx/Google Cloud Platform - '"\$HOSTNAME"'/' /var/www/html/index.nginx-debian.html
EOF
```
Create an instance template, which uses the startup script:
```
gcloud compute instance-templates create nginx-template \
         --metadata-from-file startup-script=startup.sh
```
Create a target pool. A target pool allows a single access point to all the instances in a group 
and is necessary for load balancing in the future steps.
```
gcloud compute target-pools create nginx-pool
```
Create a managed instance group using the instance template:
```
gcloud compute instance-groups managed create nginx-group \
         --base-instance-name nginx \
         --size 2 \
         --template nginx-template \
         --target-pool nginx-pool
```
List the compute engine instances and you should see all of the instances created:
```
gcloud compute instances list
```

Now configure a firewall so that you can connect to the machines on port 80 via the `EXTERNAL_IP` addresses:
```
gcloud compute firewall-rules create www-firewall --allow tcp:80
```

#### Create a Network Load Balancer
Network load balancing allows you to balance the load of your systems based on incoming IP protocol data, such as address, port, and protocol type. You also get some options that are not available, with HTTP(S) load balancing. For example, you can load balance additional TCP/UDP-based protocols such as SMTP traffic. And if your application is interested in TCP-connection-related characteristics, network load balancing allows your app to inspect the packets, where HTTP(S) load balancing does not.

Create an L3 network load balancer targeting your instance group:
```
gcloud compute forwarding-rules create nginx-lb \
         --region us-central1 \
         --ports=80 \
         --target-pool nginx-pool
```
List all Google Compute Engine forwarding rules in your project.
```
gcloud compute forwarding-rules list
```

#### Create a HTTP(s) Load Balancer
HTTP(S) load balancing provides global load balancing for HTTP(S) requests destined for your instances. You can configure URL rules that route some URLs to one set of instances and route other URLs to other instances. Requests are always routed to the instance group that is closest to the user, provided that group has enough capacity and is appropriate for the request. If the closest group does not have enough capacity, the request is sent to the closest group that does have capacity.

First, create a health check. Health checks verify that the instance is responding to HTTP or HTTPS traffic:
```
gcloud compute http-health-checks create http-basic-check
```
Define an HTTP service and map a port name to the relevant port for the instance group. Now the load balancing service can forward traffic to the named port:
```
gcloud compute instance-groups managed \
       set-named-ports nginx-group \
       --named-ports http:80
```
Create a backend service:
```
gcloud compute backend-services create nginx-backend \
      --protocol HTTP --http-health-checks http-basic-check --global
```
Add the instance group into the backend service:
```
gcloud compute backend-services add-backend nginx-backend \
    --instance-group nginx-group \
    --instance-group-zone us-central1-a \
    --global
```
Create a default URL map that directs all incoming requests to all your instances:
```
gcloud compute url-maps create web-map \
    --default-service nginx-backend
```
Create a target HTTP proxy to route requests to your URL map:
```
gcloud compute target-http-proxies create http-lb-proxy \
    --url-map web-map
```
Create a global forwarding rule to handle and route incoming requests. A forwarding rule sends traffic to a specific target HTTP or HTTPS proxy depending on the IP address, IP protocol, and port specified. The global forwarding rule does not support multiple ports.
```
gcloud compute forwarding-rules create http-content-rule \
        --global \
        --target-http-proxy http-lb-proxy \
        --ports 80
```
After creating the global forwarding rule, it can take several minutes for your configuration to propagate.
```
gcloud compute forwarding-rules list
```

