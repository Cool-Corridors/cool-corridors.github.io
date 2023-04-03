# /search

In this route, API requests are made, and the data recieved gets displayed. Take a look at the following example:

![zipcode search results](https://user-images.githubusercontent.com/97417536/229623946-c057ddda-45dc-43fe-9c5a-f65e7a5867eb.png)

When this route is triggered, it renders ``search-results.jinja``, which inherits all HTML within ``search.jinja`` (which by extension, also inherits ``layout.jinja``).

Here's how this is done from within ``app.py``:

```py
LOCAL_API_BASE_URL = "http://localhost:3000/" 
DEPLOYED_API_BASE_URL = "https://cool-corridors-api-service.onrender.com"

@app.route("/search", methods = ["GET", "POST"])
def results():

    zipcode = request.form.get("zipcode")
    params = {"zipcode": zipcode, "read_key": READ_KEY}
    
    # The API base url used depends on which API instance the developer desire to use
    zipcode_data =  requests.get(f"{DEPLOYED_API_BASE_URL}/data", params=params).json()
    
    if "error" in zipcode_data:
        zipcode_data = json.loads(zipcode_data)
        error = True
        error_data = zipcode_data["error"]
        return render_template("search.jinja", error = error, error_data = error_data)
    
    # use zipcode data and ROW_HEADERS to format the data displayed on the frontend
    climate_data = format_zipcode_data(zipcode_data)

    return render_template("search-results.jinja", climate_data = climate_data, zipcode = zipcode)
```

- When the user inputs their zipcode and presses enter, ``results()`` is triggered and in there, an HTTP GET request to the ``/data`` endpoint of the API is made. This is seen in the following line: 

> zipcode_data =  requests.get(f"{DEPLOYED_API_BASE_URL}/data", params=params).json() 


It is worth noting that if you're running the API locally on your machine, then you can replace ``DEPLOYED_API_BASE_URL`` with ``LOCAL_API_BASE_URL``