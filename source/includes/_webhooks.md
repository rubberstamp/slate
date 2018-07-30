# Webhooks

## Create a Webhook

```ruby
require 'rest-client'

RestClient.post(
  'https://app.procurmentexpress.com/api/v1/webhooks',
  {
    webhook: {
      name: 'My Awesome App',
      url: 'https://myawesomeapp.com/webhook_handler',
      archived: false,
      event_type: [
        "new_po",
        "po_approved",
        "po_delivered",
        "po_paid"
      ],
      json_wrapper: "text",
      send_as_text: false,
      basic_auth_uname: 'myawesomeapp',
      basic_auth_pword: 'securepassw0rd',
      webhook_attributes_attributes: [
        {
          attrib_type: 'root',
          key: 'name',
          value: 'geek'
        },
        {
          attrib_type: 'root',
          key: 'org',
          value: 'My awesome co.'
        },
        {
          attrib_type: 'header',
          key: 'authentication_header',
          value: 'auth-header-goes-here'
        }
      ]
    }
  },
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurmentexpress.com/api/v1/webhooks'
  -X POST
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
  -d "webhook[name]=My Awesome App"
  -d "webhook[url]=https://myawesomeapp.com/webhook_handler"
  -d "webhook[archived]=false"
  -d "webhook[event_type][]=new_po"
  -d "webhook[event_type][]=po_approved"
  -d "webhook[event_type][]=po_delivered"
  -d "webhook[event_type][]=po_paid"
  -d "webhook[json_wrapper]=text"
  -d "webhook[send_as_text]=false"
  -d "webhook[basic_auth_uname]=myawesomeapp"
  -d "webhook[basic_auth_pword]=securepassw0rd"
  -d "webhook[webhook_attributes_attributes][][attrib_type]=root"
  -d "webhook[webhook_attributes_attributes][][key]=name"
  -d "webhook[webhook_attributes_attributes][][value]=geek"
  -d "webhook[webhook_attributes_attributes][][attrib_type]=root"
  -d "webhook[webhook_attributes_attributes][][key]=org"
  -d "webhook[webhook_attributes_attributes][][value]=My awesome co."
  -d "webhook[webhook_attributes_attributes][][attrib_type]=header"
  -d "webhook[webhook_attributes_attributes][][key]=authentication_header"
  -d "webhook[webhook_attributes_attributes][][value]=auth-header-goes-here"
```

> The above command returns JSOn structured like this:

```json
{
  "id": 1,
  "name": "My Awesome App",
  "url": "https://myawesomeapp.com/webhook_handler",
  "archived": false,
  "event_type": [
    "new_po",
    "po_approved",
    "po_delivered",
    "po_paid"
  ],
  "json_wrapper": "text",
  "send_as_text": false,
  "basic_auth_uname": "rubberstamp",
  "basic_auth_pword": "rsrules",
  "webhook_attributes_attributes": [{
    "attrib_type": "root",
    "key": "name",
    "value": "geek"
  },
  {
    "attrib_type": "root",
    "key": "org",
    "value": "My awesome co."
  },
  {
    "attrib_type": "header",
    "key": "authentication_header",
    "value": "auth-header-goes-here"
  }]
}
```

Create a new Webhooks and returns the Webhook object that is created.

### HTTP Request

`POST https://app.procurmentexpress.com/api/v1/webhooks`

### Query Parameters

| Params                                               | Type       | Description                                                                                                                                                                          |
| ----------                                           | ---------- | ----------                                                                                                                                                                           |
| authentication_token                                 | header     | Authentication Token                                                                                                                                                                 |
| app_company_id                                       | header     | Company ID                                                                                                                                                                           |
| webhook[name]                                        | string     | Name your webhook                                                                                                                                                                    |
| webhook[url]                                         | string     | Your production URL that will handle webhook request                                                                                                                                 |
| webhook[archived]                                    | boolean    | `true` if you want to archive otherwise `false`                                                                                                                                      |
| webhook[event_type]                                  | array[]    | Event type that you want to trigger when they happen in Rubberstamp. <br/> Supported values are: <br /> - `new_po` <br /> - `po_approved` <br /> - `po_delivered` <br /> - `po_paid` |
| webhook[json_wrapper]                                | string     | Root key that will wrap your json data                                                                                                                                               |
| webhook[send_as_text]                                | boolean    | `true` if you want to send as plain text, otherwise `false`                                                                                                                          |
| webhook[basic_auth_uname]                            | string     | Basic Authorization username                                                                                                                                                         |
| webhook[basic_auth_pword]                            | string     | Basic Authorization password                                                                                                                                                         |
| webhook[webhook_attributes_attribute][][attrib_type] | string     | Webhook Nested attributes type                                                                                                                                                       |
| webhook[webhook_attributes_attribute][][key]         | string     | Webhook Nested attributes key                                                                                                                                                        |
| webhook[webhook_attributes_attribute][][value]       | string     | Webhook Nested attributes value                                                                                                                                                      |





## Get All Webhooks

```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurmentexpress.com/api/v1/webhooks',
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurmentexpress.com/api/v1/webhooks'
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
    "name": "My Awesome App",
    "url": "https://myawesomeapp.com/webhook_handler",
    "archived": false,
    "event_type": [
      "new_po",
      "po_approved",
      "po_delivered",
      "po_paid"
    ],
    "tested": true,
    "response_code": null,
    "json_wrapper": "text"
  },
  {
      "id": 2,
      "name": "Slack Events",
      "url": "https://hooks.slack.com/services/...",
      "archived": false,
      "event_type": [
          "new_po",
          "po_approved",
          "po_delivered",
          "po_paid"
      ],
      "tested": false,
      "response_code": null,
      "json_wrapper": "text"
  }
]
```

Returns a list of webhooks that are not `archived`.

### Filter by archived

Default result will only provide webhooks that are not already archived.
If you want to get the list of webhooks that are archived then you can pass
`archived=true` params e.g: `https://app.procurmentexpress.com/api/v1/webhooks?archived=true`

### HTTP Request

`GET https://app.procurmentexpress.com/api/v1/webhooks`

### Query Parameters

| Params               | Type       | Description          |
| ----------           | ---------- | ----------           |
| authentication_token | header     | Authentication token |
| app_company_id       | header     | Company ID           |




## Get a specific Webhook

```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurmentexpress.com/api/v1/webhooks/1',
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurmentexpress.com/api/v1/webhooks/1'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "name": "My Awesome App",
  "url": "https://myawesomeapp.com/webhook_handler",
  "archived": false,
  "event_type": [
    "new_po",
    "po_approved",
    "po_delivered",
    "po_paid"
  ],
  "tested": true,
  "response_code": null,
  "json_wrapper": "text"
}
```

Retrieves the details of an existing webhooks. You need to supply the unique
Webhook id that was returned upon budget creation.

### HTTP Request

`GET https://app.procurmentexpress.com/api/v1/webhooks/:id`

### URL Parameters

| Params               | Type       | Description          |
| ----------           | ---------- | ---------------      |
| authentication_token | header     | Authentication Token |
| app_company_id       | header     | Company ID           |
| ID                   | integer    | Webhook ID           |




## Update a Webhook

```ruby
require 'rest-client'

RestClient.put(
  'https://app.procurmentexpress.com/api/v1/webhooks/1',
  {
    webhook: {
      name: 'My Awesome App name updated',
      event_type: [
        "new_po",
        "po_approved"
      ],
    }
  },
  headers = {
    authenticaiton_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurmentexpress.com/api/v1/webhooks/1'
  -X PUT
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
  -d "webhook[name]=My Awesome App name updated"
  -d "webhook[event_type][]=new_po"
  -d "webhook[event_type][]=po_approved"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "name": "My Awesome App name updated",
  "url": "https://myawesomeapp.com/webhook_handler",
  "archived": false,
  "event_type": [
    "new_po",
    "po_approved"
  ],
  "json_wrapper": "text",
  "send_as_text": false,
  "basic_auth_uname": "rubberstamp",
  "basic_auth_pword": "rsrules",
  "webhook_attributes_attributes": [{
    "attrib_type": "root",
    "key": "name",
    "value": "geek"
  },
  {
    "attrib_type": "root",
    "key": "org",
    "value": "My awesome co."
  },
  {
    "attrib_type": "header",
    "key": "authentication_header",
    "value": "auth-header-goes-here"
  }]
}
```

Update the specified `Webhook` by setting the value of parameters passed. Any
parameters not provided will be left unchanged.

### HTTP Request

`PUT https://app.procurmentexpress.com/api/v1/webhooks/:id`

### Query Parameters

| Params                                               | Type       | Description                                                                                                                                                                          |
| ----------                                           | ---------- | ---------------                                                                                                                                                                      |
| authentication_token                                 | header     | Authentication token                                                                                                                                                                 |
| app_company_id                                       | header     | Company ID                                                                                                                                                                           |
| ID                                                   | integer    | Webhook ID                                                                                                                                                                           |
| webhook[name]                                        | string     | Name your webhook                                                                                                                                                                    |
| webhook[url]                                         | string     | Your production URL that will handle webhook request                                                                                                                                 |
| webhook[archived]                                    | boolean    | `true` if you want to archive otherwise `false`                                                                                                                                      |
| webhook[event_type]                                  | array[]    | Event type that you want to trigger when they happen in Rubberstamp. <br/> Supported values are: <br /> - `new_po` <br /> - `po_approved` <br /> - `po_delivered` <br /> - `po_paid` |
| webhook[json_wrapper]                                | string     | Root key that will wrap your json data                                                                                                                                               |
| webhook[send_as_text]                                | boolean    | `true` if you want to send as plain text, otherwise `false`                                                                                                                          |
| webhook[basic_auth_uname]                            | string     | Basic Authorization username                                                                                                                                                         |
| webhook[basic_auth_pword]                            | string     | Basic Authorization password                                                                                                                                                         |
| webhook[webhook_attributes_attribute][][attrib_type] | string     | Webhook Nested attributes type                                                                                                                                                       |
| webhook[webhook_attributes_attribute][][key]         | string     | Webhook Nested attributes key                                                                                                                                                        |
| webhook[webhook_attributes_attribute][][value]       | string     | Webhook Nested attributes value                                                                                                                                                      |

