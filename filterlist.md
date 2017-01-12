# FilterList

The FilterList form field provides a dropdown list of generic filters.

* `type` _\(mandatory\)_ must be JSolr.FilterList,

* `name` _\(mandatory\)_ is the unique name of the field,

* `label` _\(optional\)_ _\(translatable\)_ is the descriptive title of the field,

* `class` _\(optional\)_ is one or more CSS classes to apply to the field layout.

* `default` _\(optional\)_ is the default list item value.

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



