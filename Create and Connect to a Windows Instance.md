# Create and Connect to a Windows Instance
In this exercise, we are going to create a Windows Server 2016 instance (VM) on Compute Engine, connect to it via Remote Desktop (RDP), install Internet Information Services (IIS), and connect the demo website via its external IP address.

NOTE: The connection method can vary based on OS. I recommend using the Chrome RDP extension in the Chrome browser. If you don't have Chrome available, connection will be via RDP client on your OS. You can install the Chrome RDP client here: https://chrome.google.com/webstore/detail/chrome-rdp-for-google-clo/mpbbnannobiobpnfblimoapbephgifkm

1.  In the GCP web console, navigate to the screen where you can create an instance.
2.  Bring up the menu to configure and create a new instance.
3.  Name the instance `windows-iis-1`.
4.  Set the zone to your closest geographical location.
5.  Set machine type to `n1-standard-1`.
6.  Set Boot Disk to `Windows Server 2016` ('Desktop Experience', don't choose 'Server Core').
7.  Allow HTTP traffic, then create the instance.
8.  Create an administrator password for your Windows instance (leave username as default).
9.  After the instance is created, connect to instance with RDP (browser or local client).
10.  After you are connected via RDP, install IIS via Server Manager.
11.  Connect to your instance via external IP address in web browser.
12.  Shut down the Windows Server instance.
13.  Delete your instance.

1.  In the GCP web console, navigate to the screen where you can create an instance.

> From the top left menu, navigate under Compute to Compute Engine.

2.  Bring up the menu to configure and create a new instance.

> If you have no other instances created, simply click the blue Create button.

1.  Name the instance `windows-iis-1`.

> Type instance name in the 'Name' field. Notice the naming restrictions.

4.  Set the zone to your closest geographical location.

> From the 'Zone' dropdown menu, choose a zone from the nearest region to your location.

5.  Set machine type to `n1-standard-1`.

> From the 'Machine type' dropdown menu, choose the option '`n1-standard-1`'.

6.  Set Boot Disk to `Windows Server 2016` (Desktop Experience).

> Under 'Boot disk', click 'Change'. Choose '`Windows Server 2016 (Desktop Experience)`' from the list of OS Images, then click the blue 'Select' button at the bottom.

7.  Allow HTTP traffic, then create the instance.

> Under 'Firewall', select the checkboxes for 'Allow HTTP traffic'. Then click the blue 'Create' button at the bottom.

8.  Create an administrator password for your Windows instance (leave username as default).

> Click the dropdown arrow next to RDP button, click 'Set Windows password'. Leave default username and click 'SET'. Copy password to external text file for reference.

9.  After the instance is created, connect to instance with RDP (browser or local client).

> If using the Chrome RDP extension, click the RDP button next to the instance name in your instance list.
> 
> If using a local RDP client, either: Click the drop menu next to the RDP button and select 'download the RDP file', and open the file OR, within your local RDP client, enter the external IP, username, and password (set in the previous step) and connect.

10.  After you are connected via RDP, install IIS via Server Manager.

> The Server Manager Dashboard should automatically appear. If it does not, click the Windows/Start button and select Server Manager.
> 
> Click '2. Add roles and features'
> 
> At `Before You Begin`, click Next.
> 
> At `Installation Type`, leave defaults and click Next.
> 
> At `Server Selection`, leave defaults and click Next.
> 
> At `Server Roles`, place check box by `Web Server (IIS)`, and click Next. If prompted to add required features, click 'Add Features' button while leaving defaults.
> 
> For the rest of the steps, leave all defaults and keep clicking Next until the 'Confirmation' screen, and click Install.
> 
> Once installation is complete, leave RDP windows up, and go back to GCP web console.

11.  Connect to your instance via external IP address in web browser.

> From the instances list, either click the IP address under 'External IP', or type the IP address in a new browser tab. The default Internet Information Services page should appear.
> 
> Close the IIS browser tab.

12.  Shut down the Windows Server instance.

> From the Windows RDP window, click the Start/Windows button, click the power button (first button above Start button), and select 'Shut Down'. Leave shutdown reason as default option.

13.  Delete your instance.

> From the instances list page, click the checkbox by our instance, and click the DELETE button.