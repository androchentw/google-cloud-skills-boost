# GSP164 - Cloud Endpoints: Qwik Start

[GSP164 - Cloud Endpoints: Qwik Start](https://www.cloudskillsboost.google/course_sessions/6846186/labs/377271)

* A REST API that you can query to find the name of an airport from its three-letter IATA code (for example, SFO, JFK, AMS).
* A script that uploads the API configuration to Cloud Endpoints.
* A script that deploys a Google App Engine flexible backend to host the sample API.

## Task 1. Getting the sample code

```sh
gsutil cp gs://spls/gsp164/endpoints-quickstart.zip .
unzip endpoints-quickstart.zip
cd endpoints-quickstart
```

## Task 2. Deploying the Endpoints configuration

* [`deploy_api.sh`](GSP164-cloud-endpoints/deploy_api.sh)
* [`util.sh`](GSP164-cloud-endpoints/util.sh)

```sh
cd scripts
./deploy_api.sh

# Service Configuration [2023-12-13r0] uploaded for service [qwiklabs-gcp-03-f18be6e1c54c.appspot.com]
```

## Task 3. Deploying the API backend

* [`deploy_app.sh`](GSP164-cloud-endpoints/deploy_app.sh)

```sh
./deploy_app.sh
# gcloud app create --region=us-central
# Deploying ../app/app_template.yaml...
# gcloud -q app deploy ../app/app.yaml
# ...
# Deployed service [default] to [https://qwiklabs-gcp-03-f18be6e1c54c.uc.r.appspot.com]

# You can stream logs from the command line by running:
#   $ gcloud app logs tail -s default

# To view your application in the web browser run:
#   $ gcloud app browse
```

## Task 4. Sending requests to the API

* [`query_api.sh`](GSP164-cloud-endpoints/query_api.sh)

```sh
./query_api.sh
# curl "https://qwiklabs-gcp-03-f18be6e1c54c.appspot.com/airportName?iataCode=SFO"
# San Francisco International Airport

./query_api.sh JFK
# curl "https://qwiklabs-gcp-03-f18be6e1c54c.appspot.com/airportName?iataCode=JFK"
# John F Kennedy International Airport
```

## Task 5. Tracking API activity

* [`generate_traffic.sh`](GSP164-cloud-endpoints/generate_traffic.sh)
* Navigation menu > Endpoints > Services and click Airport Codes

```sh
./generate_traffic.sh
# HTTP status codes received from https://qwiklabs-gcp-03-f18be6e1c54c.appspot.com/airportName?iataCode=SFO:
# 200: 16
```

## Task 6. Add a quota to the API

```sh
./deploy_api.sh ../openapi_with_ratelimit.yaml
# Service Configuration [2023-12-13r1] uploaded for service [qwiklabs-gcp-03-f18be6e1c54c.appspot.com]

./deploy_app.sh
```

* Navigation menu > APIs & Services > Credentials > Create credentials > API Key

```sh
export API_KEY=YOUR-API-KEY
./query_api_with_key.sh $API_KEY
# curl -H 'x-api-key: YOUR-API-KEY' "https://qwiklabs-gcp-03-f18be6e1c54c.appspot.com/airportName?iataCode=SFO"
# San Francisco International Airport

./generate_traffic_with_key.sh $API_KEY
# wait 5~10 seconds then CTRL+C
# HTTP status codes received from https://qwiklabs-gcp-03-f18be6e1c54c.appspot.com/airportName?iataCode=SFO&key=YOUR-API-KEY:
# 429: 17
# 200: 6

./query_api_with_key.sh $API_KEY
# # curl -H 'x-api-key: YOUR-API-KEY' "https://qwiklabs-gcp-03-f18be6e1c54c.appspot.com/airportName?iataCode=SFO"
# {
#  "code": 8,
#  "message": "Quota exceeded for quota metric 'airport_requests' and limit 'limit-on-airport-requests' of service 'qwiklabs-gcp-03-f18be6e1c54c.appspot.com' for consumer 'project_number:503183694600'.",
#  "details": [
#   {
#    "@type": "type.googleapis.com/google.rpc.DebugInfo",
#    "stackEntries": [],
#    "detail": "internal"
#   }
#  ]
# }
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
