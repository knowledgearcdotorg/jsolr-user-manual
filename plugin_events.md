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