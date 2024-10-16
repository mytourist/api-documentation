---
title: Debtors
layout: default
---
### [Back to overview](index.html#api-endpoints)
---
# Roomtypes API
Roomtypes are groups of rooms like eg. "Doubleroom" this roomtype can contains "Room 6 1th. floor" & "Room 4 3th floor". B&B's has often not multiple rooms and most of the time their roomtype name is exact the same as the room one.

## List all roomtypes
Retreive all `roomtypes` created in MyTourist. The results will included all attached price `rates`.

**GET** `https://app.mytourist.cloud/api/v1/roomtypes`

**Query Parameters**
<table>
    <tr><td>language</td><td>optional</td><td>ISO 639-1</td></tr>
</table>

**Example results**
```JSON
[
    {
        "id":"81912063",
        "type":"double",
        "number_of_rooms":1,
        "name":"Doubleroom Deluxe with balcony",
	    "square_meters":20,
        "amenities": [
            "safe",
            "sofa",
            "shampoo",
            "hair_dryer",
            "bubble_bath",
            "conditioner",
            "seating_area",
            "bed_power_outlet",
            "electric_blankets"
        ],
        "public_names": {
            "nl": "Luxe Tweepersoonskamer",
            "en": "Luxury Double Room",
            "de": "..",
            "pt": ".."
        },
        "public_descriptions": {
            "nl": "Deze kamer is van alle luxe voorzien! Geniet van opstaan tot bedtijd van de prachtige uitzichten...",
            "en": "This room is equipped with every luxury! Enjoy getting up to bedtime from the beautiful views...",
            "de": "..",
            "pt": ".."
        },
        "default_picture": "https://cdn.mytourist.cloud/rooms/medium/21MTYZAvJBzlaJjqkPGpmhuxPewWqe0yHl3RY2W4EryoYqUh11iSGwXFLrjxK0hEx3ia.jpg",
        "pictures": [
            "https://cdn.mytourist.cloud/rooms/medium/21MTWNYBrsaKFjKiOm6bFuxDxeBADX2lOBR2QYcd3NmlvSD2mSAnHrLZsf4wWA349fO4.jpg",
            "https://cdn.mytourist.cloud/rooms/medium/21MTYZAvJBzlaJjqkPGpmhuxPewWqe0yHl3RY2W4EryoYqUh11iSGwXFLrjxK0hEx3ia.jpg",
            "https://cdn.mytourist.cloud/rooms/medium/21MTMTsinPaHlm39UEz63xG1lJzkz3ZakoncxsVZAwUb9q6h8u5NOWU1eHPwQHjpzi7K.jpg",
            "https://cdn.mytourist.cloud/rooms/medium/21MTnsBJS6RHfWvegrY6GhAzFHMdsanddCdNtmnYyDwcmKlT3XiBGr8ehxmptcU88sNp.jpg"
        ],
        "rooms": [
            {
                "id":"66118888",
                "name": "Room 1"
            },
            {
                "id":"66118777",
                "name": "Room 4"
            },
            {
                "id":"66118666",
                "name": "Room 8"
            }
        ],
        "rates":[
            {
                "id":"66118004",
                "name":"Conform arrangement",
                "public_names": {
                    "nl": "Standaardprijs 2 personen",
                    "en": "Standard price 2 persons",
                    "de": "Standardpreis 2 Personen",
                    "pt": "Preço padrão 2 pessoas"
                }
            },
            {
                "id":"82010274",
                "name":"Bubbles arrangement - Long weekend",
                "public_names": {
                    "nl": "Standaardprijs 2 personen",
                    "en": "Standard price 2 persons",
                    "de": "Standardpreis 2 Personen",
                    "pt": "Preço padrão 2 pessoas"
                }
            }
        ]
        
    },
    {
        ...
    }
]
```
