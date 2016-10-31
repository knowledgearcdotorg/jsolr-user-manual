# Plugin Events

## onJSolrBrowseBeforeQuery

### Description
Fires before the browse query is executed.

### Parameters
* \Solarium\QueryType\Select\Query\Query ```$query``` The browse query.
* JObject ```$state``` The calling model's state.

### Return
None

## onJSolrBrowseAfterQuery

### Description
Fires after the browse query is executed.

### Parameters
* \Solarium\QueryType\Select\Result ```$response``` The browse response.
* JObject ```$state``` The calling model's state.

### Return
None

## onJSolrSearchBeforeQuery

### Description
Fires before the search query is executed.

### Parameters
* \Solarium\QueryType\Select\Query\Query ```$query``` The search query.
* JObject ```$state``` The calling model's state.

### Return
None

## onJSolrSearchAfterQuery

### Description
Fires after the search query is executed.

### Parameters
* \Solarium\QueryType\Select\Result ```$response``` The search response.
* JObject ```$state``` The calling model's state.

### Return
None

## onJSolrSearchPrepareData

### Description
Fires for each record which is retrieved from the index.

### Parameters
* \Solarium\QueryType\Update\Query\Document\Document ```$document``` A single record from the index.

### Return
None

## onJSolrSearchPrepareData

### Description
Fires for each record which is retrieved from the index.

### Parameters
* \Solarium\QueryType\Update\Query\Document\Document ```$document``` A single record from the index.

### Return
None