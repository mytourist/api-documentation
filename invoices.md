# Invoices API
Invoices are (by default) automatically created when a booking is added to MyTourist. But you can also create single invoices witch has no relations with any of your bookings. This can be useful when you'll have additional business aspects. Think as `boat or bike rentals`,`bars` or `activities`.

## List your invoices
Be aware parameters are required to prevent heavy server load on fetching big loads of data.

**GET** `https://app.mytourist.cloud/api/v1/invoices?from={DATE}&until={DATE}`

**Query Parameters**
<table>
    <tr><td>from</td><td>required</td><td>ISO 639-1</td></tr>
    <tr><td>until</td><td>required</td><td>ISO 639-1</td></tr>
    <tr><td>type</td><td>optional</td><td>`proforma`,`invoice`,`creditinvoice`</td></tr>
</table>


## Create single invoice __without__ a booking attached.
<span style="border:1px solid #f1f1f1; padding:3px;"><b>GET</b> https://app.mytourist.cloud/api/invoice/{id}</span>

## Type of invoices.
<table>
    <tr><td>proforma</td><td>Invoice is not final jet. Changed can be made during this state and this invoice is fully removable.</td></tr>    
    <tr><td>invoice</td><td>These invoices are internally marked as send to the customer. Also those invoices will always have a registration in your administration.</td></tr>    
    <tr><td>creditinvoice</td><td>These invoices are credited and linked to the invoice.</td></tr>
</table>

## Financial states
<table>
    <tr><td>concept</td><td>The proforma invoice hasn't been send jet. So the total amount to pay is still in concept.</td></tr>
    <tr><td>open</td><td>Invoice has been send to the guest, now the total amount to pay is waiting for payment(s).</td></tr>
    <tr><td>payed</td><td>The invoice has been fully paid.</td></tr>
    <tr><td>credited</td><td>The total amount to pay is credited with an extra credit invoice.</td></tr>
</table>