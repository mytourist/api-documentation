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
</table>

**Example result**
```json
{
    
}
```

# Retrieve a single booking
Same `JSON` output as above with all information.

