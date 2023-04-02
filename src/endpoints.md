# Endpoints

There are currently 4 endpoints in the API. They are documented here with their expected values and reponse.

All endpoints return the zipcode they were pinged with.

The [`/data`](./endpoints/endpoint-data.md) endpoint returns a json object containing information about temperature, PM2.5 scores, the IAQI score, a description of the score and the color (for frontend visualizations).

The [`/score`](./endpoints/endpoint-score.md) endpoint returns a json object of the IAQI score.

The [`/color`](./endpoints/endpoint-color.md) endpoint returns a json object of the color that we determined for that zipcode.

The [`/descriptor`](./endpoints/endpoint-descriptor.md) endpoint returns a json object of the description text for that zipcode.