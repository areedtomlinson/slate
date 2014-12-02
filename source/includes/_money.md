# Payment

## Update Social Security Number

```http
HTTP/1.1 200 OK
{
    "message": "Successfully updated your account profile."
}
```

```shell
curl -H 'Authorization: Token YOURTOKENHERE' -d "ssn=111-11-1111" -i staging.getbellhops.com/api/v1/ssn/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.get(reverse('api-ssn'),
    {
        'ssn':'xxx-xx-xxxx',
    })
```

```objective_c

```

```java
Coming Soon!
```

This endpoint cleans up a passed SSN and tries to set it 

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/bellhopprofiles/<pk>`

Parameter | Default | Description
--------- | ------- | -----------
ssn | None | The social security number of the requesting bellhop.