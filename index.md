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

## Authentication
The API key or token must be sent along with each API request, by providing it in the HTTP call’s Authorization header using the Bearer method. For example: a valid Authorization header is `Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6`.

In the example below we use a API key on the GET method of the debtors resource. This method fetches a list of debtors.
```bash
curl -X GET https://app.mytourist.cloud/api/v1/debtors -H "Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6"
```

# Complite list of endpoints.

### [Availability API](availability.html)
Check for available roomtypes in a predefined date range. This enpoint will return the roomtypes and available Rate plan ID's. [Go to the documentation](availability.html)

### [Bookings API](bookings.html)
Get booking by ID's and change their status, attach/dettach debtors, manage individual guests and select the right price rates. [Go to the documentation](bookings.html)

### [Debtors API](debtors.html)
Obtain a single Debtor or obtain a list of your Debtors based on some filtering. You can also manage their address and contact information. [Go to the documentation](debtors.html)

### [Invoicing API](invoicing.html)
List invoices, manage products and logies, set right VAT Tax id's and register payments. [Go to the documentation](invoicing.html)

### [Products API](products.html)
List and show single products. Manage their names and pricing. Attach them to an price rate as fixed product or attach product to an booking. [Go to the documentation](products.html)

### [PriceRates API](price-rates.html)


### [Roomtypes](roomtypes.html)