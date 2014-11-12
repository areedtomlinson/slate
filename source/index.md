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
curl  -X POST -u "your_username:your_password" getbellhops.com/api/v1/auth/
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

