# Debtors API

## List all debtors
**GET** `https://app.mytourist.cloud/api/v1/debtors`

## Retrieve a single debtor
**GET** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

## Create or update a debtor
You can easally create a new debtor by calling the following URL by the `POST` method. When you want to update any debtor you'll need to use the `PUT` method with the **complete** form data and `debtor_id` inside the URL. Both endpoints will return the saved debtor as their (200 HTTP response) result.

**POST** `https://app.mytourist.cloud/api/v1/debtors`    
**PUT** `https://app.mytourist.cloud/api/v1/debtors/{DEBTOR_ID}`

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
curl --location --request POST 'https://app.mytourist.cloud/api/v1/debtors' \
--header 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6' \
--form 'first_name=Max' \
--form 'last_name=Musterman' \
--form 'company_name=MyTourist' \
--form 'company_chamber_id=123456789'
```