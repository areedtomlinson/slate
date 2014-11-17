# Bellhop Profiles

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
