---
title: Property
layout: default
---

### [Back to overview](index.html#api-endpoints)

# Property
This GET-only endpoint returns general property address data.

**GET** `https://app.mytourist.cloud/api/v1/property`

**Example result**
```json
    {
        "name": "MyTourist BV",
        "street": "Meetkamp 4",
        "zipcode": "7078AJ",
        "city": "Megchelen",
        "country": "NL",
        "website": "mytourist.cloud",
        "email": "info@mytourist.cloud",
        "phone": null,
        "mobile": "06xxxxxxxx",
        "currency": "EUR",
        "iban_name": "MyTourist",
        "iban": "NL00AAAA0123456",
        "bic": "NLMT01",
        "iban_alt_name": null,
        "iban_alt": null,
        "bic_alt": null,
        "company_id": "12345678",
        "registration_id": "987654321",
        "custom_coordinates": false
    }
```
