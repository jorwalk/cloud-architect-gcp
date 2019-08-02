Instance Groups and Load Balancers

This exercise will work with instance groups, load balancers, and autoscalers.

This will be a fairly involved exercise. You will be performing the following steps:

*   Create two instance templates, which will be customized via two different apache scripts.

*   Create a managed instance group from a ‘version 1’ template.

*   Configure an HTTP load balancer to serve traffic to your group.

*   Stress test your instance group to trigger autoscaling.

*   Update your managed instance group with a ‘version 2’ template.

Let’s get started.

Create a single compute engine instance using the n1-standard machine type, using the default Debian boot disk image. Name the instance ‘load-test’.

Use the below script when creating the instance in the startup script field to install Apache.

`#! /bin/bash`

`apt-get update`

`apt-get install -y apache2`

\-- Go to Compute Engine - VM Instances.

Create a new instance.

Name it ‘load-test’.

Choose your closest zone.

Expand the ‘management, disks, networking, SSH keys’ menu.

Paste the above script under Automation - Startup script.

Click Create to create instance.

Create your first instance template. Name the template web-template-v1. Set machine type to f1-micro. Use the default Debian boot disk image. Enable HTTP access.

In the startup script field of the template, copy/paste the below script to install Apache and set your website to a ‘version 1’ page.

`#! /bin/bash`

`apt-get update`

`apt-get install -y apache2`

`cat <<EOF > /var/www/html/index.html`

`<html><body><h1>VERSION 1</h1>`

`<h2>Welcome to your custom website.</h2>`

`</body></html>`

`EOF`

\---- Go to Compute Engine - Instance templates.

Create a new instance template.

Name it ‘web-template-v1’.

Set Machine type to f1-micro.

Place check mark in ‘Allow HTTP traffic’.

Expand the ‘management, disks, networking, SSH keys’ menu.

Paste the above script under Automation - Startup script.

Click Create to create the template.

Create your second instance template. Name the template web-template-v2. Set machine type to f1-micro. Use the default Debian boot disk image. Enable HTTP access.

In the startup script field of the template, copy/paste the below script to install Apache and set your website to a ‘version 2’ page.

`#! /bin/bash`

`apt-get update`

`apt-get install -y apache2`

`cat <<EOF > /var/www/html/index.html`

`<html><body><h1>VERSION 2</h1>`

`<h2>Welcome to your custom website.</h2>`

`</body></html>`

`EOF`

> Go to Compute Engine - Instance templates.
> 
> Create a new instance template.
> 
> Name it ‘web-template-v2’.
> 
> Set Machine type to f1-micro.
> 
> Place check mark in ‘Allow HTTP traffic’.
> 
> Expand the ‘management, disks, networking, SSH keys’ menu.
> 
> Paste the above script under Automation - Startup script.
> 
> Click Create to create the template.

Create a managed instance group from your template web-template-v1. Choose the web-template-v1 template to use. Enable Autoscaling based on HTTP load balancing usage. Under autoscaling, set a minimum of 2 instances and maximum of 6. Leave the other autoscaling metrics set to defaults. 

Before creating the group, create a health check (name it ‘web-health’). Leave protocol settings as defaults. Set the check interval and timeout to 10 seconds and unhealthy threshold to 3 consecutive failures, and save the health check.

Once the above is complete, click Create to create the instance group.

> Go to Compute Engine - Instance groups.
> 
> Create a new instance group.
> 
> Name it ‘web-group’.
> 
> Set Location to Multi-zone, and choose your closest region from the drop-down menu.
> 
> In the Instance template drop-down menu, select web-template-v1.
> 
> Set Autoscaler
> 
> Under Autoscaling options - set the ‘Autoscale based on’ drop-down to ‘HTTP load balancing usage.’
> 
> Under ‘minimum number of instances, type 2.
> 
> Under ‘maximum number of instances, type 6.
> 
> Set health check
> 
> On the drop-down menu for health check, select ‘create a health check’.
> 
> Name the health check ‘web-health’.
> 
> Leave protocol settings as default.
> 
> Under Health criteria - set both Check interval and Timeout to 10 seconds and Unhealthy threshold to 3 consecutive failures.
> 
> Click Save and continue.

Back on the main instance group screen, click Create to create the group.

Next create the HTTP load balancer.

Go to Load Balancer settings and choose to create a load balancer, and choose HTTP Load Balancing.

> From top left menu, go to Network Services - Load balancing
> 
> Click Create load balancer
> 
> Under HTTP(S) Load Balancing, click Start configuration.

Name the load balancer ‘web-lb’.

Set backend configuration to use the ‘web-group’ instance group.

> Click Backend configuration
> 
> From the drop-down menu, choose Backend services - Create a backend service.
> 
> Name the backend ‘web-backend’.
> 
> Under the New backend menu:
> 
> Select ‘web-group’ from the ‘instance group’ drop-down menu.
> 
> Under the Health check drop-down menu, select the ‘web-health’ health check.
> 
> Click Create to finish the backend configuration.

Set up the frontend configuration.

> Click Frontend configuration.
> 
> Name the frontend ‘web-frontend’.
> 
> Under IP address drop-down menu, choose Create IP address.
> 
> Name the static IP address ‘lb-static’, and click RESERVE.
> 
> Click Done to complete frontend configuration.

Click Host and path rules to place a check mark in the field, although we won’t be configuring this field.

Click Review and finalize. Save the frontend IP address somewhere, as this will be the website frontend.

Click Create to create the load balancer.

You will need to wait about 5 minutes for the load balancer to fully initialize with the instance group. Try to use the frontend IP address in a new tab. If it does not bring up your Version 1 website, wait a few minutes and try again.

Once the frontend IP address properly displays version 1 of your website, go back to your instance group.

Notice the number of instances currently created.

Let’s now stress test our website.

SSH into your ‘load-test’ instance.

Enter the following command to send a large amount of traffic to your frontend IP address:

`ab -n 1000000 -c 1000 `http`://(YOUR_FRONTEND_IP)/`

Note, you need to add the forward slash at the end of your IP address or the command will not work.

You will then see your instance start flooding your site with requests.

You may need to wait a few minutes and refresh your page a few times, but go back go your instance group and observe your group start creating additional instances to handle the load. Make sure you can still access your website by its frontend IP address in a new tab.

Next we will update our instance group to version 2 of our website.

In your instance group, click ROLLING UPDATE.

We are going to do a full update of our website. Set the configuration to use template ‘web-template-v2’. Leave all other settings as default and click update.

> Click ROLLING UPDATE in your instance group.
> 
> On the Template drop-down menu, choose ‘web-template-v2’.
> 
> Click Update.

You will again need to wait a few minutes while periodically refreshing your Instance group page. Observe at the bottom which instances are using template ‘web-template-v1’ and which ones are using ‘web-template-v2. Once most of the instances in your group are using the newer template, access your website with the frontend IP address again in a new tab and confirm you are on VERSION 2 of your website.

CLEAN UP

To avoid unwanted charges, we need to clean up our resources in a set order:

First, delete your load balancer in Load balancing settings. When deleting it, place a check mark to confirm deleting the backend service as well. Otherwise, delete the backend and frontend services separately.

Once the load balancer and backend/frontends are deleted. Next delete your instance group by going to your instance group page, and select the option to delete the group.

Delete your instance templates in the same manner.

Delete your ‘load-test’ instance.

Release your reserved static IP address by going to VPC Network - External IP addresses, and releasing the ‘lb-static’ address.

This completes the exercise. Congratulations!