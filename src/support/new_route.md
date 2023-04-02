## Creating a new API endpoint

All endpoints are defined inside `./src/app.py`. To create a new endpoint, simply create a new function and add a new route to the `api` object. 

For example, to create a new endpoint called `/test`, you would do the following:

```py
@api.route("/test")
def test():
    return "Hello World!"
```

You can also provide the methods that this endpoint supports.
```py
@api.route("/test", methods=[GET,POST,...])
def test():
    return "Hello World!"
```

This creates a new endpoint called `/test` that returns the string "Hello World!" when accessed.

The function name can be anything, but it is recommended to keep it consistent with the endpoint name.

Flask offers many different ways to return data. For more information, see the [Flask documentation](https://flask.palletsprojects.com/en/2.2.x/quickstart/). 

You can:
- return a string literal
- return a json object
- render a template (html file)
- redirect to a different route or url
- return a file
- etc...


