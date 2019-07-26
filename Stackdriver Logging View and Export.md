1.  If you don’t already have them, create two Compute Engine instances in a GCP project.

    > Create in Compute Engine.

2.  On one of the instances, assign a label of **env:prod** for the key-value pair.

    > When creating the instance, expand the ‘Management, disks, network, SSH keys’ menu, and add a label.

3.  View your current logging data in Stackdriver logging.

    > From the left menu, click **Stackdriver - Logging**

4.  In the logs view, use the basic filters to only view logs for one of your instances.

    > Click the left dropdown menu, mouse over **GCE VM Instance**, and select your instance on the new menu that pops out.

5.  Go to the advanced filter view.

    > On the left of the top search field, click the down arrow and select **Convert to advanced filter**.

6.  Enter the below string to find logs for instances with the label you created. This was not covered in the hands-on lesson, but it is the advanced filter string needed to search for your labels:  
      
    `protoPayload.request.labels.key="env"  
    protoPayload.request.labels.value="prod"  
      
    `View the details of the entry, does it match the instance name that you created?  
      
    Next, let’s export matching logs to a Cloud Storage bucket.

7.  Create a regional Cloud Storage bucket and give it a globally unique name.

    > Create new bucket in the Storage browser.

8.  Export logs for resources with the label you created to an export sink. Only export records that match your label.
    
    > In Stackdriver Logging, click **Exports**, **CREATE EXPORT**.
    > 
    > In the Edit Export screen, switch to advanced filter mode, enter the string from above, and click **Submit Filter**.
    > 
    > From the right panel, give the **Sink** the name ‘prod\_export’.
    > 
    > Select Cloud Storage for the destination.
    > 
    > Select the bucket you created in the **Sink Destination** drop down.
    > 
    > Click **Create Sink**.
    > 
    > Once your export is set up, go back to Compute Engine and stop, then start your instance again.
    > 
    > Make a new instance with the same env:prod label.
    > 
    > Create in Compute Engine, same as at top.
    > 
    > If you wish, in about an hour check your Cloud Storage bucket, you should see records from both instances in it.