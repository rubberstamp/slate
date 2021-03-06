# Internationalization

## Country and Regional Support


```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurementexpress.com/api/v1/endpoint',
  headers = {
    locale: 'es'
  }
)
```

```sh
curl https://app.procurementexpress.com/api/v1/endpoint'
  -H "locale: es"
```

> Send locale key in the Header params


We support Country specific languages

| Language   | Key          |
| ---------- | ----------   |
| English    | en (default) |
| Spanish    | es           |
| Slovak     | sk           |

We also support some regional languages

| Language   | Region     | Key   |
| ---------- | ---------- | ----  |
| Spanish    | Chile      | es-CL |
| Spanish    | Maxican    | es-MX |

## HTTP Request

`POST https://app.procurementexpress.com/api/v1/endpoint`

## Query Parameters

| Param  | Type   | Description                              |
| -----  | ---    | ---------                                |
| locale | header | locale key for required language support |

