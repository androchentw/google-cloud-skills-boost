# GSP002 - Getting Started with Cloud Shell and gcloud

[GSP002 - Getting Started with Cloud Shell and gcloud](https://www.cloudskillsboost.google/course_sessions/6826066/labs/376189)

## Task 1. Configuring your environment

```sh
gcloud config set compute/region us-central1
gcloud config get-value compute/region

gcloud config set compute/zone us-central1-b
gcloud config get-value compute/zone

gcloud config get-value project
gcloud compute project-info describe --project $(gcloud config get-value project)
```

```sh
export PROJECT_ID=$(gcloud config get-value project)
export ZONE=$(gcloud config get-value compute/zone)
echo -e "PROJECT ID: $PROJECT_ID\nZONE: $ZONE"
```

```sh
gcloud compute instances create gcelab2 --machine-type e2-medium --zone $ZONE

Created [https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-02-890605515f6d/zones/us-central1-b/instances/gcelab2].
NAME: gcelab2
ZONE: us-central1-b
MACHINE_TYPE: e2-medium
PREEMPTIBLE: 
INTERNAL_IP: 10.128.0.2
EXTERNAL_IP: 35.193.66.49
STATUS: RUNNING
```

```sh
gcloud -h
gcloud config --help
gcloud help config

gcloud config list --all
gcloud components list
```

## Task 2. Filtering command-line output

```sh
gcloud compute instances list
gcloud compute instances list --filter="name=('gcelab2')"

gcloud compute firewall-rules list
# NAME                         NETWORK      DIRECTION  PRIORITY  ALLOW                         DENY  DISABLED
# default-allow-icmp           default      INGRESS    65534     icmp                                False
# default-allow-internal       default      INGRESS    65534     tcp:0-65535,udp:0-65535,icmp        False
# default-allow-rdp            default      INGRESS    65534     tcp:3389                            False
# default-allow-ssh            default      INGRESS    65534     tcp:22                              False
# dev-net-allow-ssh            dev-network  INGRESS    1000      tcp:22                              False
# serverless-to-vpc-connector  dev-network  INGRESS    1000      icmp,udp:665-666,tcp:667            False
# vpc-connector-egress         dev-network  INGRESS    1000      icmp,udp,tcp                        False
# vpc-connector-health-check   dev-network  INGRESS    1000      tcp:667                             False
# vpc-connector-to-serverless  dev-network  EGRESS     1000      icmp,udp:665-666,tcp:667            False

gcloud compute firewall-rules list --filter="network='default'"
gcloud compute firewall-rules list --filter="NETWORK:'default' AND ALLOW:'icmp'"
# NAME                         NETWORK      DIRECTION  PRIORITY  ALLOW                         DENY  DISABLED
# default-allow-icmp           default      INGRESS    65534     icmp                                False
# default-allow-internal       default      INGRESS    65534     tcp:0-65535,udp:0-65535,icmp        False
```

## Task 3. Connecting to your VM instance

```sh
gcloud compute ssh gcelab2 --zone $ZONE

sudo apt install -y nginx
exit
```

## Task 4. Updating the firewall

Communication with the virtual machine will fail as it does not have an appropriate firewall rule. Our nginx web server is expecting to communicate on tcp:80. To get communication working we need to:

* Add a tag to the gcelab2 virtual machine
* Add a firewall rule for http traffic

```sh
gcloud compute firewall-rules list

gcloud compute instances add-tags gcelab2 --tags http-server,https-server
gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

gcloud compute firewall-rules list --filter=ALLOW:'80'
# NAME                NETWORK  DIRECTION  PRIORITY  ALLOW   DENY  DISABLED
# default-allow-http  default  INGRESS    1000      tcp:80        False

curl http://$(gcloud compute instances list --filter=name:gcelab2 --format='value(EXTERNAL_IP)')
```

## Task 5. Viewing the system logs

```sh
gcloud logging logs list
gcloud logging logs list --filter="compute"
gcloud logging read "resource.type=gce_instance" --limit 5
gcloud logging read "resource.type=gce_instance AND labels.instance_name='gcelab2'" --limit 5
```
