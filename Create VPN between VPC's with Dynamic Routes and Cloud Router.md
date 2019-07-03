View the external IP addresses that have been created for each ‘vpn-static-1’ and ‘vpn-static-2’. You will need these address when creating the VPN gateways.

> Find reserved IP's under left menu - VPC Network - External IP addresses.

Go to Compute Engine instances, and SSH into ‘vpn-1-a’. Ping ‘vpn-2-b’ by both its external and internal IP address. Which one works, and which one does not?

Since vpn-1-a is in a different VPC as the other two instances, it cannot reach them by internal IP.

We next need to set each VPC to use global dynamic routing vs. regional dynamic routing.

Go to your VPC networks, and set each custom VPC to use global dynamic routing.

> Go to VPC Networks by going to left menu - VPC Network
> 
> Click on vpn-network-1.
> 
> Click Edit at the top.
> 
> Changing 'Dynamic routing mode' from Regional to Global, and click Save.
> 
> Do the same actions for vpn-network-2.

Before creating our VPN gateways, we need to create our Cloud Routers for each network.

Go to the menu to create Cloud Routers, and choose to create a new one.

> From left menu, go to Interconnect - Cloud Routers
> 
> Click CREATE ROUTER. 

Name the first router ‘vpn-router-1’.

Assign it to the ‘vpn-network-1’ network.

Assign it to the us-west1 region.

Give it a Google ASN of 65000

Click Create to create the router.

Create the second router.

Name the first router ‘vpn-router-2’.

Assign it to the ‘vpn-network-3’ network.

Assign it to the us-central1 region.

Give it a Google ASN of 65001

Click Create to create the second router.

Now we will create the VPN gateways. Go to your VPN configuration menu, and create a new VPN connection.

> From left menu, go to Interconnect - VPN.
> 
> Click 'CREATE VPN CONNECTION'

Name the first VPN gateway ‘vpn-gateway-1’. Assign it to the ‘vpn-network-1’ network. Assign to the us-west1 region. Choose the reserved IP address labeled ‘vpn-static-1’.

Further down, create a tunnel to connect to.

Enter the remote peer IP address. This is the ‘vpn-static-2’ IP address we created (actual address will be different for everyone).

Leave IKE version as IKEv2.

Type a shared secret in the listed field (use any password you like).

Set dynamic routing options:

Choose the Dynamic (BGP) option.

Select the router we just created (‘vpn-router-1’).

> Choose from the dropdown menu.

Configure BGP session settings.

> Click the edit (pencil) icon next to BGP session settings.

In BGP settings, give the name ‘bgp-1’.

Assign the Peer ASN of 65001.

Provide the Cloud Router BGP IP of 169.254.0.1.

Provide BGP Peer IP of 169.254.0.2.

Save and continue.

Click Create to create the VPN gateway.

Start creating the second VPN gateway for vpn-network-2.

Name the first VPN gateway ‘vpn-gateway-2’. Assign it to the ‘vpn-network-2’ network. Assign to the us-central1 region. Choose the reserved IP address labeled ‘vpn-static-2’.

Further down, create a tunnel to connect to.

Enter the remote peer IP address. This is the ‘vpn-static-1’ IP address we created (actual address will be different for everyone).

Leave IKE version as IKEv2.

Type a same shared secret from the first gateway in the listed field.

Set dynamic routing options:

Select the router we just created (‘vpn-router-2’).

> Choose from the dropdown menu.

Configure BGP session settings.

> Click the edit (pencil) icon next to BGP session settings.

Configure BGP session settings.

In BGP settings, give the name ‘bgp-2’.

Assign the Peer ASN of 65000.

Provide the Cloud Router BGP IP of 169.254.0.2.

Provide BGP Peer IP of 169.254.0.1.

Save and continue.

Click Create to create the VPN gateway.

Go back to the Cloud Routers menu. You may have to wait up to 5 minutes for the connection to show as successful (green check marks). Refresh your screen to see updated status.

From the VPN gateway overview menu, wait a couple minutes and refresh your screen until you have green check marks for each gateway.

Go to Compute Engine, SSH into vpn-1-a. Attempt to ping the internal IP address of vpn-2-b. It should work. Also attempt to ping the internal IP address of vpn-2-c. They should both work because our cloud routers are able to automatically detect all subnets.

Let’s add an additional subnet to vpn-network-1. Call it ‘subnet-d’, assign to region us-east1, and assign it the IP range of 10.1.4.0/24.

> From the VPC networks menu, click on 'vpn-network-1'
> 
> Click 'Add Subnet'.
> 
> Name it 'subnet-d'
> 
> In Region dropdown menu, choose us-east1
> 
> In iP Address range, enter 10.1.4.0/24
> 
> Click ADD

Next, create a new Compute Engine instance.

Call it ‘vpn-1-d’.

Assign it to region us-east1.

Assign the network interface to vpn-network1 and subnet-d, then create the instance.

> Expand the menu 'Management, disks, networking, SSH keys
> 
> Click on Networking
> 
> Under Network interfaces, click the interface (should be on 'default). 
> 
> Change network from default to vpn-network-1, and it should automatically assign to subnet-d.
> 
> Click Done.
> 
> Click Create.

SSH into instance vpn-2-b, which is in network vpn-network-2.

Ping the internal IP address of vpn-1-d. It should work despite being a newly added subnet because the cloud router automatically updated it’s routing table.

This completes the exercise. You have now learned how to create VPN gateways and link them with dynamic routes using Cloud Router.

CLEAN UP

To avoid additional charges, delete the resources we’ve used.

In order: delete your Compute Engine instances, then your VPN gateways, then Cloud Routers, then the reserved static IP addresses (listed as 'release' vs 'delete'), then custom firewall rules, and delete the custom VPC networks last.