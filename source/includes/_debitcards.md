# Debitcards

The system provides interfaces for management of Prepaid debit cards.  Not all prepaid
debit card providers provide access to real time transactional information and card
balances.

<aside class="notice">
On test we do not provide an idea of the balances for a card.  This will be added
in the near future once the mock card management implementation has been
completed.
</aside>

## List Debit Cards allocated to a User

```shell
curl "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "details": [
        {
            "account_number": "53230000006",
            "uuid": "b5c0b0b8-9c9d-11e4-afbc-f3a644f22402",
            "description": "Jacques Freedom MasterCard",
            "account_type": "debitcard",
            "currency": "710",
            "balance": "12268",
            "available_balance": "12268",
            "masked_cardnumber": "123456XXXXXX0434"
        },
        {
            "account_number": "53230966296",
            "uuid": "e7d03afc-27f7-11e5-b016-bba1668567bc",
            "description": "Jacques Diamond MasterCard",
            "account_type": "debitcard",
            "currency": "710",
            "balance": "98765",
            "available_balance": "9966",
            "masked_cardnumber": "123456XXXXXX0657"
        }
    ]
}
```

This endpoint retrieves a collection of debit cards belonging to the specific user.

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards`

### URL Parameters

Parameter | Description
--------- | -----------
USER | The UUID of the user whose debit cards you would like to retrieve

### Response Result Set

Parameter | Type | Description
--------- | ---- | -----------
uuid | string (36) | UUID of the wallet
account_number | integer | Account number for the debit card (this is not the account number on the debit card but our internal identifier)
description | string (64) | Description of the wallet (i.e Firstname's Debit Card)
account_type | enum | `debitcard` for debit card
currency | integer | ISO4217 Code Number
balance | integer | Amount of money in cents in the ledger / actual balance (including items with a preauth)
available_balance | integer | Amount of money in cents in the available balance (excluding preauths)
masked_cardnumber | varchar(16) | Masked card number

There will be some changes for differences between available / reserved / actual balance on cards coming shortly in the implementation.
Need to also display the sponsoring bank for a debit card as well (Bank A vs Bank B).

## List Debit Card allocated to a User

```shell
curl "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/e7d03afc-27f7-11e5-b016-bba1668567bc"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "details": {
        "account_number": "53230966296",
        "uuid": "e7d03afc-27f7-11e5-b016-bba1668567bc",
        "description": "Jacques Diamond MasterCard",
        "account_type": "debitcard",
        "currency": "710",
        "balance": "98765",
        "available_balance": "9966",
        "masked_cardnumber": "123456XXXXXX0657"
    }
}
```

This endpoint retrieves the specified debit card belonging to the specific user.

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards/<CARD>`

### URL Parameters

Parameter | Description
--------- | -----------
USER | The UUID of the user whose debit cards you would like to retrieve
CARD | The UUID of the debit cards you would like to retrieve

### Response Result Set

Parameter | Type | Description
--------- | ---- | -----------
uuid | string (36) | UUID of the wallet
account_number | integer | Account number for the debit card (this is not the account number on the debit card but our internal identifier)
description | string (64) | Description of the wallet (i.e Firstname's Debit Card)
account_type | enum | `debitcard` for debit card
currency | integer | ISO4217 Code Number
balance | integer | Amount of money in cents in the ledger / actual balance (including items with a preauth)
available_balance | integer | Amount of money in cents in the available balance (excluding preauths)
masked_cardnumber | varchar(16) | Masked card number

There will be some changes for differences between available / reserved / actual balance on cards coming shortly in the implementation.
Need to also display the sponsoring bank for a debit card as well (Bank A vs Bank B).

## Fetch mini statement for a debit card

```shell
curl "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/996fdda6-c4d7-4527-b14d-a0b43a149f97/ministatement"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards/<CARD>/ministatement`

### URL Parameters

Parameter  | Type | Description
---------  | ---- | -----------
USER | The UUID of the user whose debit card you would like to retrieve
CARD | The UUID of the users debit card you would like to view the transactions for

## Fetch statement for a Debit Card

```shell
curl "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/996fdda6-c4d7-4527-b14d-a0b43a149f97/statement/30"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards/<CARD>/statement/<DAYS>`

### URL Parameters

Parameter  | Type | Description
---------  | ---- | -----------
USER | The UUID of the user whose debit card you would like to retrieve
CARD | The UUID of the users debit card you would like to view the transactions for
DAYS | The number of days you want a statement for 30 / 60 / 90 days

## Fetch transaction history for a Debit Card

```shell
curl "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/996fdda6-c4d7-4527-b14d-a0b43a149f97/transactions"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

## Example of customer with no transactions in the past 180 days

```json
{
  "status": "ok",
  "details": {
    "account": {
      "account_number": "53231234567",
      "uuid": "4f9a869e-5cd3-11e7-bf63-7396dac0ab8a",
      "description": "Vimala Debitcard",
      "account_type": "debitcard",
      "currency": "710",
      "balance": 5000,
      "available_balance": 5000,
      "masked_card_number": "123456XXXXXX2345"
    },
    "transactions": [
        {
            "txn_ref": "jcb7aqlm",
            "description": "Admin fee for primary card for year 2017 and month of June",
            "debit": -2500,
            "credit": 0,
            "processed_at": "2017-06-30 23:13:16",
            "cleared_at": "2017-06-30 23:13:16"
        },
        ...
    ]
  }
}
```

## Example of customer with no transactions in the past 90 days

```json
{
  "status": "ok",
  "details": {
    "account": {
      "account_number": "53231234567",
      "uuid": "4f9a869e-5cd3-11e7-bf63-7396dac0ab8a",
      "description": "Gandalf Debitcard",
      "account_type": "debitcard",
      "currency": "710",
      "balance": 0,
      "available_balance": 0,
      "masked_card_number": "123456XXXXXX1234"
    },
    "transactions": []
  }
}
```

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards/<CARD>/transactions`

### URL Parameters

Parameter  | Type | Description
---------  | ---- | -----------
USER | The UUID of the user whose debit card you would like to retrieve

## Report debit card as being lost / stolen

```shell
curl -X POST "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/996fdda6-c4d7-4527-b14d-a0b43a149f97/stopcard"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "message": "Card has been stopped."
}
```

This endpoint allows for stopping of a debit card belong to a user.  You can at a later stage issue a replacement card to the user.

<aside class="notice">
Please note once a card is marked to the Postilion Hotcard List it cannot be reversed.  A new card would need to be issued in this case.
</aside>

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards/<CARD>/stopcard`

### URL Parameters

Parameter  | Type | Description
---------  | ---- | -----------
USER | The UUID of the user whose debit card you would like to retrieve
CARD | The UUID of the users debit card you would like to view the transactions for

## Issue a Debit Card

```shell
curl -X POST "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/issue"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
  -d '{"cardnumber":"12345678901234","sequence_number":"123456"}'
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "details": {
        "account_number": "53231672318",
        "uuid": "c12451bc-66fd-11e7-8b56-eea0a39cd77b",
        "masked_card_number": "531162XXXXXX5932"
    }
}
```

This endpoint allows for issuing of a debit card to a user.  Additional debit cards are added as secondary cards on the users profile.

### HTTP Request

`POST https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards`

### URL Parameters

Parameter  | Type | Description
---------  | ---- | -----------
USER | The UUID of the user to whom you wish to issue a debit cards

### Response Result Set

Parameter | Type | Description
--------- | ---- | -----------
uuid | string (36) | UUID of the wallet
account_number | integer | Account number for the debit card (this is not the account number on the debit card but our internal identifier)
masked_cardnumber | varchar(16) | Masked card number

## Replace a Debit Card


```shell
curl -X POST "https://127.0.0.1.xip.io/api/v1/users/d19bff36-4733-11e5-946b-9ba904d8238e/debitcards/e7d03afc-27f7-11e5-b016-bba1668567bc/replace"
  -H "Authorization: Token token=YOURTOKEN"
  -H "Content-Type: application/json"
  -d '{"cardnumber":"12345678901234","sequence_number":"123456"}'
```

```json
{
    "status": "ok",
    "details": [
        {
            "account_number": "53230966296",
            "uuid": "e7d03afc-27f7-11e5-b016-bba1668567bc",
            "description": "Jacques Debit Card",
            "account_type": "debitcard",
            "currency": "710",
            "balance": "98765",
            "available_balance": "9966",
            "masked_cardnumber": "123456XXXXXX0657"
        }
    ]
}
```

This endpoint allows for replacing of a debit card belong to a user.

<aside class="notice">
Dependant on which sponsor bank is being utilised, cards a user has may be restricted to a ringfenced group.  If an error occurs on replacement, contact the Call Centre.
</aside>

### HTTP Request

`GET https://127.0.0.1.xip.io/api/v1/users/<USER>/debitcards/<CARD>/replace`

### URL Parameters

Parameter  | Type | Description
---------  | ---- | -----------
USER | The UUID of the user whose debit card you would like to retrieve
CARD | The UUID of the users debit card you would like to report as lost / stolen

### Response Result Set

Parameter | Type | Description
--------- | ---- | -----------
