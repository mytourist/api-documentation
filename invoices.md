# Invoices API
Invoices are (by default) automatically created when a booking is added to MyTourist.


## Create single invoice __without__ a booking attached.
<span style="border:1px solid #f1f1f1; padding:3px;"><b>GET</b> https://app.mytourist.cloud/api/invoice/{id}</span>

## States of invoices.
<table>
    <tr><td>proforma</td><td>Invoice is not final jet. Changed can be made during this state and this invoice is fully removable.</td></tr>    
    <tr><td>invoice</td><td>These invoices are internally marked as send to the customer. Also those invoices will always have a registration in your administration.</td></tr>    
    <tr><td>creditinvoice</td><td>These invoices are credited and linked to the invoice.</td></tr>    
    <tr><td>deleted</td><td>Proforma invoices witch has been deleted, accessible by the API but not found in your administration.</td></tr>
</table>

## Financial states
<table>
    <tr><td>concept</td><td>The proforma invoice hasn't been send jet. So the total amount to pay is still in concept.</td></tr>
    <tr><td>open</td><td>Invoice has been send to the guest, now the total amount to pay is waiting for payment(s).</td></tr>
    <tr><td>payed</td><td>The invoice has been fully paid.</td></tr>
    <tr><td>credited</td><td>The total amount to pay is credited with an extra credit invoice.</td></tr>
</table>