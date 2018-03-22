# Configuration
JSolr makes it easy to embed archived items within Joomla!.

**NOTE:** Some of the following topics assume you have a working knowledge of configuring components and creating menu items.

**NOTE:** This manual does not cover the installation and configuration of Apache Solr nor any topics related to Solr query building. For Solr-related information, check out [their comprehensive wiki](https://cwiki.apache.org/confluence/display/solr/Apache+Solr+Reference+Guide).

## Component Options
JSolr provides various component-wide settings; these are available from the "Options" button in the JSolr control panel.

### Connection Settings
To configure JSolr to connect to your Apache Solr server, configure the full url to your Solr core. If your Solr server requires authentication, specify the username and password as well.
There is an optional secondary connection provided for Solr infrastructures which implement an alternative location for read-only indexes. JSolr searches will use the secondary connection if configured.

### Indexing
There are various options available when indexing data to the Solr server.

#### Index attachments
JSolr provides full text indexing of files such as PDF, Open Document and Microsoft Office as well as file metadata extraction.
If you turn on index attachments you can specify the files which should be parsed and which extractor should be used. There are currently two extractors available; a local, command line-based extractor called Apache Tika, and a server known as JAXRS. The server will provide faster extraction.

#### Use Autocommit
You can force Apache Solr to automatically commit indexed data when particular requirements are met. By default, JSolr plugins will do this for you so in nearly all cases leave Autocommit off. If you need to speed up commit times, modify the Commits Within and Commit Within values.

#### Facet Separator
To deal with case-sensitivity, JSolr stores facets as both lowercase and original case. The separator allows JSolr to separate the facet value for display. If the default value causes issues, change this value. For most JSolr installations you should not need to change this value.

### Searching
JSolr exposes various Solr-specific settings for manipulating search queries.

Check out [Apache Solr's comprehensive wiki](https://cwiki.apache.org/confluence/display/solr/Apache+Solr+Reference+Guide) for details about these settings.

#### Filter by Access
Enable this setting if JSolr should only show results based on the currently logged in user.

### Search Layout

#### Link to Advanced Search
You can change the way the Advanced Search is presented to the user. 

#### Embed Facets
To show facets as part of the component, select "Yes". To use the JSolr Facet Filter module for showing facet filters, select "No".