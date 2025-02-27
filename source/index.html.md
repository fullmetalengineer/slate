---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby

toc_footers:
  #- <a href='#'>Sign Up for a Developer Key</a>
  #- <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Hodlit API docs!

We have language bindings in Shell (using curl requests) and Ruby code! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# General Information

The API base url is `https://hodlit.herokuapp.com`.

The API is structured into versions. For now, there is only `/api/v1/`.

For example, the URL to login using the above base url and api structure would be:
`https://hodlit.herokuapp.com/api/v1/users/login`.

# Authentication

> The Authorization scheme requires a header like this:

```ruby
TBD
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Bearer tokentokentoken"
```

> Make sure to replace `tokentokentoken` with your API key.

Hodlit uses a Bearer authorization scheme. Once a user has successfully logged in (or registered), their token is returned on the user object and should be used for all API requests going forward.

Hodlit expects for the Authorization header to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer tokentokentoken`

<aside class="notice">
You must replace <code>tokentokentoken</code> with the user's access token.
</aside>

`api/v1/users/login` and `api/v1/users/signup` are the only two endpoints that do not require an Authorization header with the associated token.

# Users

## Signup

```ruby
TBD
```

```shell
curl -X "POST" "https://hodlit.herokuapp.com/api/v1/users/signup" \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
  "email": "my_user@gmail.com",
  "phone": "5738675309",
  "password": "MySuperSecurePassword",
  "password_confirmation": "MySuperSecurePassword"
}'

```

> The above command returns JSON structured somewhat like this:

```json
{
  "id": 2,
  "first_name": null,
  "last_name": null,
  "token": "55781790684dc700742bb278056f33a0a00c9f2b",
  "email": "my_user@gmail.com",
  "phone": "5738675309",
  "address_line_1": null,
  "address_line_2": null,
  "city": null,
  "state": null,
  "zip_code": null,
  "accepted_round_up": null,
  "accepted_crypto_liability": null,
  "accepted_terms": null,
  "accepted_fees": null
}
```

This endpoint signs the user up for the service and logs them in (notice the filled-out token). Note that if the signup fails for any reason, the user will not have been created nor will they be logged into Hodlit.

### HTTP Request

`POST https://hodlit.herokuapp.com/api/v1/users/signup`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | | Must be a valid email and unique within Hodlit.
phone | | Must be a valid phone number (no formatting, numbers only) and unique within Hodlit.
password | |
password_confirmation | | Password confirmation must match the password

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
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
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

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
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
