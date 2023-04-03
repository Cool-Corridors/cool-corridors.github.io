# /about

**Note**: Due to pivoting to [retool](https://retool.com) for frontend development, this page will no longer being worked on

## Screenshot:

![About Page Skeleton](https://user-images.githubusercontent.com/97417536/229576253-958518a8-5c27-4e70-9ff6-760a7923268f.png)

When 'about' is clicked on the client, flask triggers a function called ``about()`` in ``app.py``, which would then render the HTML code in
``templates/about.jinja``.

- ``app.py``

  ```py
  @app.route("/about")
  def about():
      return render_template("about.jinja")
  ```

- ``templates/about.jinja``:
 
   Notice how this page contains the navigation bar and footer due to being an extension of ``template.jinja`` 
    ```html
    <link rel="stylesheet" href="{{ url_for('static', filename='css/about.css') }}">
    
    {% extends "layout.jinja" %}
    {% block about %}

    <section class="about-body">
      <h1> Empty About Page</h1>
    </section>

    {% endblock %}
    ```

- The CSS declarations in ``static/about.css`` are applied on this route