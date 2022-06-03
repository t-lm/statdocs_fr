# Get Started with the REST API

Statit can be used fully with a REST API.

Make sure you have read [**getting started with Statit on the web**](/gs/web.md) to understand the basics of how Statit works.

This section explains **how to start using Statit with the REST API**. For the complete documentation covering the REST API, please head over to the [**REST API reference**](/reference/api_rest.md).


## **Set-up and basic concepts**

### API format

The API accepts **HTTP GET and POST requests**.

All examples are presented with 'curl'. You can of course complete requests in any language.


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

Once you are authentified, you can call specific actions: getSerie, getCollection, putSerie ...

You will do this by adding a json object to the query specifying the action called and the required inputs for the action.


```bash
### request

curl -X POST \
    -H "Content-Type: application/json" \
    -d '{"action": "getSerie", "input": {"id": "xrate/weekly/eur/chf"}}' \
    -u username:apikey \
    https://api.gostatit.com/core

### response

{
  "Item": {
  "unit": "Swiss Franc",
  ...
  }
}

```

In the request above, we call the 'getSerie' action to get a single metric and pass a parameter called input with the 'id' of the metric we are requiring.

If you would like to learn the basics about metric identifiers, please head over to [Getting started on the web](/gs/web.md).


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
    -H "Content-Type: application/json" \
    -d '{"action": "getSerie", "input": {"id": "xrate/weekly/eur/chf"}}' \
    -u username:apikey \
    https://api.gostatit.com/core

### response

{
  "Item": {
    "unit": "Swiss Franc",
    "frequency": "W",
    "sources": "ECB (European Central Bank)",
    "name": "Swiss Franc for 1 EUR",
    "updated": "2021-07-19T14:55:54.320Z",
    "notes": "",
    "observations": [
      [
        "2009-01-12",
        1.5004600000000001
      ],
      [
        "2009-01-19",
        1.48424
      ],
      [
        "2009-01-26",
        1.4874800000000001
      ],
      [
        "2009-02-02",
        1.5029
      ] ...
    ]
  }
}
```


The Item object is quite explicit. It contains both metric metadata and data. Note that observations is a stringified array. You can transform it into an array using JSON parsers.


### Listing metrics

The API let you request "children" metrics with a single parent.

As an example, if you are looking to get all weekly euro exchange rates, you will call [xrate/weekly/eur](https://gostatit.com/xrate/weekly/eur) and the request will return all related metrics.

It is necessary to specify exactly the id of the parent. The size of the response is limited to 1MB.


#### Example

```bash
### request

curl -X POST \
    -H "Content-Type: application/json" \
    -d '{"action": "listSeries", "input": {"id": "xrate/weekly/eur"}}' \
    -u username:apikey \
    https://api.gostatit.com/core

### response

### response

{
  "Items":
    [{
    "unit": "Swiss Franc",
    "frequency": "W",
    "sources": "ECB (European Central Bank)",
    "name": "Swiss Franc for 1 EUR",
    "updated": "2021-07-19T14:55:54.320Z",
    "notes": "",
    "observations": [
      [
        "2009-01-12",
        1.5004600000000001
      ],
      [
        "2009-01-19",
        1.48424
      ],
      [
        "2009-01-26",
        1.4874800000000001
      ],
      [
        "2009-02-02",
        1.5029
      ] ...
    ]
  } ...
  ]
}
```

### **Next steps**

You have now learnt about the basics of the REST API to access metrics. To learn more, head over to the full [REST API reference](/reference/api_rest.md)
