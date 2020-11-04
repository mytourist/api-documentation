---
title: PriceRates
layout: default
---
### [Back to overview](index.html#api-endpoints)
---
# Products API
This API endpoint let you manage your price rates. Most useful to fetch price rates per roomtype.

**Index:** 
- [List all price rates](#list-all-price-rates)
- [Retrieve a single price rate](#retrieve-a-single-price-rate)

## List all price rates
Get a list of all price rates inside a roomtype.

**GET** `https://app.mytourist.cloud/api/v1/price-rates`

**Query Parameters**
<table>
    <tr><td>roomtype_id</td><td>optional (recommended)</td><td>The API will only return the results for this particular <a href="roomtypes.html">roomtypes</a>.</td></tr>
    <tr><td>language</td><td>optional</td><td>ISO 639-1</td></tr>
</table>

**Example result**
```json
[
    {
        "id":"23192011041",
        "parent_id":"23192010281",      // When rate acting as sub price rate.
        "roomtype_id":"23192010281",
        "internal_name":"Long weekend", // Internal name
        "public_name":{                 // Autom. translated
            "nl" : "Lang weekend",
            "en" : "Verlängertes Wochenende",
            ".." : ""
        },
        "note":"This rate is only bookable in the weekends. Based on the main price with -10%",
        "enabled_for_booking_engine":true,  // Visible on the booking engine.
        "persons":2,                        
        "min_stay":4,
        "max_stay":null,
        "closed_on_arrival":"mo,tu,we,th,sa,su", // Weekdays blocked for arrival
        "closed_on_departure":"tu,we,th,fr,sa",
        "default_price_per_night":"10.00",       // Price also used for percentages
        "price_per_night_percentage":true,       // Price value is percentage (only available when sub rate)
        "arrangement_products_inlcuded":[
            {
                "id":"231920110418",
                "name":{
                    "nl":"Ontbijt"
                },
                "calculation_methods":["person","night"]
            }
        ],
        "translated_at":"2020-11-04 13:21:29",
        "created_at":"2020-11-04 12:21:29",
        "updated_at":"2020-11-04 12:21:29"
    }
]
```

## Retrieve a single price rate
Same result as above but than a particular single price rate wil returned in `json`. The same parameters can be used as the list endpoint.

**GET** `https://app.mytourist.cloud/api/v1/price-rates/{RATE_ID}`