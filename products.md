---
title: Products
layout: default
---
### [Back to overview](index.html#start-developing-testing-and-deploy)
---
# Products API
This API endpoint let you manage your products.    

**Index:** 
- [List all products](#list-all-products)
- [Retrieve a single product](#retrieve-a-single-product)
- [Create / Update a product](#create--update-a-product)

## List all product
Get a list of all your product returned in `JSON` format.

**GET** `https://app.mytourist.cloud/api/v1/product`

**Example result**
```json
[
    {
        "id":"23192011031",
        "category_id":"23192010291",
        "tax_id":"23192011034",
        "language":"nl",
        "price":14.00,
        "name":"Bike Rental",
        "description":"Electric bike.",
        "calculation_methods":[
            "person",
            "night"
        ],
        "auto_add_when_booked_on_roomtypes":[]
    },
    {
        "id":"23192011032",
        "category_id":"23192010291",
        "tax_id":"23192011034",
        "language":"nl",
        "price":60.00,
        "name":"Final cleaning",
        "description":"Each booker has to pay this amount as final cleaning service.",
        "calculation_methods":[],
        "auto_add_when_booked_on_roomtypes":[
            {
                "id":"23192010281",
                "name":"Tweepersoonskamer met balkon"
            },
            {
                "id":"23192010282",
                "name":"6 Pers. appartement"
            }
        ]
    }
]
```
