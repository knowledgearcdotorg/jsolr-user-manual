# FilterList

The FilterList form field provides a dropdown list of generic filters.

* `type` _\(mandatory\)_ must be JSolr.FilterList,

* `name` _\(mandatory\)_ is the unique name of the field,

* `filter` _\(mandatory\)_ is the name of the Solr Index field to use for filtering the search results with the selected option,

* exactmatch \(mandatory\) specifies whether Solr should return only results which exactly match the selected option. Options are **true** or **false**. Default to **true**,

* `label` _\(optional\)_ _\(translatable\)_ is the descriptive title of the field,

* `class` _\(optional\)_ is one or more CSS classes to apply to the field layout.

* `default` _\(optional\)_ is the default list item value.

## Options

The JSolr.FilterList field must include one or more options. Depending on what is selected, each option will specify a date range that the search results should be limited to.

### Option Parameters

* `value` \(mandatory\) the value of the option. Value is used as an alias for the actual Apache Solr filter,
* `filter` _\(mandatory\)_ the filter to apply. Must be a valid Apache Solr date range. Must be specified unless the value is an empty string \(I.e. do not apply a date range\).

## Example

```
<field  
    type="jsolr.filterlist"  
    name="type"  
    filter="type_s"  
    exactmatch="true"  
    label="Document Type"  
    class="jsolr-dropdown"  
    default="">  
    <option value="">Any Type</option>  
    <option value="odt" filter="text/html">HTML</option>  
    <option value="pdf" filter="application/pdf">PDF</option>  
    <option value="odt" filter="application/vnd.oasis.opendocument.text">ODT</option>  
    <option value="odt" filter="text/plain">Text</option>  
</field>
```

For more specific list form fields, see:

* [Calendar](/calendartool.md)



