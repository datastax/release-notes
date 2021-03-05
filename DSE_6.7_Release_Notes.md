# Release notes for DataStax Enterprise 6.7
DSE 6.7.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any. Components that are indicated with an asterisk (*) (if any) are known to be updated since the prior patch version.


# DataStax Enterprise 6.7.13
5 March 2021

## Component versions for DSE 6.7.13

   * Apache Solr™ 6.0.1.2.2812
   * Apache Spark™ 2.2.3.17
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.5.61
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2

## DSE 6.7.13 Auth

* Fixes an issue where a login attempt with missing credentials logged a misleading warning message with stack trace instead of an error message about the missing username or password. (DB-4806)
* Works around a bug in JDK 1.8u282 (JDK-8260018) (DB-4884)


## DSE 6.7.13 CommitLog

* Addressed a bug where a CommitLogReplayException is caused by a bad header but correct CRC after restart (DB-3996)


## DSE 6.7.13 Distributed Read/Write

* Applied fix for CVE-2020-17516 (DB-4897)


## DSE 6.7.13 Repair

* Fixed a bug when in rare cases a terminated repair session would leak on-heap memory (DB-4833)


## DSE 6.7.13 Local Write-Read Paths

* Dropped messages metrics calculation doesn't cause assertion errors when dropped messages contain remote batch mutation. (DB-3905)


## DSE 6.7.13 Streaming

* Print a timestamp when nodetool exits due to an error (DB-4826)


## DSE 6.7.13 Tools

* SSTablePartitions tool will no longer fail with "histogram overflowed" when it is working for the server code (DB-2952)
* SStableloader now uses native_transport_port_ssl over native_transport_port when passed a config file with the property set (DB-4632)


## DSE 6.7.13 Build

* The version of dsbulk bundled with DSE has been updated to 1.7.0. (DSP-21535)


## DSE 6.7.13 Cassandra

* Data export from cqlsh is now less noisy in the logs (DSP-21494)
* Fixed intermittent ERROR: java.util.ConcurrentModificationException at org.apache.cassandra.transport.CBUtil.writeStringList (DSP-21336)
* Fixed a bug where the slow query log would fill with queries that do not meet the slow query threshold (DSP-21417)
* Fix for DESCRIBE TYPES in cqlsh (DSP-21667)
* Add support for multiple authentication sources (LDAP + DSE Internal) (DSP-14233)
* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)
* Fix a bug in `cassandra.repair.mutation_repair_rows_per_batch` setting that caused sending all repair mutations at once (DSP-21429)
* Addressed several Jackson databind vulnerabilities by upgrading jackson-databind to version 2.9.10.8 in DSE 5.1.21, 6.0.15 and 6.7.13 and version 2.10.5.1 in DSP 6.8.10. (DSP-21503) (DSP-21503)


## DSE 6.7.13 Security

* When optimized group retrieval was used in {{memberof_search}} mode ({{ldap_options.all_parent_groups_search_type}} parameter in {{dse.yaml}}), DSE confused attributes specified by {{ldap_options.user_memberof_attribute}} and {{ldap_options.all_parent_groups_memberof_attribute}} making the optimized search work only in case both attributes were set to the same value. (DSP-21537)


## DSE 6.7.13 CVE

* Update Tomcat version 8.0.53 to 8.5.61 (DSP-21394)
* Update Jetty to 9.4.34.v20201102 and update SparkVersion (DSP-21506)


## DSE 6.7.13 Spark

* SCC by default enables direct join optimization only when size_estimates for both tables are available.  (DSP-21628)
* Fix: Spark Master fails to start if keystore (used by web UI) contains more than one certificate (DSP-21703)


## DSE 6.7.13 Search

* A system property dse.solr.fuzzy.max.expansion was added. The property allows to workaround a Solr limitation (DSP-21605)
* search queries will no longer fail when querying clustering columns of certain types on which the order is reversed (DSP-21363)
* Fixed a bug where FilterCache warmup triggered by node health change can block GossipStage-1 thread for several seconds (DSP-21674)


## DSE 6.7.13 SparkConnector

* Fixed direct join optimization for spark sql. (DSP-21498)
* DSE Spark supports connections to Astra clusters  (DSP-21510)



# DataStax Enterprise 6.7.12
29 October 2020

## Components versions for DSE 6.7.12

   * Apache Solr™ 6.0.1.2.2791
   * Apache Spark™ 2.2.3.15
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.7.1
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2


## DSE 6.7.12 CommitLog/Streaming

* Fixed a bug where some part of the commit log might not be replayed after injecting a foreign sstable to a node or, on 6.8, after zero-copy streaming of an sstable (DB-4629)

## DSE 6.7.12 core

* Fix  extreme local pauses on all nodes in the cluster on a node restart (DB-4657)

## DSE 6.7.12 TPC

* Fixes problem in the scheduling of materialized view updates. (DB-4782)




## DataStax Enterprise 6.7.11
1 October 2020

## Components versions for DSE 6.7.11

   * Apache Solr™ 6.0.1.2.2791
   * Apache Spark™ 2.2.3.15
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.7.1
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2

## DSE 6.7.11 Cassandra

* Fix LDAP user permissions problem following LDAP server restart. (DSP-21284)


## DSE 6.7.11 Security

* Fix LDAP user permissions problem following LDAP server restart. (DSP-21284)


## DSE 6.7.11 Core

* New system property to cap the maximum amount of memory used by bloom filters: -Dcassandra.max_bf_memory_mb (DSP-21371)
* (6.7 only) jackson-databind upgraded to 2.9.10.4  (DSP-21257)
* Fix node restart issue after dropping a PointType column. (DSP-21326)
* Fix New system property to cap the maximum amount of memory used by bloom filters: -Dcassandra.max_bf_memory_mb. By default, this is _unlimited_. (DSP-21344)


## DSE 6.7.11 Spark

* Fix Spark Application contacting Nodes in Non Local DC  (DSP-19961)

## DSE 6.7.11 Backup and Restore

* Snapshot schema.cql files will now contain IF NOT EXISTS clause for CREATE TYPE statements (DB-4685)


## DSE 6.7.11 Compaction

* Fix a problem where races in notifying compaction strategies of added and removed sstables can cause compaction to try to use non-existing sstables and repeatedly fail to make progress. (DB-4711)


## DSE 6.7.11 Local Write-Read Paths

* Improves performance of estimation of partition counts for subranges. (DB-3679)


## TinkerPop changes for DSE 6.7.11

DataStax Enterprise (DSE) 6.7.11 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.


## Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/6.7/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse
