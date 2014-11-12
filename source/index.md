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
curl  -X POST -u "your_username:your_password" getbellhops.com/api/v1/auth/
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
Authorization: Basic ...
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
 NetworkManager.sharedInstance.resetPassword(emailTextField.text,
                success: { operation, responseObject -> () in
                    ...
                },
                failure: { operation, error -> () in
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


# Admin

Most of the endpoints here can be used by non-superusers in a limited capacity, but are really only helpful for admins.

## Get All Users

```http
GET /api/v1/users/ HTTP/1.1
Host: getbellhops.com
Content-Type: application/json
Authorization: Basic ...
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
      }
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

If you're a non-superuser, this endpoint will only return your user account (with a limited subset of fields).
If you're a superuser, this endpoint returns all users, and all fields.


## Get One User
If you're a superuser, this endpoint returns the specified user, with all data fields.
If you're a non-superuser and this is your user id, you'll get your user record with a limited subset of fields. If this isn't your user id, you'll get a 403.

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

