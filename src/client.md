# Client

Short Demo of up to date functionality (click the link if viewing the page through rust's mdbook):

[Coolcorridors Prototype Demo](https://user-images.githubusercontent.com/97417536/229569786-ca22e358-f6a0-415a-a39c-e24476110a04.mov)


## Folder Structure
```bash
.
├── README.md
├── requirements.txt
└── src
    ├── app.py
    ├── formatdata.py
    ├── requirements.txt
    ├── static
    │   ├── css
    │   │   ├── about.css
    │   │   ├── search-results.css
    │   │   ├── search.css
    │   │   └── style.css
    │   └── images
    │       └── Logo_IQSpatialLogo.png
    └── templates
        ├── about.jinja
        ├── layout.jinja
        ├── search-results.jinja
        └── search.jinja
```

Currently, the layout of the frontend is made up of 3 components within the `./frontend/template` directory:

- `layout.jinja`: defines the overall structure of the UI. It is made up of 3 sections (navigation bar, the main content, and a footer).
- `search.jinja`: search bar component. It sends an HTTP post request containing the user input (zipcode) to the ``/data`` endpoint
- `search-results.jinja`: search results component. This component receives and displays data from the API call on the ``/data`` endpoint.
- ``about.jinja`` skeleton template set up to populate information on the project and the people behind it.

The CSS file names in `./frontend/static/css` define styling rules to the corresponding Jinja components.