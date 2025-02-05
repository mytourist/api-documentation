---
title: Bookings
layout: default
---
### [Back to overview](index.html#api-endpoints)
---
# Bookings
This API endpoint let you manage your price rates. Most useful to fetch price rates per roomtype.

**Index:** 
- [List of bookings between dates](#list-of-bookings-between-dates)
- [List of bookings from specific debtor](#list-of-bookings-from-specific-debtor)
- [List of bookings currently staying](#list-of-bookings-currently-staying)
- [Retrieve a single booking](#retrieve-a-single-booking)
- [Create a booking](#create-a-booking)
- [Update a booking](#update-a-booking)
- [Cancel a booking](#cancel-a-booking)
- [Available form parameters](#available-form-parameters)
- [List guests](#list-guests)
- [Update single Guest](#update-single-guest)
- [Available channels](#available-channels)


# List of bookings between dates
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
        "expected_arrival_time": "19:00:00",
        "auto_send_email":true,
        "roomtype":{
            "id":"23192010281",
            "name":"Doubleroom with balcony",
            "placed_in_room":"Room 1"
        },
        "debtor_id":"23192010294",
        "debtor":{
            "id":"23192010299",
            "company_name":null,
            "company_chamber_id":null,
            "first_name":"Max",
            "last_name":"Musterman",
            "address":"streetname 55 Block 3",
            "latitude" : "27.606888", 
            "longitude" : "-42.670898", 
            "...":"..."
        },
        "number_of_guests":4,
        "guests": [
            {
                "salutation": "male",
                "firstname": "Max",
                "lastname": "Musterman",
                "birthday": "1985-04-01",
                "address": "Demostreet 44",
                "zipcode": "123456",
                "city": "Amsterlin",
                "country": "NL",
                "phone": "0031 0800 0101",
                "email": "example@demohotel.com"
            },
            {
                "salutation": "female",
                "firstname": "Maxine",
                "lastname": "Musterman",
                "birthday": "1985-07-01",
                "address": "Demostreet 44",
                "zipcode": "123456",
                "city": "Amsterlin",
                "country": "NL",
                "phone": "0031 0800 0101",
                "email": "example@demohotel.com"
            }
        ],
        "number_of_children":2,
        "dietary_wishes":"No Gluten",
        "access_code":"1234",
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
        "breakfast_booked":true,
        "related_bookings": [
            {
                "id": 1210531315,
                "is_main_booking": false
            },
            {
                "id": 1210531313,
                "is_main_booking": false
            },
            {
                "id": 1210531312,
                "is_main_booking": true
            },
            {
                "id": 1210531314,
                "is_main_booking": false
            }
        ],
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
# List of bookings from specific debtor
Like [List of bookings between dates](#list-of-bookings-between-dates), this function provides a list view of all bookings. But now based on a specific [debtor](debtors.html) number.
**GET** `https://app.mytourist.cloud/api/v1/bookings/from-debtor?debtor_id={DEBTOR_ID}`
**Query Parameters**
<table>
    <tr><td>debtor_id</td><td colspan="2">required</td></tr>
    <tr><td>show_cancellations</td><td>optional</td><td>boolean; true</td></tr>
</table>

# List of bookings currently staying
This function provides you with an list of all the bookings corresponding with the current (or other) date. This can be bookings who are departing, staying or arriving today. Like the insights page inside the MyTourist UI those bookings are sorted bij the order of the unit(types).

**GET** `https://app.mytourist.cloud/api/v1/bookings/current-bookings?date={DATE}&light=true`

**Query Parameters**
<table>
    <tr><td>date</td><td>optional</td><td>20300131 (YYYYMMDD) (empty is today)</td></tr>
    <tr><td>light</td><td>optional</td><td>boolean (false by default) - faster response, less data</td></tr>
</table>

# Retrieve a single booking
Same `JSON` output as above with all information.

**GET** `https://app.mytourist.cloud/api/v1/bookings/{BOOKING_ID}`

# Create a booking
This endpoint will expect that you have already validated the [availability](availability.html). Ofcourse this endpoint will validate once more the availability of the given roomtype. But it is still faster to validate the availability with the corresponding endpoint.

**POST** `https://app.mytourist.cloud/api/v1/bookings`

>Be aware that your price `rate_id` is corresponding with your `roomtype_id`.

# Update a booking
You can either post the changed `JSON` result or just the field(s) you want to change. When a field is not set, it will be ignored. When you send a empty field it will be restored to the default value or will changed to `null`.

**POST** `https://app.mytourist.cloud/api/v1/bookings/{BOOKING_ID}`

>Bookings from external providers are partial locked fur security and synchronization purposes. `arrival`, `departure` and `channel_reference` fields are not accepted in that case.

>Chaning the roomtype will mean you need to change the price rate also, when you don't send us a price rate we will take the default price rate of this roomtype. (Price rates related to roomtypes this does not apply the other way around)

>Use the field `recalculate_invoice_logies` as `true` when you want to recalculate your invoice logies.

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
    <tr><td>rate_id</td><td>optional*</td><td>ID of a <a href="price-rates.html">price rate</a> inside the selected roomtype. (default: 1th listed rate)</td></tr>
    <tr><td>unit_id</td><td>optional</td><td>Prefered unit ID. System will automatically select another available room when this unit ID isn't availble</td></tr>
    <tr><td>debtor_id</td><td>optional</td><td>Default: no <a href="debtors.html">debtor</a> attached</td></tr>
    <tr><td>state</td><td>optional</td><td>optional/confirmed (default:confirmed)</td></tr>
    <tr><td>auto_send_email</td><td>optional</td><td>true/false (default:true)</td></tr>
    <tr><td>dietary_wishes</td><td>optional</td><td>string</td></tr>
    <tr><td>access_code</td><td>optional</td><td>string</td></tr>
    <tr><td>note</td><td>optional</td><td>string</td></tr>
    <tr><td>commission_amount</td><td>optional</td><td>float</td></tr>
    <tr><td>forced_logies_price</td><td>optional</td><td>float (to force logies invoice price)</td></tr>
    <tr><td>expected_arrival_time</td><td>optional</td><td>Following times are supported:
    10.00, 10.30, 11.00, 11.30, 12.00, 12.30, 13.00, 13.30, 14.00, 14.30, 15.00, 15.30, 16.00, 16.30, 17.00, 17.30, 18.00, 18.30 19.00, 19.30, 20.00, 20.30, 21.00, 21.30, 22.00, 22.30, 23.00, 23.30, 23.59
    </td></tr>
    <tr><td>invoice_enabled</td><td>optional (only create)</td><td>true/false (default:true)</td></tr>
</table>

\* Required on creating a booking.

# List guests
List all the guests for a single booking.

**GET** `https://stage.mytourist.cloud/api/v1/bookings/{BOOKING_ID}/guests`

**Example result**
```json
[
    {
        "guest_id": 1,
        "salutation": "male",
        "firstname": "Max",
        "lastname": "Musterman",
        "birthday": "03-07-1962",
        "address": "Previewstreet 44",
        "zipcode": "1234AA",
        "city": "Amsterdam",
        "country": "NL",
        "phone": "06123456789",
        "email": "email@email.com"
    },
    {
        "guest_id": 2,
        ".." : ".."
    }
]
```

# Update single guest

To update one of your guests.

**POST** `https://stage.mytourist.cloud/api/v1/bookings/{BOOKING_ID}/guests/{GUEST_ID}`

### Available form parameters
<table>
    <tr><td>salutation</td><td>male/female</td></tr>
    <tr><td>firstname</td><td></td></tr>
    <tr><td>lastname</td><td></td></tr>
    <tr><td>birthday</td><td>YYYYMMDD</td></tr>
    <tr><td>address</td><td></td></tr>
    <tr><td>zipcode</td><td></td></tr>
    <tr><td>city</td><td></td></tr>
    <tr><td>country</td><td>ISO-2</td></tr>
    <tr><td>phone</td><td></td></tr>
    <tr><td>email</td><td></td></tr>
</table>



# Available channels

<table>
    <tr><td>mytourist</td><td>creates booking as it's been created inside the MyTourist interface</td></tr>
    <tr><td>api</td><td>creates booking as external channel. Bookings are locked until you change them via the API</td></tr>
    <tr><td>{custom}</td><td>Only available for certified software/platforms partners</td></tr>
</table>

**Custom channel connection for connectivity partners**  
Owning a online Travel Agency? For contracted partners we can create a custom channel. Then a 2-way connection can be made for bookings, availability and pricing. You can build a booking module on your platform or synchronize the bookings into our centralized database. Please <a href="https://mytourist.cloud" target="_blank">contact us</a> for more information.
