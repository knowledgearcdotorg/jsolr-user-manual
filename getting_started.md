# Getting Started
This getting started is to get your JSolr search up and running as quickly as possible. If you would like to know more about how JSolr works and explore more advanced features, you can check out the following topics:
* [Configuration](configuration.md)
* [Indexing](indexing.md)
* [Searching](searching.md)
* [Browsing](browsing.md)
* [Extending JSolr](extending_jsolr.md)

## Step 1: Get JSolr
JSolr is available from Github.

[Download JSolr](https://github.com/knowledgearcdotorg/jsolr/releases/latest/)

## Step 2: Install
The JSolr Core is deployed as a Joomla! package. Follow the [installation instructions](installation.md) to get JSolr installed. 

## Step 3: Connect to Apache Solr
You won't be able to index anything without a Solr installation. This guide does not cover the installation and configuration of Solr. Instead see http://lucene.apache.org/solr/ for a complete guide to using Solr. You will also be able to download the Apache Solr binary.

Alternatively, you can use a hosted Solr service to get up and running quickly. [KnowledgeArc](http://knowledgearc.com) is one possible hosting solution which provides managed Solr indexes for a monthly fee.

Once you have Apache Solr running, log into the Joomla! administrator and specify the url of the Solr index (along with a username and password if required) via Components -> JSolr -> Options.

If the connection is successful, you will see the state of the connection in the JSolr control panel.

## Step 4: Enable the Plugins
The content indexed will depend on what JSolr plugins you have installed. The JSolr package includes two crawler plugins; JSolr - Content and JSolr - Newsfeeds. 

Enable the JSolr - Content plugin to index your Joomla! articles. You should also enable the Content - JSolr plugin so that JSolr can update the index when your content changes. All plugins can be managed from the Joomla! Plugin Manager.

## Step 5: Index some content
You are now ready to index your content. From the command line, locate your Joomla! installation directory and then the cli directory. From here you can run the jsolr command line indexer.

On Linux systems:

```
# php jsolr.php index -v
```

With the -v (verbose) option, you will be able to see what the indexer is doing. Once completed, you are ready to search your content.

## Step 6: Search your content
On a vanilla installation of Joomla!, JSolr search is available at http://your.domain.tld/index.php?option=com_jsolr&view=search, where your.domain.tld is the url you have Joomla! installed to.

