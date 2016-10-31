# Developing a Plugin

JSolr's plugins are designed to fully integrate with Joomla!'s plugin infrastructure.

Before developing a JSolr plugin make sure you are familiar with Joomla! plugin development in general.

## Building the Plugin

Building a 3rd party plugin for JSolr is very easy as most of the "heavy lifting" is done for you.

To build your own plugin:

### Extend the \JSolr\Plugin class
The \JSolr\Plugin class implements most of the indexing functionality for you. Indexing, purging, content saving, deleting and state changes are all handled via the \JSolr\Plugin class.

#### Example
```
// Load the JSolr library.
\JLoader::registerNamespace('JSolr', JPATH_PLATFORM);

// Extend the JSolr\Plugin class. Ensure the plugin name matches Joomla!'s plugin naming convention.
class PlgJSolrExample extends \JSolr\Plugin
```

### Get the items for indexing
### Prepare the data for indexing
Next you will need to specify the data that needs to be indexed. To do this, override \JSolr\Plugin's prepare method.

The prepare method requires one parameter, $source, which contains a content item's data, and must return an array of indexable fields.

Newer versions of Apache Solr allow for on-the-fly field names, creating them as needed. However, for JSolr to provide standardized results, some field names are expected. These are:

* **id** The unique id of the item. It must be made up of two parts; the context and the id.
* **id_i** The unique id of the item. This must be an integer.
* **name** The name of the content. This will most likely be the title.
* **author** An array of author names.
* **author_ss** An aray of facetable author names.
* **title_txt_lang** The localized title of the content. lang is the two letter iso code of the item.
* **context_s** The item's context.
* **lang_s** The language the content is written in, including the locale. E.g. en-AU.
* **access_i** The Joomla access level, defined as an integer.
* **created_tdt** The date the item was created, represented by the format Y-m-d\TH:i:s\Z.
* **modified_tdt** The date the item was modified, represented by the format Y-m-d\TH:i:s\Z.

You may also wish to index information about the category the item is a part of. Recommended fields for category storage:

* **category_txt_lang** The localized category name where lang is a two letter iso code.
* **category_s** The category name as a facet.
* **category_i** The id of the category.

You may consider storing additional data for custom faceting and sorting. It is recommend you use the *_s* suffix for single values and *_ss* for multiple values. Consider using the appropriate suffix for values that are not of type string such as *_tdt* for date.

### Putting it all together

### Provide a link for each result

## Detecting Changes to Content