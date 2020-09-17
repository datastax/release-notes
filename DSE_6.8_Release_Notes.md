# Release notes for DataStax Enterprise version 6.8.4
17 September 2020

## Component versions for DSE 6.8.4

   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

## DSE 6.8.4 Compaction

* Fixes compaction getting stuck on acquiring references for non-existing sstables. (DB-4290)


## DSE 6.8.4 CQL

* Distributes Netty connections more uniformly across TPC cores (DB-4683)


## DSE 6.8.4 MessagingService

* Distributes Netty connections more uniformly across TPC cores (DB-4683)


## DSE 6.8.4 Deprecated: Core

* Adds TTL and TimeWindowCompactionStrategy (TWCS) to system_distributed.repair_history and system_distributed.parent_repair_history tables.  (DB-2009)


## DSE 6.8.4 Core

* DNS Service Discovery is now a part of the DSE/LDAP integration. (DSP-11450)
* New system property to cap the maximum amount of memory used by bloom filters: {{-Dcassandra.max_bf_memory_mb}}. By default, this is _unlimited_. (DSP-21344)


## DSE 6.8.4 Security

* DNS Service Discovery is now a part of the DSE/LDAP integration. (DSP-11450)


## DSE 6.8.4 DSEFS

*  DSEFS waits for a schema agreement before starting and issuing the first CQL query. (DSP-20743)


## DSE 6.8.4 Indexing

* Storage-Attached Indexing (SAI) adds support for creating multiple SAI indexes on the same collection map column. 
See [SAI collection map examples with keys, values, and entries](https://docs.datastax.com/en/storage-attached-index/6.8/sai/saiUsing.html#saiUsing__saiUsingCollectionsExamples). (DSP-21306)


## TinkerPop changes for DSE 6.8.4

DataStax Enterprise (DSE) 6.8.4 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.
