# GSP499 - User Authentication: Identity-Aware Proxy

[GSP499 - User Authentication: Identity-Aware Proxy](https://www.cloudskillsboost.google/course_sessions/6846186/labs/377284)

* How to write and deploy a simple App Engine app using Python
* How to enable and disable IAP to restrict access to your app
* How to get user identity information from IAP into your app
* How to cryptographically verify information from IAP to protect against spoofing

What is Identity-Aware Proxy?

Identity-Aware Proxy (IAP) is a Google Cloud service that intercepts web requests sent to your application, authenticates the user making the request using the Google Identity Service, and only lets the requests through if they come from a user you authorize. In addition, it can modify the request headers to include information about the authenticated user.

## Task 1. Deploy the application and protect it with IAP

* [`1-HelloWorld-main.py`](GSP499-iap/1-HelloWorld-main.py)

```sh
gsutil cp gs://spls/gsp499/user-authentication-with-iap.zip .
unzip user-authentication-with-iap.zip
cd user-authentication-with-iap

cd 1-HelloWorld
cat main.py

gcloud app deploy
# 12: us-east4
gcloud app browse

gcloud services disable appengineflex.googleapis.com
```

* Navigation menu Navigation menu icon > Security > Identity-Aware Proxy.
* ENABLE API > GO TO IDENTITY-AWARE PROXY > CONFIGURE CONSENT SCREEN > Internal
  * App name: `IAP Example`
  * Email: `student-04-976fc3249c86@qwiklabs.net`
  * Homepage: `https://qwiklabs-gcp-03-d70e3e6495b5.uk.r.appspot.com/`
  * Privacy: `https://qwiklabs-gcp-03-d70e3e6495b5.uk.r.appspot.com/privacy`
  * Authorized domains: `+ ADD DOMAIN`: `qwiklabs-gcp-03-d70e3e6495b5.uk.r.appspot.com`
* Return to Security > App Engine app > IAP > Turn on
* App Engine app > checkbox > Add Principal > `student-04-976fc3249c86@qwiklabs.net`
  * Role: `Cloud IAP > IAP-Secured Web App User`
  * Check: `https://qwiklabs-gcp-03-d70e3e6495b5.uk.r.appspot.com/_gcp_iap/clear_login_cookie`

## Task 2. Access user identity information

* [`2-HelloUser-main.py`](GSP499-iap/2-HelloUser-main.py)

```sh
cd ~/user-authentication-with-iap/2-HelloUser
gcloud app deploy

gcloud app browse
```

```python
user_email = request.headers.get('X-Goog-Authenticated-User-Email')
user_id = request.headers.get('X-Goog-Authenticated-User-ID')

# ...
page = render_template('index.html', email=user_email, id=user_id)

# index.html
Hello, {{ email }}! Your persistent ID is {{ id }}.
```

### Turn off IAP

```sh
curl -X GET https://qwiklabs-gcp-03-d70e3e6495b5.uk.r.appspot.com -H "X-Goog-Authenticated-User-Email: totally fake email"
```

## Task 3. Use Cryptographic Verification

* [`3-HelloVerifiedUser-main.py`](GSP499-iap/3-HelloVerifiedUser-main.py)

```sh
cd ~/user-authentication-with-iap/3-HelloVerifiedUser

gcloud app deploy
```

```python
def user():
    assertion = request.headers.get('X-Goog-IAP-JWT-Assertion')
    if assertion is None:
        return None, None

    info = jwt.decode(
        assertion,
        keys(),
        algorithms=['ES256'],
        audience=audience()
    )

    return info['email'], info['sub']
```
