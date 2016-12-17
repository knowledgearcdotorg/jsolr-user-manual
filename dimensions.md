## Dimensions

JSolr provides a way to display customized search results through the use of a feature called Dimensions. Dimensions show results which match certain filtering criteria, allowing you to have, for example, results tailored for showing images or downloadable files.

You will need to create a template override to display a dimension's search results. The name of the override must be results\_dimension-alias.php, where dimension-alias is the alias specified by your configured dimension.

Create the template override for your dimension and drop it into `templates/template-name/html/com_jsolr/search/`, where template-name is the name of the enabled template.

Finally, you can specify completely different query and filter inputs by creating a custom XML form definition. This must be named dimension-alias.xml and must reside in `templates/template-name/html/com_jsolr/forms`.

## Example

Let's assume you have built a custom JSolr crawler which indexes images and you would like to create an additional search page which only searches images. Your crawler also indexes a smaller "thumbnail" which is associated with each image and provides a preview of what the user will see when the click on a search result and are redirected to the displayed image. You want to build a simple gallery to show the search results, using the thumbnail as the preview image.

Anything indexed in JSolr must have a context so we'll assume it is "custom.image".

### Create the Dimension

First we must create the dimension.

Once you are logged into the Joomla! administrator, go to Components -&gt; JSolr. In the left slideout menu you will see "Search Dimensions". Click on it.

You are now in the Dimensions list. Click on "New" to create your new dimension.

Now you can specify the dimension settings, which looks much like a standard Joomla! component form and has a number of fields which you can use to specify customized search parameters. Specify the following field values:

* Title = "Images"
* Filter Query = "context\_s:custom.image"

Click "Save & Close" and you will see the new dimension in the dimensions list.  
There are two important things to note:

1. The alias will be automatically generated based on the "Title" field's value. In this case it will be "images",
2. We want to limit results to only those matching the images you have indexed using your custom crawler, hence we specify "context\_s:custom.image" where context\_s is the name of the Solr field we are going to limit results to and `custom.image` is the value we will filter on.

If you go to your Joomla! site's front end and run a search, you will see tabs available underneath the query box. "Images" will now be included in that tab list.

### Create the HTML Template

You now need to create a custom HTML template for your new dimension. We'll assume you are using the default protostar template.

Create a new file called `results_images.php` under `/path/to/your/joomla/site/templates/protostar/html/com_jsolr/search.` You may also need to create the directories underneath the html directory.

Inside this template add the following code and save:

```
<?php
defined('_JEXEC') or die('Restricted access');
?>
<h1>Image Gallery</h1>
```

Go back to the front-end of your site. Click on the `Images` tab. You should see the above template being loaded. You are now ready to program your search results gallery.

### Add More Query Parameters and Filters

You can also add facet filtering and additional query inputs to your new image search which will only apply to your image queries. For example, you may want to add a dropdown list of image types so a user can view just the png images.

Create another file called images.xml under `/path/to/your/joomla/site/templates/protostar/html/com_jsolr/forms`.

Open this file and add the following code, then save:

```
        <field
            type="jsolr.searchtool"
            name="type"
            filter="type_s"
            label="Image Type"
            default="">
           <option value="">All</option>
           <option value="jpeg">JPEG</option>
           <option value="png">PNG</option>
           <option value="svg">SVG</option>
        </field>
```

This will load a drop down box underneath the query box with a list of types.

See [XML Form Definitions](/xml-form-definitions.md) for more information about customizing search queries and filters.

