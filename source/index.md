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
  - authentication
  - errors


search: true
---

# Introduction

Welcome to the Bellhops API! Here you can sign up as a Bellhop or Customer, book and claim jobs, and more.

For the time being, we have language bindings in HTTP, Shell, Python (Django), Swift (listed as Objective C because Slate doesn't have Swift support yet), and Java (coming soon).





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

When Bellhops sign up, they make an interview video and it gets uploaded to cameratag.
This endpoint allows the user to the video record to the server.

### HTTP Request
`POST http://staging.getbellhops.com/api/v1/interviewvideo`


## Get All Incomplete Lessons

```http
HTTP/1.1 200 OK
{
   "count":12,
   "next":null,
   "previous":null,
   "results":[
      {
         "pk":1,
         "text":"Crush the Job",
         "video_url":"player.vimeo.com/video/64068310",
         "html":"<h2>Crush the Job</h2>\r\n<iframe id=\"question-player\" src=\"//player.vimeo.com/video/64068310?api=1&player_id=question-player\" width=\"100%\" height=\"500\" frameborder=\"0\" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>",
         "questions":[
            {
               "pk":1,
               "text":"Which of the following is a good way to WOW the customer?",
               "choices":[
                  {
                     "pk":1,
                     "text":"A. Stay up late the night before a job and act tired and grumpy.",
                     "is_correct":false
                  },
                  {...},
                  {...}
               ]
            },
            {
               "pk":2,
               "text":"How should you treat the people who you're moving in?",
               "choices":[
                  {
                     "pk":4,
                     "text":"Like they're my parents",
                     "is_correct":true
                  },
                  {...}
               ]
            }
         ]
      },
      {...},
      {...},
   ]
}
```

```shell
curl -i -H "Authorization: Token YOURTOKENHERE" staging.getbellhops.com/api/v1/lessons/

```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-lessons-list'))
```

```objective_c

```

```java
Coming Soon!
```

Before a bellhop can claim jobs, they must undergo training.
This endpoint returns all unfinished lessons.

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/lessons/`

## Get A Specific Lesson

```http
HTTP/1.1 200 OK

```

```shell
curl -i -H "Authorization: Token YOURTOKENHERE" staging.getbellhops.com/api/v1/lessons/1/

```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-lessons-detail', args=[PK]), )
```

```objective_c

```

```java
Coming Soon!
```

Before a bellhop can claim jobs, they must undergo training.
This endpoint returns a specific lesson given a PK.

Parameter | Default | Description
--------- | ------- | -----------
pk | None | The primary key of the lesson you wish to GET

## Get All UserAnswers

```http
HTTP/1.1 200 OK
{
   "count":223423,
   "next":"http://staging.getbellhops.com/api/v1/useranswers/?page=2",
   "previous":null,
   "results":[
      {
         "pk":1,
         "user":{
            "pk":3021,
            "email":"xxx.xxx@getbellhops.com",
            "is_superuser":true,
            "first_name":"xxx",
            "last_name":"xxx",
            "profiles":[  ]
         },
         "choice":{  },
         "question":{  },
         "created_at":"2014-02-02T23:38:19.010Z"
      },
      {
         "pk":2,
         "user":{  },
         "choice":{  },
         "question":{  },
         "created_at":"2014-02-02T23:38:19.019Z"
      },
```

```shell
curl -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/useranswers/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-useranswers-list'))
```

```objective_c

```

```java
Coming Soon!
```

Before a bellhop can claim jobs, they must undergo training.
This endpoint returns all of the answers that the requesting user has submitted for each lesson.

<aside class="notice">
If the requesting user is a superuser, then this returns all user answers.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/useranswers/`

## Get A Specific UserAnswer

```http
HTTP/1.1 200 OK
{
   "pk":1,
   "user":{
      "pk":3021,
      "email":"xxx@getbellhops.com",
      "is_superuser":false,
      "first_name":"xxx",
      "last_name":"xxx",
      "profiles":[
         {
            "profile_type":"token",
            "key":"d7207300ed4d7701e349632c5463a8947b4edf48",
            "created":"2014-08-26T15:50:42.789Z"
         },
         {
            "href":"http://staging.getbellhops.com/api/v1/bellhopprofiles/2387/",
            "profile_type":"bellhop"
         },
         {
            "href":"http://staging.getbellhops.com/api/v1/photoprofiles/13248/",
            "profile_type":"photo",
            "image":"https://bellhops-staging.s3.amazonaws.com/profiles/563e1d1ee9374078ae01bf7d0b004a4a.png"
         }
      ]
   },
   "choice":{
      "pk":2,
      "text":"B. \"Surprise! I brought you a couple bottled waters because I'm awesome and it's hot out here. Sorry I'm only 10 minutes early, I stopped to rescue a family of kittens on the side of the highway.\"",
      "is_correct":true
   },
   "question":{
      "pk":1,
      "text":"Which of the following is a good way to WOW the customer?",
      "choices":[
         {
            "pk":1,
            "text":"A. Stay up late the night before a job and act tired and grumpy.",
            "is_correct":false
         },
         {
            "pk":2,
            "text":"B. \"Surprise! I brought you a couple bottled waters because I'm awesome and it's hot out here. Sorry I'm only 10 minutes early, I stopped to rescue a family of kittens on the side of the highway.\"",
            "is_correct":true
         },
         {
            "pk":3,
            "text":"C. \"Surprise! I got lost and I\u2019m late because I'm a disorganized idiot.\"",
            "is_correct":false
         }
      ]
   },
   "created_at":"2014-02-02T23:38:19.010Z"
}
```

```shell
curl -i -H "Authorization: Token YOURTOKENHERE" staging.getbellhops.com/api/v1/useranswers/1/

```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-useranswer-detail', args=[PK]), )
```

```objective_c

```

```java
Coming Soon!
```

Before a bellhop can claim jobs, they must undergo training.
This endpoint returns a specific user answer from a completed lesson.

Parameter | Default | Description
--------- | ------- | -----------
pk | None | The primary key of the user answer you wish to GET

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/useranswers/PK`

## Set SMS Preferences

```http

```

```shell
curl -X POST -i -H "Authorization: Token YOURTOKENHERE" -d "notify=True" staging.getbellhops.com/api/v1/setsmspreferences/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-useranswer-detail'), {'fulfilled':'True'})
```

```objective_c

```

```java
Coming Soon!
```

### HTTP Request
`POST http://staging.getbellhops.com/api/v1/setsmspreferences`

## Training Video URL

```http

```

```shell
curl -X POST -i -H "Authorization: Token YOURTOKENHERE" -d "notify=True" staging.getbellhops.com/api/v1/trainingvideourl/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-useranswer-detail'), {'fulfilled':'True'})
```

```objective_c

```

```java
Coming Soon!
```

### HTTP Request
`POST http://staging.getbellhops.com/api/v1/setsmspreferences`

## Get All Markets

```http
HTTP/1.0 200 OK
{
   "count":152,
   "next":"http://localhost:8000/api/v1/markets/?page=2",
   "previous":null,
   "results":[
      {
         "directors":[  ],
         "verified_local_address":{  },
         "url":"http://xxx.xxx/api/v1/markets/151/",
         "name":"x",
         "geographic_center":null,
         "state":"AL",
         "time_zone":"Africa/Abidjan",
         "landing_page_slug":"1",
         "local_website":"http://getbellhops.com",
         "local_craigslist":"",
         "local_phone_number":"1",
         "bing_store_code":"",
         "accepting_applications":true,
         "accepting_orders":true,
         "recruiting_start_date":"2014-10-13T15:47:10.299Z",
         "market_open_date":"2014-10-13T15:47:10.299Z",
         "yelp_url":"",
         "google_place_url":"",
         "moving_company_url":"",
         "region":null
      },
      {  },
      {  },
      {  },
      {  },
      {  },
      {  },
      {  },
      {  },
      {  }
   ]
}
```

```shell
curl -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/markets/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-markets-list'))
```

```objective_c

```

```java
Coming Soon!
```

This endpoint returns all markets

<aside class="notice">
For security reasons, this endpoint returns a 403 for all but superusers.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/markets/`

## Get A Single Market

```http
HTTP/1.0 200 OK
{
   "count":1,
   "results":[
      {
         "directors":[  ],
         "verified_local_address":{  },
         "url":"http://xxx.xxx/api/v1/markets/151/",
         "name":"x",
         "geographic_center":null,
         "state":"AL",
         "time_zone":"Africa/Abidjan",
         "landing_page_slug":"1",
         "local_website":"http://getbellhops.com",
         "local_craigslist":"",
         "local_phone_number":"1",
         "bing_store_code":"",
         "accepting_applications":true,
         "accepting_orders":true,
         "recruiting_start_date":"2014-10-13T15:47:10.299Z",
         "market_open_date":"2014-10-13T15:47:10.299Z",
         "yelp_url":"",
         "google_place_url":"",
         "moving_company_url":"",
         "region":null
      }
   ]
}
```

```shell
curl -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/markets/PK/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-markets-list'),args=[PK])
```

```objective_c

```

```java
Coming Soon!
```

This endpoint returns a single market!

<aside class="notice">
For security reasons, this endpoint returns a 403 for all but superusers.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/markets/PK/`

## Get A Single School

```http

```

```shell
curl -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/schools/PK/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-schools-detail'), args=[PK])
```

```objective_c

```

```java
Coming Soon!
```

This endpoint returns a single school.

<aside class="notice">
For security reasons, this endpoint returns a 403 for all but superusers.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/schools/PK/`

## Get All Schools

```http

```

```shell
curl -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/schools/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-schools-list'))
```

```objective_c

```

```java
Coming Soon!
```

This endpoint returns a single school.

<aside class="notice">
For security reasons, this endpoint returns a 403 for all but superusers.
</aside>

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/schools/`