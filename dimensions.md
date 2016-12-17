## Dimensions

JSolr provides a way to display customized search results through the use of a feature called Dimensions. Dimensions show results which match certain filtering criteria, allowing you to have, for example, results tailored for showing images or downloadable files.

You will need to create a template override to display a dimension's search results. The name of the override must be results\_dimension-alias.php, where dimension-alias is the alias specified by your configured dimension.

Create the template override for your dimension and drop it into `templates/template-name/html/com_jsolr/search/`, where template-name is the name of the enabled template.
