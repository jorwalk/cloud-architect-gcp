In this hands-on lab, we are going to perform a variety of actions to create, resize, attach, and initialize disks on Compute Engine. From a high level, we are going to perform the following actions:

*   Create a disk
    
*   Increase disk size
    
*   Create a Linux instance, and attach the disk we made
    
*   Mount disk to our Linux instance
    
*   Create, attach, initialize and resize a new disk on a Windows instance, this time using only gcloud commands
    

Let’s get started!

The first thing we are going to do is create a new stand-alone disk. For the first examples, we will use the web console. To do this:

*   From the top left menu, scroll down to Compute Engine - Disks
    
*   Click **CREATE DISK**
    
*   Name the disk `disk-1`
    
*   Assign the disk to the us-east1 region, and zone ‘us-east1-b’. Remember the zone it is in, as we will come back to that later!
    
*   Change the size (in GB) to 100
    
*   Before clicking on Create, view the gcloud command line reference beneath the Create button.
    

*   Copy/paste the gcloud command line reference in a text editor, we will refer to it later in this lab.

*   Close out of the gcloud reference, then click Create to create the disk.

After our `disk-1` disk is ready, let’s now resize it:

*   From the Disks screen, click on ‘disk-1’
    
*   Click **EDIT**
    
*   Attempt to change the size from 100 GB to 50, notice that you cannot go down in size, only up.
    
*   Go ahead and change the size from 100 to 150, and click Save
    

Next, we will create a new instance, and attach the disk we just created:

*   From your current screen, click on ‘VM instances’ in the top left
    
*   Click Create
    
*   Name the instance `linux-instance`
    
*   Under ‘Region’ choose ‘us-east1’, under ‘Zone’ choose ‘us-east1-c’ (this is not the same zone we created our disk in)
    
*   Scroll down and expand the menu for ‘Management, security, disks, networking, sole tenancy’
    
*   Click on ‘Disks’
    
*   Click Attach existing disk, then notice that there are no options in the ‘Disk’ dropdown menu. This is because we can only attach a disk in the same zone as our instance. Scroll back up and change the zone to ‘us-east1-b’, then our disk should be available to attach from the same menu.
    
*   After setting the correct zone, go ahead and choose ‘disk-1’ from the dropdown menu.
    

*   Notice that we can choose read-only and read/write as options. If we wanted multiple instances to mount the same disk, we would use ‘read only’ to achieve this
    
*   We can also choose whether to keep the disk if the instance is deleted, or delete the disk with instance deletion. We will keep the default option.
    

*   Click Create to create the instance

Next, we will SSH into our Linux instance to format and mount the disk. The disk is attached in Google Cloud, however our instance cannot use it yet. Let’s fix that:

*   SSH into our ‘linux-instance’ instance
    
*   Type `lsblk` to view all disks. We will be formatting and mounting disk `sdb`
    
*   We will next format and mount or ‘sdb’ disk
    
*   Format disk ‘sdb’
    

*   `sudo mkfs.ext4 -m 0 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb`

*   Create disk mount directory

*   `sudo mkdir -p /mnt/disks/disk2`

*   Mount disk

*   `sudo mount -o discard,defaults /dev/sdb /mnt/disks/disk2`

*   Set read/write permissions

*   `sudo chmod a+w /mnt/disks/`

*   Verify that the disk is mounted using either the `lsblk` or \`df -h commands

Excellent! We have successfully created, resized, attached, and mounted a disk on a Linux instance. Let’s now do the exact same thing, except this time using exclusively gcloud commands and using a Windows instance.

We will again create a new disk, this time naming it ‘disk-2’, and modifying the same gcloud reference we copy/pasted when we created our first disk earlier. We do not need all fields in the cross reference. The only required field is the disk name and zone, however we are also going to manually set the size to 100GB (it will default to 500GB). Let’s do that now:

*   Open the Cloud Shell
    
*   Type the following command to create a disk named ‘disk-2’ in the zone us-east1-b, and set the size to 100GB
    

*   `gcloud compute disks create disk-2 --size=100GB --zone=us-east1-b`

*   If you wish, go back to the Disks menu in the web console to verify every step completes successfully
    
*   Next, resize our ‘disk-2’ disk to 150GB. Confirm that you want to complete this when prompted
    

*   `gcloud compute disks resize disk-2 --size=150 --zone=us-east1-b`

*   Next, enter the gcloud command to create a Windows instance named `windows-instance` in zone ‘us-east1-b’. We will not attach our ‘disk-2’ disk until after we create the instance

*   `gcloud compute instances create windows-instance --zone=us-east1-b --image=windows-server-2019-dc-v20190225 --image-project=windows-cloud --boot-disk-size=50GB`

*   Now that we have created out Windows instance, let’s attach our ‘disk-2’ disk to the instance

*   `gcloud compute instances attach-disk windows-instance --disk=disk-2 --zone=us-east1-b`

At this point, we have successfully attached the disk, now we need to format and initialize it in Windows itself. To do so, we need to set an admin password and connect to our instance via RDP. The steps to do this may vary depending on your operating system and browser, but the general guide is as follows:

First, create an admin password for your Windows instance:

*   From the web console, go back to your VM Instances page
    
*   Under ‘windows-instance, select the dropdown menu next to ‘RDP’, and select ‘Set Windows password’
    
*   Keep username as ‘admin’, and click SET
    
*   When it generates a password, copy and paste it into a text editor for reference, then click CLOSE
    
*   Connect to your Windows instance via RDP. This can be done by either clicking the RDP button to if you have the Remote Desktop extension for Chrome, or select the dropdown menu next to RDP, and choosing to download and run the RDP file.
    
*   For whichever RDP method you choose, once connected enter the ‘admin’ username and the generated password your created above to connect to the instance. If you receive a server certificate warning, choose to continue anyway
    

*   Note: You may need to wait a few minutes after creating the Windows instance before you can successfully connect to it. If you receive an error when connecting, wait a couple minutes and try again. It takes longer to boot up compared to your Linux instance.

Once you are in the Windows desktop, we need to enter our Disk Management utility:

*   First, close out of the Server Manager - Dashboard screen
    
*   Click the magnifying glass icon in the bottom left
    
*   Type ‘create and format hard disk partitions’ - it should auto-match your suggestion before you are done typing, select the above match by the same name
    
*   You may automatically get a prompt to initialize our disk, if so you can ignore the below step:
    

*   If you are not automatically prompted, from Disk Management, scroll down to ‘Disk 1’, which is listed as ‘Not Initialized’. Right click on ‘Disk 1’ on the left side, and click on ‘Initialize Disk’

*   Make sure that ‘Disk 1’ is selected, and choose ‘GPT (GUID Partition Table)’ for the partition style, then click OK.

*   Note: There are compatibility reasons to choose MBR over GPT, but we are not concerned about those for this demo.

*   Next, right-click on the disk ‘bar’ next to ‘Disk 1’, and select ‘New Simple Volume’

*   Click Next through all prompts, accepting all defaults, to quickly format and allocate space

*   When complete, we should have a new disk at drive D of the disk we just set up

This completes the lab.