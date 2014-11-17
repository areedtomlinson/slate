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
