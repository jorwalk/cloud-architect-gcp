# Working with Custom Images on Google Compute Engine

## Create custom image from base-apache instance using web console:

* Stop the instance
* Go to Compute Engine > Images
* Click CREATE IMAGE
* Name image "webserver-base"
* Set Family to "webserver"
* In the Source dropdown menu, select Disk
* In the Source disk dropdown menu, select base-apache
* Click Create

## Create image from custom-webpage instance using gcloud command:

* Stop the instance
* Open Cloud Shell
* Enter command to create image from the custom-webpage disk, name the image "custom-webpage", and add to the webserver image family
    * `gcloud compute images create custom-webpage --source-disk=custom-webpage --source-disk-zone=us-central1-a --family=webserver`
* Verify that image is created and in the appropriate family using the web console

## View images in web console and view webserver image family information in command line:

* In web console, go to Compute Engine > Images
* To describe image family and view latest image, enter command:
* `gcloud compute images describe-from-family webserver`
* Shown image is the latest version

## Deprecate base version using command line:

* First, view process in web console:
* Go back to Compute Image > Images
* Place check next to webserver-base, and click DEPRECATE
* Set State to Deprecated, and set Replacement as custom-page-1
* Cancel out and do the same thing via command line.
* In Cloud Shell, enter:
    * `gcloud compute images deprecate webserver-base --state DEPRECATED`
* Verify in web console

## Create a new web server from custom image:

* Go to Compute Engine > VM Instances
* Click Create Instance
* Place it in any region and zone you want
* Name the instance "new-web-server"
* Under Boot disk, click Change
* Click on Custom images from the top menu
* Click on Show deprecated images to view all images
* Select custom-webpage, and click Select
* Check the box for Allow HTTP traffic under Firewall settings
* Click Create
* Once the instance is up, click the external IP address to verify the new web page works