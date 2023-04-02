# GET /data

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
       "zip_code": 11101,
       "pm2.5": 2.4,
       "pm2.5_30minute": 2.4,
       "pm2.5_60minute": 2.6,
       "pm2.5_1week": 3.4,
       "temperature": 52,
       "IAQI": {
           "score": 105,
           "descriptor": "Good"
          }
   }
```
