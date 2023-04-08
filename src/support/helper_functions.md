# Helper Functions

There are a few helper functions that are used throughout the codebase. These functions are defined in `/src/helpers.py`.

It is recommended to  define **new endpoints** in `/src/app.py`, and define any **helper functions** in `/src/helpers.py` to keep the codebase organized.

Our main helper function is `get_info()`. This function takes no input, but returns the same json object that the `/data` endpoint returns. Every other endpoints data is just taken from this larger json object.

The function does the following:

1. Obtain `zip_code` and `api_key`

    Query strings are accessed through the flask `request` object.

    ```py
    zipcode = request.args.get("zipcode")
    read_key = request.args.get("read_key")
    ```
    <span class="caption">A query string is anything after a `?` in the url. They have a name, value, and separated by a `&`. </span>

    If the zipcode or read key is not provided, we return an error message. 

2. Convert zipcode into lat/long and create binding box.

    To convert a zipcode, we have a lookup table called `ZIP_DICT`. Access it using `lat,lng = ZIP_DICT[zipcode]` 

    Another helper function is already defined to create the binding box. It returns a tuple of the northeast, northwest, southeast, and southwest coordinates of the box.
    ```python
    nwlat,nwlng,selat,selng = get_binding_box(lat,lng,RANGE)
    ```

3. Create the url to ping PurpleAir with.

    To provide PurpleAir with the bounding box and the many other fields we want, we use the `requests.get()` function from the requests library. The function allows us to pass an url and a dictionary of query parameters. 

    There is a helper function to create the params dictionary for you, but it may be removed due to redundancy. My suggestion is to use the following code blocks as a guide.

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
    > **NOTE**
    > 
    > If we are to move away from using purpleair as our data source, we can simply change the url and the contents of the `params` dictionary.

4. Create the dictionary of data to be returned.

    A dictionary named `scores` is created and the data to be returned is inserted. This is what the function ultimately returns to the end user.

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

## Creating a new helper function

1. Navigate to `./src/helpers.py`.

2. Define a new function which (ideally) is a refactoring of code that would otherwise be put in `./src/app.py`.

    For example, we defined a function to ping the PurpleAir API, converting zipcodes to their coordinates and creating bounding boxes for those coordinates. The logic of our API has been factored out into `./src/helpers.py`. We use these functions for simplicity and keeping the main `./src/app.py` clean.

3. Use function in `./src/app.py`.  
    
    All functions defined within `./src/helpers.py` are imported into `./src/app.py` for you. There is no need to import the function manually. Use as necessary.