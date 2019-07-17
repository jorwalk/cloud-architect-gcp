# Create and Connect to a Linux Instance
In this exercise, we are going to create a Linux instance (VM) on Compute Engine, connect to it via SSH, install Apache, and connect the demo website via its external IP address.

1.  In the GCP web console, navigate to the screen where you can create an instance.
2.  Bring up the menu to configure and create a new instance.
3.  Name the instance `test-apache-1`.
4.  Set the zone to your closest geographical location.
5.  Set machine type to `f1-micro`.
6.  Set Boot Disk to `Ubuntu 16.04 LTS`.
7.  Allow HTTP traffic, then create the instance.
8.  After instance is created, SSH into instance via the web console.
9.  Update repositories, and install Apache.
10.  Connect to your instance via external IP address in web browser.
11.  Shut down the instance via terminal command.
12.  Delete your instance.

1.  In the GCP web console, navigate to the screen where you can create an instance.

> From the top left menu, navigate under Compute to Compute Engine.

2.  Bring up the menu to configure and create a new instance.

> If you have no other instances created, simply click the blue Create button.

3.  Name the instance `test-apache-1`.

> Type instance name in the 'Name' field. Notice the naming restrictions.

4.  Set the zone to your closest geographical location.

> From the 'Zone' dropdown menu, choose a zone from the nearest region to your location.

5.  Set machine type to `f1-micro`.

> From the 'Machine type' dropdown menu, choose the first option '`f1-micro`'.

6.  Set Boot Disk to `Ubuntu 16.04 LTS`.

> Under 'Boot disk', click 'Change'. Choose '`Ubuntu 16.04 LTS`' from the list of OS Images, then click the blue 'Select' button at the bottom.

7.  Allow HTTP traffic, then create the instance.

> Under 'Firewall', select the checkboxes for 'Allow HTTP traffic'. Then click the blue 'Create' button at the bottom.

8.  After instance is created, SSH into instance via the web console.

> Back in the instance list screen, click on 'SSH' underneath the 'Connect' field on the right side.

9.  Update repositories, and install Apache.

> From the terminal window:
> 
> sudo apt-get update
> 
> Then:
> 
> sudo apt-get install apache2
> 
> Type 'Y' to continue installation. Keep terminal window open and go back to instance list on web console.

10.   Connect to your instance via external IP address in web browser.

> From the instances list, either click the IP address under 'External IP', or type the IP address in a new browser tab. The default Apache page should appear.
> 
> Close the Apache tab.

11.  Shut down the instance via terminal command.

> Back in the terminal window, enter `sudo shutdown`

12.  Delete your instance.

> From the instances list page, click the checkbox by our instance, and click the DELETE button.