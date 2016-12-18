# Sort

The JSolr Sort form field applies a sort field and direction to the search results.

## Parameters

* `type` _\(mandatory\)_ must be JSolr.Sort,

* `name` _\(mandatory\)_ is the unique name of the field,

* `label` _\(optional\)_ _\(translatable\)_ is the descriptive title of the field,

* `class` _\(optional\)_ is one or more CSS classes to apply to the field layout.


## Options

The JSolr.Sort field must include one or more options. Depending on what is selected, each option will specify the sort and direction of the search results.

### Option Parameters

* `sort` _\(mandatory\)_ the field to sort on. Must correspond to an indexed field name in Apache Solr which supports sorting,
* `direction` _\(optional\)_ the order of the sorted results. Can be either `asc` for ascending or `desc` for descending.

## Example

```
<field
	name="sort"
	type="jsolr.sort"
	label="Sort By"
	class="jsolr-dropdown">
	<option value="">Relevance</option>
	<option value="date" field="date_tdt" direction="desc">Date</option>
</field>
```



