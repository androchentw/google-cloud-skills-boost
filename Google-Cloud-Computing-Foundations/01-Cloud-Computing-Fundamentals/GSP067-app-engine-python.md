# GSP067 - App Engine: Qwik Start - Python

[GSP067 - App Engine: Qwik Start - Python](https://www.cloudskillsboost.google/course_sessions/6826066/labs/376202)

## Task 1. Enable Google App Engine Admin API

* App Engine Admin API

```sh
gcloud config set compute/region us-east1
```

## Task 2. Download the Hello World app

```sh
git clone https://github.com/GoogleCloudPlatform/python-docs-samples.git
cd python-docs-samples/appengine/standard_python3/hello_world
```

## Task 3. Test the application

* Web preview (web preview icon) > Preview on port 8080

```sh
dev_appserver.py app.yaml
```

## Task 4. Make a change

```sh
cd python-docs-samples/appengine/standard_python3/hello_world
nano main.py
```

## Task 5. Deploy your app

```sh
gcloud app deploy
# 11: us-east1

# Creating App Engine application in project [qwiklabs-gcp-02-cca4f26fe0a3] and region [us-east1]....w
# orking.                                                                                             
# Creating App Engine application in project [qwiklabs-gcp-02-cca4f26fe0a3] and region [us-east1]....d
# one.
# Services to deploy:
# descriptor:                  [/home/student_01_e1a2851b428b/python-docs-samples/appengine/standard_python3/hello_world/app.yaml]
# source:                      [/home/student_01_e1a2851b428b/python-docs-samples/appengine/standard_python3/hello_world]
# target project:              [qwiklabs-gcp-02-cca4f26fe0a3]
# target service:              [default]
# target version:              [20231212t121921]
# target url:                  [https://qwiklabs-gcp-02-cca4f26fe0a3.ue.r.appspot.com]
# target service account:      [qwiklabs-gcp-02-cca4f26fe0a3@appspot.gserviceaccount.com]
```

## Task 6. View your application

```sh
gcloud app browse
```
