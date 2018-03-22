# Language Management

JSolr is designed to index content in multiple languages and integrates seamlessly with Joomla's multilingual features.

## Localizing Fields

Fields which can be "localized" \(I.e. which should store a value in a particular language\) are appended with a language placeholder. This placeholder is an underscore followed by an asterisk \(\*\):

> fieldname\_\*

JSolr localizes these fields by replacing the \_\* suffix with the appropriate two letter iso code, ensuring that the field is correctly localized. JSolr determines the two letter iso code based on the languages installed \(via the Joomla Language Manager\) and the language specified in the content item.

## Localization for Indexing 

As almost all language fields are text-based in Apache Solr, you will notice that all fields end with \_txt followed by another underscore and a two letter iso code. For example `_txt_en` stores text-based content in the English language. Storing text in the correct language ensures Apache Solr will correctly parse the text, improving indexing and providing much more relevant search results.

Some common examples of fields which are localized in JSolr are:

* title\_txt\_\*
* content\_txt\_\*
* description\_txt\_\*

## Localization for Searching

All queries are localized by JSolr before being sent to the Apache Solr search engine to ensure that only results which match the current language are retrieved and also localizes content when a list of results is displayed.

Users can also specify field names using the asterisk \(\*\) placeholder in their queries and JSolr will localize each field name according to the current language.





