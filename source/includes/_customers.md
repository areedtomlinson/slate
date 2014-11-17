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