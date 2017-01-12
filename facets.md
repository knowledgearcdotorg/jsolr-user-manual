# Facet

The Facets form field provides a list of facet values for a particular field indexed in Solr.

* `type` _\(mandatory\)_ must be JSolr.Facet,

* `name` _\(mandatory\)_ is the unique name of the facet,

* `label` _\(optional\)_ _\(translatable\)_ is the descriptive title of the field,

* `class` _\(optional\)_ is one or more CSS classes to apply to the field layout.

* `default` _\(optional\)_ is the default list item value.

## Example

```
<field
    name="author"
    facet="author"
    filter="author"
    type="jsolr.facets"
    label="Limit by Author"
    class="inputbox jsolrquery"
    count="true"
    limit="5"/>
```



