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

# NAME: lab-cluster
# LOCATION: us-west1-c
# MASTER_VERSION: 1.27.3-gke.100
# MASTER_IP: 34.168.154.214
# MACHINE_TYPE: e2-medium
# NODE_VERSION: 1.27.3-gke.100
# NUM_NODES: 3
# STATUS: RUNNING
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
# NAME           TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
# hello-server   LoadBalancer   10.64.3.180   35.247.58.5   8080:32260/TCP   2m2s
# kubernetes     ClusterIP      10.64.0.1     <none>        443/TCP          7m51s
```

* http://[EXTERNAL-IP]:8080

## Task 5. Deleting the cluster

```sh
gcloud functions logs read helloWorld
```
