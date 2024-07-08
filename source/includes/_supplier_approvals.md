# Supplier Approvals

## Get All Supplier Approvals

```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurementexpress.com/api/v1/supplier_approvals',
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurementexpress.com/api/v1/supplier_approvals'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
```

> The above command returns JSON structured like this

```json
{
    "supplier_approvals": [
        {
            "id": 37,
            "name": "YouDesks",
            "notes": "",
            "phone_number": "",
            "address": "",
            "email": "",
            "status": "approved",
            "requester": {
                "id": 32197,
                "email": "member@procurementexpress.com",
                "name": "Requester User",
                "roles": [
                    "companyadmin",
                    "approver",
                    "finance",
                    "teammember"
                ]
            },
            "approver": {
                "id": 32197,
                "email": "finance@procurementexpress.com",
                "name": "Approver User",
                "roles": [
                    "companyadmin",
                    "approver",
                    "finance",
                    "teammember"
                ]
            },
            "created_at": 1559220513,
            "updated_at": 1592925602
        }
    ]
}
```

This API endpoint returns list of supplier requests that are either `pending`, `approved` or `rejected`. Please note that this list can be different from actual Supplier list.

**Requester**: contains the user information like id, email, name, roles, etc of the requester user.

**Approver**:  contains the user information like id, email, name, roles, etc of the approver user.

**created_at**: is the date in unix timestamp and used to find out when the supplier request was created by requester.

**updated_at**: is the date when the supplier request was last updated. We don't store specific approval date in our db, so you can use `updated_at` as a approval date.

### Feature Flag (enable_supplier_approval_api_access)

Feature flag must be enabled to access this API endpoint otherwise it will return error response.

```json
{
    "error": "Please enable supplier approval setting from your company setting, Supplier tab.",
    "status": 400
}
```

### Supplier approval is disabled in company setting

If the supplier approval company setting is disabled it will return error response.

```json
{
    "error": "Please contact support/success team to enable supplier approval.",
    "status": 400
}
```

### Pagination

You can paginate records by passing `page` params, example:
`/api/v1/supplier_approvals?page=2`. If you enable pagination, the output will include
`meta` object which contains information like `current_page`, `next_page`,
`previous_page`, `total_pages` and `total_count`. You can use these information
to write your own pagination logic.

### Search by name, email or phone number

I’m 
You can paginate records by passing `page` params, example:
`/api/v1/supplier_approvals?page=2`. If you enable pagination, the output will include
`meta` object which contains information like `current_page`, `next_page`,
`previous_page`, `total_pages` and `total_count`. You can use these information
to write your own pagination logic.

### Search by name, email or phone number

You can pass `/api/v1/supplier_approvals?search=supplier+name` as an additional query params to search for supplier matching name or email or phone number of supplier request.

### HTTP Request

`GET https://app.procurementexpress.com/api/v1/supplier_approvals`

### Query Parameters

| Params               | Type    | Description                                    |
| -------------------- | ------- | ---------------------------------------------- |
| authentication_token | header  | Authentication token                           |
| app_company_id       | header  | Company ID                                     |
| page                 | integer | Page number to paginate                        |
| search               | string  | Search supplier approval request by name, email or phone                        |
