# Cool Corridors API

Welcome to the Cool Corridors API! 

This project aims to inform NYC communities of Air Quality in their neighborhoods
using our very own IAQI score!

## RapidAPI Users

If you are a RapidAPI user, you can use the following url to access the API: https://coolcorridors.p.rapidapi.com. RapidAPI provides a gateway url that allows users to acces the API from within RapidAPI's website. 

## Creating a new API endpoint

All endpoints are defined inside `/src/app.py`. To create a new endpoint, simply create a new function and add a new route to the `app` object. 

For example, to create a new endpoint called `/test`, you would do the following:

```py
@app.route("/test")
def test():
    return "Hello World!"
```

This creates a new endpoint called `/test` that returns the string "Hello World!" when called.

The function name can be anything, but it is recommended to keep it consistent with the endpoint name.

Flask offers many different ways to return data. For more information, see the [Flask documentation](https://flask.palletsprojects.com/en/2.2.x/quickstart/). 

You can:
- return a string literal
- return a json object
- render a template (html file)
- redirect to a different route or url
- return a file
- etc...

## Helper Functions

There are a few helper functions that are used throughout the codebase. These functions are defined in `/src/helpers.py`.

It is recommended to  define new endpoints in `/src/app.py`, and define any helper functions in `/src/helpers.py` to keep the codebase organized.

Our main helper function is `get_info()`. This function does most of the heavy lifting for the API endpoints. 

We begin by getting the query parameters from the request. 
Query strings are accessed through the flask `request` object.

```py
zipcode = request.args.get("zipcode")
read_key = request.args.get("read_key")
```

If the zipcode or read key is not provided, we return an error message. 

We then convert the zipcode into a latitude and longitude. We use the latitude and longitude to create a binding box around the zipcode. This binding box is used to query the PurpleAir API for sensors within the zipcode. To provide PurpleAir with the bounding box and the many other fields we access, we use the `requests.get()` function from teh requests library. The function allows us to pass in a url and a dictionary of query parameters. 

```py
url = "https://www.api.purpleair.com/v1/sensors/"
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
@app.route("/example")
def example():
    return jsonify({
        "IAQI": IAQI,
        "zipcode": zipcode
    })
```
