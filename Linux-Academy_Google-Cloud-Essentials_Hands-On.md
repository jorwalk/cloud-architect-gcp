# Linux Academy Hands-On Lab
## Deploying an App Engine Application
Google Cloud App Engine provides a solid, easy-to-access platform for a wide range of web apps. Its interoperability with other Google Cloud services, such as Cloud Datastore, enhances its effectiveness. In this hands-on lab, we’ll deploy an app to App Engine that allows users to enter details into a NoSQL database, Cloud Datastore, and displays the proper HTML template and CSS. The process requires that we customize the `config.py` file before deploying the app.
### Learning Objectives
#### Enable APIs and clone GitHub repository.
1. From the main navigation, visit the **APIs & Services > Libraries** page, and search for "Datastore".
1. Select the `Cloud Datastore API`.
1. If the API is not available, click Enable.
1. Activate the Cloud Shell.
1. When it spins up, create the necessary bucket (bucket name must be unique):
     ```
     gsutil mb -c regional -l us-east1 gs://[BUCKET_NAME]
     gsutil acl ch -u AllUsers:R gs://[BUCKET_NAME]
     ```
1. Clone the GitHub repository:
    ```
    git clone https://github.com/linuxacademy/content-gc-essentials
     ```
1. Change directory to the `content-gc-essentials/app-engine-lab` folder.
#### Configure `config.py` file.
1. From the Cloud Shell Editor, open `config.py` in the `app-engine-lab` folder.
1. Change `PROJECT_ID` to the current project, as shown in the Cloud Shell.
1. Change the `"CLOUD_STORAGE_BUCKET"` variable value to your unique bucket name.
1. Save the file.
#### Deploy the app.
1. In the Cloud Shell, enter the following code:
    ```
    gcloud app deploy
    ```
1. When prompted, choose the nearest region.
#### Test the app.
1. In the Cloud Shell, enter the following code:
    ```
    gcloud app browse
    ```
1. If the browser window does not open, click the generated link.
---
## Triggering a Cloud Function with Cloud Pub/Sub
Cloud Functions can be triggered in two ways: through a direct HTTP request or through a background event. One of the most frequently used services for background events is Cloud Pub/Sub, Google Cloud’s platform-wide messaging service. In this pairing, Cloud Functions becomes a direct subscriber to a specific Cloud Pub/Sub topic, which allows code to be run whenever a message is received on a specific topic. In this hands-on lab, we’ll walk through the entire experience, from setup to confirmation.
### Learning Objectives
#### Enable required APIs.
1. Use the API Library to find and enable the Cloud Pub/Sub API.
1. Use the API Library to find and enable the Cloud Functions API.
#### Create Pub/Sub topic.
1. From the main console navigation, go to `Cloud Pub/Sub`.
1. Click `Create a topic`.
1. In the dialog, enter a name `greetings` for the topic.
1. Click `Create`.
#### Create a Cloud Function.
1. From the main console, go to Cloud Functions.
1. Click Create function.
1. Configure the function with the following values:
    * Name: la-pubsub-function
    * Trigger: Cloud Pub/Sub
    * Topic: greetings
    * Source code: Inline editor
    * Runtime: Python 3.7
1. In the main.py field, enter the following code:
    ```
    import base64
    
    def greetings_pubsub(data, context):
    
        if 'data' in data:
            name = base64.b64decode(data['data']).decode('utf-8')
        else:
            name = 'folks'
        print('Greetings {} from Linux Academy!'.format(name))
    ```    
1. Set Function to Execute to greetings_pubsub.
1. Click Create.
#### Publish message to topic from console.
1. Click the newly created Cloud Function name.
1. Switch to Trigger.
1. Click the topic link to go to the Cloud Pub/Sub topic.
1. From the Topic page, click Publish Message.
1. In the Message field, enter everyone around the world.
1. Click Publish.
#### Confirm Cloud Function execution.
1. Return to the Cloud Functions dashboard.
1. Click the Cloud Function's name.
1. From the Cloud Function navigation, click View Logs.
1. Locate the most recent log.
1. Confirm function execution.
#### Trigger Cloud Function directly from command line.
1. Click Activate Cloud Shell from the top row of the console.
1. In the Cloud Shell, enter the following code:
    ```
    DATA=$(printf 'my friends' | base64)
    gcloud functions call la-pubsub-function --data '{"data":"'$DATA'"}'
    ```
1. After a moment, refresh the logs page and confirm the Cloud Function execution.
#### Publish message to topic from command line.
1. In the Cloud Shell, enter the following command:
    ```
    gcloud pubsub topics publish greetings --message "y'all"
     ```
1. After a moment, refresh the log page to confirm the function has executed.
---
## Working with Compute Engine Windows Instances
Compute Engine VM instances can utilize a wide range of boot disks; Google Cloud currently offers well over 50 disk images to choose from. Cloud computing professionals must be adept in spinning up a variety of operating systems, including Windows server. In this hands-on lab, you’ll experience the creation of a Windows-based Compute Engine VM instance, set up an IIS server, and push your first web page live to confirm the server’s operation.
### Learning Objectives
#### Create a Compute Engine VM instance.
1. From the main navigation, choose Compute Engine > VMs.
1. In the VM Instances area, click Create.
1. With New VM instance chosen from the options on the left, configure your instance:
    - In the name field, provide a relevant name using hyphens, like la-windows-1.
    - Keep the suggested Region and Zone.
    - In the Boot Disk section, click Change and select Windows Server 2019 Datacenter, Server with Desktop Experience from the list; click Select.
1. Under Firewall, choose the Allow HTTP traffic option.
1. Click Create.
#### Set Windows password.
1. From the RDP options, click Set Windows password.
1. In the dialog, confirm your username is correct and click Set.
1. Copy the supplied password and click Close.

#### Launch RDP window.
1. Launch the RDP window by using one of the following methods:
    * If you're on a Windows system, click RDP.
    * If you're on a Mac using Chrome in a standard window, first install the Chrome RDP extension, and then click RDP.
    * If you're on a Mac using another browser or Incognito window, from the App Store, download and install the latest version of the Microsoft Remote Desktop app. Then, choose Download the RDP file from the RDP options and open the file.
#### Install IIS.
1. From the Windows Start menu, right-click on Windows Powershell and choose Run as administrator.
1. In the PowerShell window, enter the following commands:
    ```
    import-module servermanager
    add-windowsfeature web-server -includeallsubfeature
    echo '<!doctype html><html><body><h1>Greetings from Linux Academy!</h1></body></html>' > C:\inetpub\wwwroot\index.html
    ```
#### Test your page.
1. From the Compute Engine VM page, click the External link for your Windows VM instance.
1. Review the page in your browser.
---
## Setting Cloud Storage Lifecycle Rules
While saving an object in a Cloud Storage bucket is relatively inexpensive, there is, nonetheless, a cost. The cost varies depending on the storage class selected. Certain objects are required to be more available at first, requiring the storage class with the highest availability — and cost. Such objects may eventually be relegated to less available and less expensive storage classes and, even, be deleted. Management of these objects over time can be handled automatically by establishing and implementing lifecycle rules. In this hands-on lab, we'll set a variety of lifecycle rules for Google Cloud Storage buckets both from the console and the command line.
### Learning Objectives
#### Create a Cloud Storage bucket.
1. From the Google Cloud console main navigation, choose Cloud Storage.
1. Click Create bucket.
1. Name the bucket uniquely.
1. In the Storage Class section, select Regional.
1. Click Create.
#### Define first lifecycle rule. 
1. From the Cloud Storage browser page, click None in the Lifecycle column for the bucket just created.
1. Click Add rule.
1. Under Select object conditions, set the following:
    - Age: 180
    - Storage class: Regional, Standard
1. Click Continue.
1. Under Select action, choose Set to Nearline.
1. Click Continue.
1. Click Save.
#### Define second lifecycle rule.
1. From the Cloud Storage browser page, click Enabled in the Lifecycle column.
1. Click Add rule.
1. Under Select object conditions, set the following:
    - Age: 365
    - Storage class: Nearline
1. Click Continue.
1. Under Select action, choose Set to Coldline.
1. Click Continue.
1. Click Save.
#### From command line, get lifecycle rules.
1. Click Activate Cloud Shell.
1. In the Cloud Shell, enter the following code:
    ```
    gsutil lifecycle get gs://[BUCKETNAME]
    ```
1. Review output.
#### Set lifecycle rule with JSON file.
1. Clone a repo and change to the lab's directory:
    ```
    git clone https://github.com/linuxacademy/content-gc-essentials
    cd content-gc-essentials/cloud-storage-lifecycle-lab
    ``` 
1. Review file in editor.
1. In the Cloud Shell, enter the following code:
    ```
    gsutil lifecycle set delete-after-two-years.json gs://[BUCKET_NAME]
    ```
1. Confirm the lifecycle rule has been added in the console.
---
## Managing Google Cloud SQL Instances
When working with Cloud SQL on any scale, you’ll need to manage multiple instances: creating, cloning, starting, stopping, restarting, and — eventually — deleting them. This hands-on lab gives you the experience of performing all those tasks so you’ll be familiar with the steps necessary to handle Cloud SQL instances completely.
### Learning Objectives
#### Create instance.
1. From the main navigation, click Cloud SQL.
1. Click Create Instance.
1. Choose your database engine.
1. Enter an instance ID.
1. Provide a password.
1. Click Create.
#### Create a database.
1. Select the recently created Cloud SQL instance.
1. Choose Create database.
1. Name the database and leave the other fields at their default values.
1. Click Create.
#### Clone the instance.
1. From the Instance details page, choose Create clone.
1. Enter a new name for the clone if desired.
1. Choose Clone latest state of instance.
1. Click Create clone.
#### Stop and start an instance.
1. Select the first instance created.
1. Click Stop.
1. After the instance has stopped, click Start.
#### Restart an instance.
1. Select the cloned instance.
1. Click Restart.
#### Delete an instance.
1. Select the cloned instance.
1. Click Delete.
1. Enter the name of the instance in the dialog to confirm the deletion.
1. Click Delete.
---
## Exploring Cloud Firestore in Datastore Mode
Data comes in all shapes, sizes, and use cases. A relational database service like Cloud SQL isn't always the answer. Cloud Datastore is a NoSQL database service, ideal for semi-structured data that needs to be highly scalable and available. Cloud Firestore is the next generation of Datastore with enhanced features, and in this hands-on lab, you'll see how to build a Firestore NoSQL database in Cloud Datastore mode for the best of both worlds.
### Learning Objectives
#### Enable APIs.
1. From the main navigation, click APIs and Libraries > Library.
1. Search for Datastore.
1. Click Enable.
#### Create the database.
1. From the main navigation, click Datastore.
1. Choose Datastore Mode.
1. Select your closest location.
1. Click Create database.
#### Define entities.
1. For Kind, enter Flights.
1. Click Create Entity.
1. Click Add property for each of the following entries, of the specified type:
    - Airline: String
    - Flight Number: Integer
    - Arrival: Data and Time
    - OnTime: Boolean
1. Click Save.
1. Repeat steps 3 and 4 twice more with different values.
1. For the final entry, add another property:
    - Note: Text
1. Click Save.
#### Query the data.
1. Switch to Query by GQL.
1. In the Query field, enter the following:
    ```
    SELECT * FROM Flights
    ```
1. Click Run Query.
1. In the Query field, enter the following:
    ```
    SELECT * FROM Flights WHERE OnTime = false
    ```
1. Click Run Query.
1. Review results.
---
## Connecting to Cloud Bigtable with cbt
Sometimes data is relatively straight-forward — there's just an overwhelming amount of it. That's exactly what Cloud Bigtable is meant for. Cloud Bigtable is a fully managed NoSQL database service designed to handle massive amounts of information. In this hands-on lab, you’ll configure database instances and clusters for Cloud Bigtable in the console and then use command line cbt commands to create a schema and populate the table with data.
### Learning Objectives
#### Enable API.
1. From the main navigation, choose APIs & Services > Library.
1. In the search field, enter Bigtable.
1. Select the Cloud Bigtable Admin API card.
1. Click Enable.
#### Create Bigtable instance.
1. From the main navigation, choose Bigtable in the Storage section.
1. Choose Create instance.
1. Set the following fields:
    - Name: la-data-cbt
    - Instance type: Development
    - Storage type: HDD
    - Cluster Region: us-east1
    - Cluster Zone: us-east1-b
1. Click Done and then Create.
#### Install and configure `cbt`.
1. Activate the Cloud Shell by clicking its icon in the top row.
1. In the Cloud Shell, enter the following:
    ```
    gcloud components update
    gcloud components install cbt
    ```
1. Configure cbt with the following commands:
    ```
    echo project = [PROJECT_ID] > ~/.cbtrc
    echo instance = la-data-cbt >> ~/.cbtrc
    ```
#### Create data table.
1. In the Cloud Shell, enter the following:
    ```
    cbt createtable la-table
    cbt ls
    ```
#### Define table structure and add data.
1. In the Cloud Shell, enter the following:
    ```
    cbt createfamily la-table offerings
    cbt set la-table r1 offerings:c1=labs
    cbt read la-table
    ```
1. Review results.
1. Enter the following:
    ```
    cbt set la-table r1 offerings:c2=courses
    cbt read la-table
    ```
#### Delete Bigtable instance.
1. From the console, select the Bigtable instance.
1. Choose Delete instance.
