# Debtors API
This API endpoint let you manage your debtors. [Parameters](#available-parameters) can be found on the very end of this page.

## List all debtors
**GET** `https://app.mytourist.cloud/api/v1/debtors`

## Retrieve a single debtor
**GET** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

## Create a debtor
You can easally create a new debtor by calling the following URL by the `POST` method. This endpoints will return the saved debtor as their (200 HTTP response) result.

**POST** `https://app.mytourist.cloud/api/v1/debtors`    

**Example creating a Debtor**
```bash
curl --location --request POST 'https://app.mytourist.cloud/api/v1/debtors' \
--header 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6' \
--form 'first_name=Max' \
--form 'last_name=Musterman' \
--form 'company_name=MyTourist' \
--form 'company_chamber_id=123456789'
```

## Update a debtor
When you want to update any debtor you'll need to use the same `POST` method with the `debtor_id` appended to the URL. 

**POST** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

_You can do either rewrite the whole block of parameters and push it back or just put the fields you want to change. When you don't call particular paramaters we won't do anything and ignoring this parameter. When you put a parameter as `null` we will emtpying this parameter inside our database also._

```bash
curl --location --request POST 'http://localhost:8004/api/v1/debtors/82010288' \
--header 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6' \
--form 'first_name=Max' \
--form 'address=Previewstreet 66 Block A' \
--form 'note=This is an test note'
```


**Available Parameters**
<table>
    <tr><td>first_name</td><td>required</td><td>When POST</td></tr>    
    <tr><td>last_name</td><td>required</td><td>When POST</td></tr>
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