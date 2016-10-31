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

## onJSolrIndex

### Description
Fires the indexing event.

Derived classes should override the index() method when implementing a custom index task.

### Parameters
None

### Return
None

## onJSolrPurge

### Description
Fires the purging event.

Derived classes should override the purge() method when implementing a custom purge task.

### Parameters
None

### Return
None

## onJSolrIndexUpdate

### Description
Fires the index update event.

The index update event is used to index items that have been created or modified since the index date. It should be used for content that are being indexed from an external source. For content that implements Joomla! content events, use onContentAfterSave, onContentAfterDelete and onContentStateChanged instead.

### Parameters
None

### Return
None

## onJSolrAfterSave

### Description
Fires when an item is saved.

### Parameters
* string ```$context``` The context of the item being saved.
* StdClass ```$item``` The item being saved (must have an id property).
* bool ```$isNew``` True if the item is new, false otherwise.

### Return
None

## onJSolrAfterDelete

### Description
Fires when an item is deleted.

### Parameters
* string ```$context``` The context of the item being saved.
* StdClass ```$item``` The item being deleted (must have an id property).

### Return
None

## onJSolrChangeState

### Description
Fires when the state of an item changes.

### Parameters
* string ```$context``` The context of the changed items.
* array ```$pks``` An array of ids of the changed items.
* int ```$value``` The new state.

### Return
None