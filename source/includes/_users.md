# Users


## Register

```shell
curl 'https://app.rubberstamp.io/api/v1/register'
  -X POST
  -H "Content-Type: application/json"
  -d "email=api@example.com"
  -d "password=pass1234"
  -d "password_confirmation=pass1234"
  -d "name=Api user"
  -d "phone_number=98xxxxxxxx"
```

```ruby
require 'rest-client'

response = RestClient.post(
  'https://app.rubberstamp.io/api/v1/register',
  {
    email: 'api@example.com',
    password: 'pass1234',
    password_confirmation: 'pass1234',
    name: 'Api user',
    phone_number: '98xxxxxx'
  }
)

response.body
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "email": "api@example.com",
  "name": "Api user",
  "phone_number": "98xxxxxxxx",
  "setup_incomplete": true,
  "employer_id": null,
  "authentication_token": "t0k3n",
  "approval_limit": 1000000,
  "companies": null
}
```

This endpoint will register you as a rubberstamp user, send confirmation link
to your email and you can confirm it. It will returns `User` object along
with `authentication_token`.

### HTTP Request

`POST https://app.rubberstamp.io/api/v1/register`

### Query Parameters

| Param                 | Type    | Description                   |
| ---------             | ------- | -----------                   |
| email                 | string  | Your registered email address |
| password              | string  | strong password               |
| password_confirmation | string  | password confirmation         |
| name                  | string  | Your First Name and Last Name |
| phone_number          | string  | Phone number                  |





## Login

```ruby
require 'rest-client'

response = RestClient.post(
  'https://app.rubberstamp.io/api/v1/login',
  {
    email: 'api@example.com',
    password: 'pass1234'
  }
)

response.body
```

```shell
curl 'https://app.rubberstamp.io/api/v1/login'
  -X POST
  -H "Content-Type: application/json"
  -d "email=api@example.com"
  -d "password=pass1234"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "email": "api@example.com",
  "name": "Api user",
  "phone_number": "98xxxxxxxx",
  "setup_incomplete": false,
  "employer_id": 1,
  "authentication_token": "t0k3n",
  "approval_limit": 0,
  "companies": [
    {
      "id": 1,
      "name": "My Demo Company"
    }
  ]
}
```

This endpoint returns `User` object along with `authentication_token`.

RubberStamp expects for the Authentication token to be included in all API
requests to the server in a header.


### HTTP Request

`POST https://app.rubberstamp.io/api/v1/login[.json]`

### Query Parameters

| Param     | Type    | Description                   |
| --------- | ------- | -----------                   |
| email     | string  | Your registered email address |
| password  | string  | strong password               |

<aside class="success">
Remember — You need to be a valid user to get authenticated. If you haven't
registered yet, try register api.
</aside>




## GET Current User

```ruby
require 'rest-client'

response = RestClient.get(
  'https://app.rubberstamp.io/api/v1/currentuser',
  headers = {
    authentication_token: 'your token',
    app_company_id: '1'
  }
)

response.body
```

```shell
curl 'https://app.rubberstamp.io/api/v1/currentuser'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "email": "api@example.com",
  "name": "Api user",
  "phone_number": "98xxxxxxxx",
  "setup_incomplete": false,
  "employer_id": 1,
  "authentication_token": "t0k3n",
  "approval_limit": 0,
  "companies": [
    {
      "id": 1,
      "name": "My Demo Company"
    }
  ]
}
```

Retrieves the details of current logged in user. You need to supply the user's
authentication token and company id as a header params.

### HTTP Request

`GET https://app.rubberstamp.io/api/v1/currentuser`

### URL Parameters

| Params               | Type    | Description                      |
| -----                | -----   | ---------                        |
| authentication_token | header  | Authentication token             |
| app_company_id       | header  | registered company id            |






## Update User

```ruby
require 'rest-client'

RestClient.put(
  'https://app.rubberstamp.io/api/v1/currentuser',
  {
    email: 'john@example.com',
    password: 'password',
    name: 'John Doe',
    phone_number: '98xxxxxxxx'
  },
  headers = { authentication_token: 'your token', }
)
```

```shell
curl https://app.rubberstamp.io/api/v1/currentuser
  -X PUT
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
  -d "email=john@example.com"
  -d "password=password"
  -d "name=John Doe"
  -d "phone_number=98xxxxxxxx"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "email": "john@example.com",
  "name": "John Doe",
  "phone_number": "98xxxxxxxx",
  "setup_incomplete": false,
  "employer_id": 1,
  "authentication_token": "newt0k3n",
  "approval_limit": 0,
  "companies": [
    {
      "id": 1,
      "name": "My Demo Company"
    }
  ]
}
```

Update current logged in user setting the value of parameters passed. Any
parameters not provided will be left unchanged.

### HTTP Request

`PUT https://app.rubberstamp.io/api/v1/currentuser`

### Query Parameters

| Param                | Type   | Description              |
| -----                | ---    | ---------                |
| authentication_token | header | Authentication token     |
| app_company_id       | header | registered company id    |
| email                | string | email                    |
| password             | string | strong password          |
| name                 | string | Your First and Last name |
| phone_number         | string | Phone number             |





## Reset Password

```shell
curl 'https://app.rubberstamp.io/api/v1/reset_password'
  -X POST
  -H "Content-Type: application/json"
  -d "email=api@example.com"
```

```ruby
require 'rest-client'

response = RestClient.post(
  'https://app.rubberstamp.io/api/v1/reset_password',
  { email: 'api@example.com' }
)
```

> The above command returns JSON structured like this:

```json
{
  "success": "true"
}
```

Sends password reset instructions in your email inbox. You need to pass your
valid email address as a parameter. After you get the password reset instruction
in your inbox, you can click on the link which will redirect you to the password
reset page and you can reset your password from there.

### HTTP Request

`POST https://app.rubberstamp.io/api/v1/reset_password`

### Query Parameters

| Param                 | Type    | Description                   |
| ---------             | ------- | -----------                   |
| email                 | string  | Your registered email address |




## Google Login

```shell
curl 'https://app.rubberstamp.io/api/v1/google_login'
  -X POST
  -H "Content-Type: application/json"
  -d "email=api@example.com"
```

```ruby
require 'rest-client'

response = RestClient.post(
  'https://app.rubberstamp.io/api/v1/google_login',
  { email: 'api@example.com' }
)
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "email": "api@example.com",
  "name": "Api user",
  "phone_number": "98xxxxxxxx",
  "setup_incomplete": false,
  "employer_id": 1,
  "authentication_token": "t0k3n",
  "approval_limit": 0,
  "companies": [
    {
      "id": 1,
      "name": "My Demo Company"
    }
  ]
}
```
It will return `User` object back with the matching email address.

### HTTP Request

`POST https://app.rubberstamp.io/api/v1/google_login`

### Query Parameters

| Param                 | Type    | Description                   |
| ---------             | ------- | -----------                   |
| email                 | string  | Your registered email address |




## Get My Currencies

```ruby
require 'rest-client'

response = RestClient.get(
  'https://app.rubberstamp.io/api/v1/currencies',
  headers = {
    authentication_token: 'your token',
    app_company_id: '1'
  }
)
```

```shell
curl 'https://app.rubberstamp.io/api/v1/currencies'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "iso_code": "EUR",
    "iso_numeric": "978",
    "name": "Euro",
    "symbol": "€"
  },
  {
    "id": 2,
    "iso_code": "GBP",
    "iso_numeric": "826",
    "name": "British Pound",
    "symbol": "£"
  },
  ...
]
```

Returns a list of currencies that are enabled for given company id.

### HTTP Request

`GET https://app.rubberstamp.io/api/v1/currencies`

### Query Parameters

| Param                | Type   | Description           |
| -----                | ---    | ---------             |
| authentication_token | header | Authentication token  |
| app_company_id       | header | registered company id |




## Get All Currencies

```ruby
require 'rest-client'

response = RestClient.get(
  'https://app.rubberstamp.io/api/v1/all_currencies',
  headers = {
    authentication_token: 'your token',
  }
)
```

```shell
curl 'https://app.rubberstamp.io/api/v1/all_currencies'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 8,
    "iso_code": "AFN",
    "iso_numeric": "971",
    "name": "Afghan Afghani",
    "symbol": "؋"
  },
  {
    "id": 9,
    "iso_code": "ALL",
    "iso_numeric": "008",
    "name": "Albanian Lek",
    "symbol": "L"
  },
  {
    "id": 45,
    "iso_code": "DZD",
    "iso_numeric": "012",
    "name": "Algerian Dinar",
    "symbol": "د.ج"
  },
  {
    "id": 12,
    "iso_code": "AOA",
    "iso_numeric": "973",
    "name": "Angolan Kwanza",
    "symbol": "Kz"
  },
  {
    "id": 13,
    "iso_code": "ARS",
    "iso_numeric": "032",
    "name": "Argentine Peso",
    "symbol": "$"
  },
  {
    "id": 10,
    "iso_code": "AMD",
    "iso_numeric": "051",
    "name": "Armenian Dram",
    "symbol": "դր."
  },
  {
    "id": 14,
    "iso_code": "AWG",
    "iso_numeric": "533",
    "name": "Aruban Florin",
    "symbol": "ƒ"
  },
  {
    "id": 5,
    "iso_code": "AUD",
    "iso_numeric": "036",
    "name": "Australian Dollar",
    "symbol": "$"
  },
  ...
]
```

Returns a list of all available currencies.

### HTTP Request

`GET https://app.rubberstamp.io/api/v1/all_currencies`

### Query Parameters

| Param                | Type   | Description           |
| -----                | ---    | ---------             |
| authentication_token | header | Authentication token  |





## Logout

```ruby
require 'rest-client'

RestClient.post(
  'https://app.rubberstamp.io/api/v1/logout',
  headers = {
    authentication_token: 'your token'
  }
)
```

```shell
curl https://app.rubberstamp.io/api/v1/logout
  -X POST
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "info": "Logged out"
}
```

Logout user and set authentication_token to nil. If you want new
authentication_token you need to login again.

### HTTP Request

`POST https://app.rubberstamp.io/api/v1/logout`

### Query Parameters

| Param                | Type   | Description          |
| ----                 | ----   | ---------            |
| authentication_token | header | Authentication token |
