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
When indexing for the first time or rebuilding the index after a purge, items need to be retrieved in bulk by \JSolr\Plugin's index method.

The parent class \JSolr\Plugin expects items to be retrieved in a way that will not overburden Joomla! or the underlying database. This can be done by overriding the getItems method, which is passed some paging information to reduce load on the database.

In most cases this can be done using an existing component's JModel implementation, which provides a getItems method for easy retrieval.

To retrieve items, you will need to override two abstract methods:

* **getTotal()** Gets the total number of items to index,
* **getItems()** Gets the items for indexing.

Check out the JSolr - Content plugin for an example of [retrieving items using JModelLegacy](https://github.com/knowledgearcdotorg/jsolr/blob/master/plugins/jsolr/content/content.php#L29).

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

#### Example
```
protected function prepare($source)
{
    $lang = $this->getLanguage($source->language, false);
    $author = JFactory::getUser($source->created_by);
    $category = JCategories::getInstance('content')->get($source->catid);

    $array = array();

    $array['id'] = $this->buildId($source->id);
    $array['id_i'] = $source->id;
    $array['name'] = $source->title;
    $array["author"] = array($author->name);
    $array["author_ss"] = array($this->getFacet($author->name));
    $array["author_i"] = $author->id;
    $array["title_txt_$lang"] = $source->title;
    $array['alias_s'] = $source->alias;
    $array['context_s'] = $this->get('context');
    $array['lang_s'] = $source->language;
    $array['access_i'] = $source->access;
    $array["category_txt_$lang"] = $category->title;
    $array["category_s"] = $this->getFacet($category->title); // for faceting
    $array["category_i"] = $category->id;
    $array["parent_id_i"] = $source->catid;

    $created = JFactory::getDate($source->created);
    $modified = JFactory::getDate($source->modified);

    if ($created > $modified) {
        $modified = $created;
    }

    $array['created_tdt'] = $created->format('Y-m-d\TH:i:s\Z', false);
    $array['modified_tdt'] = $modified->format('Y-m-d\TH:i:s\Z', false);

    foreach ($source->tags->getItemTags('com_example.content', $source->id) as $tag) {
        $array["tag_ss"][] = $tag->title;
    }

    return $array;
}
```

### Provide a link for each result
When JSolr displays a list of results, the user should be able to click on each result and view the resulting content. JSolr doesn't handle content urls, so your plugin will need to add this to each relevant result.

To add the link, you simply intercept each item, check the context, and, if it matches the context of your plugin, add the url to the item. The recommended method is to add the link via the onJSolrSearchPrepareData event.

#### Example
```
public function onJSolrSearchPrepareData($document)
{
    if ($this->get('context') == $document->context_s) {
        require_once(JPATH_ROOT."/components/com_example/helpers/route.php");

        $document->link = ExampleHelperRoute::getContentRoute($document->id_i, $document->parent_id_i);
    }
}
```

### Putting it all together
We now have all the parts required for indexing content and making it easily searchable.

#### Example
```
\JLoader::registerNamespace('JSolr', JPATH_PLATFORM);

class PlgJSolrExample extends \JSolr\Plugin
{
    protected $context = "com_example.document";

    protected function getTotal()
    {
        // The getStoreId throws an error if catid array is used.
        // Therefore, block the error.
        return @(int)$this->getDocuments()->getTotal();
    }

    protected function getItems($start, $limit)
    {
        $items = $this->getDocuments();

        $items->setState('list.start', $start);
        $items->setState('list.limit', $limit);
        $items->setState('list.ordering', 'a.id');
        $items->setState('list.direction', 'asc');

        // The getStoreId throws an error if catid array is used.
        // Therefore, block the error.
        return @$items->getItems();
    }

    private function getDocuments()
    {
        $path = JPATH_ROOT.'/administrator/components/com_example/models/documents.php';
        \JLoader::register('ExampleModelDocuments', $path);

        $documents = \JModelLegacy::getInstance(
                        'Documents',
                        'ExampleModel',
                        array('ignore_request'=>true));


        $catids = $this->params->get('categories', array());

        if (($pos = array_search(1, $catids)) !== false) {
            unset($catids[$pos]);
        }

        if (count($catids)) {
            $documents->setState("filter.category_id", $catids);
        }

        return $documents;
    }
    
    protected function prepare($source)
    {
        $lang = $this->getLanguage($source->language, false);
        $author = JFactory::getUser($source->created_by);
        $category = JCategories::getInstance('document')->get($source->catid);

        $array = array();

        $array['id'] = $this->buildId($source->id);
        $array['id_i'] = $source->id;
        $array['name'] = $source->title;
        $array["author"] = array($author->name);
        $array["author_ss"] = array($this->getFacet($author->name));
        $array["author_i"] = $author->id;
        $array["title_txt_$lang"] = $source->title;
        $array['alias_s'] = $source->alias;
        $array['context_s'] = $this->get('context');
        $array['lang_s'] = $source->language;
        $array['access_i'] = $source->access;
        $array["category_txt_$lang"] = $category->title;
        $array["category_s"] = $this->getFacet($category->title); // for faceting
        $array["category_i"] = $category->id;
        $array["parent_id_i"] = $source->catid;

        $created = JFactory::getDate($source->created);
        $modified = JFactory::getDate($source->modified);

        if ($created > $modified) {
            $modified = $created;
        }

        $array['created_tdt'] = $created->format('Y-m-d\TH:i:s\Z', false);
        $array['modified_tdt'] = $modified->format('Y-m-d\TH:i:s\Z', false);

        foreach ($source->tags->getItemTags('com_example.document', $source->id) as $tag) {
            $array["tag_ss"][] = $tag->title;
        }

        return $array;
    }

    public function onJSolrSearchPrepareData($document)
    {
        if ($this->get('context') == $document->context_s) {
            require_once(JPATH_ROOT."/components/com_example/helpers/route.php");

            $document->link = ExampleHelperRoute::getDocumentRoute($document->id_i, $document->parent_id_i);
        }
    }
}
```

## Detecting Changes in Content
