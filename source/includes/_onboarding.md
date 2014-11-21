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
`POST http://staging.getbellhops.com/api/v1/setsmspreferences/`

## Set SMS Preferences
HTTP/1.1 201 CREATED
```http

{
    "message": "SMS Notification Preferences Set"
}

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
    response = c.post(reverse('api-setsmspreferences-detail'), {'fulfilled':'True'})
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

## Get Training Video URL
HTTP/1.0 200 OK
```http
{
    "url": "https://s3.amazonaws.com/bellhops/training/cam_example_interview.mp4"
}
```

```shell
curl -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/trainingvideourl/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-trainingvideourl'))
```

```objective_c

```

```java
Coming Soon!
```
We currently have a video that is Cam showing potential bellhops how to record an interview video. 
This gets the URL to where that is hosted.

## Send Verification Text
HTTP/1.0 201 
```http
{
    "url": "https://s3.amazonaws.com/bellhops/training/cam_example_interview.mp4"
}
```

```shell
curl -X POST -H 'Authorization: Token YOURKEYHERE' -i staging.getbellhops.com/api/v1/verifyphone/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-verify-phone-list'))
```

```objective_c

```

```java
Coming Soon!
```

This endpoint triggers a phone verification text to be sent to the requesting bellhop. 

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/verifyphone/`