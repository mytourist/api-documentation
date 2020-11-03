---
title: Product Categories
layout: default
---
### [Back to overview](index.html#api-endpoints)
---
# Product Categories
This endpoint makes it possible to list, create, update and delete your product categories. 

**Index:** 
- [List all product categories](#list-all-product-categories)
- [Create or update a product category](#create-or-update-a-product-category)
- [Remove a product category](#remove-a-product-category)
- [Available form parameters](#available-form-parameters)

## List all product
Get a list of all your product returned in `JSON` format. The first item of your output is always the default category marked as `locked`. You cannot update this default category. All other categories are freely changeable.

**GET** `https://app.mytourist.cloud/api/v1/product-categories`

**Output Example**
```json
[
    {
        "id":"23192010291",
        "name":null,
        "color":"55BB5A",
        "locked":true,
        "created_at":"2020-10-29 13:58:07",
        "updated_at":"2020-10-29 13:58:07"
    },
    {
        "id":"23192011032",
        "name":"Bike rental",
        "color":"e44a7c",
        "locked":false,
        "created_at":"2020-11-03 15:11:41",
        "updated_at":"2020-11-03 15:11:41"
    }
]
```

## Create or Update a product category
You can easily create a product category by posting to the following URL. The naming of this product category is for internal purposes only and won't be showed to your customers. You can also add a HEX color of your choice.

**POST (Create)** `https://app.mytourist.cloud/api/v1/product-categories`   
**POST (Update)** `https://app.mytourist.cloud/api/v1/product-categories/{CATEGORY_ID}`

## Remove a product category
When you remove a product category all products inside will be moved into the `locked` default category.

**DELETE** `https://app.mytourist.cloud/api/v1/product-categories/{CATEGORY_ID}`   

## Available form parameters
<table>
    <tr><td>name</td><td>required on create</td><td>string</td></tr>    
    <tr><td>color</td><td>optional</td><td>string: hex color</td></tr>    
</table>

