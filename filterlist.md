# FilterList

The FilterList form field provides a dropdown list of generic filters.

For more specific list form fields, see:

* Calendar

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



