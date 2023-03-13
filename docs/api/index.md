# Getting started with the REST API

This page will help you get started accessing metrics from Statit with the API.

- [**Set-up and basic concepts**](#set-up-and-basic-concepts)

- [**Accessing metrics**](#accessing-time-series)
    - Getting a single metric
    - Getting multiple metrics


## **Set-up and basic concepts**

### API format

The API accepts **HTTP GET and POST requests**.

All examples are presented with 'curl'. You can run requests with any client. 


### End-point

All requests must be addressed to: **https://api.gostatit.com/core**.

Core stands for the core API.

```bash
### request

curl https://api.gostatit.com/core

### response

{
  "message": "Welcome on Statit core API"
}

```

### Authentication

Your **requests must be identified with your credentials**: your username and API Key.

Your **username** and **API key** can be found in the **account section** in the home page for your profile.

The API uses **basic Http authentication**. On the command line, it looks like

```bash
### request

curl  -X POST \
      -u username:apikey \
      https://api.gostatit.com/core

### response

{
  "code": "ERROR_PARAM_REQUIRED", ...
}
```

### Actions

Once you are authentified, you can call specific actions: getSerie, listSeries ...

You will do this by adding a json object to the query specifying the action called and the required inputs for the action.


```bash
### request

curl -X POST \
    -u username:apikey \
    -H "Content-Type: application/json" \
    -d '{"action": "getSerie", "input": {"id": "clim/copernicus-r/daily/frh0/temp/real"}}' \
    https://api.gostatit.com/core

### response

{
  "Item": {
  "unit": "Degree Celcius",
  ...
  }
}

```

In the request above, we call the 'getSerie' action to get a single serie and pass a parameter called input with the 'id' of the serie we are requiring.


### Errors

If your request can not be processed, the API will return an error code with an error message.


```bash
### request

curl -X POST \
    -u username:apikey \
    -H "Content-Type: application/json" \
    -d '{"action": "getSerie" }' \
    https://api.gostatit.com/core

### response

{
  "code": "ERROR_PARAM_REQUIRED",
  "message": "Error. Your request is missing a required parameter. Please check the documentation"
}

```


## **Accessing metrics**

### Getting a single metric

We have already explored this in the example above.

#### Example

```bash
### request

curl -X POST \
    -u username:apikey \
    -H "Content-Type: application/json" \
    -d '{"action": "getSerie", "input": {"id": "clim/copernicus-r/daily/frh0/temp/real"}}' \
    https://api.gostatit.com/core

### response

{
  "Item": {
    "unit": "Degree Celcius",
    "frequency": "M",
    "sources": "Copernicus. Climate and Environmental Series",
    "name": "Monthly real temperature",
    "updated": "2021-03-10T17:14:45.504Z",
    "observations": "[[\"1979-01-01\", \"1.6\"], [\"1979-02-01\", \"5.3\"], [\"1979-03-01\", \"6.7\"], [\"1979-04-01\", \"8.5\"], [\"1979-05-01\", \"11.0\"], [\"1979-06-01\", \"14.6\"] ..."
    "description": "Average monthly temperature (degree Celcius)",
    "id": "clim/copernicus-r/daily/frh0/temp/real",
    "tags": []
  }
}
```


The Item object is quite explicit. It contains both serie metadata and data. Note that observations is a stringified array. You can transform it into an array using JSON parsers.


### Listing metrics

The API lets you access multiple metrics by providing part of the path to the metric.

As an example, if you are looking to get all indicators for waste in "Paris", you will call [dechets-fr/dma-dpt/paris/dechets-menagers-associes](https://gostatit.com/dechets/dma-dpt/paris/dechets-menagers-associes) and the request will return all related time series.

It is necessary to specify exactly the id of the parent. The size of the response is limited to 1MB.


#### Example

```bash
### request

curl -X POST \
    -u username:apikey \
    -H "Content-Type: application/json" \
    -d '{"action": "listSeries", "input": {"id": "dechets/dma-dpt/paris/dechets-menagers-associes"}}' \
    https://api.gostatit.com/core

### response

{
  "Items": [
    {
      "unit": "Tons",
      "frequency": "Y",
      "sources": "Base Sinoe de l'Ademe" ,
      "name": "Paris | Déchets ménagers et associés | Valorisation énergétique",
      "updated": "2021-02-24T07:05:32.120Z",
      "observations": "[[\"2009-01-01\", \"842125.33407\"], [\"2011-01-01\", \"833876.24514\"], [\"2013-01-01\", \"803965.81276\"], ...]",
      "description": "Paris. Déchets ménagers et associés. Valorisation énergétique",
      "id": "dechets-fr/dma-dpt/paris/dechets-menagers-associes/valo_energetique"
    },
    {...}
  ]
}

```


### Next steps

You will find the full API reference [here](reference.md)
