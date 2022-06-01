# REST API Reference
*API version: 1.0.1*

The REST API reference covers **core Statit API functions**:

**Managing collections**:

- [putCollection](#putcollection)
- [updateCollection](#updatecollection)
- [getCollection](#getcollection)
- [deleteCollection](#deletecollection)

**Managing collection access**:

- [putCollectionAuth](#putcollectionauth)
- [deleteCollectionAuth](#deletecollectionauth)

**Managing series**:

- [putSerie](#putserie)
- [batchPutSerie](#batchputserie)
- [getSerie](#getserie)
- [listSeries](#listseries)
- [deleteSerie](#deleteserie)


## **Errors**

Requests with errors return a response object with the following attributes:

- code: An explicit error code
- message: An explicit error message


## **putCollection**

**putCollection** is used to **create a new collection**.

putCollection can not be used to overwrite an existing collection. Collection updates are performed with updateCollection.

#### Parameters

- **action**: putCollection
- **input** - **Object**:
    - **id** - **String** - *required*. ID of the collection. Accepted characters: alphanumerical (A to z, 0 to 9), ".", "-" and "_"
    - **name** - **String** - *required*. Name of the collection
    - **about** - **String** - *optional*. A field describing the collection in one sentence. Text format
    - **frequency** - **String** - *optional*. A descriptive field. Accepted values: D (day), W (week), M (month), Q (quarter), S (semester), Y (year)
    - **description** - **String** - *optional*. A descriptive field. Text or markdown format.
    - **tags** - **Array** - *optional*. Tags related to the collection

#### Response

- **input** - **Object**:
    - **id**: id the collection




## **updateCollection**

**updateCollection** is used to **update the fields of an existing collection**

#### Parameters

- **action**: updateCollection
- **input** - **Object**:
    - **id** - **String** - *required*. ID of the collection. Needs to be the id an existing collection.
    - **name** - **String** - *optional*. Name of the collection
    - **about** - **String** - *optional*. A field describing the collection in one sentence. Text format
    - **frequency** - **String** - *optional*. A descriptive field. Accepted values: D (day), W (week), M (month), Q (quarter), S (semester), Y (year)
    - **description** - **String** - *optional*. A descriptive field. Text or markdown format.
    - **tags** - **Array** - *optional*. Tags related to the collection

#### Response

- **input** - **Object**:
    - **id**: id the collection





## **getCollection**

**getCollection** is used to access a collection

#### Parameters

- **action**: getCollection
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the collection requested

#### Response

- **Item** - **Object**:
    - **id** - **String**. ID of the collection.
    - **name** - **String**. Name of the collection
    - **about** - **String**. A field describing the collection in one sentence.
    - **frequency** - **String**. A descriptive field.
    - **description**  - **String**. A descriptive field.
    - **tags** - **Array**. Tags related to the collection




## **deleteCollection**

**deleteCollection is used to delete a collection**.

Only empty collections with no active series and no authorisations can be deleted.

#### Parameters

- **action**: deleteCollection
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the collection to be deleted

#### Response

- **input** - **Object**:
    - **id**: id the collection





## **putCollectionAuth**

**putCollectionAuth** is used to **grant an access right to a collection to a Statit user**

Access rights are of different types: reading rights, editing rights, user management rights.

#### Parameters

- **action**: putCollectionAuth
- **input** - **Object**:
    - **id** - **String** - *required*. ID of the collection
    - **username** - **String** - *required*. The username for the person being granted the authorisation
    - **type** - **String** - *required*. The type of authorisation. Accepted values: viewer, member, editor, administrator


Statit accepts the **following types**:

- **Viewers** can access the collection and all the series
- **Members** can access the collection and series and comment on series
- **Editors** can access the collection and series and edit them
- **Administrators** can access the collection and series, edit them and manage access

"public" must be used as a username to make your collection publicly visible and accessible by anyone.

#### Response

- **input** - **Object**:
    - **id**: id the collection
    - **username**: username
    - **type**: type of access granted




## **deleteCollectionAuth**

**deleteCollectionAuth** is used to **remove an access right for a specific user**

#### Parameters

- **action**: deleteCollectionAuth
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the collection requested
    - **username** - *required* - **String**. username of the user

#### Response

- **input** - **Object**:
    - **id**: id the collection
    - **username**: username of the user




## **putSerie**

**putSerie** is used to **put a serie inside a collection**

putSerie is used to create the serie as well as to update it. Every putSerie creates a new saved version of the serie

#### Parameters

- **action**: putSerie
- **input** - **Object**:
    - **id** - **String** - *required*. ID of the serie. Accepted characters: alphanumerical (A to z, 0 to 9) and ".", "-", "_" and "/"
    - **name** - **String** - *required*. Name of the serie
    - **frequency** - **String** - *required*. Frequency of the serie. Accepted values: D, W, M, Q, S, Y
    - **description** - **String** - *optional*. Description of the serie. Text format
    - **unit**- **String** - *optional*. Unit of the serie
    - **sources** - **String** - *optional*. Sources
    - **tags** - **Array** - *optional*. List of tags for the serie
    - **notes** - **String** - *optional*. Publication notes
    - **observations** - **String** - *optional*. A stringified array of individual observations, for instance "[\"2021-03-07\", 62.0], [\"2021-03-08\", 105.0]". Observation metadata can be added as a third element in each observation array ("[\"2021-03-08\", 105.0, \"value computed\"]"). If metadata is added, it must be added on everyline
    - **version** - **String** - *optional*. A short comment that will be recorded with the specific serie update


#### Response

- **input** - **Object**:
    - **id**: id of the serie




## **batchPutSerie**

**batchPutSerie** is used to put multiple series inside a collection.

Up to 25 series can be put in a single call.

#### Parameters

- **action**: batchPutSerie
- **input** - **Array**:
    - Serie object as in putSerie

#### Response

- **input** - Array:
    - **ids** of the series pushed





## **getSerie**

**getSerie** is used to **get a single time serie** from a collection

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

## **listSeries**

listSeries is used to get all children series under a single parent ID.

As an example, a/b/c is the parent ID of a/b/c/serie1 and a/b/c/serie2

#### Parameters

- **action**: listSeries
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the parentID

#### Response

- **Items** - Array of Item (see get serie)





## **deleteSerie**

deleteSerie is used to remove a serie.

#### Parameters

- **action**: deleteSerie
- **input** - **Object**:
    - **id** - *required* - **String**. ID of the serie

#### Response

- **input** - **Object**:
    - **id**: id of the serie
