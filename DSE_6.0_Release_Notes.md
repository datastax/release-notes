# Release notes for DataStax Enterprise 6.0
DSE 6.0.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any.

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


## DSE 6.0.14 CommitLog

* Fixed a bug where some part of the commit log might not be replayed after injecting a foreign SSTable to a node or, on 6.8, after zero-copy streaming of an SSTable (DB-4629)


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
