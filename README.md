## Create GKE cluster in default network
```
export PROJECT_ID='data-protection-01'
gcloud config set project ${PROJECT_ID}
gcloud config set compute/zone us-west1-a
gcloud config set compute/region us-west1
gcloud auth login
gcloud container clusters create dmilan-wordpress-01 --region us-west1-a


```
## create a cloud SQL MySQL (Optional)

```
gcloud sql instances create blog-db --root-password="mypass123" --database-version=MYSQL_5_7 --zone=us-west1-a
```

## Run the kubernetes deployment

```

gcloud container clusters get-credentials dmilan-wordpress-01 --zone us-west1-a --project data-protection-01

export KNS=wordpress
kubectl create ns ${KNS}
kubectl -n ${KNS} apply -f k8s-manifests/
```

## Get the service ip

`kubectl -n ${KNS} get svc `
# Copy External IP and access the cluster




