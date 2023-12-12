# GSP100 - Kubernetes Engine: Qwik Start

[GSP100 - Kubernetes Engine: Qwik Start](https://www.cloudskillsboost.google/course_sessions/6826066/labs/376208)

## Task 1. Set a default compute zone

```sh
gcloud config set compute/region us-west1
gcloud config set compute/zone us-west1-c
```

## Task 2. Create a GKE cluster

```sh
gcloud container clusters create --machine-type=e2-medium --zone=us-west1-c lab-cluster
```

## Task 3. Get authentication credentials for the cluster

```sh
gcloud container clusters get-credentials lab-cluster
```

## Task 4. Deploy an application to the cluster

```sh
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
kubectl expose deployment hello-server --type=LoadBalancer --port 8080
kubectl get service
```

* http://[EXTERNAL-IP]:8080

## Task 5. Deleting the cluster

```sh
gcloud functions logs read helloWorld
```
