# Module_2_What_Makes_Up_Splunk
Here is the Splunk Architecture:
![image](http://karunsubramanian.com/wp-content/uploads/2020/04/Hf.png)

There are 3 main components in Splunk:

- Splunk Forwarder, used for data forwarding
- Splunk Indexer, used for Parsing and Indexing the data
- Search Head, is a GUI used for searching, analyzing and reporting

![image](https://hkrtrainings.com/storage/photos/500/Splunk-Architecture6.png)

## Forwarder (F) 

Splunk Forwarder is the component which you have to use for collecting the logs. Suppose, you want to collect logs from a remote machine, then you can accomplish that by using Splunk’s remote forwarders which are independent of the main Splunk instance.

In fact, you can install several such forwarders in multiple machines, which will forward the log data to a Splunk Indexer for processing and storage. What if you want to do real-time analysis of the data? Splunk forwarders can be used for that purpose too. You can configure the forwarders to send data to Splunk indexers in real-time. You can install them in multiple systems and collect the data simultaneously from different machines in real time.

To understand how real time forwarding of data happens, you can read my blog on how Domino’s is using Splunk to gain operational efficiency.

Compared to other traditional monitoring tools, Splunk Forwarder consumes very less cpu ~1-2%. You can scale them up to tens of thousands of remote systems easily, and collect terabytes of data with minimal impact on performance.

![image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/11/Heavy-Forwarder-Functionality.png)
- Your sender of data
- Lives on the machine
- Feeds your raw data to the index

## Indexer (I)
ndexer is the Splunk component which you will have to use for indexing and storing the data coming from the forwarder. Splunk instance transforms the incoming data into events and stores it in indexes for performing search operations efficiently. If you are receiving the data from a Universal forwarder, then the indexer will first parse the data and then index it. Parsing of data is done to eliminate the unwanted data. But, if you are receiving the data from a Heavy forwarder, the indexer will only index the data.

As the Splunk instance indexes your data, it creates a number of files. These files contain one of the below:

Raw data in compressed form
Indexes that point to raw data (index files, also referred to as tsidx files), plus some metadata files
These files reside in sets of directories called buckets.

Let me now tell you how Indexing works.

Splunk processes the incoming data to enable fast search and analysis. It enhances the data in various ways like:

Separating the data stream into individual, searchable events
Creating or identifying timestamps
Extracting fields such as host, source, and sourcetype
Performing user-defined actions on the incoming data, such as identifying custom fields, masking sensitive data, writing new or modified keys, applying breaking rules for multi-line events, filtering unwanted events, and routing events to specified indexes or servers
This indexing process is also known as event processing.

Another benefit with Splunk Indexer is data replication. You need not worry about loss of data because Splunk keeps multiple copies of indexed data. This process is called Index replication or Indexer clustering. This is achieved with the help of an Indexer cluster, which is a group of indexers configured to replicate each other’s’ data.

![image](https://www.edureka.co/blog/wp-content/uploads/2016/11/Splunk-Indexer-150x150.png)

- Process your data
- Stores your events
- Has your raw data

## Search Head (SH)

Search head is the component used for interacting with Splunk. It provides a graphical user interface to users for performing various operations. You can search and query the data stored in the Indexer by entering search words and you will get the expected result.

You can install the search head on separate servers or with other Splunk components on the same server. There is no separate installation file for search head, you just have to enable splunkweb service on the Splunk server to enable it.

A Splunk instance can function both as a search head and a search peer. A search head that performs only searching, and not indexing is referred to as a dedicated search head. Whereas, a search peer performs indexing and responds to search requests from other search heads.

In a Splunk instance, a search head can send search requests to a group of indexers, or search peers, which perform the actual searches on their indexes. The search head then merges the results and sends them back to the user. This is a faster technique to search data called distributed searching.

Search head clusters are groups of search heads that coordinate the search activities. The cluster coordinates the activity of the search heads, allocates jobs based on the current loads, and ensures that all the search heads have access to the same set of knowledge objects.

![image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/11/Splunk-advanced-Architecture.png)

- Executes your search requests
- Where you put in your SPL
- Your interface to searching your indexers 

Look at the above image to understand the end to end working of Splunk. The images shows a few remote Forwarders that send the data to the Indexers. Based on the data present in the Indexer, you can use the Search Head to perform functions like searching, analyzing, visualizing and creating knowledge objects for Operational Intelligence.

The Management Console Host acts as a centralized configuration manager responsible for distributing configurations, app updates and content updates to the Deployment Clients. The Deployment Clients are Forwarders, Indexers and Search Heads.


# Splunk Architecture 
![image](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/11/SPLUNK-COMPLETE-ARCHITECURE.png)

- You can receive data from various network ports by running scripts for automating data forwarding
- You can monitor the files coming in and detect the changes in real time
- The forwarder has the capability to intelligently route the data, clone the data and do load balancing on that data before it reaches the indexer. Cloning is done to create multiple copies of an event right at the data source where as load balancing is done so that even if one instance fails, the data can be forwarded to another instance which is hosting the indexer
- As I mentioned earlier, the deployment server is used for managing the entire deployment, configurations and policies
W- hen this data is received, it is stored in an Indexer. The indexer is then broken down into different logical data stores and at each data store you can set permissions which will control what each user views, accesses and uses
- Once the data is in, you can search the indexed data and also distribute searches to other search peers and the results will merged and sent back to the Search head
- Apart from that, you can also do scheduled searches and create alerts, which will be triggered when certain conditions match saved searches
- You can use saved searches to create reports and make analysis by using Visualization dashboards
- Finally you can use Knowledge objects to enrich the existing unstructured data
- Search heads and Knowledge objects can be accessed from a Splunk CLI or a Splunk Web Interface. This communication happens over a REST API connection


## Cheat sheets
- [SANS Ultimate Cheat sheets](https://www.sans.org/blog/the-ultimate-list-of-sans-cheat-sheets/)

- [Extra from the Splunk documentation](https://www.testpreptraining.com/blog/splunk-enterprise-certified-admin-cheat-sheet/)

- [Splunk Best Practices](https://www.aplura.com/splunk-best-practices/)