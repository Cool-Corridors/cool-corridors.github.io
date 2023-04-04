# Home Route ("/")

## Screenshot:

![home route](https://user-images.githubusercontent.com/97417536/229579066-f3a7cb57-242c-48bc-a6e8-e662a706b138.png)

`layout.jinja`: defines the overall structure of the UI. It is made up of 3 sections (navigation bar, the main content, and a footer). This is not whats getting rendered in the app, but rather it is ``search.jinja`` which inherits everything from within ``layout.jinja``. More on this below.

Here's what the main content of ``layout.jinja`` looks like:

```html

<body>
    <header class="nav-bar">
        <div>
            <a class="link" href="/"><img id = "logo" max-width="120px" max-height ="30px" src=".\..\static\images\Logo_IQSpatialLogo.png"/></a>
            <span> <a class="link" href="/about">About</a></span>
        </div>
    </header>
    
    {# Search form and search results go here #}
    <section class="content">
        {% block searchbar %} {% endblock %}
        {% block about %} {% endblock %}
    </section>

    <footer>
    </footer>
    {# Needed for bootstrap components/features that use javascript #}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"
        crossorigin="anonymous"></script>
</body>
```

Some important information to keep in mind:

- The navigation bar is contained within the ``<header></header>`` tag. In there is the IQS Logo, which can be used to navigate back to this route from any other route, as well as the About text to navigate to the about route.

- The the jinja code within ``<section></section>`` is what allows this route to be extendable to other routes. Said routes can be specified within the jinja code blocks:

    ```html
        <section class="content">
            {% block searchbar %} {% endblock %}
            {% block about %} {% endblock %}
        </section>
    ```

- ``search.jinja`` is specified as the jinja file to render in this route (the searchbar component within the jinja block) due to the following code in ``app.py``:

    ```py
    @app.route("/")
    def home():
        # app homepage will default to rendering the search form
        return render_template("search.jinja")
    ```

    ``search.jinja`` is able to inherit all the HTML code within ``layout.jinja`` due to specifying the following inside it:

    ```html

    {% extends "layout.jinja" %}
    {% endblock %}
    ```
    > the HTML content we'd like to present from this route is then written between the preoceeding two lines. 

- The ``<footer></footer>`` tag is meant to contain information relating to the project and the people behind it. However, it is empty at the moment.   

- The CSS declarations in ``static/style.css`` is applied on to ``layout.jinja`` while ``static/search.css`` is applied on to ``search.jinja`` on this route.

