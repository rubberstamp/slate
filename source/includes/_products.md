# Products

## Create a Product

```ruby
require 'rest-client'

RestClient.post(
  'https://app.procurementexpress.com/api/v1/products',
  {
    product: {
      description: '1 IPad Charging Station',
      sku: 'SKU-001',
      unit_price: 44.23,
      supplier_id: 1
    }
  },
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurementexpress.com/api/v1/products'
  -X POST
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
  -d "product[description]=1 IPad Charging Station"
  -d "product[sku]=SKU-001"
  -d "product[unit_price]=44.23"
  -d "product[supplier_id]=1"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "supplier_id": 1,
  "sku": "SKU-001",
  "description": "1 IPad Charging Station",
  "unit_price": "44.23",
  "currency_id": null,
  "archived": false
}
```

Create a new products and returns the `Product` object that is created.

### HTTP Request

`POST https://app.procurementexpress.com/api/v1/products`

### Query Parameters

| Params               | Type    | required | Description                      |
| -------------------- | ------- | -------- | -------------------------------- |
| authentication_token | header  | required | Authentication token             |
| app_company_id       | header  | required | Company ID                       |
| product[description] | string  | required | `Required` Product Description   |
| product[sku]         | string  | optional | Product Stock Keeping Unit (sku) |
| product[unit_price]  | decimal | optional | Product Unit Price               |
| product[supplier_id] | integer | optional | Supplier ID                      |

## Get all Products

```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurementexpress.com/api/v1/products',
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurementexpress.com/api/v1/products'
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
    "supplier_id": 1,
    "sku": "SKU-001",
    "description": "1 IPad Charging Station",
    "unit_price": "44.23",
    "currency_id": null,
    "archived": false
  },
  {
    "id": 2,
    "supplier_id": 1,
    "sku": "SKU-002",
    "description": "Macbook Air Retina",
    "unit_price": "1300",
    "currency_id": null,
    "archived": false
  }
]
```

Returns a list of your products.

### Filter products by supplier

you can pass `supplier_id` query params to filter products by supplier like:
`/api/v1/products?supplier_id=1`

### Filter archived products

If you want to filter archived products you can pass `archived` params like:
`/api/v1/products?archived=true`

### HTTP Request

`GET https://app.procurementexpress.com/api/v1/products`

### Query Parameters

| Params               | Type    | Description              |
| -------------------- | ------- | ------------------------ |
| authentication_token | header  | Authentication token     |
| app_company_id       | header  | Company ID               |
| supplier_id          | integer | filter by supplier       |
| archived             | boolean | filter archived products |

## Get Product details

```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurementexpress.com/api/v1/products/1',
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurementexpress.com/api/v1/products/1'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "supplier_id": 1,
  "sku": "SKU-001",
  "description": "1 IPad Charging Station",
  "unit_price": "44.23",
  "currency_id": null,
  "archived": false
}
```

Retrieves the details of an existing products. You need to supply the unique
product id, that was returned upon product creation.

### HTTP Request

`GET https://app.procurementexpress.com/api/v1/products/:id`

### URL Parameters

| Params               | Type    | Description          |
| -------------------- | ------- | -------------------- |
| authentication_token | header  | Authentication token |
| app_company_id       | header  | Company ID           |
| ID                   | integer | Product ID           |

## Update Product

```ruby
require 'rest-client'

RestClient.put(
  'https://app.procurementexpress.com/api/v1/products/1',
  {
    product: {
      description: 'updated'
    }
  },
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurementexpress.com/api/v1/products/1'
  -X PUT
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
  -d "product[description]=updated"
```

> the above command returns JSON structured like this:

```json
{
  "id": 1,
  "supplier_id": 1,
  "sku": "SKU-001",
  "description": "updated",
  "unit_price": "44.23",
  "currency_id": null,
  "archived": false
}
```

Update the specified department by setting the value of parameters passed.
Any parameters not provided will be left unchanged.

### HTTP Request

`PUT https://app.procurementexpress.com/api/v1/products/:id`

### Query Parameters

| Params               | Type    | Description                      |
| -------------------- | ------- | -------------------------------- |
| authentication_token | header  | Authentication token             |
| app_company_id       | header  | Company ID                       |
| ID                   | integer | Product ID                       |
| product[description] | string  | `Required` Product Description   |
| product[sku]         | string  | Product Stock Keeping Unit (sku) |
| product[unit_price]  | decimal | Product Unit Price               |
| product[supplier_id] | integer | Supplier ID                      |

## Get SKUS

```ruby
require 'rest-client'

RestClient.get(
  'https://app.procurementexpress.com/api/v1/products/skus',
  headers = {
    authentication_token: 'your token',
    app_company_id: 1
  }
)
```

```shell
curl 'https://app.procurementexpress.com/api/v1/products/skus'
  -X GET
  -H "Content-Type: application/json"
  -H "authentication_token: your token"
  -H "app_company_id: 1"
```

> The above command returns JSON structured like this:

```json
["SKU-001", "SKU-002"]
```

Returns a list of your products's SKUs.

### Filter skus by supplier

you can pass `supplier_id` query params to filter skus by supplier like:
`/api/v1/products/skus?supplier_id=1`

### Filter skus by keyword

To filter sku list based on user input keyword, you can pass `query` params in URL like:

`/api/v1/products/skus?query=SKU`

### Filter archived skus

If you want to filter archived skus you can pass `archived` params like:
`/api/v1/products/skus?archived=true`

### HTTP Request

`GET https://app.procurementexpress.com/api/v1/products/skus`

### Query Parameters

| Params               | Type    | Description              |
| -------------------- | ------- | ------------------------ |
| authentication_token | header  | Authentication token     |
| app_company_id       | header  | Company ID               |
| supplier_id          | integer | filter by supplier       |
| archived             | boolean | filter archived products |
