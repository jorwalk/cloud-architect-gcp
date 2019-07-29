Now that our resources are created, note that the external IP addresses that have been created for each ‘vpn-static-1’ and ‘vpn-static-2’. You will need these address when creating the VPN gateways.

> Find reserved IP's under left menu - VPC Network - External IP addresses.

Go to Compute Engine instances, and SSH into ‘vpn-1-a’. Ping ‘vpn-2-b’ by both its external and internal IP address. Which one works, and which one does not?

Since vpn-1-a is in a different VPC as the other two instances, it cannot reach them by internal IP.

Now we will create the VPN gateways. Go to your VPN configuration menu, and create a new VPN connection.

> From left menu, go to Interconnect - VPN.
> 
> Click 'CREATE VPN CONNECTION'

Name the first VPN gateway ‘vpn-gateway-1’. Assign it to the ‘vpn-network-1’ network. Assign to the us-west1 region. Choose the reserved IP address labeled ‘vpn-static-1’.

> Populate the listed fields as above.

Further down, create a tunnel to connect to.

Enter the remote peer IP address. This is the ‘vpn-static-2’ IP address we created (actual address will be different for everyone).

Enter the vpn-static-2 address listed in External IP addresses.

Leave IKE version as IKEv2.

Type a shared secret in the listed field (use any password you like).

Set static routing options:

Enter the remote IP range of subnet-b on vpn-network-2. Do not enter subnet-c’s range for now.

> In the 'Remote network IP ranges' field, enter 10.1.2.0/24

Choose a local subnetwork from the listed options, and click OK. It should automatically populate the ‘Local IP ranges’ field.

Click Create to create the VPN gateway.

Start creating the second VPN gateway for vpn-network-2.

> From the VPN menu, click CREATE VPN CONNECTION again.

Name the first VPN gateway ‘vpn-gateway-2’. Assign it to the ‘vpn-network-2’ network. Assign to the us-central1 region. Choose the reserved IP address labeled ‘vpn-static-2’.

> Enter in the listed fields similar to above

Further down, create a tunnel to connect to.

Enter the remote peer IP address. This is the ‘vpn-static-1’ IP address we created (actual address will be different for everyone).

> Enter the 'vpn-static-1' IP address from the External IP addresses menu.

Leave IKE version as IKEv2.

Type a same shared secret from the first gateway in the listed field.

Set static routing options:

Enter the remote IP range of subnet-a on vpn-network-1.

> Address will be 10.1.1.0/24, then hit Enter.

Choose a local subnetwork from the listed options, and click OK. It should automatically populate the ‘Local IP ranges’ field.

Click Create to create the VPN gateway.

From the VPN gateway overview menu, wait a couple minutes and refresh your screen until you have green check marks for each gateway.

Go to Compute Engine, SSH into vpn-1-a. Attempt to ping the internal IP address of vpn-2-b. It should work. Attempt to ping the internal IP address of vpn-2-c. It should not work. Let’s fix that.

Back in listed VPN gateways, click on vpn-gateway-1. Edit the connection. Edit the tunnel.

> In the Interconnect - VPN menu, click on 'vpn-gateway-1', click Edit at the top of the screen, and click the edit (pencil) icon next to the tunnel (listed as 'Remote peer IP address: (address for vpn-static-2)).

Add the IP range for subnet-c and press Enter to complete add.

> Under 'Remote network IP ranges' enter '10.1.3.0/24' alongside the other address already there, and hit Enter to confirm entry.

Save changes.

Now go back to instance vpn-1-a and ping vpn-2-c’s internal IP address. It should work this time.

This completes the exercise. You have now learned how to create VPN gateways and link them with static routes.

Clean Up
--------

If you intend on following this exercise with the Cloud Router exercise, only delete your VPN gateways as we will recreate them again. If you do not plan on continuing with the Cloud Router exercise, delete all resources to avoid additional charges.

In order: Delete your Compute Engine instances, then your VPN gateways, then the reserved static IP addresses (listed as 'release' vs 'delete'), then custom firewall rules, then delete the custom VPC networks last.