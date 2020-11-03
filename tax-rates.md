---
title: TaxRates
layout: default
---
### [Back to overview](index.html#start-developing-testing-and-deploy)
---
# TaxRates API
This API endpoint let you manage your tax rates.

**Index:** 
- [List all rates](#list-all-rates)
- [Create / Update a rate](#create--update-a-rate)
- [Delete a single rate](#delete-a-single-rate)

## List all rates
Get a list of all your tax rates returned in `JSON` format. 

**GET** `https://app.mytourist.cloud/api/v1/tax-rates`

**Example results**
```json
[
    {
        "id":"23192011033",
        "label":"Low",
        "rate":10,
        "created_at":"2020-11-03T09:52:42.000000Z",
        "updated_at":"2020-11-03T09:52:42.000000Z"
    },
    {
        "id":"23192011034",
        "label":"High",
        "rate":20,
        "created_at":"2020-11-03T09:52:46.000000Z",
        "updated_at":"2020-11-03T09:52:46.000000Z"
    }
]
```

## Create / Update a rate
However tax rates are normally unchanged for a long time, you *can* manage your tax rates by this endpoint.

**POST (add)** `https://app.mytourist.cloud/api/v1/tax-rates`
**POST (update** `https://app.mytourist.cloud/api/v1/tax-rates/{RATE_ID}`

**Parameters**
<table>
    <tr><td>label</td><td>required on add</td><td>string</td></tr>    
    <tr><td>rate</td><td>required</td><td>float</td></tr>    
</table>

## Delete a single rate