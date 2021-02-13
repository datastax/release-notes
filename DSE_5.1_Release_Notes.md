# Release notes for DataStax Enterprise 5.1
DSE 5.1.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any. Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.


# DataStax Enterprise 5.1.22
12 February 2021

## Components versions for DSE 5.1.21

   * Apache Solr™ 6.0.1.0.2810
   * Apache Spark™ 2.0.2.38
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240


## DSE 5.1.22 Auth

* Works around a bug (JDK-8148854) in JDK 1.8u282.  (DB-4884)
* Fixed an issue where "Failed to check permissions org.apache.cassandra.exceptions.InvalidRequestException: Key may not be empty" would appear excessively in logs. (DB-4806)


## DSE 5.1.22 CVE

* Update Tomcat version 8.0.53 to 8.5.61 (DSP-21394)


## DSE 5.1.22 Search

* Fixed a bug where FilterCache warmup triggered by node health change can block GossipStage-1 thread for several seconds (DSP-21674)

## DSE 5.1.22 Spark

*  Fix: Spark Master fails to start if keystore (used by web UI) contains more than one certificate (DSP-21703)



# DataStax Enterprise 5.1.21
5 February 2021
:warning: **NOTE**: This release was retracted due to a bug involving DSE Spark.  

## Components versions for DSE 5.1.21

   * Apache Solr™ 6.0.1.0.2810
   * Apache Spark™ 2.0.2.38&ast;
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.8.3-dse+20201217&ast;
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

## 5.1.21 DSE Cassandra

* Fix for `DESCRIBE TYPES` in cqlsh (DSP-21667)

## 5.1.21 DSE Core

* Add support for multiple authentication sources (LDAP + DSE Internal) (DSP-14233)
* Addressed several Jackson databind vulnerabilities by upgrading _jackson-databind_ to version `2.9.10.8` in DSE `5.1.21`, `6.0.15` and `6.7.13` and version `2.10.5.1` in DSE `6.8.10`. (DSP-21503)

## 5.1.21 DSE Spark

* Update _Jetty_ to `9.4.34.v20201102` and update Spark Version to `2.0.2.38` (DSP-21506)

## 5.1.21 DSE DSEFS

* Backport fsck throttling and LocationService to `5.1.21` (DSP-21258)

## 5.1.21 DSE Search

* A system property `dse.solr.fuzzy.max.expansion` was added. The property allows to workaround https://issues.apache.org/jira/browse/SOLR-4824 / DSP-19459 by defining a custom number of fuzzy query expansions. The maximal possible value is `1024`. When unset, the default number of max expansions is `50`. (DSP-21605)

## 5.1.21 DSE Security

* When optimized group retrieval was used in `memberof_search` mode (`ldap_options.all_parent_groups_search_type` parameter in `dse.yaml`), DSE confused attributes specified by `ldap_options.user_memberof_attribute` and `ldap_options.all_parent_groups_memberof_attribute` making the optimized search work only in case both attributes were set to the same value. (DSP-21537)

## 5.1.21 DSE SparkConnector

* DSE Spark supports connections to Astra clusters (DSP-21510)

## 5.1.21 DSE CommitLog

* Fixed a bug where some part of the commit log might not be replayed after injecting a foreign sstable to a node or, on 6.8, after zero-copy streaming of an sstable (DB-4629)

## 5.1.21 DSE Repair

* Fixed a bug when in rare cases a terminated repair session would leak on-heap memory (DB-4833)

## 5.1.21 DSE Tools

* SSTablePartitions tool will no longer fail with "histogram overflowed" when its working for the server code (DB-2952)
* SStableloader now uses `native_transport_port_ssl` over `native_transport_port` when passed a config file with the property set (DB-4632)


# DataStax Enterprise 5.1.20
8 October 2020

## Components versions for DSE 5.1.20
   * Apache Solr™ 6.0.1.0.2789
   * Apache Spark™ 2.0.2.37
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.2.8
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

## 5.1.20 DSE Security
* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)
* DNS Service Discovery is now a part of the DSE/LDAP integration. (DSP-11450)


## 5.1.20 DSE Core
* Adds TTL and `TimeWindowCompactionStrategy` (TWCS) to `system_distributed.repair_history` and `system_distributed.parent_repair_history` tables. (DB-2009)


## 5.1.20 DSE DSEFS
*  DSEFS waits for a schema agreement before starting and issuing the first CQL query. (DSP-20743)


## 5.1.20 DSE Spark
* Fix Spark Application contacting nodes in a Non Local DC  (DSP-19961)


## 5.1.20 DSE Backup and Restore
* Snapshot schema.cql files will now contain `IF NOT EXISTS` clause for `CREATE TYPE` statements (DB-4685)


## 5.1.20 DSE Compaction
* Fixes a problem where races in notifying compaction strategies of added and removed SSTables can cause compaction to try to use non-existing SSTables and repeatedly fail to make progress. (DB-4711)


## 5.1.20 DSE Schema
* Remove a race condition that may lead to reopening a keyspace during keyspace drop. (DB-4564)


## TinkerPop changes for DSE 5.1.20
DataStax Enterprise (DSE) DSE 5.1.20 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.2.11/upgrade/#_upgrading_for_users) for all changes.


# Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/5.1/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse

---
