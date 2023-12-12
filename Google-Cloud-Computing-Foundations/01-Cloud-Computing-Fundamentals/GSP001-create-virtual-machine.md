# GSP001 - Creating a Virtual Machine

[GSP001 - Creating a Virtual Machine](https://www.cloudskillsboost.google/course_sessions/6826066/labs/376198)

## Task 1. Create a new instance from the Cloud console

```sh
gcloud config set compute/zone us-west1-c
```

## Task 2. Install an NGINX web server

```sh
sudo apt-get update
sudo apt-get install -y nginx
ps auwx | grep nginx
```

http://EXTERNAL_IP/

## Task 3. Create a new instance with gcloud

```sh
gcloud compute instances create gcelab2 --machine-type e2-medium --zone=$ZONE
gcloud compute ssh gcelab2 --zone=$ZONE
```
