# Chapter 2
Add API Gateway endpoint and configure it. 
A bitcoin app to fetch coin prices.

## add API endpoint
In the `amplify/backend/function/<function name>/src/app.js`, add a new route endpoint.

Then, add new endpoint by amplify
```
amplify add api
```


## Lambda functions for API Gateway endpoint
```
const axios = require('axios');

// Example return route
app.get('/coins', function (req, res) {
  // Define base url
  let apiUrl = `https://api.coinlore.com/api/tickers?start=0&limit=10`;

  // Check if there are any query string parameters
  // If so, reset the base url to include them
  if (req.apiGateway && req.apiGateway.event.queryStringParameters) {
    const { start = 0, limit = 10 } = req.apiGateway.event.queryStringParameters;
    apiUrl = `https://api.coinlore.com/api/tickers/?start=${start}&limit=${limit}`;
  }

  // Call API and return response
  axios.get(apiUrl)
    .then(response => {
      res.json({ coins: response.data.data });
    })
    .catch(err => res.json({ error: err }));
}
```
