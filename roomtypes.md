# Roomtypes API
Retreive all `roomtypes` created in MyTourist. The results will included all attached price `rates`.

**GET** `https://app.mytourist.cloud/api/v1/roomtypes`

**Query Parameters**
<table>
    <tr><td>language</td><td>optional</td><td>ISO 639-1</td></tr>
</table>

**Example**
```bash
curl --location --request GET 'https://app.mytourist.cloud/api/v1/roomtypes' \
--header 'Authorization: Bearer $2y$10$FP4s6cunWIGSjohTBDRO5eXNQAxWeG1.OxySTKv6FVVbaVhgwh7I6'
```

**Results**
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