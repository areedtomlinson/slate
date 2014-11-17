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
