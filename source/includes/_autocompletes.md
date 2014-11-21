# Autocompletes
These endpoints all exist to autocomplete fields on any api-serving app.

## Schools 

```http
HTTP/1.0 200 OK
[  
   {  
      "id":1395,
      "name":"Antonelli College-Hattiesburg"
   },
   {  
      "id":3965,
      "name":"Asbury Theological Seminary"
   },
   {  
      "id":3966,
      "name":"Asbury University"
   },
   ...
]
```

```shell
curl -X POST -H 'Authorization: Token YOURTOKENHERE' -d "autocompleteString=xxxx&format=simple" -i staging.getbellhops.com/api/v1/schoolsautocomplete/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-schoolautocomplete-list'),
        {
            'autocompleteString':'xxxx',
            'format':'simple',
        }
    )
```

```objective_c

```

```java
Coming Soon!
```

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/api-schoolautocomplete-list`

Parameter | Default | Description
--------- | ------- | -----------
autocompleteString | None | The start of the string that will be autocompleted.
format | "simple" | Determines how matching occurs. "simple" or "non-simple"

### Formatting: 
“Simple” returns all matching results in alphabetical order. 

“Non-Simple” returns all of results that start with the 
query string (in alphabetical order) followed by all results that don’t start with the query (in alphabetical order).
#### Simple Query w/ Autocomplete String 'bur':
1. Auburn
2. Burnsides
3. Burt Reynolds
4. Lesser Auburn (aka Alabama)

#### Non-Simple Query w/ Autocomplete String 'bur':
1. Burnsides
2. Burt Reynolds
3. Auburn
4. Lesser Auburn (aka Alabama)


## Student Organizations

```http
HTTP/1.0 200 OK
[  
   "Acm- Association For Computing Machinery",
   "Air Force Rotc, Arnold Air Society, Association For Computing Machinery",
   "Alpha Sigma Phi (Social), Alpha Kappa Psi (Business), Beta Alpha Psi (Finance And Accounting), Relay For Life, People'S Bank Case Competition",
    ...
]
```

```shell
curl -X POST -H 'Authorization: Token YOURTOKENHERE' -d "autocompleteString=xxxx&format=simple" -i staging.getbellhops.com/api/v1/studentorgsautocomplete/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-studentorgsautocomplete-list'),
        {
            'autocompleteString':'xxxx',
            'format':'simple',
        }
    )
```

```objective_c

```

```java
Coming Soon!
```

Parameter | Default | Description
--------- | ------- | -----------
autocompleteString | None | The start of the string that will be autocompleted.
format | "simple" | Determines how matching occurs. "simple" or "non-simple"

### Formatting: 
“Simple” returns all matching results in alphabetical order. 

“Non-Simple” returns all of results that start with the 
query string (in alphabetical order) followed by all results that don’t start with the query (in alphabetical order).

#### Simple Query w/ Autocomplete String 'bur':
1. Auburn
2. Burnsides
3. Burt Reynolds
4. Lesser Auburn (aka Alabama)

#### Non-Simple Query w/ Autocomplete String 'bur':
1. Burnsides
2. Burt Reynolds
3. Auburn
4. Lesser Auburn (aka Alabama)

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/api-studentorgsautocomplete-list`

## Majors

```http
HTTP/1.0 200 OK
[  
   "Actuarial Science / Comp Sci",
   "Applied Computing",
   "Biology & Computer Science",
   ...
]
```

```shell
curl -X POST -H 'Authorization: Token YOURTOKENHERE' -d "autocompleteString=xxxx&format=simple" -i staging.getbellhops.com/api/v1/majorsautocomplete/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-majorsautocomplete-list'),
        {
            'autocompleteString':'xxxx',
            'format':'simple',
        }
    )
```

```objective_c

```

```java
Coming Soon!
```

Parameter | Default | Description
--------- | ------- | -----------
autocompleteString | None | The start of the string that will be autocompleted.
format | "simple" | Determines how matching occurs. "simple" or "non-simple"

### Formatting: 
“Simple” returns all matching results in alphabetical order. 

“Non-Simple” returns all of results that start with the 
query string (in alphabetical order) followed by all results that don’t start with the query (in alphabetical order).

#### Simple Query w/ Autocomplete String 'bur':
1. Auburn
2. Burnsides
3. Burt Reynolds
4. Lesser Auburn (aka Alabama)

#### Non-Simple Query w/ Autocomplete String 'bur':
1. Burnsides
2. Burt Reynolds
3. Auburn
4. Lesser Auburn (aka Alabama)

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/api-majorsautocomplete-list`

## Bellhop Referrals
```http
HTTP/1.0 200 OK
[  
   {  
      "last":"B.",
      "school":"University of Iowa",
      "img_url":"/media/profiles/xxx.jpg",
      "id":"000",
      "first":"Matthew"
   },
   {  
      "school":"Samford University",
      "last":"B.",
      "id":"001",
      "first":"Jack"
   },
   ...
]
```

```shell
curl -X POST -H 'Authorization: Token YOURTOKENHERE' -d "autocompleteString=xxxx&format=simple" -i staging.getbellhops.com/api/v1/bellhopreferralsautocomplete/
```

```python
    from django.core.urlresolvers import reverse
    from rest_framework.test import APIClient
    user = User.objects.create_user(username='test@user.com', email='test@user.com', password='password')
    c = APIClient()
    c.credentials(HTTP_AUTHORIZATION='Token ' + user.auth_token.key)
    response = c.post(reverse('api-bellhopreferralsautocomplete-list'),
        {
            'autocompleteString':'xxxx',
            'format':'simple',
        }
    )
```

```objective_c

```

```java
Coming Soon!
```

Parameter | Default | Description
--------- | ------- | -----------
autocompleteString | None | The start of the string that will be autocompleted.
format | "simple" | Determines how matching occurs. "simple" or "non-simple"

### Formatting: 
“Simple” returns all matching results in alphabetical order. 

“Non-Simple” returns all of results that start with the 
query string (in alphabetical order) followed by all results that don’t start with the query (in alphabetical order).

#### Simple Query w/ Autocomplete String 'bur':
1. Auburn
2. Burnsides
3. Burt Reynolds
4. Lesser Auburn (aka Alabama)

#### Non-Simple Query w/ Autocomplete String 'bur':
1. Burnsides
2. Burt Reynolds
3. Auburn
4. Lesser Auburn (aka Alabama)

### HTTP Request
`GET http://staging.getbellhops.com/api/v1/api-bellhopreferralautocomplete-list`