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

## Create a debtor
You can easally create a new debtor by calling the following URL by the `POST` method. This endpoints will return the saved debtor as their (200 HTTP response) result.

**POST** `https://app.mytourist.cloud/api/v1/debtors`    


## Update a debtor
When you want to update any debtor you'll need to use the same `POST` method with the `debtor_id` appended to the URL. 

**POST** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

_You can do either overwrite the whole JSON result with your parameters and push it back in JSON format (use the header `Content-Type: application/json`) or just change individual; fields by using the `formData` method. When you don't call particular parameters we won't do anything and ignoring this parameter. When you put a parameter as an empty string we will emptying this parameter inside our database also._

## Available Parameters
<table>
    <tr><td>first_name</td><td>required</td><td>When POST</td></tr>    
    <tr><td>last_name</td><td>required</td><td>When POST</td></tr>
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