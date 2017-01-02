# Field Aliasing

JSolr identifies field names using the underscore suffix. For example, a category name is stored in the Solr field categorys and a field storing the price of an item might be stored in modified\_tdt where \_tdt tells Solr that the price should be treated as a date and time. However, there may be situations where having to specify the Solr field name may be undesirable and you may prefer to use an alias for the actual field.

JSolr provides a feature called field aliasing which allows you to specify an alternative name for a particular field, so, for example, the field name "date\_tdt" can be mapped to the alias "date".

Reasons for aliasing a field vary; you may want to provide cleaner search urls for SEO purposes, or use names for fields which are easier to remember. Aliases are very useful for fields which store content in different languages because users only have to remember to use the alias and JSolr will [handle the localization](/language-management.md) for them.

## Configuring an Alias

Configuring query field aliases is configured using JSolr's Options. To configure:

1. Log into the Joomla administrator,
2. Navigate to Components -&gt; JSolr
3. Click on the Options button,
4. Navigate to the Search Layout tab.

Locate "Query Field Aliases"; you can now specify one or more aliases. Aliases take the form `alias:fieldname` where alias is the alias of the field and fieldname is the corresponding Solr field name.

Multiple aliases can be defined. List each one on a separate line.

Field names that can be localized, such as description, can use the [localization placeholder](/language-management.md), I.e. alias:field\_name\_txt\_\*. For example, if we wanted to specify an alias "description" for all description\_txt fields, we would specify the following alias:

> description:description\_txt\_\*

Once you have  configured your aliases, Save or Save & Close.

## Using an Alias

You can now use your alias in a query. From your search page, search using the alias instead of the field name, I.e.

> alias:phrase or term

For example, if we have configured an alias called "description" for the field "description\_txt\_\*, we can now use the description field no matter what langauge we search in:

> description:"Joomla the content managment system"
>
> description:"Joomla El sistema de gestión de contenidos"



