---
title: Debtors
layout: default
---
### [Back to overview](index.html#start-developing-testing-and-deploy)
---
# Debtors
This API endpoint let you manage your debtors. [Parameters](#available-parameters) can be found on the very end of this page.

**Index:** 
- [List all debtors](#list-all-debtors)
- [Retrieve a single debtor](#retrieve-a-single-debtor)
- [Search debtors](#search-debtors)
- [Create / Update a debtor](#create--update-a-debtor)

## List all debtors
Get a list of all your debtors returned in `JSON` format.     
**GET** `https://app.mytourist.cloud/api/v1/debtors`

**Results**
```json
{
    "id":"23192010299",
    "company_name":null,
    "company_chamber_id":null,
    "first_name":"Max",
    "last_name":"Musterman",
    "address":"streetname 55 Block 3",
    "latitude" : "27.606888", 
    "longitude" : "-42.670898", 
    "...":"..."
},
{
    "id":"23192010300",
    "company_name":null,
    "company_chamber_id":null,
    "first_name":"Daniel",
    "last_name":"Musterman",
    "address":"streetname 66",
    "latitude" : "27.606888", 
    "longitude" : "-42.670898", 
    "...":"..."
}
```

## Retrieve a single debtor
Get a single Debtor returned in `JSON` format. We also add all the bookings attached to this debtor and also all invoices.

**GET** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`


**Results**
```json
{
    "id":"23192010299",
    "company_name":null,
    "company_chamber_id":null,
    "first_name":"Max",
    "last_name":"Musterman",
    "address":"streetname 55 Block 3",
    "latitude" : "27.606888", 
    "longitude" : "-42.670898", 
    "...":"...",

    "bookings":[
        {
            "id":231920102956,
            "state":"archived",            
            "arrival":"20201008",
            "departure":"20201011"
        }
    ],
    "invoices":[
        {
            "id":"P1120078",
            "state":"open",
            "type":"proforma"
        }
    ]
}
```

## Search debtors
Receive a list of debtors based on **all** given search term(s)
**GET** `https://app.mytourist.cloud/api/v1/debtors?search={keyterm1,keyterm2...}`
Response exists debtor results that corresponds each search term (comma seperated).
Fields used for search query: first_name, last_name, company_name, company_id, email, phone, street, city, zipcode, debtor ID

## Create / Update a debtor
You can create or update a debtor by posting to the following URL. This endpoints will return (when success) the saved debtor (200 HTTP response). You can either post the full JSON file or single individual fields. When the field is posted we always overwrite them. When a field is not posted trough the API we won't overwrite it and keep the existing data.

**POST (Create)** `https://app.mytourist.cloud/api/v1/debtors`   
**POST (Update)** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

### Available Parameters
<table>
    <tr><td>first_name</td><td>required</td><td>when creating debtor</td></tr>    
    <tr><td>last_name</td><td>required</td><td>when creating debtor</td></tr>
    <tr><td>company_name</td><td>optional</td><td>-</td></tr>
    <tr><td>company_chamber_id</td><td>optional</td><td>Chamber / KVK nr.</td></tr>
    <tr><td>vat_id</td><td>optional</td><td></td></tr>
    <tr><td>bank_account</td><td>optional</td><td></td></tr>
    <tr><td>address</td><td>optional</td><td></td></tr>
    <tr><td>zipcode</td><td>optional</td><td></td></tr>
    <tr><td>city</td><td>optional</td><td></td></tr>
    <tr><td>country</td><td>optional</td><td>ISO 3166-2</td></tr>
    <tr><td>mobile</td><td>optional</td><td></td></tr>
    <tr><td>phone</td><td>optional</td><td></td></tr>
    <tr><td>email</td><td>optional</td><td></td></tr>
    <tr><td>note</td><td>optional</td><td></td></tr>
    <tr><td>latitude</td><td>optional</td><td>Float like eg. 27.606888</td></tr>
    <tr><td>longitude</td><td>optional</td><td>Float like eg. -42.670898</td></tr>
</table>
