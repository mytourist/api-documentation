---
title: My First Page
layout: default
---

# RESTful API Documentation.
Use the MyTourist API to integrate availability check, debtors and a lot more intro your website or app. MyTourist and your website or app back-end will communicate by sending HTTP requests back and forth. This page provides an overview of the MyTourist API. The topics in the chapter deal with a number of specific aspects of the API. We recommend to read these topics entirely.

If you have any questions about integrating our API, please contact us. We’re happy to help!

## The MyTourist REST API
The API implements a Representational state transfer (REST) architecture. Sounds technical, but it’s really quite easy. It mainly breaks down to HTTP-methods GET, PATCH, POST and DELETE matching the operations to read, update, create and delete.

REST also implies a nice and clean structure for URLs or endpoints. This means you can reach any part of the MyTourist API on https://app.mytourist.com/api/ adding the name of the resource you want to interact with.

## Get an API key
The first thing you need is a API key. Each location/company profile has a API key printed inside the API page found in preferences. Of course it’s very important to keep your API key secure. Do not ever share them. 

## Use at your own risk / No warranty
We validate each request based on basic validation rules and you will operate outside the GUI of MyTourist with all the nice checks inside. You are responsible for the data you will add or change via the API. Each call is logged and kept for at least 24 month. We strongly recommend to test your API first in an dummy company profile before you use your production based company profile. Inside your account settings you are free to manage your company profiles. If your connection causes data to become corrupt, we can charge you to restore a backup of your company profile.

## Authentication
The API key or token must be sent along with each API request, by providing it in the HTTP call’s Authorization header using the Bearer method. For example: a valid Authorization header is `Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6`.

In the example below we use a API key on the GET method of the debtors resource. This method fetches a list of debtors.
```bash
curl -X GET https://app.mytourist.cloud/api/v1/debtors -H 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6'
```

## Start developing, testing and Deploy
By far [Postman](https://www.postman.com/) is a great tool to help you out in the first steps of build any connection with us. This tool enables you to test all GET/POST/PUT/Etc.. requests. We do sometimes host custom API's on our high-end cluster infrastructure for our customers and direct partners. Please contact us for more information.

### [Availability API](availability.html)
Check for available roomtypes in a predefined date range. This endpoint will return the roomtypes and available Rate plan ID's. [Go to the documentation](availability.html)

### [Debtors API](debtors.html)
Manage your debtors easily from this endpoint. [Go to the documentation](debtors.html) or jump direct to [List all debtors](#list-all-debtors), [Retrieve a single debtor](#retrieve-a-single-debtor), [Create / Update a debtor](#create--update-a-debtor).

### [Invoices API](invoices.html)
With this endpoint you can manage your invoices, payments and product lines. [Go to the documentation](invoices.html) or jump direct to [List invoices](invoices.html#list-invoices), [Retrieve a single Invoice](invoices.html#retrieve-a-single-invoice), [Add or Update a simple invoice](invoices.html#add-or-update-a-simple-invoice), [Make invoice official by adding an unique ID](invoices.html#make-invoice-official-by-adding-an-unique-id), [Manage product lines](invoices.html#manage-product-lines), [Manage Payments](invoices.html#manage-payments), [Download invoices](invoices.html#download-invoice).

### [TaxRates API](tax-rates.html)
You can manage your tax rates by this endpoint. Its based on an label and rate itself. Most of the time tax rates stay untouched, but *can* be changed via this API. [Go to the documentation](tax-rates.html) or jump direct to [List all rates](tax-rates.html#list-all-rates), [Create / Update a rate](tax-rates.html#create--update-a-rate), [Delete a single rate](tax-rates.html#delete-a-single-rate).

### [Roomtypes API](roomtypes.html)
Via this endpoint you can obtain information about your roomtypes and rooms bellow. Changing roomtypes and their rooms need to be done via the MyTourist interface. [Go to the documentation](roomtypes.html) 

### [Products API](products.html)
Manage your products. 

### [ProductCategories API](product-categories.html)
Manage your product categories. 


# Coming soon ..
We currently migrating our API to this centralized API. Please come back later..

### [Bookings API](#)
### [PriceRates API](#)


# HTTP responses table
<table>
    <tr><td>200</td><td>OK</td><td>Request is done without any exceptions.</td></tr>
    <tr><td>400</td><td>FAILED</td><td>Not all required parameters/fields are set to execute this request.</td></tr>
    <tr><td>404</td><td>FAILED</td><td>URL incorrect or requested data no longer exists.</td></tr>
</table>
