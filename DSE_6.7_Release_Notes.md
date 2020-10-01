# Release notes for DataStax Enterprise 6.7



# Release notes for DataStax Enterprise 6.7.11
10 October 2020

# Components versions for DSE 6.7.11

   * Apache Solr™ 6.0.1.2.2791
   * Apache Spark™ 2.2.3.15
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.7.1
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2

## DSE 6.7.11 Cassandra

* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)


## DSE 6.7.11 Security

* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)


## DSE 6.7.11 Core

* New system property to cap the maximum amount of memory used by bloom filters: -Dcassandra.max_bf_memory_mb (DSP-21371)
* (6.7 only) jackson-databind upgraded to 2.9.10.4  (DSP-21257)
* Fixes node restart issue after dropping a PointType column. (DSP-21326)
* Fix:New system property to cap the maximum amount of memory used by bloom filters: {{-Dcassandra.max_bf_memory_mb}}. By default, this is _unlimited_. This should be added to https://docs.datastax.com/en/dse/6.8/dse-admin/datastax_enterprise/config/cassandraSystemProperties.html page. (DSP-21344)


## DSE 6.7.11 Spark

* fix: Spark Application contacting Nodes in Non Local DC  (DSP-19961)

## DSE 6.7.11 Backup and Restore

* snapshot schema.cql files will now contain IF NOT EXISTS clause for CREATE TYPE statements (DB-4685)


## DSE 6.7.11 Compaction

* Fixes a problem where races in notifying compaction strategies of added and removed sstables can cause compaction to try to use non-existing sstables and repeatedly fail to make progress. (DB-4711)


## DSE 6.7.11 Local Write-Read Paths

* Improves performance of estimation of partition counts for subranges. (DB-3679)


## TinkerPop changes for DSE 6.7.11

DataStax Enterprise (DSE) 6.7.11 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.


## Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/6.7/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse
