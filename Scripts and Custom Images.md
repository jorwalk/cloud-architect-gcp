Create a new Compute Engine instance named ‘web-1-base’. Enable HTTP access, and directly paste the below text into the startup script field.

`#! /bin/bash`

`apt-get update`

`apt-get install -y apache2`

`cat <<EOF > /var/www/html/index.html`

`<html><body><h1>VERSION 1</h1>`

`<h2>Welcome to your custom website.</h2>`

`</body></html>`

`EOF`

> From the instance configuration screen, expand ‘Management, disks, networking, SSH keys’, scroll down to Automation - Startup script, and paste the above script into the script field.

After adding the above startup script, create the instance.

You may need to wait a few minutes for the script to complete. After a few minutes, click the external IP address of your instance, and confirm you have a ‘VERSION 1’ of your custom website.

Using the web console, create a custom image from your instance called ‘web-1’ and assign it to image family ‘webserver’.

> Stop your instance.
> 
> Once stopped, from the Compute Engine menu, click Images. Click CREATE IMAGE. Name the image ‘web-1’. Name family ‘webserver’. Source - Disk. Source disk - web-1-base.
> 
> Click Create.

Once the image is complete, create a new instance. Name it ‘web-2-base’. Use the ‘web-1’ custom image you created for the boot disk. Enable HTTP access and create the instance. Take note which zone your instance is in.

> Create a new instance as usual. Under Boot Disk, click Change. Click on Custom images from the top row. Select custom image ‘web-1’ from the list. Click Select to confirm boot disk.

Once the instance is created, SSH into the instance.

Once in your instance, modify your index.html using the below command to edit it using VIM as a text editor:

`sudo vim /var/www/html/index.html`

Press ‘I’ to insert text, and replace ‘`VERSION 1`’ with ‘`VERSION 2`’.

Press Esc - :wq - Enter to exit VIM and save changes

Exit your instance.

Using Cloud Shell and gcloud commands, create a new image from your instance you just modified. Name the image ‘web-2’ and add it to the ‘webserver’ family. You will need to include the zone of the source instance you’re creating an image from.

> First, stop your instance.
> 
> Once stopped, from Cloud Shell, type `gcloud compute images create web-2 --source-disk web-2-base --source-disk-zone (Your disk’s ZONE) --family webserver`

After the image is created, deprecate your ‘web-1’ image.

> Go to Images. Place a check in your ‘web-1’ instance and click DEPRECATE. Toggle Deprecate in the drop-down menu, and choose ‘web-2’ as it’s replacement, and click DEPRECATE IMAGE.

Clean up: delete your existing instances and custom images to avoid charges.

> From your Images menu, scroll to the bottom and click ‘Show deprecated images’. Scroll back to the top and place a check in both custom images, and click DELETE. Confirm deletion.
> 
> Go back to VM instances, and delete your instances.