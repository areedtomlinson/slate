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

For the time being, we have language bindings in HTTP and Shell (see right sidebar). More to come!

# Authentication

> To authorize, use this code:  

```http
POST /api/v1/auth/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Basic ...


HTTP/1.0 200 OK
Content-Type: Application/json
{
    "pk": 1,
    "email": "your_email",
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
auth_headers = {'HTTP_AUTHORIZATION': 'Basic ' + base64.b64encode('test@user.com:password'),}
token = user.auth_token
c = Client()
response = c.post(reverse('api-auth'), **auth_headers)
# User's token will be at response.data['profiles'][0]['key']
```

```objective_c
// NOTE jk this is actually swift, but there's no Swift support in Slate yet, so we alias it as objective_c
// Your username will be the same as your email address.
RKObjectManager.sharedManager().HTTPClient.setAuthorizationHeaderWithUsername(email, password:password)
NetworkManager.sharedInstance.POST("api/v1/auth/",
            parameters: nil,
            success: { { operation, mappingResult in
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

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>


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
    from django.test import Client
    c = Client()
    auth_headers = {'HTTP_AUTHORIZATION': 'Token YOURTOKENHERE'}
    response = c.get(reverse('api-bellhopprofile-list'), {'pk':'19100',}, **auth_headers)
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
    from django.test import Client
    c = Client()
    auth_headers = {'HTTP_AUTHORIZATION': 'Token YOURTOKENHERE'}
    response = c.get(reverse('api-bellhopprofile-list'), **auth_headers)
```

```objective_c

```

```java
Coming Soon!
```

This endpoint retrieves all bellhop profiles.

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/bellhopprofiles/`



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

