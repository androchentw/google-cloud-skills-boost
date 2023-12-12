# ARC122 - Analyze Images with the Cloud Vision API: Challenge Lab

[ARC122 - Analyze Images with the Cloud Vision API: Challenge Lab](https://www.cloudskillsboost.google/games/4713/labs/30680)

## Task 1. Verify your resources

* APIs & Services > Credentials > Create Credentials > API key
* Create and save environment variable `API_KEY`
* Create: `PROJECT ID`-bucket = `-bucket`
`qwiklabs-gcp-01-4a0dbc9fe2a7-bucket`
* Edit Object ACL
  * Entity: Public
  * Name: allUsers
  * Access: Reader

```sh
export API_KEY=<YOUR_API_KEY>
```

## Task 2. Create Request.json file

## Task 3. Update the json file

### `TEXT_DETECTION`

```json
{
  "requests": [
    {
      "image": {
        "source": {
          "gcsImageUri": "gs://qwiklabs-gcp-01-4a0dbc9fe2a7-bucket/manif-des-sans-papiers.jpg"
        }
      },
      "features": [
        {
          "type": "TEXT_DETECTION",
          "maxResults": 10
        }
      ]
    }
  ]
}
```

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @text-request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o text-response.json
```

```sh
gsutil cp text-response.json gs://qwiklabs-gcp-01-4a0dbc9fe2a7-bucket
```

### `LANDMARK_DETECTION`

```sh
curl -s -X POST -H "Content-Type: application/json" --data-binary @landmark-request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o landmark-response.json
```

```sh
gsutil cp landmark-response.json gs://qwiklabs-gcp-01-4a0dbc9fe2a7-bucket
```
