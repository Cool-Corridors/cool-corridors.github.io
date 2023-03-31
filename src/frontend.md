## Frontend

Short Demo of up to date functionality:

https://user-images.githubusercontent.com/97417536/223229967-11e12cef-dae1-4c03-adb7-8d4cd798c06f.mov

Currently, the layout of the frontend is made up of 3 components within the `./frontend/template` directory:

- `layout.jinja`: defines the overall structure of the UI. It is made up of 3 sections (navigation bar, the main content, and a footer)
- `search.jinja`: search bar component. It sends an HTTP post request containing the user input to `results()` in `./frontend/app.py`.
- `search-results.jinja`: serach results component. This component receives data from `results()` in `./frontend/app.py`

The CSS file names in `./frontend/static/css` define styling rules to the corresponding Jinja components.
