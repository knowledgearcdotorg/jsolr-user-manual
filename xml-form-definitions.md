## XML Form Definitions

With JSolr you can customize the way your users search your web site content.

JSolr uses [Joomla!'s XML form definitions](https://docs.joomla.org/XML_JForm_form_definitions) to provide additional methods of filtering search results; you can even change the search query field if you need a different type of query input.

## JSolr Form Fields

JSolr provides a number of form fields specifically desinged for querying, filtering and sorting search results. JSolr form fields must be used for [field linking](#field-linking) or when you want JSolr to apply a query filter without exposing Solr index field names.

See [Form Fields](/form-fields.md) for more information.

## Search Form Syntax

A JSolr Search XML form file looks very similar to any other Joomla! form definition. The standard search form definitions are stored in a file called search.xml which is located in `/path/to/joomla/site/components/com_jsolr/models/forms`.

Below is the basic syntax which you can extend to provide highly customized searches for your users:

```XML
<?xml version="1.0" encoding="utf-8"?>
<form>
    <fieldset
        name="query"
        label="COM_JSOLR_ADVANCED_SEARCH_TITLE"
        addfieldpath="administrator/components/com_jsolr/models/fields">

        <!-- only JSolrFormFields should be used here -->
        <field
            name="q"
            type="jsolr.autosuggest"
            label=""
            size="20"
            class="inputbox jsolrquery"
            maxlength="50"
            query="title_s"/>
    </fieldset>

    <fieldset
        name="facets"
        addfieldpath="administrator/components/com_jsolr/models/fields">
        <field
            name="author"
            facet="author"
            filter="author"
            type="jsolr.facets"
            label="COM_JSOLR_SEARCH_FACET_AUTHOR_LABEL"
            class="inputbox jsolrquery"
            count="true"
            limit="5"/>
    </fieldset>

    <fieldset
        name="tools"
        addfieldpath="administrator/components/com_jsolr/models/fields">
        <field
            type="jsolr.calendartool"
            name="date"
            filter="modified_tdt"
            filter_quoted="false"
            label="COM_JSOLR_SEARCH_TOOL_DATE_LABEL"
            class="jsolr-dropdown"
            default="">
           <option value="">COM_JSOLR_CALENDAR_ANYTIME</option>
           <option value="h" filter="[NOW-1HOUR TO NOW]">COM_JSOLR_CALENDAR_HOUR</option>
           <option value="d" filter="[NOW-1DAY TO NOW]">COM_JSOLR_CALENDAR_DAY</option>
           <option value="w" filter="[NOW-7DAY TO NOW]">COM_JSOLR_CALENDAR_WEEK</option>
           <option value="m" filter="[NOW-1MONTH TO NOW]">COM_JSOLR_CALENDAR_MONTH</option>
           <option value="y" filter="[NOW-1YEAR TO NOW]">COM_JSOLR_CALENDAR_YEAR</option>
        </field>
        <field type="jsolr.queryfilter" name="in">
    </fieldset>
</form>
```

The search XML is broken down into three fieldsets:

### The Query Fieldset

The query fieldset specifies the query search box. In most cases you won't need to change this but it does allow you to specify other query inputs if the query field which ships with JSolr is inadequate. The only requirement is that a field called `q` be specified. You can even specify multiple fields in this fieldset if necessary although it will be up to you to display on them on the screen by overriding the default\_form.php template.

### The Facets Fieldset

Facets provide groups or categories of terms which reside in multiple results. Authors, keywords, tags and categories are examples of terms which may apply to multiple items.

The facet fieldset provides a mechanism for users to filter or "drill-down" on particular category terms. For example, users may want to only view results which reside in a particular category or a written by certain authors.

### The Tools Fieldset

The tools fieldset provides additional query and filter inputs which may enhance search results, for example, only showing results where the query only appears in the heading or displaying only those results modified in the last 7 days.

## Advanced Search Form Syntax

Like the standard JSolr search form, the advanced search form works like any other Joomla! form definition file.

The standard search form definitions are stored in a file called advanced.xml which is located in `/path/to/joomla/site/components/com_jsolr/models/forms`.

Syntax may look like:

```XML
<?xml version="1.0" encoding="utf-8"?>
<form>
    <fieldset
        name="query"
        label="COM_JSOLR_ADVANCED_SEARCH_TITLE"
        addfieldpath="components/com_jsolr/model/fields">

        <!-- eventually only our FacetFields fields should be used here -->
        <field
            name="aq"
            facet="title"
            type="text"
            label="COM_JSOLR_ADVANCED_SEARCH_AQ_LABEL"
            size="40"
            class="inputbox jsolrquery"
            maxlength="50"/>
        <field
            name="eq"
            facet="title"
            type="text"
            label="COM_JSOLR_ADVANCED_SEARCH_EQ_LABEL"
            size="40"
            class="inputbox jsolrquery"
            maxlength="50"/>
        <field
            name="oq"
            facet="title"
            type="text"
            label="COM_JSOLR_ADVANCED_SEARCH_OQ_LABEL"
            size="40"
            class="inputbox jsolrquery"
            maxlength="50"/>
        <field
            name="nq"
            facet="title"
            type="text"
            label="COM_JSOLR_ADVANCED_SEARCH_NQ_LABEL"
            size="40"
            class="inputbox jsolrquery"
            maxlength="50"/>
    </fieldset>

    <fields
        name="as"
        addfieldpath="/libraries/JSolr/Form/Fields/Legacy">
       <fieldset name="advanced">
           <field
               name="lang"
               type="language"
               label="Language"
               default="">
               <option value="">COM_JSOLR_LANGAUGE_ANY</option>
           </field>
            <field
                name="date"
                type="list"
                label="Date">
               <option value="">COM_JSOLR_CALENDAR_ANYTIME</option>
               <option value="h">COM_JSOLR_CALENDAR_HOUR</option>
               <option value="d">COM_JSOLR_CALENDAR_DAY</option>
               <option value="w">COM_JSOLR_CALENDAR_WEEK</option>
               <option value="m">COM_JSOLR_CALENDAR_MONTH</option>
               <option value="y">COM_JSOLR_CALENDAR_YEAR</option>
            </field>
            <field
                name="in"
                type="list"
                label="Search">
               <option value="">Anywhere</option>
               <option value="title_txt_*">Only in the title</option>
               <option value="content_txt_*">Only in the body</option>
            </field>
        </fieldset>
    </fields>
</form>
```

### The Query Fieldset

The query fieldset functions in a similar way to the standard search query fieldset but it provides a much more configurable query builder. For example, users can specify all words be matched in their query, the exact phrase be matched, any words be matched or even specify words whcand phrase which shouldn't be matched.

Because Advanced Search expects these fields exist, it is highly recommended you do not change them unless you really know what you are doing.

### The AS Fieldset

The AS or Advanced Search fieldset specifies additional filters for providing highly customized search results.

## Field Linking

Field linking is a concept used by JSolr when an advanced form field value is submitted to the search results and vice versa.

Field linking allows values to be automatically processed by JSolr without exposing Solr field names such as author\_ss or date\_tdt to the end user, improving search engine friendliness, making search filters easier to remember for end users.

To better understand field linking, let's take a look at the "in" filter field which limits JSolr to searching within only the title or the content.

In search.xml you will see:

```XML
<field type="jsolr.queryfilter" name="in">
```

and in advanced.xml you will see:

```XML
<field name="in" type="list" label="Search">
    <option value="">Anywhere</option>
    <option value="title_txt_*">Only in the title</option>
    <option value="content_txt_*">Only in the body</option>
</field>
```

Now, let's assume that the user has used the advanced search to specify that they only want to search in the title. In order for JSolr to apply the "in" filter, it needs to know that the "in" filter exists. Therefore, search.xml must contain a definition for the "in" field.

Also notice that search.xml uses the field type `jsolr.queryfilter`. While you can use any type of Joomla! form field in advanced.xml, you must use the [JSolr form fields](#jsolr-form-fields) if you want queries and filters to automatically be applied to your search results.

