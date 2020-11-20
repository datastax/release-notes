# Release notes for DataStax Enterprise 5.1
DSE 5.1.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any.

## DataStax Enterprise 5.1.20
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


## Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/5.1/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse
