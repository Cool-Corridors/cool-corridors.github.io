# GET /score

## Parameters

| name    | type     | data type | description                |
| ------- | -------- | --------- | -------------------------- |
| zipcode | required | int       | zipcode of user's location |
| api_key | required | string    | user's purpleair API key   |

## Responses

| http code | content-type       | response                                                       |
| --------- | ------------------ | -------------------------------------------------------------- |
| `200`     | `application/json` | `JSON object`                                                  |
| `400`     | `application/json` | `{error: "Invalid zipcode"}`                                   |
| `400`     | `application/json` | `{"error": "No sensors found within the range of "x" miles."}` |
| `400`     | `application/json` | `{"error": "No read key or zipcode provided."}`                |

## Example response

```py
   {
       "IAQI": 105,
       "zipcode": 11101
   }
```
