---
title: Debtors
layout: default
---
### [Back to overview](index.html)
---
# Debtors API
This API endpoint let you manage your debtors. [Parameters](#available-parameters) can be found on the very end of this page.

## List all debtors
Get a list of all your debtors returned in `JSON` format.     
**GET** `https://app.mytourist.cloud/api/v1/debtors`

**Results**
```json
{
    "debtor_id":"23192010299",
    "company_name":null,
    "company_chamber_id":null,
    "first_name":"Max",
    "last_name":"Musterman",
    "address":"streetname 55 Block 3",
    "...":"..."
},
{
    "debtor_id":"23192010300",
    "company_name":null,
    "company_chamber_id":null,
    "first_name":"Daniel",
    "last_name":"Musterman",
    "address":"streetname 66",
    "...":"..."
}
```

## Retrieve a single debtor
Get a single Debtor returned in `JSON` format. We also add all the bookings attached to this debtor and also all invoices.

**GET** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`


**Results**
```json
{
    "debtor_id":"23192010299",
    "company_name":null,
    "company_chamber_id":null,
    "first_name":"Max",
    "last_name":"Musterman",
    "address":"streetname 55 Block 3",
    "...":"...",

    "bookings":[
        {
            "state":"archived",
            "unique":231920102956,
            "arrival":"20201008",
            "departure":"20201011"
        }
    ],
    "invoices":[
        {
            "state":"open",
            "type":"proforma",
            "unique":"P1120078"
        }
    ]
}
```

## Create / Update a debtor
You can create or update a debtor by posting to the following URL. This endpoints will return (when success) the saved debtor (200 HTTP response). You can either post the full JSON file or single individual fields. When the field is posted we always overwrite them. When a field is not posten trough the API we won't overwrite is and keep the existing data.

**POST (Create)** `https://app.mytourist.cloud/api/v1/debtors`   
**POST (Update)** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

### Available Parameters
<table>
    <tr><td>first_name</td><td>required</td><td>when creating debtor</td></tr>    
    <tr><td>last_name</td><td>required</td><td>when creating debtor</td></tr>
    <tr><td>company_name</td><td>optional</td><td>-</td></tr>
    <tr><td>company_chamber_id</td><td>optional</td><td>Chamber / KVK nr.</td></tr>
    <tr><td>vat_id</td><td>optional</td><td></td></tr>
    <tr><td>address</td><td>optional</td><td></td></tr>
    <tr><td>zipcode</td><td>optional</td><td></td></tr>
    <tr><td>city</td><td>optional</td><td></td></tr>
    <tr><td>country</td><td>optional</td><td>ISO 639-1</td></tr>
    <tr><td>phone</td><td>optional</td><td></td></tr>
    <tr><td>email</td><td>optional</td><td></td></tr>
    <tr><td>note</td><td>optional</td><td></td></tr>
</table>