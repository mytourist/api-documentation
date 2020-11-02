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
        "id":"81912063",
        "type":"double",
        "number_of_rooms":1,
        "name":"Doubleroom Deluxe with balcony",
        "description":"Our best room with an amazing view over the city!",
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
            },
            {
                "id":"82010274",
                "name":"Bubbles arrangement - Long weekend",
            }
        ]
        
    },
    {
        ...
    }
]
```

## Create or update an roomtype
At this point we **do not** support any changes made by the API. This because roomtypes and individual rooms are most likely connected to external providers and their price rates. 