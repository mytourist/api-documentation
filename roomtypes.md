---
title: Debtors
layout: default
---
### [Back to overview](index.html#start-developing-testing-and-deploy)
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
        "id":"81912063",                            // ID of the roomtype
        "type":"double",                            // single,double,appartement etc..
        "number_of_rooms":1,                        // Indiviual rooms under this roomtype.
        "name":"Doubleroom Deluxe with balcony",
        "description":"Our best room with an amazing view over the city!",
        "rates":[
            {
                "id":"66118004",                    // ID of the price rate
                "name":"Conform arrangement",
            },
            {
                "id":"82010274",                    // ID of the price rate
                "name":"Bubbles arrangement - Long weekend",
            }
        ]
    },
    {
        ...
    }
]
```