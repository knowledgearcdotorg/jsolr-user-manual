# Calendar

The CalenderTool form field provides a dropdown list of date ranges.

## Example

```
<field
    type="jsolr.calendartool"
    name="date"
    filter="modified_tdt"
    filter_quoted="false"
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



