This demo app is a REST API to manage transaction history of products.

(Deployed on Heroku: https://wp-backend-test.herokuapp.com)

## Installation

Install 'jq' with brew command.

```bash
brew install jq
```

## DEMO

You can try following commands to create or get records on this API.

### 1: Add a purchaser (POST)

```terminal
curl -H 'Content-Type:application/json' -d '{"name":"hoge"}' \
-X POST https://wp-backend-test.herokuapp.com/purchaser
```

### 2: Add a product (POST)

```terminal
curl -H 'Content-Type:application/json' -d '{"name":"hoge"}' \
-X POST https://wp-backend-test.herokuapp.com/product
```

### 3: Add a transaction (POST)

```terminal
curl -H 'Content-Type:application/json' \
-d '{ "purchaser_id": 4, "product_id": 34, "purchase_timestamp": 1553094444 }' \
-X POST https://wp-backend-test.herokuapp.com/purchaser_product
```

### 4: Check full transaction history of a purchaser (GET)

```terminal
curl 'https://wp-backend-test.herokuapp.com/purchaser/4/product' | jq .
```

### 5: Check transaction history of a purchaser during a period (GET)

```terminal
curl 'https://wp-backend-test.herokuapp.com/purchaser/4/product?start_date=2019-03-20&end_date=2020-11-11' | jq .
```

※ date range filtering by start date and end date parameters is optional.

#### sample response

```terminal
{
  "purchases": {
    "2019-03-20": [
      {
        "product": "Trumpet"
      },
      {
        "product": "Diamond"
      }
    ]
  }
}
```

## ER Diagram

<img width="865" alt="Screen Shot 2021-04-07 at 1 42 14" src="https://user-images.githubusercontent.com/74521093/113747952-e1641380-9742-11eb-829c-1ee79db566c7.png">

## Supplementary information

- Ruby 2.6.5
- Ruby on Rails 6.0.3.4
