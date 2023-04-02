# Helper Functions

There are a few helper functions that are used throughout the codebase. These functions are defined in `/src/helpers.py`.

It is recommended to  define **new endpoints** in `/src/app.py`, and define any **helper functions** in `/src/helpers.py` to keep the codebase organized.

Our main helper function is `get_info()`. This function takes no input, but returns the same json object that the `/data` endpoint returns. Every other endpoints data is just taken from this larger json object.

We begin by getting the query parameters from the request. 
Query strings are accessed through the flask `request` object.

```py
zipcode = request.args.get("zipcode")
read_key = request.args.get("read_key")
```

If the zipcode or read key is not provided, we return an error message. 

We then convert the zipcode into a latitude and longitude. We use the latitude and longitude to create a binding box around the zipcode. This binding box is used to query the PurpleAir API for sensors within the zipcode. To provide PurpleAir with the bounding box and the many other fields we want, we use the `requests.get()` function from the requests library. The function allows us to pass an url and a dictionary of query parameters. 

```py
# base url
url = "https://www.api.purpleair.com/v1/sensors/"
# dictionary of parameters we want to access
params = {
    "fields": "sensor_index,latitude,longitude,temperature,IAQI",
    "key": read_key,
    "nwlat": nwlat,
    "nwlng": nwlng,
    "selat": selat,
    "selng": selng,
}
response = requests.get(url, params=params)
```

If we are to move away from using purpleair as our data source, we can simply change the url and the contents of the `params` dictionary.

If no sensors are found, we return an error message. Otherwise, we take the returned sensor data and format it accordingly to be returned.

To send data back as a json object, we use the `jsonify()` function from the flask library. 

```py
@api.route("/example")
def example():
    return jsonify({
        "IAQI": IAQI,
        "zipcode": zipcode
    })
```