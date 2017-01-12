# Calendar

The CalenderTool form field provides a dropdown list of date ranges.

* `type` _\(mandatory\)_ must be JSolr.Calendar,

* `name` _\(mandatory\)_ is the unique name of the field,

* `filter` _\(mandatory\)_ is the name of the Solr Index field to use for filtering the search results with the selected calendar range,

* `label` _\(optional\)_ _\(translatable\)_ is the descriptive title of the field,

* `class` _\(optional\)_ is one or more CSS classes to apply to the field layout.

* `default` _\(optional\)_ is the default list item value.

## Options

The JSolr.Calendar field must include one or more options. Depending on what is selected, each option will specify a date range that the search results should be limited to.

### Option Parameters

* `value` \(mandatory\) the value of the option. Value is used as an alias for the actual Apache Solr filter,
* `filter` _\(mandatory\)_ the filter to apply. Must be a valid Apache Solr date range. Must be specified unless the value is an empty string \(I.e. do not apply a date range\).

## Example

```
<field
    type="jsolr.calendar"
    name="date"
    filter="modified_tdt"
    label="Date Range"
    class="jsolr-dropdown"
    default="">
    <option value="">Anytime</option>
    <option value="h" filter="[NOW-1HOUR TO NOW]">Hour</option>
    <option value="d" filter="[NOW-1DAY TO NOW]">Day</option>
    <option value="w" filter="[NOW-7DAY TO NOW]">Week</option>
    <option value="m" filter="[NOW-1MONTH TO NOW]">Month</option>
    <option value="y" filter="[NOW-1YEAR TO NOW]">Year</option>
</field>
```



