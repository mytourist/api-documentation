---
title: Availability
layout: default
---

### [Back to overview](index.html#api-endpoints)

# Availability check for date range
To check the availability on a single or all `roomtypes` in a specific date-range. The API will always return the number of available `rooms` in this `roomtype`. The API will also return some additional information about your roomtype to prevent extra API calls to the roomtype endpoint. Inside each `roomtype` you will find the price rates.

You can use the preferred [roomtype](roomtypes.html) and [price-rate](price-rates.html) to create a booking on this date-range (when available).

**GET** `https://app.mytourist.cloud/api/v1/availability?arrival={DATE}&departure={DATE}`

**Query Parameters**
<table>
    <tr><td>arrival</td><td>required</td><td>YYYY-MM-DD</td></tr>    
    <tr><td>departure</td><td>required</td><td>YYYY-MM-DD</td></tr>
    <tr><td>roomtype_id</td><td>optional</td><td>The API will only return the results for this particular <a href="roomtypes.html">roomtypes</a>.</td></tr>
    <tr><td>language</td><td>optional</td><td>ISO 639-1</td></tr>
</table>

**Example result**
```JSON
[
    {
        "id":"81912063",                            // ID of the Roomtype.
        "rooms_available":1,                        // Exact (live) number of available rooms inside this roomtype.
        "name":"Doubleroom Deluxe with balcony",
        "description":"Our best room with an amazing view over the city!",
        "rates":[
            {
                "id":66118004,                      // ID of the Price rate.
                "rate_available":true,
                "total_price":200,                  // Calculated price (without additional bookable addons)
                "name":"Conform arrangement",
                "reasons":[]                        // Is empty when rate is available.
            },
            {
                "id":82010274,
                "rate_available":false,
                "total_price":0,
                "name":"Bubbles arrangement - Long weekend",
                "reasons":[
                    "closedonarrival",              // Arrival is not possible for this rate on this day.
                    "closedondeparture",            // Departure is not possible for this rate on this day.
                    "maxstay",                      // Number of nights extends the maxstay.
                    "minstay",                      // Number of nights is less than minstay.
                ]
            }
        ]
    },
    {
        ...
    }
]
```

# Availability calendar
This endpoint will return the `available` rooms and current price per `price rate` for each day of the given month. You can take all your roomtypes or just one single

**POST** `https://app.mytourist.cloud/api/v1/availability/`

**Query Parameters**
<table>
    <tr><td>date</td><td>required</td><td>YYYY-MM-DD (it will automatically determine the month range)</td></tr>    
    <tr><td>roomtype_id</td><td>optional</td><td>@id from <a href="roomtypes.html">roomtypes</a></td></tr>    
</table>

**Example result**
```json
{
    "23192010281":{
        "2020-12-01":{
            "availability":{
                "value":2,
                "custom_value":false
            },
            "prices":{
                "23192010281":{
                    "name":"Standaard",
                    "custom_value":false,
                    "price":80
                },
                "..." : "..."
            }
        },
        "2020-12-02":{
            "availability":{
                "value":1,
                "custom_value":false
            },
            "prices":{
                "23192010281":{
                    "name":"Standaard",
                    "custom_value":false,
                    "price":80
                },
                "..." : "..."
            }
        },
        "..." : "..."
    },
    "23192010281":{
        "2020-12-01" : {
            "..." : "..."
        }
    }
}
```