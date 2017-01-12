# Facet

The Facets form field provides a list of facet values for a particular field indexed in Solr.

* `type` _\(mandatory\)_ must be JSolr.Facet,

* `name` _\(mandatory\)_ is the unique name of the facet. It is used as an alias for the actual facet field as defined by the facet parameter,

* facet \(mandatory\) is the name of the Solr Index facet field,

* filter \(mandatory\) is the name of the Solr Index field to use for filtering the search results when one or more facet values are selected,

* `label` _\(optional\)_ _\(translatable\)_ is the descriptive title of the facet,

* `class` _\(optional\)_ is one or more CSS classes to apply to the facet layout.

* showcount \(optional\) specifies whether the facet count should be shown. The default is to not show the count,

* sort \(optional\) specifies in what order the facets should be shown. The two options are **count** and **index**. The default is **count**,

* mincount \(optional\) specifies the minimum count a facet must have in order to be included in the list,

* limit \(optional\) is the maximum number of facet values to show. The default is to show all,

* `default` _\(optional\)_ is the default value selected.

## Example

```
<field
    name="author"
    facet="author"
    filter="author"
    type="jsolr.facets"
    label="Limit by Author"
    class="inputbox jsolrquery"
    showcount="true"
    sort="count"
    mincount="1"
    limit="5"/>
```



