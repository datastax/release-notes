# Release notes for DataStax Enterprise
DSE 6.8.x is compatible with Apache Cassandra 3.11 and adds additional production-certified changes, if any.  

# Release notes for DataStax Enterprise version 6.8.6
12 November 2020

## Components versions for DSE 6.8.6

   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

## DSE 6.8.6 Bootstrap

* A node may be stuck in repair while joining the cluster if broadcast_address is set differently than local_address (DB-4786)


# Release notes for DataStax Enterprise version 6.8.5
20 October 2020

   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

## DSE 6.8.5 Backup and Restore

* Server side backup and restore now supports Microsoft Azure cloud storage as a backup target. (DB-3894)
* snapshot `schema.cql` files will now contain `IF NOT EXISTS` clause for `CREATE TYPE` statements (DB-4685)


## DSE 6.8.5 Compaction

* Fixes a problem where races in notifying compaction strategies of added and removed sstables can cause compaction to try to use non-existing sstables and repeatedly fail to make progress. (DB-4711)


## DSE 6.8.5 Core

* Fixes node restart issue after dropping a PointType column. (DSP-21326)
* Fix extreme local pauses on all nodes in the cluster on a node restart. (DB-4657)


## DSE 6.8.5 Local Write-Read Paths

* Improves performance of estimation of partition counts for subranges. (DB-3679)


## DSE 6.8.5 Virtual Tables

* Fsync nodes metadata to prevent FSReadError issues on startup. (DB-4672)

## DSE 6.8.5 Cassandra

* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)


## DSE 6.8.5 Security

* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)


## DSE 6.8.5 Graph

* No text in Doc Notes field. (DSP-21450)

## DSE 6.8.5 Spark

* fix: Spark Application contacting Nodes in Non Local DC  (DSP-19961)

## TinkerPop changes for DSE 6.8.5

DataStax Enterprise (DSE) 6.8.4 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.



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


## DSE 6.8.4 Core

* Adds TTL and TimeWindowCompactionStrategy (TWCS) to system_distributed.repair_history and system_distributed.parent_repair_history tables.  (DB-2009)
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


## Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/6.8/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse
