# Endpoints

There are currently 4 endpoints in the API. They are documented here with their expected values and reponse.

<!-- <code>GET</code> <code><b>/data?zipcode={zipcode}&read_key={read_key}</b></code> -->

## GET /data

> ### Parameters

| name    | type     | data type | description                |
| ------- | -------- | --------- | -------------------------- |
| zipcode | required | int       | zipcode of user's location |
| api_key | required | string    | user's purpleair API key   |

> ### Responses

| http code | content-type       | response                                                       |
| --------- | ------------------ | -------------------------------------------------------------- |
| `200`     | `application/json` | `JSON object`                                                  |
| `400`     | `application/json` | `{error: "Invalid zipcode"}`                                   |
| `400`     | `application/json` | `{"error": "No sensors found within the range of "x" miles."}` |
| `400`     | `application/json` | `{"error": "No read key or zipcode provided."}`                |

> ### Example response

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

<code>GET</code> <code><b>/score?zipcode={zipcode}&read_key={read_key}</b></code>

### Parameters

| name    | type     | data type | description                |
| ------- | -------- | --------- | -------------------------- |
| zipcode | required | int       | zipcode of user's location |
| api_key | required | string    | user's purpleair API key   |

### Responses

| http code | content-type       | response                                                       |
| --------- | ------------------ | -------------------------------------------------------------- |
| `200`     | `application/json` | `JSON object`                                                  |
| `400`     | `application/json` | `{error: "Invalid zipcode"}`                                   |
| `400`     | `application/json` | `{"error": "No sensors found within the range of "x" miles."}` |
| `400`     | `application/json` | `{"error": "No read key or zipcode provided."}`                |

### Example response

```py
   {
       "IAQI": 105,
       "zipcode": 11101
   }
```

<code>GET</code> <code><b>/descriptor?zipcode={zipcode}&read_key={read_key}</b></code>

### Parameters

| name    | type     | data type | description                |
| ------- | -------- | --------- | -------------------------- |
| zipcode | required | int       | zipcode of user's location |
| api_key | required | string    | user's purpleair API key   |

### Responses

| http code | content-type       | response                                                       |
| --------- | ------------------ | -------------------------------------------------------------- |
| `200`     | `application/json` | `JSON object`                                                  |
| `400`     | `application/json` | `{error: "Invalid zipcode"}`                                   |
| `400`     | `application/json` | `{"error": "No sensors found within the range of "x" miles."}` |
| `400`     | `application/json` | `{"error": "No read key or zipcode provided."}`                |

### Example response

```py
   {
       "description": "Good",
       "zipcode": 11101
   }
```

<code>GET</code> <code><b>/color?zipcode={zipcode}&read_key={read_key}</b></code>

### Parameters

| name    | type     | data type | description                |
| ------- | -------- | --------- | -------------------------- |
| zipcode | required | int       | zipcode of user's location |
| api_key | required | string    | user's purpleair API key   |

### Responses

| http code | content-type       | response                                                       |
| --------- | ------------------ | -------------------------------------------------------------- |
| `200`     | `application/json` | `JSON object`                                                  |
| `400`     | `application/json` | `{error: "Invalid zipcode"}`                                   |
| `400`     | `application/json` | `{"error": "No sensors found within the range of "x" miles."}` |
| `400`     | `application/json` | `{"error": "No read key or zipcode provided."}`                |

### Example response

```py
   {
       "color": "0xFF00FF",
       "zipcode": 11101
   }
```
