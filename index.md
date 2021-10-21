---
title: API V1 MyTourist
page.title: test
layout: default
---

# RESTful API Documentation.
Use the MyTourist API to integrate availability check, debtors and a lot more intro your website or app. MyTourist and your website or app back-end will communicate by sending HTTP requests back and forth. This page provides an overview of the MyTourist API. The topics in the chapter deal with a number of specific aspects of the API. We recommend to read these topics entirely.

If you have any questions about integrating our API, please contact us. We’re happy to help!

**Quick jump to:**   
- [Get an API key](#get-an-api-key)
- [Risk and warranty](#use-at-your-own-risk--no-warranty)
- [Authentication](#authentication)
- [Start developing, test and deploy](#start-developing-test-and-deploy)
- [Webhooks](#webhooks)
- [HTTP responses table](#http-responses-table)
- [API Endpoints](#api-endpoints)

> [Availability](availability.html), [Bookings](bookings.html), [Debtors](debtors.html), [Invoices](invoices.html), [Products](products.html), [ProductCategories](product-categories.html), [PriceRates](#PriceRates), [Roomtypes](roomtypes.html) or [TaxRates](tax-rates.html)

- [API Endpoints (certified access only)](#api-endpoints-certified-access-only)
- [ObtainBearerToken](obtain-bearer-token.html)

- [Updates](#updates) <sub>22th october '21</sub>

## The MyTourist REST API
The API implements a Representational state transfer (REST) architecture. Sounds technical, but it’s really quite easy. It mainly breaks down to HTTP-methods GET, PATCH, POST and DELETE matching the operations to read, update, create and delete.

REST also implies a nice and clean structure for URLs or endpoints. This means you can reach any part of the MyTourist API on https://app.mytourist.com/api/v1 adding the name of the resource you want to interact with.

Default the throttle limit is 25 requests each 60 seconds. We can individually increase this amount but only on good substantiation. All endpoints will return their data in `JSON` format.

## Obtain a API token
The first thing you need is a API token. Each location-/company profile has a API token printed inside the API page found in preferences. Of course it’s very important to keep your API token secure. Do not ever share them. 

## Use at your own risk / No warranty
We validate each request based on basic validation rules and you will operate outside the GUI of MyTourist with all the nice checks inside. You are responsible for the data you will add or change via the API. Each call is logged and kept for at least 24 month. We strongly recommend to test your API first in an dummy company profile before you use your production based company profile. Inside your account settings you are free to manage your company profiles. If your connection causes data to become corrupt, we can charge you to restore a backup of your company profile.

## Authentication
The API token must be sent along with each API request, by providing it in the HTTP call’s Authorization header using the Bearer method. For example: a valid Authorization header is `Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6`.

In the example below we use a API token on the GET method of the debtors resource. This method fetches a list of debtors.
```bash
curl -X GET https://app.mytourist.cloud/api/v1/debtors -H 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6'
```

## Certification
For some eg. `create/update` endpoints an really good understanding of the OTA process is required. Thats why these functions are only available for contracted software/platform partners. To request access, please <a href="https://mytourist.cloud" target="_blank">contact us</a>.

## Start developing, test and Deploy
By far [Postman](https://www.postman.com/) is a great tool to help you out in the first steps of build any connection with us. This tool enables you to test all GET/POST/PUT/Etc.. requests. We do sometimes host custom API's on our high-end cluster infrastructure for our customers and direct partners. Please contact us for more information.

# Webhooks
In Mytourist you will find the webhooks page within the settings page. Here you can enter URLs with a corresponding trigger point. As soon as a booking is checked in, checked out, created, edited or canceled, we will send a POST request to the URL you entered. This request contains `trigger` field and all booking data as described in the example `json` on [the booking endpoint](bookings.html) documentation page.

To test your webhooks, we recommend using <a href="https://webhook.site/" target="_blank">https://webhook.site/</a>.

# HTTP responses table
<table>
    <tr><td>200</td><td>OK</td><td>Request is done without any exceptions.</td></tr>
    <tr><td>400</td><td>FAILED</td><td>Not all required parameters/fields are set to execute this request.</td></tr>
    <tr><td>404</td><td>FAILED</td><td>URL incorrect or requested data no longer exists.</td></tr>
    <tr><td>500</td><td>FAILED</td><td>Data you'll send us, can not be parsed.</td></tr>
</table>

# API Endpoints

>### [Availability](availability.html)
>Check for available roomtypes in a predefined date range. This endpoint will return the roomtypes and available Rate plan ID's. [Go to the documentation](availability.html) or jump direct to [Availability check](availability.html#availability-check), [Availability calendar results](availability.html#availability-calendar-results)

>### [Debtors](debtors.html)
>Manage your debtors easily from this endpoint. [Go to the documentation](debtors.html) or jump direct to [List all debtors](#list-all-debtors), [Retrieve a single debtor](#retrieve-a-single-debtor), [Create / Update a debtor](#create--update-a-debtor).

>### [Bookings](bookings.html)
>Via this endpoint it is possible to add and manage bookings. It will create fully automatically the invoice and debtor. Bookings already placed by other connected providers are not editable. [Go to the documentation](bookings.html) or jump direct to [List bookings between dates](bookings.html#list-bookings-between-dates), [List of bookings from specific debtor](bookings.html#list-of-bookings-from-specific-debtor), [Retrieve a single booking](bookings.html#retrieve-a-single-booking), [Create a booking](bookings.html#create-a-booking), [Update a booking](bookings.html#update-a-booking), [Cancel a booking](bookings.html#cancel-a-booking), [Available form parameters](bookings.html#available-form-parameters), [Available channels](bookings.html#available-channels).

>### [Invoices](invoices.html)
>With this endpoint you can manage your invoices, payments and product lines. [Go to the documentation](invoices.html) or jump direct to [List invoices](invoices.html#list-invoices), [Retrieve a single Invoice](invoices.html#retrieve-a-single-invoice), [Add or Update a simple invoice](invoices.html#add-or-update-a-simple-invoice), [Make invoice official by adding an unique ID](invoices.html#make-invoice-official-by-adding-an-unique-id), [Manage product lines](invoices.html#manage-product-lines), [Manage Payments](invoices.html#manage-payments), [Download invoices](invoices.html#download-invoice).

>### [TaxRates](tax-rates.html)
>You can manage your tax rates by this endpoint. Its based on an label and rate itself. Most of the time tax rates stay untouched, but *can* be changed via this API. [Go to the documentation](tax-rates.html) or jump direct to [List all rates](tax-rates.html#list-all-rates), [Create / Update a rate](tax-rates.html#create--update-a-rate), [Delete a single rate](tax-rates.html#delete-a-single-rate).

>### [Roomtypes](roomtypes.html)
>Via this endpoint you can obtain information about your roomtypes and rooms bellow. Changing roomtypes and their rooms need to be done via the MyTourist interface. [Go to the documentation](roomtypes.html) 

>### [Products](products.html)
>Products can be added to your invoices or as selectable additional product inside your booking engine. You can also add product fixed to bookings this becomes handy when you want to add final cleaning to each booking invoice. It is also possible to automatically calculate the price times the number of both guests and/or nights. [Go to the documentation](products.html) or jump direct to [List all products](products.html#list-all-products), [Retrieve a single product](products.html#retrieve-a-single-product), [Create a product](products.html#create-a-product), [Update a product](products.html#update-a-product), [Remove a product](products.html#remove-a-product), [Available form parameters](products.html#available-form-parameters).

>### [ProductCategories](product-categories.html)
>To keep a clean overview of all the product you'll have. You can add a name and color to your categories, they only be visible for you and not for your customers. [Go to the documentation](product-categories.html) or jump direct to [List all product categories](product-categories.html#list-all-product-categories), [Create or update a product category](product-categories.html#create-or-update-a-product-category), [Remove a product category](product-categories.html#remove-a-product-category), [Available form parameters](product-categories.html#available-form-parameters).

>### [PriceRates](price-rates.html)
>Each roomtype has his own set of price rates. You can have as many as you want, you can create eg. weekend arrangements or long and short-stay price rates based on a small amount of criteria. These price rates can be connected to platforms like booking.com. [Go to the documentation](price-rates.html) or jump direct to .. [List all price rates](price-rates.html#list-all-price-rates),[Retrieve a single price rate](price-rates.html#retrieve-a-single-price-rate), [Create a price rate](price-rates.html#create-a-price-rate), [Update a price rate](price-rates.html#create-a-price-rate), [Delete a price rate](price-rates.html#create-a-price-rate).


# API Endpoints (certified access only)
For the endpoints below, your own authentication bearer token in MyTourist must be marked as `certified`. Please <a href="https://mytourist.cloud" target="_blank">contact us</a> or start a ticket to begin the certification process.

### [ObtainBearerToken](obtain-bearer-token.html)
>This function makes it possible to request a bearer token on behalf of your customer in order to use the API. This way your customer does not have to log in to mytourist first to request his or her bearer token. [Go to the documentation](obtain-bearer-token.html)

# Updates

**2021 10 22** - Latitude and Longitude (view and editable) added to the [debtors](debtors.html) endpoint.

**2021 10 19**    
- Added mobile phone number to the endpoint [debtor](debtors.html).
- Full debtor data is also shown on the [bookings](bookings.html) endpoint.
- Expected arrival is retrieve and editable from the [bookings](bookings.html) endpoint.
- We now trigger also the webhook `booking_updated` when an debtor is detached from the booking itself.

**2021 07 07** - We added a new bookings endpoint [List of bookings from specific debtor](#list-of-bookings-from-specific-debtor). Like [List of bookings between dates](#list-of-bookings-between-dates), this function provides a list view of all bookings. But now based on a specific [debtor](debtors.html) ID.

**2021 06 02** - We added `related_bookings` to the response JSON for the endpoints [Retrieve a single booking](bookings.html#retrieve-a-single-booking) and [List bookings between dates](bookings.html#list-bookings-between-dates). This way you can retrieve directly all the related sub-bookings (each booked room has their own booking `id`). Also check which booking is the _main_ booking. In previous version only the main-booking gave back all the invoice data. We'd changed that so either the _main_ of related _sub_ booking return _the_ invoice.