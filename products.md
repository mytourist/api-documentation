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

**GET** `https://app.mytourist.cloud/api/v1/products`

**Example result**
```json
[
    {
        "id":"23192011031",
        "category":{
            "id":"23192010291",
            "name":"Rental",
            "color":"#55BB5A"
        }
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
        "category":{
            "id":"23192010292",
            "name":"General",
            "color":"#55BB5A"
        }
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

## Retrieve a single product
Same type of results as the list function above, only this endpoint will return only the Product you just requested.

**GET** `https://app.mytourist.cloud/api/v1/products/{PRODUCT_ID}`

## Create a product
For products we always advise to fill the content variables with the language of your Invoices. So that the products displayed on your Invoices not printing the automatically translated information. For a list of [Available form parameters](#available-from-parameters) see bottom of this page.

*Automatically translations for the `name` and `description` fields will be generated after 30 minutes of your last change*

**POST** `https://app.mytourist.cloud/api/v1/products`

## Update a product
The update function is exactly the same as above. The only difference is that no fields are required. Only the fields you push to us will be changed (even empty ones). All other fields will be ignored. For a list of [Available form parameters](#available-from-parameters) see bottom of this page.

*Automatically translations for the `name` and `description` fields will be generated after 30 minutes of your last change*

**POST** `https://app.mytourist.cloud/api/v1/products/{DEBTOR_ID}`

## Remove a product
This has no effect on your proforma invoices. When you want to delete those products also from your proforma invoices you'll need to remove those product lines. See [Invoices API](invoices.html) documentation for more information about invoice product lines.

**DELETE** `https://app.mytourist.cloud/api/v1/products`

# Available form parameters
The `calculation_methods` provide you with the possibility to automatically calculate the price per night or/and nights .. when the product is added to your invoice it will calculate the price based on those two items. But is always optional.

The `auto_add_when_booked_on_roomtypes` becomes handy when you want to add this product automatically to the booking Invoice. Mostly used with final cleaning purposes.

<table>
    <tr><td>language</td><td>required*</td><td>iso</td><td>nl, de, fr or en</td></tr>    
    <tr><td>name</td><td>required*</td><td>string</td><td>In the language you set</td></tr>    
    <tr><td>description</td><td>required*</td><td>string</td><td>In the language you set</td></tr>    
    <tr><td>price</td><td>required*</td><td>float</td><td>Per piece</td></tr>    
    <tr><td>category_id</td><td>required*</td><td>integer</td><td>@category_id <a href="#">ProductCategories API</a></td></tr>    
    <tr><td>calculation_methods</td><td>optional</td><td>string</td><td>Pick: person or/and night (devided by comma)</td></tr>    
    <tr><td>tax_id</td><td>optional</td><td>integer</td><td>@tax_id <a href="#">TaxRates API</a></td></tr>    
</table>
<table>
    <tr><td>auto_add_when_booked_on_roomtypes</td><td>optional</td><td>string</td><td>@roomtype_id's devided by a comma <a href="#">Roomtypes API</a></td></tr>    
</table>

\* required when creating a product.