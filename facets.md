# Facet

The Facets form field provides a list of facets for a particular field indexed in Solr.

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



