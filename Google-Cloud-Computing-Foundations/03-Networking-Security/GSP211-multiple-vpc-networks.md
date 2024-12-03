# GSP211 - Multiple VPC Networks

[GSP211 - Multiple VPC Networks](https://www.cloudskillsboost.google/course_sessions/6875708/labs/377208)

## Task 1. Create custom mode VPC networks with firewall rules

### Create the managementnet network

* VPC network > VPC networks > Create VPC Network
  * Name: managementnet
  * Subnet creation mode: Custom
  * Name: managementsubnet-<REGION>
  * Region: <REGION>
  * IPv4 range: 10.130.0.0/20

### Create the privatenet network

```sh
gcloud compute networks create privatenet --subnet-mode=custom
gcloud compute networks subnets create privatesubnet-Region --network=privatenet --region=Region --range=172.16.0.0/24
gcloud compute networks subnets create privatesubnet-Region --network=privatenet --region=Region --range=172.20.0.0/20

gcloud compute networks list
gcloud compute networks subnets list --sort-by=NETWORK
```

### Create the firewall rules for managementnet

* VPC network > Firewall > Create Firewall Rule.
  * Name: managementnet-allow-icmp-ssh-rdp
  * Network: managementnet
  * Targets: All instances in the network
  * Source filter: IPv4 Ranges
  * Source IPv4 ranges: 0.0.0.0/0
  * Protocols and ports: Specified protocols and ports, and then check tcp, type: 22, 3389; and check Other protocols, type: icmp.

### Create the firewall rules for privatenet

```sh
gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

gcloud compute firewall-rules list --sort-by=NETWORK
```

## Task 2. Create VM instances

```sh
curl https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Ada_Lovelace_portrait.jpg/800px-Ada_Lovelace_portrait.jpg --output ada.jpg
gsutil cp ada.jpg gs://qwiklabs-gcp-03-20303124adfb
rm ada.jpg
```

## Task 3. Download an object from your bucket

```sh
gsutil cp -r gs://qwiklabs-gcp-03-20303124adfb/ada.jpg .
```

## Task 4. Copy an object to a folder in the bucket

```sh
gsutil cp gs://qwiklabs-gcp-03-20303124adfb/ada.jpg gs://qwiklabs-gcp-03-20303124adfb/image-folder/
```

* http://[EXTERNAL-IP]:8080

## Task 5. List contents of a bucket or folder

```sh
gsutil ls gs://qwiklabs-gcp-03-20303124adfb
```

## Task 6. List details for an object

```sh
gsutil ls -l gs://qwiklabs-gcp-03-20303124adfb/ada.jpg
```

## Task 7. Make your object publicly accessible

```sh
gsutil acl ch -u AllUsers:R gs://qwiklabs-gcp-03-20303124adfb/ada.jpg
```

## Task 8. Remove public access

```sh
gsutil acl ch -d AllUsers gs://qwiklabs-gcp-03-20303124adfb/ada.jpg
gsutil rm gs://qwiklabs-gcp-03-20303124adfb/ada.jpg
```
