Let’s first tag our instances so we can create firewall rules to match.

Using the web console, give instance-1 the network tag of ‘ssh-allow’.

> Edit instance-1, and in the Network tags field, type ssh-allow.

Using gcloud command in Cloud Shell, give instance-2 the network tag of ‘icmp-allow’.

> `gcloud compute instances add-tags --zone us-central1-a instance-2 --tags icmp-allow`

Now create the following firewall rules for network ‘custom-network’.

Using the web console, create a rule to allow SSH (TCP port 22) from any source address to any instance with the tag ‘ssh-allow’.

> Go to top left menu, scroll down to VPC Network, and click on Firewall rules.
> 
> Click CREATE FIREWALL RULE
> 
> Name the rule ssh-allow.
> 
> Select Network ‘custom-network’.
> 
> Leave Priority at 1000.
> 
> Leave Targets as ‘specified target tags’.
> 
> Add Target tags of ‘ssh allow’.
> 
> Set Source IP ranges to 0.0.0.0/0.
> 
> Leave radio button checked for ‘Specified protocols and ports’ under ‘Protocols and ports.
> 
> Type ‘tcp:22’ for the port.
> 
> Click Create.

Using gcloud command in Cloud Shell, create another rule to allow ICMP to any instance with the tag ‘icmp-allow’, but only from instances with the tag ‘ssh-allow’ AND that are part of your VPC network range (source range will be 10.1.0.0/22). If needed, you can construct the rule using the web console and click the gcloud reference link at the bottom for cross reference.

> `gcloud compute firewall-rules create icmp-allow --direction=INGRESS --priority=1000 --network=custom-network --action=ALLOW --rules=icmp --source-ranges=10.1.0.0/22 --target-tags=icmp-allow`

Now SSH into instance-1.

Ping instance-2’s internal IP address.

Ping instance-2’s external IP address. Notice it did not work. This is because we’ve limited ICMP to our internal VPC only. Ping the external IP comes from an outside source.

CLEAN UP 

To avoid additional charges, delete the resources we’ve used.

In order: delete your Compute Engine instances, then custom firewall rules, and delete the custom VPC network last.