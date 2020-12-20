---
title: Bookings
layout: default
---
### [Back to overview](index.html#api-endpoints)
---
# Obtain bearer token
This function makes it possible to request a bearer token on behalf of your customer in order to use the API. This way your customer does not have to log in to mytourist first to request his or her bearer token.

> For this endpoint, your own authentication bearer token in MyTourist must be marked as `certified`. Please <a href="https://mytourist.cloud" target="_blank">contact us</a> or start a ticket to begin the certification process.

**POST** `https://app.mytourist.cloud/api/v1/obtain-bearer-Token`

**Query Parameters**
<table>
    <tr><td>email</td><td>required</td></tr>    
    <tr><td>password</td><td>required</td></tr>
</table>

## HTTP responses
<table>
    <tr><td>200</td><td>OK</td><td>Returns the bearer token.</td></tr>
    <tr><td>400</td><td>FAILED</td><td>Validation fails (email/password required).</td></tr>
    <tr><td>403</td><td>FAILED</td><td>Credentials (email, password or both) incorrect.</td></tr>
</table>
