# Searching

JSolr provides a powerful searching experience out-of-the-box; simply type what you are looking for and get back a list of relevant results. However, you can also write more complex queries using Solr's query syntax.

## Query Syntax

JSolr passes queries directly through to the Apache Solr search engine, so you can use all of Solr's syntax to execute powerful searches.

Solr's query syntax is is very comprehensive and provides a number of special features which improve accuracy of your search results.

Some of the more common queries are outlined below:

### Basic Query

The simplest query is a single term query. A single term query is just that; a single word:

> Joomla

### Query with Field Name

With Solr you can also narrow your search to a particular field, for example:

> title:Joomla

Here we narrow the query to only search for the term in the title.

Multiple field names can be applied to a single query:

> title:Joomla type\_s:article

Using field names can be used in all kinds of queries and will add precision when searching for specific terms, phrases or ranges.

### Phrase Query

A phrase query is much like a basic query except you are searching for multiple terms instead of one:

> Joomla content management system

You can also use more natural language when specifying a phrase query, for example:

> Using JSolr with Joomla

Adding a field name will add precision to your phrase:

> title:I want to believe

You can even ask questions:

> How do I install and configure Joomla?

Search results are returned by relevance; that means Solr will try and return records which most closely match what you are trying to search for.

In many cases, the relevance of your search results will be dependent on the number of records you have indexed and the amount of information indexed about each record, but Solr does a pretty good job of matching results to what you are looking for.

### Exact Match

An exact match query is an extension of the Phrase Query. With an exact match, you want to find all records which exactly match the phrase \(rather than simply trying to find the most relevant results\).

Specifying an exact match query is simple; just wrap your phrase in double quotes:

> "Installing and configuring Joomla!"

Using quotes is also a good way to search for terms and phrases which may have special characters such as boolean operators \(which we will cover next\):

> title:"The X-Files"

### Boolean Query

Sometimes you want to include certain terms but exclude others. This achieved using the `+` and `-` signs. For example, we want to search for Joomla but exclude other content management systems that might turn up in the search results:

> Joomla -Wordpress -Drupal

We can also specify search terms which MUST be included in search results:

> content management system +joomla

And we can use a combination of the above to search for content management systems that MUST be joomla and MUST NOT be wordpress or drupal:

> content management system +joomla -wordpress -drupal

Alternatively Solr supports the OR, AND and NOT operators, which can be used to achieve similar results. For example, if we want to search for all content which contains both "Joomla" and "Wordpress" we can use the AND operator:

> Joomla AND wordpress

If we want results which include Joomla AND Wordpress but not Drupal, we can use:

> Joomla AND Wordpress NOT Drupal

We can also use the OR operator if we want any of the content management systems to show in the search results:

> Joomla OR Wordpress OR Drupal

By default, most Solr search engines will default to the OR operator.

One final feature of Solr is the ability to use both types of operators in the same query, for example:

> +\(joomla AND content AND management AND system\) -\(Wordpress AND Drupal\)
>
> \(+scully +mulder\) OR \(+reyes +doggett\) NOT skinner

We can also use field names to more accurately target our query. For example, if we want to search for authors:

> title:"The X-Files" author:\(+mulder +scully\) OR author:\(reyes OR doggett\) -author:skinner

### Range Query

Range queries allow you to search the index for records which fall between a lower and an upper value.

> price:\[100 TO 200\]

You can also mix ranges with other search queries:

> type\_s:"unsolved x-file" date\_s:\[1992-01-01 TO 2016-01-01\]

### Proximity Query

A proximity search tells Solr to search for particular words that are within a particular distance from one another:

> "mulder scully"~10

In this example, the terms mulder and scully must be within 10 words of each other.

### Boost Query {#TheStandardQueryParser-FuzzySearches}

You can give certain terms more relevance over other terms by "boosting" the particular term:

> mulder^10 scully

The above boost will make the term mulder more relevant than scully.

You can also boost entire phrases:

> "The Lone Gunmen"^10 "The X-Files"

And, you can specify boosts for search terms on a particular field:

> author:\(mulder AND scully\)^10 author:\(byers AND Frohike AND Langly\) title:"The Lone Gunmen"

Boost queries differ from boost fields in that you are boosting only the query not the entire field.

### Futher Reading

The above topics only cover the basics of what is available with Solr querying. For more information about these and other query syntax, check out:

* [Solr's Query Syntax](https://cwiki.apache.org/confluence/display/solr/Query+Syntax+and+Parsing) - Comprehensive documentation about querying in Solr
* [Writing Queries in Solr]([https://cwiki.apache.org/confluence/display/solr/The+Standard+Query+Parser\\#TheStandardQueryParser-SpecifyingTermsfortheStandardQueryParser](https://cwiki.apache.org/confluence/display/solr/The+Standard+Query+Parser#TheStandardQueryParser-SpecifyingTermsfortheStandardQueryParser) - Documentation and examples of the various methods of querying in Solr
* [Boolean Search]([https://cwiki.apache.org/confluence/display/solr/The+Standard+Query+Parser\\#TheStandardQueryParser-BooleanOperatorsSupportedbytheStandardQueryParser](https://cwiki.apache.org/confluence/display/solr/The+Standard+Query+Parser#TheStandardQueryParser-BooleanOperatorsSupportedbytheStandardQueryParser) - More information about boolean queries and how they work
* [Grouping](https://cwiki.apache.org/confluence/display/solr/The+Standard+Query+Parser#TheStandardQueryParser-GroupingTermstoFormSub-Queries) - Grouping query terms and phrases

## Multilingual Capabilities

JSolr is designed to index and search across multiple languages and seamlessly integrates with Joomla multilingual configuration. Search results are localized to the language the user is currently viewing the site in.

Language Management provides more information about multilingual capabilities and may be useful to programmers and webmasters.

## Advanced Features

There may be times when additional filters or advanced search may enhance the user experience. That's why JSolr provides powerful search capabilities which can be further enhanced through advanced configuration.

Extend JSolr's search capabilities by:

* [Providing an advanced search form for targeted queries and filters](/advanced-search.md)
* [Aliasing for easier querying on field names](/field-aliasing.md)
* [Using dimensions for targeting specific result types](/dimensions.md)
* [Customizing the user experience with JForm XML form definitions](/xml-form-definitions.md)



