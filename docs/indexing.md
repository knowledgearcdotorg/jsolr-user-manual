# Indexing
The first thing you will need to do when you install JSolr is to index some Joomla! content.

JSolr indexes content in one of two ways:
1. Via the command line tool,
2. Via JSolr plugin event triggers.

When you first index data or when you wish to rebuild your index, you will want to run the command line tool. There is currently no way to index existing data from the Joomla! web user interface; this is due to the nature of the index, which, for large amounts of content, may take minutes or even hours.

## Enabling some crawlers
JSolr uses Joomla!'s plugin framework to index and search specific content. Before you run the indexer, you will need to use the Joomla! Plugin Manager to enable and configure plugins for content you want to index (and ultimately search). Configuration varies from plugin to plugin, so you should consult the associated plugin documentation.

## Indexing from the command line
To index content in bulk, navigate to Joomla's cli directory. From there you will see the jsolr.php command line utility.
Run:
```
php jsolr.php index
```
If you need to purge (clean out) all results from the index, run:
```
php jsolr.php purge
```
For all jsolr command line options, run:
```
php jsolr.php help
```
You can also run help on particular commands:
```
php jsolr index help
```

## Indexing on-the-fly
To index in realtime (that is, when content is saved, deleted or changed) enable the relevant Content and JSolr plugins.
