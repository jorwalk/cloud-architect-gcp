Create a Linux instance named ‘instance-1’ on Compute Engine, choose a zone in your nearest region, and leave all other settings as default.

Using gcloud commands, extend the size of your ‘instance-1’ root disk to 20GB.

> `gcloud compute disks resize instance-1 --zone (YOUR_ZONE) --size 20`

SSH into your ‘instance-1’ instance.

Without shutting down your machine, extend your root disk volume to use the new space.

> First, view your disk partition with `sudo lsblk`
> 
> Increase the partition to take the entire size of the disk
> 
> `sudo growpart /dev/sda 1  `
> 
> Then increase the file system in the same manner
> 
> `sudo resize2fs /dev/sda1  `

Create a new Compute Engine instance using the Windows Server 2016 image named ‘windows’. Create it in a zone in your nearest region. Leave all other settings as default, and note which zone you’ve created the machine in.

Using the web console, create a new SSD persistent disk called ‘new-disk’, make it 20GB in size, and attach it to your Windows instance.

> From VM Instances in Compute Engine, click on your ‘windows’ instance.
> 
> Click Edit.
> 
> Underneath Additional Disks, click Add Item.
> 
> Click the drop-down menu under Name, and select Create Disk.
> 
> Name the disk ‘new-disk’.
> 
> Set Disk Type to SSD persistent disk
> 
> Click None (blank disk) in the source type tabs.
> 
> Set Size to 20.
> 
> Click Create.
> 
> Back the Additional disks drop-down menu, select ‘new-disk’ from the Name drop-down.
> 
> Save changes to your instance at the very bottom Save button.

RDP into your Windows instance and initialize/attach your new disk.

> In Compute Engine VM Instances, Set Windows password by clicking the drop-down menu next to RDP and click ’Set Windows Password’, leave username as admin and click SET. Copy and paste the provided password for reference.
> 
> RDP into Windows method with your preferred method (local client, Chrome extension, etc).
> 
> Enter your password from above when prompted.
> 
> Go to Disk Management by right-clicking the Start Menu and clicking on Disk Management.
> 
> Right-click on the text of ‘Disk 1 - Unknown’, and click Initialize Disk.
> 
> Select GPT for the partition style, and click OK.
> 
> Now right click on the storage amount to the right of the ‘Disk 1 - Basic’ text, and click ‘New Simple Volume’.
> 
> Click Next.
> 
> Leave size as defaults and click Next.
> 
> Assign drive letter of D, and click Next.
> 
> Change the Volume label to ‘New Disk’, leave other settings as default, and click Next.
> 
> Click Finish.
> 
> Open Windows Explorer, and click This PC to confirm the new disk is shows as drive D.