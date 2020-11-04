---
title: Bookings
layout: default
---
### [Back to overview](index.html#api-endpoints)
---
# Bookings
This API endpoint let you manage your price rates. Most useful to fetch price rates per roomtype.

**Index:** 
- [List bookings between dates](#list-bookings-between-dates)
- [Retrieve a single booking](#retrieve-a-single-booking)
- [Create a booking](#create-a-booking)
- [Update a booking](#update-a-booking)
- [Cancel a booking](#cancel-a-booking)

# List bookings between dates
To prevent heavy requests you need to give us an `from` and `until` date. These dates may not deviate by more than 36 days. All bookings made in this period will be shown for each roomtype in your account. It is also possible to set an `roomtype_id` to only fetch bookings for this roomtype.

**GET** `https://app.mytourist.cloud/api/v1/bookings?from={DATE}&until={DATE}`

**Query Parameters**
<table>
    <tr><td>from</td><td>required</td><td>YYYY-MM-DD</td></tr>    
    <tr><td>until</td><td>required</td><td>YYYY-MM-DD</td></tr>
    <tr><td>roomtype_id</td><td>optional</td><td>The API will only return the results for this particular <a href="roomtypes.html">roomtypes</a>.</td></tr>
    <tr><td>show_cancellations</td><td>optional</td><td>boolean; true</td></tr>
</table>

**Example result**
```json
[
    {
        "id":231920102956,
        "state":"confirmed",
        "arrival":"2023-10-08",
        "departure":"2023-10-11",
        "auto_send_email":true,
        "roomtype":{
            "id":"23192010281",
            "name":"Doubleroom with balcony",
            "placed_in_room":"Room 1"
        },
        "debtor_id":"23192010294",
        "number_of_guests":4,
        "number_of_children":2,
        "dietary_wishes":"No Gluten",
        "note":"Brings bicycles and would like to park them in the garage",
        "commission_amount":null,
        "rate":{
            "id":"23192010281",
            "name":"Default Price rate"
        },
        "channel":{
            "id":"115TALSTRIPADVISORC1603970714",
            "label":"tripadvisor",
            "reference":"35e9bad0-3b889511e41a@rentals.tripadvisor.com",
            "info":"Booking imported from tripadvisor"
        },
        "forced_logies_price":300.00,
        "invoice_enabled":true,
        "invoice":{
            "id":"P102006",
            "total_amount_incl_vat":300,
            "total_amount_excl_vat":240,
            "has_amount_to_pay":true
        },
        "created_at":"2020-10-29 12:25:16",
        "updated_at":"2020-10-29 12:25:16",
        "checkin_at":"2020-11-04 14:35:51",
        "checkout_at":null
    },
    {
        "..."
    }
]
```

# Retrieve a single booking
Same `JSON` output as above with all information.

