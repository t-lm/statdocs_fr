# REST API Reference

This API reference covers **core Statit functions** to access metrics. Please head to editor guide if you want to push metrics.

**Accessing series**:

- [getSerie](#getserie)
- [batchGetSeries](#listseries)
- [listSeries](#listseries)


## **Errors**

Requests with errors return a response object with the following attributes:

- code: An explicit error code
- message: An explicit error message


## **getSerie**

**getSerie** is used to **get a single metric** from a collection

#### Parameters

- **action**: getSerie
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the serie requested

#### Response

- **Item** - **Object**:
    - **id** - **String** - *required*. ID of the serie
    - **name** - **String** - *required*. Name of the serie
    - **frequency** - **String** - *required*. Frequency of the serie
    - **description** - **String** - *optional*. Description of the serie
    - **observations** - **String** - *optional*. A stringified array of individual observations
    - **unit**- **String** - *optional*. Unit of the serie
    - **sources** - **String** - *optional*. Sources (separated with a ";")
    - **tags** - **Array** - *optional*. List of tags for the serie
    - **notes** - **String** - *optional*. Publication notes
    - **version** - **String** - *optional*. A comment linked to the version


## **batchGetSeries**

batchGetSeries is used to get multiple metrics in a single call

#### Parameters

- **action**: batchGetSeries
- **input** - **Object**:
    - **ids** - *required* - **Array**. IDs of the metrics

#### Response

- **Items** - Array of Item (see get serie)


## **listSeries**

listSeries is used to get all children series under a single parent ID.

As an example, a/b/c is the parent ID of a/b/c/serie1 and a/b/c/serie2

#### Parameters

- **action**: listSeries
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the parentID

#### Response

- **Items** - Array of Item (see get serie)

