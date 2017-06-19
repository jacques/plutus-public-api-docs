# Documents

As part of the regulatory requirements, documentation is collected from 
customers as part of the process of KYC / FICA.

## List Documents for a User

```shell
curl "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/documents"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "details": [
    {
      "uuid": "895b2fcc-545f-11e7-8279-67635886d357",
      "file_name": "POID - GOVID - Vin Diesel.pdf",
      "created_at": "2017-06-01 15:33:20"
    },
    {
      "uuid": "8a9e349c-545f-11e7-9a2b-273aed7d1a54",
      "file_name": "POA - GOVID - Vin Diesel.pdf",
      "created_at": "2017-06-01 15:33:45"
    }
  ]
}
```

## Upload a Document

## Download a Document


