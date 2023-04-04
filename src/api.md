# API

The API is hosted by [render.com](https://render.com/). The base url is [here](https://cool-corridors-api-service.onrender.com). All other endpoints are relative to this url. The GitHub link for the API is [here](https://github.com/Cool-Corridors/cool-corridors-API).

## Folder Structure
```bash
.
├── LICENSE
├── README.md
├── requirements.txt
├── run.py
└── src
    ├── app.py
    ├── helpers.py
    ├── __init__.py
    ├── zip_lat_long.csv
    └── zip_lat_long.json
```
## Data

PurpleAir returns their data as a json object formatted as such:

```json
{
    // metadata
    "fields": [
        "name",
        "location",
        "pm2.5",
        "temperature",
        ...
    ],
    "location_types": [
        "outside",
        "inside"
    ],
    // data is a list of lists. each list/array in data is the data for a certain sensor
    "data": [
        [
            1284751,
            "City College",
            56,
            ...
        ],
        ...
    ]

}

```

The `/score` endpoint will take the above json and format it into the following python dictionary:

```py
    {
        "zip_code": int,
        "pm2.5": float,
        "pm2.5_30minute": float,
        "pm2.5_60minute": float,
        "pm2.5_1week": float,
        "temperature": int,
        "IAQI": dict{
            "score": int,
            "category": str
            }
    }
```

The frontend will then take this json object and embed data into components in the HTML. Data is subject to change as we add different functionalities.