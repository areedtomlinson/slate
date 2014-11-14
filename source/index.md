---
title: API Reference

language_tabs:
  - http
  - shell
  - python
  - objective_c
  - java

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Bellhops API! Here you can sign up as a Bellhop or Customer, book and claim jobs, and more.

For the time being, we have language bindings in HTTP, Shell, Python (Django), Swift (listed as Objective C because Slate doesn't have Swift support yet), and Java (coming soon).

# Authentication

## Tokens! Get Your Tokens!

```http
POST /api/v1/auth/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Basic ...
``` 

```http
HTTP/1.0 200 OK
Content-Type: Application/json
{
    "pk": 1,
    "email": "your_email@test.com",
    "is_superuser": false,
    "first_name": "Fernbuckle",
    "last_name": "McDragbottom",
    "profiles": [
        {
            "profile_type": "token",
            "key": "your-auth-token",
            "created": "2014-09-08T18:31:13.615Z"
        },
        {
            "href": "http://getbellhops.com/api/v1/bellhopprofiles/1/",
            "profile_type": "bellhop"
        },
        {
            "href": "http://localhost:4567/api/v1/photoprofiles/1/",
            "profile_type": "photo",
            "image": "https://bellhops-staging.s3.amazonaws.com/profiles/your-photo-profile-url.png"
        }
    ]
}
```

```shell
# Your username will be the same as your email address.
curl -X POST -u "your_username:your_password" getbellhops.com/api/v1/auth/
```

```python
# Your username will be the same as your email address.
from django.core.urlresolvers import reverse
from django.test import Client
import base64
user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
c = APIClient()
c.credentials(HTTP_AUTHORIZATION = "Basic " + base64.b64encode('test1@user.com:password'))
response = c.post(reverse('api-auth'))
# User's token will be at response.data['profiles'][0]['key']



```

```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c
// Your username will be the same as your email address.
NetworkManager.sharedInstance.login(
          email: your_email,
          password: your_password, 
          success: { operation, mappingResult in
                        ...
                    },
          failure: { operation, error in
            ...
          }
      )
/* 
  The login function sets the Authorization header with the returned Token for all future requests. 

  Logout is achieved by deleting authorization headers (as well as UserDefaults, etc). This is achieved with the NetworkManager.sharedInstance.logout() function. 
*/
```



```java
// Coming soon!
```

The Bellhops API uses basic auth for login. That endpoint returns a Token that can be used for subsequent requests with token auth.


<aside class="notice">
Basic and Token Auth should only be used over HTTPS.

On the bellhops production server, hitting any endpoint on HTTP will give you a 301 response, because all traffic is forwarded to HTTPS.
</aside>


## Reset Your Password

```http
POST /api/v1/auth/reset-password/your.email@fake.com/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
``` 

```http
HTTP/1.0 205 RESET CONTENT
Content-Type: application/json
{
    "message": "Password reset email has been sent. Please check your inbox."
}

```

```shell
curl -X POST getbellhops.com/api/v1/auth/reset-password/your.email@fake.com/
```

```python
from django.core.urlresolvers import reverse
from rest_framework.test import APIClient
c = APIClient()
response = c.post(reverse('api-reset-password', args=['your.email@fake.com']))
# response.status_code will be 205 no matter what.
```

```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c
 NetworkManager.sharedInstance.resetPassword(emailAddress, 
                success: { operation, responseObject in
                    ...
                },
                failure: { operation, error in
                    ...
                }
            )
```



```java
// Coming soon!
```

The password reset endpoint will always return a 205 status ("Reset Content"), even if the specified email address is not associated with a user. This way, the endpoint does not
reveal which email addresses are in use.

Downstream effect: If there is a user with this email address, they will receive an email with a password reset link.


# Users

## Get All Users

```http
GET /api/v1/users/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Token ...
``` 

```http
HTTP/1.0 200 OK
Content-Type: application/json
{
   # Always 1 for non-superuser:
   "count":25241,  
   # Always null for non-superuser:
   "next":"https://getbellhops.com/api/v1/users/?page=2",
   "previous":null,
   "results":[
      {
         "pk":36,
         "email":"fern@buckle.com",
         "is_superuser":false,
         "first_name":"Fernbuckle",
         "last_name":"McDragbottom",
         "profiles":[ ... see /auth/ for an example of profiles ... ]
         ]
      },
      ...
    ]
}
```

```shell
curl -X GET -H "Authorization: Token your-token-here" https://getbellhops.com/api/v1/users/
```

```python
from django.core.urlresolvers import reverse
from rest_framework.test import APIClient
user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
c = APIClient()
c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
response = c.get(reverse('api-user-list'))
```


```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c

// Coming soon!
```



```java
// Coming soon!
```

If you're a non-superuser, this endpoint will only return your user account.
If you're a superuser, this endpoint returns all users.


## Get One User

```http
GET /api/v1/users/<pk>/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Token ...
``` 

```http
HTTP/1.0 200 OK
Content-Type: application/json
{
   "pk":<pk>,
   "email":"fern@buckle.com",
   "is_superuser":false,
   "first_name":"Fernbuckle",
   "last_name":"McDragbottom",
   "profiles":[ ... see /auth/ for an example of profiles ... ]
   ]
}
```

```shell
curl -X GET -H "Authorization: Token your-token-here" https://getbellhops.com/api/v1/users/<pk>/
```

```python
from django.core.urlresolvers import reverse
from rest_framework.test import APIClient
user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
c = APIClient()
c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
response = c.get(reverse('api-user-detail', args=[<pk>]))
```


```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c
NetworkManager.sharedInstance.getUserInfo(userID, 
                success: { operation, responseObject in
                    ...
                },
                failure: { operation, error in
                    ...
                }
            )
```



```java
// Coming soon!
```


If you're a superuser, this endpoint returns the specified user.
If you're a non-superuser and this is your user id, you'll get your user record. If this isn't your user id, you'll get a 403.

## Post a User

```http
POST /api/v1/users/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
``` 


```http
HTTP/1.0 200 OK
Content-Type: application/json
```

```shell
curl -X POST -d "first_name=FirstName&last_name=LastName&email=test@email.com&password=password" https://getbellhops.com/api/v1/users/
```

```python
from django.core.urlresolvers import reverse
from rest_framework.test import APIClient
c = APIClient()
response = c.post(reverse('api-user-list'), {
      'first_name':'FirstName',
      'last_name':'LastName',
      'email':'test@email.com',
      'password':'password'
    }
  )
```


```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c
User.postUser(
                email,
                password: password,
                firstName: firstName,
                lastName: lastName,
                success:{ operation, mappingResult in
                    ...
                },
                failure: { operation, error in
                   ...
                }
            )
// Coming soon!
```



```java
// Coming soon!
```


This endpoint always returns a 200, empty response, no matter what.


# Customers

## Get All Customers

```http
GET /api/v1/customers/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Token ...
``` 

```http
HTTP/1.0 200 OK
Content-Type: application/json
{
   "count":12923,
   "next":"https://getbellhops.com/api/v1/customers/?page=2",
   "previous":null,
   "results":[
      {
         "url":"https://getbellhops.com/api/v1/customers/2/",
         "id":2,
         "first_name":"Fernbuckle",
         "last_name":"McDragbottom",
         "email":"fern@buckle.edu",
         "phone":"123-546-7890",
         "orders":{
            "count":1,
            "next":null,
            "previous":null,
            "results":[
               {
                  ...see /order/ for an example...
               }
            ]
         }
      },
      ...
   ]
}
```

```shell
curl -X GET -H "Authorization: Token your-token-here" https://getbellhops.com/api/v1/customers/
```

```python
from django.core.urlresolvers import reverse
from rest_framework.test import APIClient
user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
c = APIClient()
c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
response = c.get(reverse('api-customer-list'))
```


```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c

// Coming soon!
```



```java
// Coming soon!
```

No matter who you are, this endpoint returns all customers.

<aside class="warning">
For a non super-user, we should only return a subset of Customers. <a href="https://www.pivotaltracker.com/story/show/82597272">See this pivotal story.</a>
</aside>

<aside class="warning">
Customer serialization needs to be re-worked. <a href="https://www.pivotaltracker.com/story/show/82598804">See this pivotal story.</a>
</aside>


## Get One Customer

```http
GET /api/v1/customers/<pk>/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Basic ...
``` 

```http
HTTP/1.0 200 OK
Content-Type: application/json
{
  "url":"https://getbellhops.com/api/v1/customers/2/",
  "id":2,
  "first_name":"Fernbuckle",
  "last_name":"McDragbottom",
  "email":"fern@buckle.edu",
  "phone":"123-546-7890",
  "orders":{
    "count":1,
    "next":null,
    "previous":null,
    "results":[
       {
          ...see /order/ for an example...
       }
    ]
}
```

```shell
curl -X GET -H "Authorization: Token your-token-here" https://getbellhops.com/api/v1/customers/<pk>/
```

```python
from django.core.urlresolvers import reverse
from rest_framework.test import APIClient
user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
c = APIClient()
c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
response = c.get(reverse('api-user-detail', args=[<pk>]))
```


```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c

// Coming soon!
```

```java
// Coming soon!
```

This endpoint returns the specified customer, regardless of the user.

# Bellhop Profile Endpoints

## Get A Bellhop Profile

```http
HTTP/1.1 200 OK
    {
   "pk":19100,
   "user":26579,
   "school":2,
   "hometown":"Chattanooga",
   "grad_season":"SPG",
   "grad_year":"15",
   "major":"CompSci",
   "is_phone_verified":false,
   "student_orgs":"None",
   "coupon":42104,
   "address":null,
   "created_at":"2014-10-08T15:10:57.405Z",
   "modified_at":"2014-10-08T15:10:58.920Z",
   "referrer":null,
   "employment_status":"pending",
   "agreed_to_labor_release":true,
   "can_you_lift_75_lbs":true,
   "rankable":true,
   "craigslist_director":false,
   "how_did_you_hear":"fake",
   "notify_of_new_jobs_via_sms":null,
   "job_board_requirements":[
      {
         "url":"",
         "text":"Your account is inactive.",
         "app_text":"Your account is inactive.",
         "fulfilled":true,
         "requirement_name":"account_active"
      },
      {
         "url":"",
         "text":"Unfortunately, we aren't operational in a market near your school.",
         "app_text":"We aren't operating near you currently.",
         "fulfilled":true,
         "requirement_name":"market_operational"
      },
      {
         "url":"/hophr/verify-phone/",
         "text":"You have not verified your phone. Verify it <a href='/hophr/verify-phone/'>here</a>.",
         "app_text":"You haven't verified your phone!",
         "fulfilled":false,
         "requirement_name":"phone_verified"
      },
      {
         "url":"/training/onboarding/",
         "text":"You've not watched all the training videos and answered all the questions correctly. Finish this <a href='/training/onboarding/'>here</a>.",
         "app_text":"You've not finished the required lessons.",
         "fulfilled":false,
         "requirement_name":"training_complete"
      },
      {
         "url":"/hophr/profile/edit/",
         "text":"You've not answered ALL the personality questions and your profile is not complete. Complete it <a href='/hophr/profile/edit/'>here</a>.",
         "app_text":"You've not finished the personality questions!",
         "fulfilled":true,
         "requirement_name":"profile_complete"
      },
      {
         "url":"/dashboard/",
         "text":"You have not been accepted. Once a decision is made, you will be notified via email.</br> Want to re-record your interview video? <a href='/dashboard/?record=true'>Click Here</a>",
         "app_text":"Your application has not been accepted yet.",
         "fulfilled":false,
         "requirement_name":"is_hired"
      },
      {
         "url":"/hophr/profile/edit/",
         "text":"You haven't got a profile photo yet. Let us see your pretty face by uploading to your <a href='/hophr/profile/edit/'>profile</a>.",
         "app_text":"We need a profile photo from you!",
         "fulfilled":true,
         "requirement_name":"photo_present"
      },
      {
         "url":"/hophr/profile/edit/",
         "text":"We need your address on file for end of year accounting and tax purposes.<br/>Please click the following link to fill in your address <a href='/hophr/profile/edit/'>here</a>",
         "app_text":"We need your address!",
         "fulfilled":false,
         "requirement_name":"address_present"
      },
      {
         "url":"/hophr/profile/edit/",
         "text":"We need you to set your communications preferences regarding receiving SMSs from Bellhops. You can do it by <a href='/hophr/profile/edit/'> editing your profile here</a>",
         "app_text":"Please set your communication preferences.",
         "fulfilled":false,
         "requirement_name":"communication_preferences_set"
      },
      {
         "url":"",
         "text":"In order to be approved you'll need to submit a video interview.",
         "app_text":"In order to be approved you'll need to submit a video interview.",
         "fulfilled":false,
         "requirement_name":"interview_video_recorded"
      }
   ],
   "can_claim_jobs":false,
   "phone":"4232229999",
   "pretty_phone":"(423) 222-9999"
}
```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -i staging.getbellhops.com/api/v1/bellhopprofiles/19100/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-bellhopprofile-detail', args=[<pk>]))
```

```objective_c

```

```java
Coming Soon!
```

This endpoint retrieves a single bellhop profile.

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/bellhopprofiles/<pk>`

Parameter | Default | Description
--------- | ------- | -----------
pk | None | The primary key of the bellhop you wish to GET

## Get All Bellhop Profiles

```http
HTTP/1.1 200 OK
    {
   "count":3,
   "next":null,
   "previous":null,
   "results":[
      {  },
      {  },
      {  }
   ]
}
```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -i staging.getbellhops.com/api/v1/bellhopprofiles/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-bellhopprofile-list'))
```

```objective_c

```

```java
Coming Soon!
```

This endpoint retrieves all bellhop profiles.

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/bellhopprofiles/`

## Get All Bellhop Profiles Currently Being Reviewed

```http
HTTP/1.1 200 OK
    {
   "count":3,
   "next":null,
   "previous":null,
   "results":[
      {  },
      {  },
      {  }
   ]
}
```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -i staging.getbellhops.com/api/v1/applications/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-applications-list'))
```

```objective_c

```

```java
Coming Soon!
```

This endpoint retrieves all bellhop profiles that are awaiting approval.
<aside class="notice">
You must be a superuser to GET from this endpoint.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/applications/`

## Get PhotoProfile Of Currently Authenticated User

```http
HTTP/1.1 200 OK
{
   "count":1,
   "next":null,
   "previous":null,
   "results":[
      {
         "href":"http://staging.getbellhops.com/api/v1/photoprofiles/",
         "profile_type":"photo",
         "image":"your-image-url-will-go-here"
      }
   ]
}

```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -i staging.getbellhops.com/api/v1/photoprofiles/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-photoprofile-list'))
```

```objective_c

```

```java
Coming Soon!
```

PhotoProfiles are how we keep track of a User's photo (Bellhop or Customer).
This Endpoint serves up the current user's photo profile.

<aside class="notice">
If the authenticated user is a superuser, this endpoint returns all PhotoProfiles.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/photoprofiles/`

## Get A Specific PhotoProfile

```http
HTTP/1.1 200 OK
{
   "count":1,
   "next":null,
   "previous":null,
   "results":[
      {
         "href":"http://staging.getbellhops.com/api/v1/photoprofiles/<pk>/",
         "profile_type":"photo",
         "image":"your-image-url-will-go-here"
      }
   ]
}

```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -i staging.getbellhops.com/api/v1/photoprofiles/<pk>/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-photoprofile-list', args=[<pk>]))
```

```objective_c

```

```java
Coming Soon!
```

PhotoProfiles are how we keep track of a User's photo (Bellhop or Customer).
This Endpoint serves up the photo profile that matches the pk that was passed in.

<aside class="notice">
If the user requests a photoprofile that is not his own and the user is not a superuser,
this will return a 403.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/photoprofiles/<pk>`

Parameter | Default | Description
--------- | ------- | -----------
pk | None | The primary key of the photo profile you wish to GET


## Post a PhotoProfile

```http
HTTP/1.1 100 Continue
HTTP/1.0 200 OK
{
    "href": "http://localhost:4567/api/v1/photoprofiles/<pk>/",
    "profile_type": "photo",
    "image": "your-image-url-will-go-here"}

```

```shell
curl -X POST -i -H "Authorization: Token your-token-here" -F "image=@test_file_name.png" localhost:4567/api/v1/photoprofiles/
```

```python
# Nonesuch right now
```

```objective_c
class func postPhotoProfile(
        image: UIImage!,
        success: { operation, response in
          ...
        }
        failure: { operation, error in 
          ...
        }
    {
```

```java
Coming Soon!
```

Posting a photoProfile with an image file either creates a photoProfile for this user, or updates this user's photoProfile to use the uploaded photo.

# Onboarding
## Get Interview Video

```http
HTTP/1.1 200 OK
{
   "created_at":"2014-02-27T02:20:20.181Z",
   "cameratag_uuid":"v-59f4dfd0-8183-0131-32ab-22000a499ea4",
   "video_url":null,
   "cameratag_status":null,
   "bellhop":5598
}
```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -i staging.getbellhops.com/api/v1/interviewvideo/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-interviewvideo-list'))
```

```objective_c

```

```java
Coming Soon!
```

When Bellhops sign up, they make an interview video.
This endpoint gets the interview video the requesting user has submitted.
If no interview video has been recorded, this returns 400.

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/interviewvideo`

## Post Interview Video

```http
HTTP/1.1 200 OK
{
    "created_at": "2014-11-14T14:24:16.347Z",
    "cameratag_uuid": "xxxx",
    "video_url": "http://www.xxxx.com/",
    "cameratag_status": "ready",
    "bellhop": xxxxx}
}
```

```shell
curl -X POST -i -H "Authorization: Token YOURTOKENHERE" -d "cameratag_uuid=xxxx&video_url=http://www.xxxx.com/&cameratag_status=ready" staging.getbellhops.com/api/v1/interviewVideo/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-interviewvideo-list'),
                        {
                            'cameratag_uuid':'xxxx',
                            'video_url':'xxxx',
                            'cameratag_status':'ready'
                        }
                      )
```

```objective_c

```

```java
Coming Soon!
```

When Bellhops sign up, they make an interview video.
This endpoint allows the user to POST the video record to the server.

### HTTP Request
`POST http://staging.getbellhops.com/api/v1/interviewvideo`

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

