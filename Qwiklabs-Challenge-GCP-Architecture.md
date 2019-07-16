# Challenge: GCP Architecture

## Build and Deploy a Docker Image to a Kubernetes Cluster
- Build and tag a Docker Image of a sample application
- Push the tagged image to Google Container Registry
- Create a Kubernetes Cluster
- Deploy the application to the Kubernetes Cluster


```
gcloud config set compute/zone us-central1-a
```

```
gcloud container clusters create echo-cluster
```

Run the following command from the directory containing
```
gcloud builds submit --tag gcr.io/qwiklabs-gcp-f12cc47854371267/echo-app:v1 .
```

```
gcloud container clusters get-credentials echo-cluster
```

```
kubectl run echo-web --image=gcr.io/qwiklabs-gcp-f12cc47854371267/echo-app:v1 --port 8000
```

```
kubectl expose deployment echo-web --type="LoadBalancer"
```

```
kubectl apply -f echoweb-deployment.yaml
```

Copy a file from GCS
```
gsutil cp gs://my-bucket/*.txt .	
```

Unpack a tarball that is gzipped
```
tar -xzf rebol.tar.gz
```

Scale a resource specified in "foo.yaml" to 3
```
kubectl scale --replicas=3 -f foo.yaml
```

## Migrate a MySQL Database to Google Cloud SQL
```
gsutil cp [OBJECT_LOCATION] gs://[DESTINATION_BUCKET_NAME]/
```
```
mysqldump --databases [DATABASE_NAME] -h [INSTANCE_IP] -u [USERNAME] -p \
--hex-blob --skip-triggers --set-gtid-purged=OFF --ignore-table [VIEW_NAME1] [...] \
--default-character-set=utf8mb4 > [SQL_FILE].sql
```

gsutil cp bk_wordpress.sql gs://my-wordpress-bucket-001/


mysqldump --databases wordpress -u blogadmin -p --skip-triggers  > bk_wordpress.sql


user called blogadmin with password Password1*, which provides full access to that d