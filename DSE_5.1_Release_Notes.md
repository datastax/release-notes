# Release notes for DataStax Enterprise 5.1
DSE 5.1.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any. Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

# DataStax Enterprise 5.1.23
3 May 2021

## Components versions for DSE 5.1.23

   * Apache Solr™ 6.0.1.0.2841
   * Apache Spark™ 2.0.2.42
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

## DSE 5.1.23 Core

* Adds a new flag -t <number of days> for sstablescrub to update deletion times which are in the future. It accepts a command-line argument: -t <number of days>. All deletion times further in the future than the given number of days will be reset to the current time. (DB-4912)
* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)

## DSE 5.1.23 CQL

* Fix an error in cqlsh encoding unicode in multi-line statements (DB-4855)
* Make cqlsh prefer newer TLS versions. (DB-4966)


## DSE 5.1.23 Schema

* CDC property per table is now propagated regardless CDC is enabled in yaml or not. CDC property is not propagated when there are nodes running C&ast; 3.0 or DSE 5.0 in the cluster (upgrade state). During the upgrade we also prohibit toggling CDC property on per-table basis. (DB-4926)


## DSE 5.1.23 SSTables

* Fixes a problem with nulls in tuples in the byte-comparable translation (i.e. sstables in bti format) as well as the comparator (i.e. sstables in big format, see CASSANDRA-19538). (DB-4813)


## DSE 5.1.23 Streaming

* Print a timestamp when nodetool exits due to an error (DB-4826)


## DSE 5.1.23 Cassandra

* Data export from cqlsh is now less noisy in the logs (DSP-21494)


## DSE 5.1.23 Security

* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)
* Fixes an issue where a user-defined function can be defined without arguments and then cannot be read when listing UDFs.   (DSP-21791)


## DSE 5.1.23 CVE

* Upgrade apache commons-compress to address CVE-2019-12402 (DSP-21679)
* Addresses CVE-2018-11796, CVE-2018-11761, CVE-2019-10094, CVE-2019-10088 in the Apache Tika library. (DSP-21689)
* Update tomcat version 8.5.61 to 8.5.65 (DSP-21798)
* Applied fix for CVE-2020-17516 (DB-4897)
* Fixed CVE-2020-1945 affecting Apache Ant (DSP-21716)
* Fixes SRCCLR-SID-22742: Insecure Input Validation Vulnerability in the Apache Commons Codec library (DSP-21747)


## DSE 5.1.23 Search

* Fixed a bug where FilterCache warmup triggered by node health change can block GossipStage-1 thread for several seconds (DSP-21674)
* Fixed a bug where under heavy load solr query worker threads would use 100% CPU due to contention on thread local map (DSP-21746)


# DataStax Enterprise 5.1.22
12 February 2021

## Components versions for DSE 5.1.22
   * Apache Solr™ 6.0.1.0.2810
   * Apache Spark™ 2.0.2.38
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

## DSE 5.1.22 Spark
* Fix: Spark Master fails to start if keystore (used by web UI) contains more than one certificate (DSP-21703)

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

## DSE 5.1.21 Auth
* Works around a bug (JDK-8148854) in JDK 1.8u282.  (DB-4884)

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
