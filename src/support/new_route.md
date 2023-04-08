## Creating a new API endpoint

All endpoints are defined inside `./src/app.py`. To create a new endpoint, simply create a new function and add a new route to the `api` object. 

1. Navigate to `./src/app.py`.
2. Define a new route (name and methods) through the following syntax:
    ```py
    @api.route("/test", methods=[GET,POST])
    def test():
        return "Hello World!"
    ```
    <span class="caption"> An example endpoint called "test" that takes methods `GET` and `POST`</span>

    The above code will create an endpoint called `test` such that when accessed will show `"Hello World!"`.

> **NOTE**
>    
> The function name can be anything, but it is recommended to keep it
> consistent with the endpoint name.

3. Define logic for endpoint.  
    * Inside the function body, you can access the query string provided through the `request.args.get("<query name>")`  
    * Handle errors, do computations, etc... 

    Flask offers many different ways to return data. For more information, see the [Flask documentation](https://flask.palletsprojects.com/en/2.2.x/quickstart/). 

    You can:
    - return a string literal
    - return a json object
    - render a template (html file)
    - redirect to a different route or url
    - return a file
    - etc...


