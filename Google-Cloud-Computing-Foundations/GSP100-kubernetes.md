# GSP100 - Kubernetes Engine: Qwik Start

[GSP100 - Kubernetes Engine: Qwik Start](https://www.cloudskillsboost.google/course_sessions/6826066/labs/376208)

## Task 1. Set a default compute zone

```sh
gcloud config set compute/region "REGION"
gcloud config set compute/zone "ZONE"
```

```js
/**
* Background Cloud Function to be triggered by Pub/Sub.
* This function is exported by index.js, and executed when
* the trigger topic receives a message.
*
* @param {object} data The event payload.
* @param {object} context The event metadata.
*/
exports.helloWorld = (data, context) => {
const pubSubMessage = data;
const name = pubSubMessage.data
    ? Buffer.from(pubSubMessage.data, 'base64').toString() : "Hello World";

console.log(`My Cloud Function: ${name}`);
};
```

## Task 2. Create a cloud storage bucket

```sh
gsutil mb -p qwiklabs-gcp-00-691356bd2d57 gs://qwiklabs-gcp-00-691356bd2d57
```

## Task 3. Deploy your function

```sh
gcloud functions deploy helloWorld \
  --stage-bucket qwiklabs-gcp-00-691356bd2d57 \
  --trigger-topic hello_world \
  --runtime nodejs20

gcloud functions describe helloWorld
```

## Task 4. Test the function

```sh
DATA=$(printf 'Hello World!'|base64) && gcloud functions call helloWorld --data '{"data":"'$DATA'"}'
```

## Task 5. View logs

```sh
gcloud functions logs read helloWorld
```
