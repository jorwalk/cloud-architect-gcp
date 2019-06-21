# Notes from my Google Cloud Professional Cloud Architect Exam

This was the exam I originally planned to take first, but then I completed the Associate Cloud Engineer first. The notes I have on this seem to be fairly thin. So it’s kind of automatically sanitized and doesn’t divulge much details.

* Datastore. Indexes — creating them, updating them. Which file do you update for this? Can you do this only using gcloud or also from the console?
https://cloud.google.com/datastore/docs/concepts/indexes

* Datastore. Data retrieval using identifiers, batch. I was glad I’d covered the entire spectrum of GCP products as part of my learning.
https://cloud.google.com/datastore/docs/best-practices

* Deployment Manager . How do you templatize a repeatable infrastructure setup?

* GKE. When is gcloud used as opposed to kubectl. When is Deployment Manager used and when is Kubernetes deployment.
https://cloud.google.com/kubernetes-engine/docs/quickstart

* PCI compliance. Payment Card Industry Data Security Standards. Are GCP products compliant? Are all of them? What additional work do you need to do to make it compliant? 
https://cloud.google.com/security/compliance/pci-dss/

* GDPR. You don’t have to know the GDPR law thoroughly, but know what implications there are to be compliant with it and therefore which products/services should be used and in what way. I would also suggest you gather high level information on HIPAA, COPPA, and GDPR.

* Networking. Networking is a topic in all certifications. Definitely useful to brush up your networking knowledge — CIDR, primary and secondary networks, how VPNs work, OSI layer, netstat, etc.

* As with other exams, remember that as a Professional on GCP you are also expected to know solutions, products, and project processes outside GCP also.

* MountKirk, Dress4Win, TerramEarth. Know the case studies thoroughly. The case studies are there during the exam and you can go through it. But you’d be better off studying it prior and making notes during your practice/learning. But don’t by-heart the solutions.

* BigQuery. Various types of partitioning. And retention/expiration rules.
https://cloud.google.com/bigquery/docs/best-practices-storage

* BigTable. For time series data. What are the best practices for BigTable time series data?
https://cloud.google.com/bigtable/docs/schema-design-time-series

* Know the speeds possible on VPN. Know how to calculate the amount of time it will take to transfer, say 100TB, of data. So, if large transfers were required, should you be using VPN or Direct Interconnect. I’ve got a more detailed note on this in the overall notes, which is linked below.

* Data Rehydration. 
https://cloud.google.com/transfer-appliance/docs/2.0/data-rehydration

* GCE vs GKE. Which do you choose and for what kind of workloads?

* Snapshots, Images, Disks. Learn the difference between them. How they are created and shared? What is the recommended process of creating them? Do they cross over zones, regions, projects?
https://cloud.google.com/compute/docs/images/sharing-images-across-projects

* Cloud SQL. Note that it is regional. It can span zones in a region but not regions. 
https://cloud.google.com/sql/docs/mysql/locations

* Cloud Functions. A serverless option that can be used to absorb very large workloads. Know the ways in which they can be triggered.
https://cloud.google.com/functions/docs/concepts/overview

* Cloud Armor. In general, know where this is used and how. You don’t have to go into the details.
https://cloud.google.com/armor/

* Cloud Directory Sync. How do you bring on users onto GCP from their current LDAP/Active Directory setup?
https://support.google.com/a/answer/106368?hl=en

* IAM. Again, don’t by-heart. Figure out the patterns and nomenclature and then apply them.

* Cloud Transfer Service == Storage Transfer service. I was mostly used to this being called Storage Transfer Service in the Linux Academy course but in the exam it was called Cloud Transfer Service and I was unsure if it was the same thing or not.I̶t̶ ̶i̶s̶ ̶t̶h̶e̶ ̶s̶a̶m̶e̶ ̶t̶h̶i̶n̶g̶.̶ (Editing in Roman’s comment: Its actually not exactly the same thing — Cloud Data Transfer Service is a collection of different transfer services of which, Cloud Storage Transfer is one… https://cloud.google.com/products/data-transfer/. So there’s clearly more to it, but I’m leaving my original comment as it is.)

* Cloud Storage. Life cycle management policies. All courses cover this. 
https://cloud.google.com/storage/docs/lifecycle

* VPC, VPN, Peer Gateways. In general, brush up your general networking knowledge.

* IAM. In answering IAM related questions, a suggestion … Given all the possible predefined/curated roles, it is difficult to know whether a particular role actually exists or is made up. My assumption usually was that if they have mentioned it, it probably exists and now figure out if it seems right. There is no guarantee that a policy/role they mention in the options actually exist, but I assumed it to simplify my life.

* Networking. Various options to connect between cloud and on-premises.

* Data Loss Prevention API. Is there a way to automatically scrub/sanitize private customer data in, say, logs. 
https://cloud.google.com/dlp/

* Stackdriver. Know this well. Including the custom installed monitoring agent.
https://cloud.google.com/stackdriver/

* Cloud Armor, Security Scanning, Jenkins, Spinnaker, cloud identity aware proxy, cloud sql proxy, cloud launcher (vs deployment manager), etc. Would be good to know in general what these are even if you don’t go in-depth.

* Networking. Firewall, network tags. This is taught in the various courses. 
https://cloud.google.com/vpc/docs/add-remove-network-tags

* Data prep vs Datalab. Which is used for what? Doing just one lab on Qwiklabs will give you enough knowledge.

* Cloud Spanner.

* Cloud SQL. K̶n̶o̶w̶ ̶t̶h̶a̶t̶ ̶C̶l̶o̶u̶d̶ ̶S̶Q̶L̶ ̶o̶n̶l̶y̶ ̶s̶u̶p̶p̶o̶r̶t̶s̶ ̶M̶y̶S̶Q̶L̶ ̶a̶n̶d̶ ̶P̶o̶s̶t̶g̶r̶e̶S̶Q̶L̶.̶ ̶O̶t̶h̶e̶r̶ ̶S̶Q̶L̶ ̶d̶a̶t̶a̶b̶a̶s̶e̶s̶ ̶w̶i̶l̶l̶ ̶r̶e̶q̶u̶i̶r̶e̶ ̶c̶u̶s̶t̶o̶m̶ ̶i̶n̶s̶t̶a̶l̶l̶a̶t̶i̶o̶n̶.̶ This has changed — https://cloud.google.com/sql-server/. Cloud SQL supports MySQL, Postgres, and SQLServer. GCP is constantly updating their solutions and offerings, so check the docs when you are preparing.
https://cloud.google.com/sql/docs/

* Cloud Storage. Know the storage class options — standard (regional and multiregional), nearline, coldline. T̶h̶e̶r̶e̶ ̶a̶r̶e̶ ̶n̶o̶ ̶o̶t̶h̶e̶r̶s̶.̶ (There is also an ice cold storage now — https://cloud.google.com/blog/products/storage-data-transfer/whats-cooler-than-being-cool-ice-cold-archive-storage)
https://cloud.google.com/storage/docs/storage-classes

* Questions on the exam are much longer than in the coursera or linux academy courses. You need to practice taking the exam for 2 full hours and reading the longwinded questions and answer options. Don’t get bored or distracted because you’ve been practising with the shorter straightforward questions in some of the courses or practice tests.


