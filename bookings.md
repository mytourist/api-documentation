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
- [Available form parameters](#available-form-parameters)


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

**GET** `https://app.mytourist.cloud/api/v1/bookings/{BOOKING_ID}`

# Create a booking
This endpoint will expect that you have already validated the [availability](availability.html). Ofcourse this endpoint will validate once more the availability of the given roomtype. But it is still faster to validate the availability with the corresponding endpoint.

**POST** `https://app.mytourist.cloud/api/v1/bookings`

# Update a booking
You can either post the changed `JSON` result or just the field(s) you want to change. When a field is not set, it will be ignored. When you send a empty field it will be restored to the default value or will changed to `null`.

>Bookings from external providers are partial locked fur security and synchronization purposes. `arrival`, `departure`, `channel` and `channel_reference` fields are not accepted in that case.

# Cancel a booking
Only bookings from `mytourist`, `website` (booking engine) or `api` can be cancelled from this API. We do not allow you to cancel bookings with a live synchronization connection to external platforms.

**DELETE** `https://app.mytourist.cloud/api/v1/bookings/{BOOKING_ID}`

> If, for some reason a booking is out-of-sync, please contact support. 

# Available form parameters
<table>
    <tr><td>channel</td><td>optional</td><td>default: mytourist (<a href="#available-channels">list</a>)</td></tr>
    <tr><td>arrival</td><td>required*</td><td>DATE: YYYYMMDD</td></tr>
    <tr><td>departure</td><td>required*</td><td>DATE: YYYYMMDD</td></tr>
    <tr><td>roomtype_id</td><td>required*</td><td>ID of <a href="price-rates.html">roomtypes</a></td></tr>
    <tr><td>rate_id</td><td>optional*</td><td>ID of <a href="price-rates.html">price rates</a> (default: 1th listed rate)</td></tr>
    <tr><td>debtor_id</td><td>optional</td><td>Default: no <a href="debtors.html">debtor</a> attached</td></tr>
    <tr><td>auto_send_email</td><td>optional</td><td>true/false (default:true)</td></tr>
    <tr><td>number_of_guests</td><td>optional</td><td>float</td></tr>
    <tr><td>number_of_children</td><td>optional</td><td>float (number of children inside the guests total)</td></tr>
    <tr><td>dietary_wishes</td><td>optional</td><td>string</td></tr>
    <tr><td>note</td><td>optional</td><td>string</td></tr>
    <tr><td>commission_amount</td><td>optional</td><td>float</td></tr>
    <tr><td>forced_logies_price</td><td>optional</td><td>float (to force logies invoice price)</td></tr>
    <tr><td>invoice_enabled</td><td>optional</td><td>true/false (default:true)</td></tr>
</table>

\* Required on creating a booking.

# Available channels

<table>
    <tr><td>mytourist</td><td>creates booking as it's been created inside the MyTourist interface</td></tr>
    <tr><td>api</td><td>creates booking as external channel. Bookings are locked until you change them via the API</td></tr>
</table>