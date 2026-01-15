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
                "120022112": {
                    "id": "120022112",
                    "min_stay": 2,
                    "max_stay": 3,
                    "closed_on_arrival": false,
                    "closed_on_departure": true,
                    "name": "Weekend arrangement",
                    "public_name": "Verblijf met 15% korting - vanaf 3 nachten",
                    "current_price": 100,
                    "default_price": 100,
                    "is_custom_price": false,
                },
                "120022113": {
                    "id": "120022112",
                    "min_stay": 3,
                    "max_stay": 14,
                    "closed_on_arrival": false,
                    "closed_on_departure": true,
                    "name": "OTA (booking.com)",
                    "public_name": "",
                    "current_price": 110,
                    "default_price": 110,
                    "is_custom_price": false,
                    "is_subrate": true,
                    "subrate": {
                        "adjusted_by": "percentage",
                        "value": "10"
                    }
                },
                "120022114": {
                    "id": "120022112",
                    "min_stay": 3,
                    "max_stay": 14,
                    "closed_on_arrival": false,
                    "closed_on_departure": true,
                    "name": "Midweek",
                    "public_name": "",
                    "current_price": 150,
                    "default_price": 140,
                    "is_custom_price": true,
                },
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
With this function you can manage and overwrite the following values; `available`, `price_per_night`, `min_stay`, `max_stay`, `close_to_arrival`, `close_to_departure` per `price_rate` per day or just a selected period. With this functions it's no longer needed to make bulk changes to your calendar via the MyTourist GUI. 

**POST** `https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}`

**Query Parameters**
<table>
    <tr><td>from</td><td>required</td><td>YYYY-MM-DD</td></tr>    
    <tr><td>until</td><td>required</td><td>YYYY-MM-DD</td></tr>       
    <tr><td>rooms_to_sell</td><td>optional</td><td>Won't go higher than the exact number of rooms. `rooms_to_sell` = `rooms_to_sell` MINUS `number_of_bookings` (calculated automatically) or use `auto` for the default value</td></tr>       
    <tr><td>min_stay</td><td>optional</td><td>Nights or use `auto` for the default value</td></tr>       
    <tr><td>max_stay</td><td>optional</td><td>Nights or use `auto` for the default value</td></tr>         
    <tr><td>close_to_arrival</td><td>optional</td><td>`closed` or `open`. Or `default` to reset to price rate settings</td></tr>       
    <tr><td>close_to_departure</td><td>optional</td><td>`closed` or `open`. Or `default` to reset to price rate settings</td></tr>       
    <tr><td>price_per_night</td><td>optional</td><td>decimal 10,2  or use `auto` for the default value</td></tr>       
</table>

#### Example 1 | change availability for one single day.
In this example we will lower the number of available rooms from 4 to just 1 available room.

```
curl --location --request POST 'https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}' \
--header 'Authorization: Bearer {YOUR_SECRET_BEARER}' \
--form 'from="2030-01-01"' \
--form 'until="2030-01-01"' \
--form 'rooms_to_sell="1"'
```

#### Example 2 | setup only arrivals on Monday/Tuesday and Departures on Friday/Saturday between longer period.
In this example we give the weekdays witch allowed to arrive and depart. The weekdays now given will be closed for arrival or departure.

```
curl --location --request POST 'https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}' \
--header 'Authorization: Bearer {YOUR_SECRET_BEARER}' \
--form 'from="2030-01-01"' \
--form 'until="2030-05-15"' \
--form 'close_to_arrival="closed"' \
--form 'close_to_departure="open"'
```

#### Example 3 | Change price for one week
For this period we will change te price from 120 to 100.

```
curl --location --request POST 'https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}' \
--header 'Authorization: Bearer {YOUR_SECRET_BEARER}' \
--form 'from="2030-01-01"' \
--form 'until="2030-01-07"' \
--form 'price_per_night="100,00"'
```

#### Example 4 | Reset everything into their defaults
This will take the default availability and the price and restrictions from the price rate.

```
curl --location --request POST 'https://app.mytourist.cloud/api/v1/calendar/{RATE_ID}' \
--header 'Authorization: Bearer {YOUR_SECRET_BEARER}' \
--form 'from="2030-01-01"' \
--form 'until="2030-01-07"' \
--form 'rooms_to_sell="auto"'\
--form 'price_per_night="auto"'\
--form 'min_stay="auto"'\
--form 'max_stay="auto"'\
--form 'close_to_arrival="closed"'\
--form 'close_to_departure="default"'\
```

### Handling multiple bulkchanges in one API request
Post JSON to push multiple bulkchanges in one single API call.

**POST** `https://app.mytourist.cloud/api/v1/calendar/bulk`

Body:
```json
[
    {
        "rate_id":"12345678",
        "from":"2025-08-14",
        "until":"2025-08-14",
        "price_per_night":"55",
        "min_stay":3
    },
    {
        "rate_id":"87654321",
        "from":"2025-08-15",
        "until":"2025-08-17",
        "price_per_night":"60",
        "min_stay":2
    }
]
```
