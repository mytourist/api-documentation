---
title: Invoices
layout: default
---
### [Back to overview](index.html#start-developing-testing-and-deploy)
---
# Invoices API
Invoices are (by default) automatically created when a booking is added to MyTourist. Then the logies price, tourist tax and fixed products will be automatically calculated. But you can also create single invoices witch has no relations with any of your bookings. This can be useful when you'll have additional business aspects. Think as `boat or bike rentals`,`bars` or `activities`.

**Possibilities described below:** [List invoices](#list-invoices), [Register a payment](#register-payment), [Remove a payment](#remove-payment)

## List invoices
Be aware the `from` and `until` parameters are required to prevent heavy server load on fetching big loads of data. You can fetch a maximum of 36 days each time.

**GET** `https://app.mytourist.cloud/api/v1/invoices?from={DATE}&until={DATE}`

**Query Parameters**
<table>
    <tr><td>from</td><td>required</td><td>DATE: YYYYMMDD</td></tr>
    <tr><td>until</td><td>required</td><td>DATE: YYYYMMDD</td></tr>
    <tr><td>type</td><td>optional</td><td>`proforma`,`invoice`,`creditinvoice`</td></tr>
</table>

**Types of invoices**
<table>
    <tr><td>proforma</td><td>Invoice is not final jet. Changed can be made during this state and this invoice is fully removable.</td></tr>    
    <tr><td>invoice</td><td>These invoices are internally marked as send to the customer. Also those invoices will always have a registration in your administration.</td></tr>    
    <tr><td>creditinvoice</td><td>These invoices are credited and linked to the invoice.</td></tr>
</table>

**Financial states**
<table>
    <tr><td>concept</td><td>The proforma invoice hasn't been send jet. So the total amount to pay is still in concept.</td></tr>
    <tr><td>open</td><td>Invoice has been send to the guest, now the total amount to pay is waiting for payment(s).</td></tr>
    <tr><td>payed</td><td>The invoice has been fully paid.</td></tr>
    <tr><td>credited</td><td>The total amount to pay is credited with an extra credit invoice.</td></tr>
</table>

**Product Line types**
<table>
    <tr><td>logies</td><td>This line will calculated automatically by MyTourist. If you want to force this amount, you'll need to set this amount inside the booking.</td></tr>
    <tr><td>product</td><td>Can be a product managed inside MyTourist or an manually added product.</td></tr>
</table>

**JSON example Result**
```json
{
   "id":"P1020077",
   "invoice_id":null,
   "language":"en",
   "type":"proforma",
   "financial_state":"open",
   "debtor_id":"23192010282",
   "footnote":"",
   "product_lines":[
      {
         "id":"2319201102165", // Line ID
         "type":"logies",
         "number":1,
         "description":"Doubleroom with balcony - \
         7 night(s) - 2 guest(s) - 04\/11'20 11\/11'20",
         "price_incl_vat":"560.00",
         "price_excl_vat":"504.50",
         "tax_amount":"55.50",
         "tax_rate":"11.00"
      },
      {
         "id":"2319201102164",
         "product_id":null,  // Manually created
         "type":"product",
         "number":8,
         "description":"Bottle of red wine",
         "price_incl_vat":"352.00",
         "price_excl_vat":"317.12",
         "tax_amount":"34.88",
         "tax_rate":"11.00",         
      }
   ],
   "tourist_tax":{
      "amount":"0.00",
      "based_on_guests":0,
      "outdated":false
   },
   "vat_lines":{
      "11":90.38 // Rate + value
   },
   "payments":[
      {
         "id":"23192011021",
         "payment_method":"bank_card",
         "amount":"10.00",
         "description":""
      }
   ],
   "financial":{
      "has_amount_to_pay":true,
      "custom_logies_price":false,
      "deposit_amount":"112.00",
      "deposit_open_to_pay":102,
      "total_amount_incl_vat":912,
      "total_amount_excl_vat":821.62,
      "total_payed":10
   }
}
```

## Add or Update a **simple invoice**
Simple invoices are invoices created *without any bookings attached.* This becomes handy when you sell/rent products other than your customers staying in your accommodation. In fact the technic itself is exactly the same, the only difference is that the automatically price calculation based on price rates and tourist taxes is not activated. 

The endpoints will return always the created or updated invoice (HTTP 200)

**POST (Create)**    
`https://app.mytourist.cloud/api/v1/invoices`   
**POST (Update)**    
`https://app.mytourist.cloud/api/v1/invoices/{INVOICE_ID}`   
**DELETE (Removes proforma invoices)**   
`https://app.mytourist.cloud/api/v1/invoices/{INVOICE_ID}`      

**POST (Add Invoice ID, Make final Invoice)**    
`https://app.mytourist.cloud/api/v1/invoices/add-invoice-id/{INVOICE_ID}`   
*Your freshly created invoice has always the `proforma` type. Call the URL above to attach an invoice ID from your administration. The state will automatically change from proforma to invoice state. An invoice is not removable after this action.* 

**Parameters**
<table>
    <tr><td>debtor_id</td><td>optional</td><td></td></tr>
    <tr><td>language</td><td>optional</td><td>Account standard or `nl/es/en/fr`</td></tr>
    <tr><td>footnote</td><td>optional</td><td>Account standard or own text</td></tr>
    <tr><td>invoiced_at</td><td>optional</td><td>DATE: YYYYMMDD, (will always be updated when invoice ID is attached afterwards)</td></tr>
</table>

## Manage product lines
You can use the pre defined products you have already been added in MyTourist or set your own product line in this invoice. Both add and update calls will return (HTTP 200) the full result of the line you just created/updated.

**POST (Add)**    
`https://app.mytourist.cloud/api/v1/invoices/{INVOICE_ID}/lines`    

**POST (Update)**    
`https://app.mytourist.cloud/api/v1/invoices/{INVOICE_ID}/lines/{LINE_ID}`    

**Parameters when no product_id attached**
<table>
   <tr><td>product_id</td><td>optional</td><td>Integer</td><td>@product_id  <a href="#">Products API</a></td></tr>
   <tr><td>number</td><td>optional</td><td>Integer</td><td>Number of items (Autom. +1 when adding same product twice or more)</td></tr>
   <tr><td>price_incl</td><td>required*</td><td>Float</td><td>Price per item incl. VAT</td></tr>
   <tr><td>description</td><td>required*</td><td>String</td><td></td></tr>
   <tr><td>tax_id</td><td>optional</td><td>Integer</td><td>@tax_id <a href="#">Tax rates API</a></td></tr> 
</table>

\* only required on lines without `product_id` attached.




## Manage Payments

## Send invoice by email

## Download invoice