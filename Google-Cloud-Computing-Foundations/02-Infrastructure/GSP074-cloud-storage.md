# GSP074 - Cloud Storage: Qwik Start - CLI/SDK

[GSP074 - Cloud Storage: Qwik Start - CLI/SDK](https://www.cloudskillsboost.google/course_sessions/6846186/labs/377256)

## Task 1. Create a bucket

```sh
gcloud config set compute/region us-central1
gsutil mb gs://qwiklabs-gcp-03-20303124adfb
```

## Task 2. Upload an object into your bucket

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
