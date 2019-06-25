# Challenge: GCP Architecture
This quest of "Challenge Labs" gives the student preparing for the Google Cloud Certified Professional Cloud Architect certification hands-on practice with common business/technology solutions using GCP architectures. Challenge Labs do not provide the "cookbook" steps, but require solutions to be built with minimal guidance, across many GCP technologies. All labs have activity tracking and in order to earn this badge you must score 100% in each lab. This quest is not easy and will put your GCP technology skills to the test. Be aware that while practice with these labs will increase your knowledge and abilities, we recommend additional study, experience, and background in cloud architecture to prepare for this certification.

## [Google Cloud Essential Skills: Challenge Lab](https://google.qwiklabs.com/focuses/1734?parent=catalog)
### Topics tested
* Create a Linux Virtual Machine Instance
* Enable public access to VM instance
* Running basic Apache Web Server
* Test your server 

### Challenge scenario
Your company is ready to launch a brand new product! Because you are entering a totally new space, you have decided to deploy a new website as part of the product launch. The new site is complete, but the person who built the new site left the company before they could deploy it.

### Running a Basic Apache Web Server
A virtual machine instance on Google Compute Engine can be controlled like any standard Linux server. Deploy a simple Apache web server (a placeholder for the new product site) to learn the basics of running a server on a virtual machine instance.

#### Create a Linux VM Instance

Create a Linux virtual machine, name it "apache" and specify the zone as "us-central1-a".

a) Create a Compute Engine instance, add necessary firewall rules.
```
gcloud compute firewall-rules create vm1-allow-ingress-tcp-port80-from-subnet1 \
    --action allow \
    --direction ingress \
    --rules tcp:80 \
    --priority 50 \
    --target-tags http-server
```

```
gcloud compute instances create apache --machine-type n1-standard-2  --tags http-server --zone us-central1-a
```

b) Add Apache2 HTTP Server to your instance
```
sudo apt-get update && sudo apt-get install apache2 -y
```
#### Enable Public Access to VM Instance

While creating the Linux instance, make sure to apply the appropriate firewall rules so that potential customers can find your new product.

- Your VM instance is not publicly accessible because the VM instance does not have the proper tag that allows Compute Engine to apply the appropriate firewall rules, or your project does not have a firewall rule that allows traffic to your instance's external IP address.

- You are trying to access the VM using an https address. Check that your URL is http:// EXTERNAL_IP and not https:// EXTERNAL_IP

## [Deploy a Compute Instance with a Remote Startup Script](https://google.qwiklabs.com/focuses/1735?parent=catalog)
### Topics tested
- Create a storage bucket for startup scripts.
- Create a virtual machine that runs a startup script from cloud storage.
- Configure HTTP access for the virtual machine.
- Deploy an application on an instance.
### Challenge scenario
You have been given the responsibility of managing the configuration of your organization's Google Cloud virtual machines. You have decided to make some changes to the framework used for managing the deployment and configuration machines - you want to make it easier to modify the startup scripts used to initialize a number of the compute instances. Instead of storing startup scripts directly in the instances' metadata, you have decided to store the scripts in a Cloud Storage bucket and then configure the virtual machines to point to the relevant script file in the bucket.

A basic bash script that installs the Apache web server software called install-web.sh has been provided for you as a sample startup script. You can download this from the Student Resources links on the left side of the page.
### Your challenge
- Configure Instance Metadata. The Running Startup Scripts documentation page explains how Compute Engine instance metadata can be used to configure startup scripts.
- Check if your Compute Engine instance is executing the startup script. Use the Serial Console for the running virtual machine to look at the startup events to make sure that the startup script is being executed.
- Check permissions. Your Compute Engine instance might not have the correct permissions required to read the startup-script from the storage bucket. The virtual machine needs to be given permissions that align with the storage permissions.
- Check firewalls. If the startup script has installed the software you may be unable to connect if a firewall has not been correctly configured.
- Check the URL and address. You will be unable to connect to the Apache web server if you are trying to access the Compute Engine instance using an https address rather than http; or you are using the incorrect IP address. Check that your URL is `http://[EXTERNAL_IP]` rather than `https://[EXTERNAL_IP]` or `http://[INTERNAL_IP]`

a) Create a firewall rule that allows http access to compute engine
```
gcloud compute firewall-rules create vm1-allow-ingress-tcp-port80-from-subnet1 \
    --action allow \
    --direction ingress \
    --rules tcp:80 \
    --priority 50 \
    --target-tags http-server
```


b) Create a storage bucket for startup scripts.
```
gsutil mb gs://my-storage-bucket-001122334455666
```


c) Create a virtual machine that runs a startup script from cloud storage.
```
gcloud compute instances create apache3 --scopes storage-ro \
    --tags http-server \
    --zone us-central1-a \
    --metadata startup-script-url=gs://my-storage-bucket-001122334455666/install-web.sh
```

## [Configure a Firewall and a Startup Script with Deployment Manager](https://google.qwiklabs.com/focuses/1736?parent=catalog)
### Topics tested
- Configure a deployment template to include a startup script
- Configure a deployment template to add a firewall rule allowing http traffic
- Configure a deployment template to add a networking tag to a compute instance
- Deploy a configuration using Deployment Manager

### Challenge scenario
Your company is ready to launch a brand new product and you have been asked to develop a Deployment Manager template to deploy and configure the Google Cloud environment that is required to support this product. To start off, you've been given an existing basic deployment manager template that just deploys a single compute instance.

### Your challenge
Modify the deployment manager template to add a firewall rule to:

- Allow inbound HTTP traffic to tagged instances.
- Include a startup script for the compute instance that installs the apache web server application.
- Add the firewall tag to the compute instance that is created so that it can be accessed from the internet.
```
   tags:
        items: ["http"]
    metadata:
      items:
      - key: startup-script
        value: "apt-get update \n apt-get install -y apache2"
    # Add resource
    - type: compute.v1.firewall
      name: http-firewall
      properties:
        targetTags: ["http"]
        sourceRanges: ["0.0.0.0/0"]
        allowed:
        - IPProtocol: TCP
          ports: ["80", "8080"]
```

```
gcloud deployment-manager deployments create deploy-qwik --config qwiklabs.yaml
```
