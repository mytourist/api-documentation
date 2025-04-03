---
title: Vouchers
layout: default
---
### [Back to overview](index.html#start-developing-testing-and-deploy)
---
# Voucher
This API endpoint let you manage your vouchers. [Parameters](#available-parameters) can be found on the very end of this page.

**Index:** 
- [List all vouchers](#list-all-vouchers)
- [Retrieve a single vouchers](#retrieve-a-single-vouchers)
- [Create / Update a vouchers](#create--update-a-vouchers)

## List all vouchers
Get a list of all your debtors returned in `JSON` format.     
**GET** `https://app.mytourist.cloud/api/v1/vouchers`

**Results**
```json
{
    "id": "04250025",
    "code": "4863-6862",
    "type": "discount",
    "is_percentage": false,
    "amount": "50.00",
    "label": "label",
    "description": "Example discount",
    "expires_at": "2025-04-19T22:00:00.000000Z",
    "language": "en",
    "limit_date_from": "2025-03-31T22:00:00.000000Z",
    "limit_date_until": "2025-04-09T22:00:00.000000Z",
    "times_to_use": 3
},
{
    "id": "04250026",
    "code": "my-own-code",
    "type": "voucher",
    "is_percentage": true,
    "amount": "10.00",
    "label": "label",
    "description": "Example voucher",
    "expires_at": "2025-04-19T22:00:00.000000Z",
    "language": "en",
    "limit_date_from": "2025-03-31T22:00:00.000000Z",
    "limit_date_until": "2025-04-09T22:00:00.000000Z",
    "times_to_use": 1
}
```

## Retrieve a single voucher
Get a single voucher returned in `JSON` format.

**GET** `https://app.mytourist.cloud/api/v1/vouchers/{VOUCHER_ID}`


**Results**
```json
{
    "id": "04250025",
    "code": "4863-6862",
    "type": "discount",
    "is_percentage": false,
    "amount": "50.00",
    "label": "label",
    "description": "Example voucher",
    "expires_at": "2025-04-19T22:00:00.000000Z",
    "language": "en",
    "limit_date_from": "2025-03-31T22:00:00.000000Z",
    "limit_date_until": "2025-04-09T22:00:00.000000Z",
    "times_to_use": 3
}
```

## Create / Update a voucher
You can create or update a voucher by posting to the following URL. This endpoints will return (when success) the saved voucher (200 HTTP response). You can either post the full JSON file or single individual fields. When the field is posted we always overwrite them. When a field is not posted trough the API we won't overwrite it and keep the existing data.

**POST (Create)** `https://app.mytourist.cloud/api/v1/vouchers`   
**POST (Update)** `https://app.mytourist.cloud/api/v1/vouchers/{VOUCHER_ID}`

### Available Parameters
<table>
    <tr><td>code</td><td>optional</td><td>discount code (auto generated when blank)</td></tr>    
    <tr><td>type</td><td>optional</td><td>'discount' or 'voucher'. (Default 'discount')</td></tr>
    <tr><td>is_percentage</td><td>optional</td><td>boolean (Default 'false')</td></tr>
    <tr><td>amount</td><td>required</td><td>float</td></tr>
    <tr><td>label</td><td>optional</td><td>string</td></tr>
    <tr><td>description</td><td>optional</td><td>description</td></tr>
    <tr><td>expires_at</td><td>optional</td><td>datetime (Format yyyy-mm-dd hh:ii:ss)</td></tr>
    <tr><td>language</td><td>optional</td><td>ISO-639 2 (Only when type is 'voucher')</td></tr>
    <tr><td>limit_date_from</td><td>optional</td><td>date (Format yyyy-mm-dd)</td></tr>
    <tr><td>limit_date_until</td><td>optional</td><td>date (Format yyyy-mm-dd)</td></tr>
    <tr><td>times_to_use</td><td>optional</td><td>int</td></tr>
</table>
