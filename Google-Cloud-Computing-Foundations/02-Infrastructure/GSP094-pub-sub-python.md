# GSP094 - Google Cloud Pub/Sub: Qwik Start - Python

[GSP094 - Google Cloud Pub/Sub: Qwik Start - Python](https://www.cloudskillsboost.google/course_sessions/6846186/labs/377275)

* Learn the basics of Pub/Sub.
* Create and list a Pub/Sub topic.
* Create and list a Pub/Sub subscription.
* Publish messages to a topic.
* Use a pull subscriber to output individual topic messages.

## Task 1. Create a virtual environment

```sh
sudo apt-get install -y virtualenv
python3 -m venv venv
source venv/bin/activate
```

## Task 2. Install the client library

```sh
pip install --upgrade google-cloud-pubsub
git clone https://github.com/googleapis/python-pubsub.git
cd python-pubsub/samples/snippets
```

## Task 3. Pub/Sub - the Basics

A `topic` is a shared string that allows applications to connect with one another through a common thread.

`Publishers` push (or publish) a message to a Cloud Pub/Sub topic. `Subscribers` will then make a subscription to that thread, where they will either pull messages from the topic or configure webhooks for push subscriptions. Every subscriber must acknowledge each message within a configurable window of time.

In sum, a `publisher` creates and sends messages to a topic and a `subscriber` creates a subscription to a topic to receive messages from it.

## Task 4. Create a topic

* [`publisher.py`](https://github.com/googleapis/python-pubsub/blob/main/samples/snippets/publisher.py)

```sh
echo $GOOGLE_CLOUD_PROJECT
cat publisher.py
python publisher.py -h

python publisher.py $GOOGLE_CLOUD_PROJECT create MyTopic
# Created topic: projects/qwiklabs-gcp-01-601aa9a49039/topics/MyTopic
python publisher.py $GOOGLE_CLOUD_PROJECT list
```

## Task 5. Create a subscription

* [subscriber.py](https://github.com/googleapis/python-pubsub/blob/main/samples/snippets/subscriber.py)

```sh
python subscriber.py $GOOGLE_CLOUD_PROJECT create MyTopic MySub

python subscriber.py $GOOGLE_CLOUD_PROJECT list-in-project
# projects/qwiklabs-gcp-01-601aa9a49039/subscriptions/MySub
```

## Task 6. Publish messages

```sh
gcloud pubsub topics publish MyTopic --message "Hello"
gcloud pubsub topics publish MyTopic --message "Publisher's name is <YOUR NAME>"
gcloud pubsub topics publish MyTopic --message "Publisher likes to eat <FOOD>"
gcloud pubsub topics publish MyTopic --message "Publisher thinks Pub/Sub is awesome"
```

## Task 7. View messages

```sh
python subscriber.py $GOOGLE_CLOUD_PROJECT receive MySub
```

output:

```text
Listening for messages on projects/qwiklabs-gcp-01-601aa9a49039/subscriptions/MySub..

Received Message {
  data: b'Hello'
  ordering_key: ''
  attributes: {}
}.
Received Message {
  data: b"Publisher's name is <YOUR NAME>"
  ordering_key: ''
  attributes: {}
}.
Received Message {
  data: b'Publisher likes to eat <FOOD>'
  ordering_key: ''
  attributes: {}
}.
Received Message {
  data: b'Publisher thinks Pub/Sub is awesome'
  ordering_key: ''
  attributes: {}
}.
```
