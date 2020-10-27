# RESTful API Documentation.
Use the MyTourist API to integrate availability check, debtors and a lot more intro your website or app. MyTourist and your website or app back-end will communicate by sending HTTP requests back and forth. This page provides an overview of the MyTourist API. The topics in the chapter deal with a number of specific aspects of the API. We recommend to read these topics entirely.

If you have any questions about integrating our API, please contact us. We’re happy to help!

### Jump to
- [The MyTourist REST API](#the-mytourist-rest-api)
- [Get an API key](#get-an-api-key)
- [Authentication](#authentication)
    - [Debtors API](#debtors-api)

## The MyTourist REST API
The API implements a Representational state transfer (REST) architecture. Sounds technical, but it’s really quite easy. It mainly breaks down to HTTP-methods GET, PATCH, POST and DELETE matching the operations to read, update, create and delete.

REST also implies a nice and clean structure for URLs or endpoints. This means you can reach any part of the MyTourist API on https://app.mytourist.com/api/ adding the name of the resource you want to interact with.

## Get an API key
The first thing you need is a API key. Each location/company profile has a API key printed inside the API page found in preferences. Of course it’s very important to keep your API key secure. Do not ever share them. 

## Authentication
The API key or token must be sent along with each API request, by providing it in the HTTP call’s Authorization header using the Bearer method. For example: a valid Authorization header is `Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6`.

In the example below we use a API key on the GET method of the debtors resource. This method fetches a list of debtors.
```bash
curl -X GET https://app.mytourist.cloud/api/debtors -H "Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6"
```

# Availability API
To check the availability on a single or all available `roomtypes` in a specific date-range. The API will always return the number of available `rooms` in this `roomtype`. The API will also return some additional information about your roomtype to prevent extra API calls to the roomtype endpoint. Inside each `roomtype` you will find the price `rates`.

**GET** `https://app.mytourist.cloud/api/availability?arrival={DATE}&departure={DATE}`

**Query Parameters**
<table>
    <tr><td>arrival</td><td>required</td><td>YYYY-MM-DD</td></tr>    
    <tr><td>departure</td><td>required</td><td>YYYY-MM-DD</td></tr>
    <tr><td>roomtype_id</td><td>optional</td><td>The API will only return the results for this particular roomtype.</td></tr>
    <tr><td>language</td><td>optional</td><td>ISO 639-1</td></tr>
</table>

**Example**
```bash
curl --location --request GET 'https://app.mytourist.cloud/api/availability?arrival={date}&departure={date}' \
--header 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6'
```

**Results**
```JSON
[
    {
        "id":"81912063",
        "rooms_available":1,
        "name":"Doubleroom Deluxe with balcony",
        "description":"Our best room with an amazing view over the city!",
        "rates":[
            {
                "id":66118004,
                "rate_available":true,
                "total_price":200,
                "name":"Conform arrangement",
                "reasons":[]
            },
            {
                "id":82010274,
                "rate_available":false,
                "total_price":0,
                "name":"Bubbles arrangement - Long weekend",
                "reasons":[
                    "closedonarrival",
                    "closedondeparture"
                ]
            }
        ]
    },
    {
        ...
    }
]
```

# Debtors API

## List all debtors
**GET** `https://app.mytourist.cloud/api/debtors`

## Retrieve a single debtor
**GET** `https://app.mytourist.cloud/api/debtors/{DEBTOR_ID}`

## Create or update a debtor
You can easally create a new debtor by calling the following URL by the `POST` method. When you want to update any debtor you'll need to use the `PUT` method with the **complete** form data and `debtor_id` inside the URL. Both endpoints will return the saved debtor as their (200 HTTP response) result.

**POST** `https://app.mytourist.cloud/api/debtors`    
**PUT** `https://app.mytourist.cloud/api/debtors/{DEBTOR_ID}`

**FORM Parameters**
<table>
    <tr><td>first_name</td><td>required</td><td>-</td></tr>    
    <tr><td>last_name</td><td>required</td><td>-</td></tr>
    <tr><td>company_name</td><td>optional</td><td>-</td></tr>
    <tr><td>company_chamber_id</td><td>optional</td><td>Chamber / KVK nr.</td></tr>
    <tr><td>vat_id</td><td>optional</td><td></td></tr>
    <tr><td>address</td><td>optional</td><td></td></tr>
    <tr><td>zipcode</td><td>optional</td><td></td></tr>
    <tr><td>city</td><td>optional</td><td></td></tr>
    <tr><td>country</td><td>optional</td><td>ISO 639-1</td></tr>
    <tr><td>phone</td><td>optional</td><td></td></tr>
    <tr><td>email</td><td>optional</td><td></td></tr>
    <tr><td>note</td><td>optional</td><td></td></tr>
</table>

**Example**
```bash
curl --location --request POST 'https://app.mytourist.cloud/api/debtors' \
--header 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6' \
--form 'first_name=Max' \
--form 'last_name=Musterman' \
--form 'company_name=MyTourist' \
--form 'company_chamber_id=123456789'
```