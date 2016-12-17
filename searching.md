# Searching

JSolr provides a powerful searching experience out-of-the-box where users can simply type what they are looking for and get back a list of relevant results. 

However, there may be times when additional filters or advanced search may enhance the user experience. That's why JSolr provides powerful search capabilities which can be further enhanced through advanced configuration.

## Dimensions

JSolr provides a way to display customized search results through the use of a feature called Dimensions. Dimensions show results which match certain filtering criteria, allowing you to have, for example, results tailored for showing images or downloadable files.

You will need to create a template override to display a dimension's search results. The name of the override must be results\_dimension-alias.php, where dimension-alias is the alias specified by your configured dimension.

Create the template override for your dimension and drop it into `templates/template-name/html/com_jsolr/search/`, where template-name is the name of the enabled template.

## Search XML Form Definitions

With JSolr you can customize the way your users search your web site content.

JSolr uses [Joomla!'s XML form definitions](https://docs.joomla.org/XML_JForm_form_definitions) to provide additional methods of filtering search results; you can even change the search query field if you need a different type of query input.

