# Release notes for DataStax Enterprise 6.0
DSE 6.0.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any. Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

# DataStax Enterprise 6.0.16
11 May 2021

**NOTE**: DSE `6.0.16` is the final release of the 6.0.x line.  Please consider upgrading to [DSE 6.8](./DSE_6.8_Release_Notes.md) for our latest features and patches.

## Components versions for DSE 6.0.16
   * Apache Solr™ 6.0.1.1.2838&ast;
   * Apache Spark™ 2.2.3.18&ast;
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.5.65&ast;
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.3&ast;

## DSE 6.0.16 Auth
* Fixes an issue where a login attempt with missing credentials logged a misleading warning message with stack trace instead of an error message about the missing username or password. (DB-4806)

## DSE 6.0.16 CQL
* Fix an error in cqlsh encoding unicode in multi-line statements (DB-4855)
* Make cqlsh prefer newer TLS versions. (DB-4966)

## DSE 6.0.16 Distributed Read/Write
* Applied fix for CVE-2020-17516 (DB-4897)
* Single node crash will no longer result in downtime with write in multi-DC setup when "dse.write.forwarding.disabled.consistency.levels" property is set for relevant Consistency Levels. (DB-2410)

## DSE 6.0.16 Legacy Repair
* Fixed a bug when in rare cases a terminated repair session would leak on-heap memory (DB-4833)

## DSE 6.0.16 SSTables
* Fixes a problem with nulls in tuples in the byte-comparable translation (i.e. sstables in bti format) as well as the comparator (i.e. sstables in big format, see CASSANDRA-19538). (DB-4813)

## DSE 6.0.16 AOSS
* AOSS returns additional parameter in ‘status' endpoint: “connection_hostname“. The new parameter is a FQDN of the node hosting AOSS, it may be used for connections (instead of connection_address) if needed. (DSP-21811)

## DSE 6.0.16 Cassandra
* Data export from cqlsh is now less noisy in the logs (DSP-21494)
* Fixed intermittent "ERROR: java.util.ConcurrentModificationException at org.apache.cassandra.transport.CBUtil.writeStringList" (DSP-21336)
* Fix for `DESCRIBE TYPES` in CQLSH (DSP-21667)

## DSE 6.0.16 Core
* Fixes SRCCLR-SID-22742: Insecure Input Validation Vulnerability in the Apache Commons Codec library (DSP-21747)
* Fixed an issue with DSE daemon unable to stop after the default timeout expired. The issue only happened in the systems that use package install and init.d, such as centos. (DSP-21804)
* Print a timestamp when nodetool exits due to an error (DB-4826)

## DSE 6.0.16 Security
* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)

## DSE 6.0.16 Hadoop
* Fixed CVE-2020-1945 affecting Apache Ant (DSP-21716)

## DSE 6.0.16 CVE
* Update tomcat version 8.0.53 to 8.5.61 (DSP-21394)
* upgrade apache `commons-compress` to address CVE-2019-12402 (DSP-21679)
* fixed CVE-2018-17197 affecting Apache Tika (DSP-21680)
* Addresses CVE-2018-11796, CVE-2018-11761, CVE-2019-10094, CVE-2019-10088 in the Apache Tika library. (DSP-21689)
* Update tomcat version 8.5.61 to 8.5.65 (DSP-21798)

## DSE 6.0.16 Search
* Fixed a bug where FilterCache warmup triggered by node health change can block GossipStage-1 thread for several seconds (DSP-21674)
* Fixed a bug where under heavy load solr query worker threads would use 100% CPU due to contention on thread local map
 (DSP-21746)
* A new jvm option is added: “dse.search.fc.warmup”: AUTO, ALWAYS & NEVER.  (DSP-21813)

## DSE 6.0.16 Spark
* Fixed CVE-2014-0114, CVE-2014-0114 (DSP-21668)

# DataStax Enterprise 6.0.15
12 February 2021

## Components versions for DSE 6.0.15
   * Apache Solr™ 6.0.1.1.2811&ast;
   * Apache Spark™ 2.2.3.17&ast;
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.8.3-dse+20201217&ast;
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2

## DSE 6.0.15 Auth
* Works around a bug (JDK-8148854) in JDK 1.8u282.  (DB-4884)

## DSE 6.0.15 CommitLog
* Addressed a bug where a `CommitLogReplayException` is caused by a bad header but correct CRC after restart (DB-3996)


## DSE 6.0.15 CommitLog

* Fixed a bug where some part of the commit log might not be replayed after injecting a foreign SSTable to a node or, on 6.8, after zero-copy streaming of an SSTable (DB-4629)

## DSE 6.0.15 Local Write-Read Paths
* Dropped messages metrics calculation doesn't cause assertion errors when dropped messages contain remote batch mutation. (DB-3905)

## DSE 6.0.15 Tools
* SSTablePartitions tool will no longer fail with "histogram overflowed" when its working for the server code (DB-2952)
* SStableloader now uses `native_transport_port_ssl` over `native_transport_port` when passed a config file with the property set (DB-4632)

## DSE 6.0.15 TPC
* Fixes a problem in the scheduling and counting of active materialized view updates that could cause too many to be executed concurrently, overwhelming the node. (DB-4782)

## DSE 6.0.15 Build
* The version of DSBulk bundled with DSE has been updated to 1.7.0. (DSP-21535)

## DSE 6.0.15 Cassandra
* Fixed a bug where the slow query log would fill with queries that do not meet the slow query threshold (DSP-21417)

## DSE 6.0.15 Core
* Add support for multiple authentication sources (LDAP + DSE Internal) (DSP-14233)
* fix a bug in `cassandra.repair.mutation_repair_rows_per_batch` setting that caused sending all repair mutations at once (DSP-21429)
* Addressed several Jackson databind vulnerabilities by upgrading jackson-databind to version 2.9.10.8 in DSE 5.1.21, 6.0.15 and 6.7.13 and version 2.10.5.1 in DSP 6.8.10. (DSP-21503) (DSP-21503)

## DSE 6.0.15 Docke
* Update Jetty to 9.4.34.v20201102 and update Spark Version (DSP-21506)

## DSE 6.0.15 Spark
* SCC by default enables direct join optimization only when size_estimates for both tables are available.  (DSP-21628)
* Fix: Spark Master fails to start if keystore (used by web UI) contains more than one certificate (DSP-21703)

## DSE 6.0.15 Search
* A system property dse.solr.fuzzy.max.expansion was added. The property allows to workaround [https://issues.apache.org/jira/browse/SOLR-4824](SOLR-4824) by defining a custom number of fuzzy query expansions. The maximal possible value is 1024.  When unset, the default number of max expansions is 50. (DSP-21605)
* Search queries will no longer fail when querying clustering columns of certain types on which the order is reversed (DSP-21363)

## DSE 6.0.15 Security
* When optimized group retrieval was used in {`memberof_search` mode (`ldap_options.all_parent_groups_search_type` parameter in `dse.yaml`), DSE confused attributes specified by `ldap_options.user_memberof_attribute` and `ldap_options.all_parent_groups_memberof_attribute` making the optimized search work only in case both attributes were set to the same value. (DSP-21537)

## DSE 6.0.15 SparkConnector
* Fixed direct join optimization for Spark SQL. (DSP-21498)
* DSE Spark now supports connections to Astra clusters.  (DSP-21510)

## DataStax Enterprise 6.0.14
26 October 2020

## Components versions for DSE 6.0.14

   * Apache Solr™ 6.0.1.1.2793
   * Apache Spark™ 2.2.3.15
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.6.10
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2

## DSE 6.0.14 Backup and Restore

* Snapshot `schema.cql` files now contain `IF NOT EXISTS` clause for `CREATE TYPE` statements (DB-4685)


## DSE 6.0.14 Compaction

* Fixed a problem where races in notifying compaction strategies of added and removed SSTables can cause compaction to try to use non-existing SSTables and repeatedly fail to make progress. (DB-4711)


## DSE 6.0.14 core

* Fixed extreme local pauses on all nodes in the cluster on a node restart. (DB-4657)
* Added TTL and `TimeWindowCompactionStrategy` (TWCS) to `system_distributed.repair_history` and `system_distributed.parent_repair_history` tables. (DB-2009)
* Fixed node restart issue after dropping a `PointType` column. (DSP-21326)
* Added new system property to cap the maximum amount of memory used by bloom filters: `-Dcassandra.max_bf_memory_mb`. By default, this is _unlimited_. (DSP-21344)


## DSE 6.0.14 Local Write-Read Paths

* Improved performance of estimation of partition counts for subranges. (DB-3679)


## DSE 6.0.14 Schema

* Removed a race condition that may lead to reopening a keyspace during keyspace drop. (DB-4564)


## DSE 6.0.14 Security

* Fixed LDAP user permissions problem following LDAP server restart. (DSP-21284)



## DSE 6.0.14 DSEFS

*  DSEFS waits for a schema agreement before starting and issuing the first CQL query. (DSP-20743)


## DSE 6.0.14 Spark

* SPARK-18838 backported to DSE Spark 2.2.3. (DSP-21300)
* Fixed Spark Applications contacting Nodes in non-local DC.  (DSP-19961)


## Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/6.0/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse
