---
title: Calendar
layout: default
---

### [Back to overview](index.html#api-endpoints)

# Calendar
The MyTourist calendar is the centralized space where all the magic happens. Your bookings, price rates, available rooms, and restrictions like min./max. stay and check-in/out restrictions printed into one single calendar.

>This endpoint returns fully cached results, the cache will refresh after a change took place in your account. It may take a few minutes to implement those changes into the cache.

**Index:** 
- [Fetch the calendar data](#fetch-the-calendar-data)
- [Bulk changes](#bulk-changes)

## Fetch the calendar data
This endpoint will return the number of `available` rooms and current logies price per `price rate` for each day of the given month. You can take all your roomtypes or just a single one.

**POST** `https://app.mytourist.cloud/api/v1/calendar`

**Query Parameters**
<table>
    <tr><td>date</td><td>required</td><td>YYYY-MM-DD (it will automatically determine the month range)</td></tr>    
    <tr><td>roomtype_id</td><td>optional</td><td>@id from <a href="roomtypes.html">roomtypes</a></td></tr>    
    <tr><td>language</td><td>optional</td><td>ISO 639-1</td></tr>    
</table>

**Example result**
```json
{
    "@roomtype_id":{
        "@date(YYYYMMDD)":{
            "availability":{
                ".." : ".."
            },
            "prices": {
                "@rate_id" : {
                    ".." : ".."
                }
            }
        }
    },

    "4719120611":{
        "20201130":{
            "availability":{
                "value":2,
                "custom_value":false
            },
            "prices":{
                "23192010281":{
                    "name":"My Default price rate",
                    "custom_value":false,
                    "price":80,
                    "min_stay":2,
                    "max_stay":null,
                    "closed_on_arrival":true,
                    "closed_on_departure":false
                },
                "..." : "..."
            }
        },
        "20201201" : {
            "..." : "..."
        }
    },
    "23192010281":{
        "2020-12-01" : {
            "..." : "..."
        }
    }
}
```


## Bulk changes
With this function you can manage and overwrite the following values of; `available`, `price_per_night`, `min_stay`, `max_stay`, `may_checkin_on`, `may_checkout_on` per `price_rate` per day or just a selected period. With this functions it's no longer needed to make bulk changes to your calendar via the MyTourist GUI. 

**POST** `https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}`

**Query Parameters**
<table>
    <tr><td>from</td><td>required</td><td>YYYY-MM-DD</td></tr>    
    <tr><td>until</td><td>required</td><td>YYYY-MM-DD</td></tr>       
    <tr><td>rate_id</td><td>required</td><td>The unique price_rate @id</td></tr> 
    <tr><td>rooms_to_sell</td><td>optional</td><td>Won't go higher than the exact number of rooms. `rooms_to_sell` = `rooms_to_sell` MINUS `number_of_bookings`</td></tr>       
    <tr><td>min_stay</td><td>optional</td><td>Nights</td></tr>       
    <tr><td>max_stay</td><td>optional</td><td>Nights</td></tr>         
    <tr><td>may_checkin_on</td><td>optional</td><td>mo,tu,we,th,fr,sa,su (comma separated)</td></tr>       
    <tr><td>may_checkout_on</td><td>optional</td><td>mo,tu,we,th,fr,sa,su (comma separated)</td></tr>       
    <tr><td>price_per_night</td><td>optional</td><td>decimal 10,2</td></tr>       
</table>

### Example 1 | change availability for one single day.
In this example we will lower the number of available rooms from 4 to just 1 available room.

```
curl --location --request POST 'https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}' \
--header 'Authorization: Bearer {YOUR_SECRET_BEARER}' \
--form 'from="2030-01-01"' \
--form 'until="2030-01-01"' \
--form 'available="1"'
```