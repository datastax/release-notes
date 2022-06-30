# Release notes for DataStax Enterprise 6.7
DSE 6.7.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any. Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

:warning: **NOTE**: DSE `6.7.x` line has [EOSL date of November 30, 2022](https://www.datastax.com/legal/supported-software).  Please consider upgrading to [DSE 6.8](./DSE_6.8_Release_Notes.md) for our latest features and patches.

# Release notes for 6.7.17
31 May 2022

## Components versions for DSE 6.7.17
 * Apache Solr™ 6.0.1.2.2886&ast;
 * Apache Spark™ 2.2.3.18
 * Apache TinkerPop™ 3.3.11-20210727-ba40007e&ast;
 * Apache Tomcat® 8.5.75&ast;
 * DSE Java Driver 1.8.3-dse+20201217
 * Netty 4.1.25.7.dse
 * Spark JobServer 0.8.0.45.3

## 6.7.17 DSE Core
* Improved reading logic to ensure that sstables are not unnecessarily read for columns that are not selected. See CASSANDRA-16737. (Previously DB-4974). (DSP-22478)
* Fixed a bug that {{mode_by_authentication}} is not being picked up when using sstableloader. (DSP-22067)
* Fixed stack overflow error with secondary indexes on collections. (DSP-22070)
* Fixed the URISyntaxException: Malformed IPv6 address when using nodetool or dsetool with Java 8u331 or 11.0.15. This is due to the recent changes of JDK-8278972, in which parsing of URL Strings in Built-in JNDI Providers is more strict. (DSP-22474)

## 6.7.17 DSE Cassandra
* Enabled periodic logging of system status (default every 5 minutes, configurable). (DSP-22039)
* Made await timeout for shutting down non periodic tasks configurable with the new jvm option {{cassandra.non_periodic_tasks_shutdown_timeout_in_minutes}}. When timeout is reached, force shutdown those tasks. (DSP-22241)
* Lowered commitlog replay sstable origin warning to info. (DSP-22270)
* Fixed -h/--help option not working in sstableloader and other tools in the package installed DSE. (DSP-20375)
* Added warning message in case of cases where dse was started with duplicated -Xmx options when used in jvm-server.options. (DSP-21795)
* Fixed swapped greater than ('>') and less than ('<') operators in the slow query log for a table with DESC clustering keys (port CASSANDRA-15503). (DSP-22369)
* Fixed a rare race condition where attempting to read from a sstable would fail with an assertion error. (DSP-22431)

## 6.7.17 DSE Spark
* Fixed broken partition filtering in hive metastore leading to missing data in the spark-sql queries results for queries involving numeric partition keys or complex conditions. (DSP-21651)
* Fixed and updated javax.mail dependency to com.sun.mail. (DSP-22085)

## 6.7.17 DSE Upgrade
* Fixed a bug of not retaining changes to /etc/security/limits.d/cassandra.conf on yum upgrade. (DSP-21928)

## 6.7.17 DSE Security
* Upgraded Bouncy Castle to the latest 1.70 version. (DSP-22352)
* Fixed an issue in the LDAP group_search_filter default value that meant that group hierarchies were not being loaded if the group_search_filter was not explicitly set in the dse.yaml. (DSP-21874)

## 6.7.17 DSE CVE
* Upgraded apache-commons compress library to 1.21 version. This version upgrade fixed several vulnerabilities that could be used to mount a denial of service attack against specially-crafted services that use a compress or decompress sevenz, tar, or zip package. (DSP-22383, [CVE-2021-35515](https://nvd.nist.gov/vuln/detail/CVE-2021-35515), [CVE-2021-35516](https://nvd.nist.gov/vuln/detail/CVE-2021-35516), [CVE-2021-35517](https://nvd.nist.gov/vuln/detail/CVE-2021-35517), [CVE-2021-36090](https://nvd.nist.gov/vuln/detail/CVE-2021-36090))
* Upgraded snakeyaml version to 1.30. (DSP-22386, [CVE-2017-18640](https://nvd.nist.gov/vuln/detail/CVE-2017-18640))
* Upgraded Tomcat version from 8.5.65 to 8.5.70. (DSP-21996, [CVE-2021-33037](https://nvd.nist.gov/vuln/detail/CVE-2021-33037))
* Updated snake yaml version 1.15 to 1.28 in TinkerPop. Updated TinkerPop version to 3.3.11-20210601-5204e405. (DSP-21395, [CVE-2017-18640](https://nvd.nist.gov/vuln/detail/CVE-2017-18640))
* Upgraded version of Apache Tomcat from 8.5.70 to 8.5.72. (DSP-22098, [CVE-2021-42340](https://nvd.nist.gov/vuln/detail/CVE-2021-42340))
* Upgraded Bootstrap version from 3.1.1 to 3.4.1 and Flask from 0.10.1 to 1.1.4. (DSP-21682, [CVE-2019-8331](https://nvd.nist.gov/vuln/detail/CVE-2019-8331), [CVE-2016-10735](https://nvd.nist.gov/vuln/detail/CVE-2016-10735), [CVE-2018-1000656](https://nvd.nist.gov/vuln/detail/CVE-2018-1000656), [CVE-2019-1010083](https://nvd.nist.gov/vuln/detail/CVE-2019-1010083))
* Ported fix from SOLR-12514 to dse lucene-Solr. (DSP-21685, [CVE-2018-11802](https://nvd.nist.gov/vuln/detail/CVE-2018-11802))
* Upgraded version of PDFBox and FontBox to 2.0.24, and version of JempBox to 1.8.16. (DSP-21688, [CVE-2018-8036](https://nvd.nist.gov/vuln/detail/CVE-2018-8036), [CVE-2018-11797](https://nvd.nist.gov/vuln/detail/CVE-2018-11797))
* Upgraded version of directory-ldap-api from DSE 1.0.0.2.dse to OSS 1.0.3. (DSP-21758, [CVE-2018-1337](https://nvd.nist.gov/vuln/detail/CVE-2018-1337))
* Upgraded version of groovy to 2.4.21 in DSE 5.1, 6.0, 6.7 and 2.5.14 in DSE 6.8. Upgraded version of TinkerPop to {{3.2.11-20210716-faea8d16}} in 5.1, {{3.3.11-20210727-ba40007e}} in 6.0, 6.7, and {{3.4.5-20210816-c28c0de2}} in 6.8. (DSP-21767, [CVE-2020-17521](https://nvd.nist.gov/vuln/detail/CVE-2020-17521))
* Upgraded logback version to 1.2.11. This fixes a vulnerability affecting logback-classic and logback-core. (DSP-22237, [CVE-2021-42550](https://nvd.nist.gov/vuln/detail/CVE-2021-42550))
* Upgraded version of Apache Tomcat from 8.5.72 to 8.5.75. (DSP-22360, [CVE-2022-23181](https://nvd.nist.gov/vuln/detail/CVE-2022-23181))
* Removed log4j 1.2.x dependency from dse-spark/client/lib and replace it with reload4j 1.2.19. (DSP-22279, [CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228), [CVE-2019-17571](https://nvd.nist.gov/vuln/detail/CVE-2019-17571), [CVE-2022-23305](https://nvd.nist.gov/vuln/detail/CVE-2022-23305), [CVE-2022-23302](https://nvd.nist.gov/vuln/detail/CVE-2022-23302), [CVE-2021-4104](https://nvd.nist.gov/vuln/detail/CVE-2021-4104))
* Upgraded version of Bouncy Castle to 1.67. (DSP-22301, [CVE-2018-1000613](https://nvd.nist.gov/vuln/detail/CVE-2018-1000613), [CVE-2018-1000180](https://nvd.nist.gov/vuln/detail/CVE-2018-1000180), [CVE-2020-28052](https://nvd.nist.gov/vuln/detail/CVE-2020-28052))

# DataStax Enterprise 6.7.16
17 February 2022

## Components versions for DSE 6.7.16
   * Apache Solr™ 6.0.1.2.2839
   * Apache Spark™ 2.2.3.18
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.3

## 6.7.16 DSE Cassandra
* Ported fix from CASSANDRA-17352: Remote code execution for scripted UDFs (DSP-22321, [CVE-2021-44521](https://nvd.nist.gov/vuln/detail/CVE-2021-44521))

# DataStax Enterprise 6.7.15
17 June 2021

## Components versions for DSE 6.7.15
   * Apache Solr™ 6.0.1.2.2839
   * Apache Spark™ 2.2.3.18
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.3

## 6.7.15 DSE CVE
* Upgraded jetty version from 9.4.34.v20201102 to 9.4.41.v20210516 (DSP-21684, DSP-21687)

## 6.7.15 DSE Search
* Fix for a bug where in rare cases search query routing might start to spin endlessly for a particular query (DSP-21838)

## 6.7.15 DSE Core
* Adding a new flag `-t <number of days>` for `sstablescrub` to update deletion times which are in the future. It accepts a command-line argument: `-t <number of days>`. All deletion times further in the future than the given number of days will be reset to the current time. Also fixed a potential issue that users may have the deletion time in the future updated to the current time if they run `nodetool scrub`. (DB-4964)

## 6.7.15 DSE CQL
* Added unit test cases for logic cqlsh TLS version. (DB-4979)

## 6.7.15 DSE SSTables
* When the Bloom filter is recreated due to FP chance change, sstable metadata is loaded and re-written in order to update validation metadata with the new fp chance. However, the loaded metadata lacked compaction metadata, so when rewritten, compaction metadata got truncated. (DB-5005)

# DataStax Enterprise 6.7.14
17 May 2021

## Components versions for DSE 6.7.14
   * Apache Solr™ 6.0.1.2.2839&ast;
   * Apache Spark™ 2.2.3.18&ast;
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.5.65&ast;
   * DSE Java Driver 1.8.3-dse+20201217
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.3&ast;

## DSE 6.7.14 CQL
* Fix an error in cqlsh encoding unicode in multi-line statements (DB-4855)
* Make cqlsh prefer newer TLS versions. (DB-4966)

## DSE 6.7.14 SSTables
* Fixes a problem with nulls in tuples in the byte-comparable translation (i.e. sstables in `bti` format) as well as the comparator (i.e. sstables in `big` format, see CASSANDRA-19538). (DB-4813)

## DSE 6.7.14 AOSS
* AOSS returns additional parameter in 'status' endpoint: "connection_hostname". The new parameter is a FQDN of the node hosting AOSS, it may be used for connections (instead of `connection_address`) if needed. (DSP-21811)

## DSE 6.7.14 Core
* Fixed CVE-2020-1945 affecting Apache Ant (DSP-21716)
* Fixes SRCCLR-SID-22742: Insecure Input Validation Vulnerability in the Apache Commons Codec library (DSP-21747)
* Fixed an issue with DSE daemon unable to stop after the default timeout expired. The issue only happened in the systems that use package install and init.d, such as centos. (DSP-21804)

## DSE 6.7.14 CVE
* Upgrade apache `commons-compress` to address CVE-2019-12402 (DSP-21679)
* Fixed CVE-2018-17197 affecting Apache Tika (DSP-21680)
* Addresses CVE-2018-11796, CVE-2018-11761, CVE-2019-10094, CVE-2019-10088 in the Apache Tika library. (DSP-21689)
* Update tomcat version 8.5.61 to 8.5.65 (DSP-21798)

## DSE 6.7.14 Search
* Fixed a bug where under heavy load solr query worker threads would use 100% CPU due to contention on thread local map (DSP-21746)
* A new jvm option is added: `dse.search.fc.warmup`: `AUTO`, `ALWAYS` & `NEVER`.  (DSP-21813)

## DSE 6.7.14 Spark
* Fixed CVE-2014-0114, CVE-2014-0114 (DSP-21668)

# DataStax Enterprise 6.7.13
5 March 2021

## Component versions for DSE 6.7.13
   * Apache Solr™ 6.0.1.2.2812&ast;
   * Apache Spark™ 2.2.3.17&ast;
   * Apache TinkerPop™ 3.3.7-20190521-f71ce0d7
   * Apache Tomcat® 8.5.61&ast;
   * DSE Java Driver 1.8.3-dse+20201217&ast;
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.45.2

## DSE 6.7.13 Auth
* Fixes an issue where a login attempt with missing credentials logged a misleading warning message with stack trace instead of an error message about the missing username or password. (DB-4806)
* Works around a bug in JDK 1.8u282 (JDK-8260018) (DB-4884)

## DSE 6.7.13 CommitLog/Streaming
* Addressed a bug where a *CommitLogReplayException* is caused by a bad header but correct CRC after restart (DB-3996)
* Fixed a bug where some part of the commit log might not be replayed after injecting a foreign sstable to a node or, on 6.8, after zero-copy streaming of an sstable (DB-4629)


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
* SStableloader now uses `native_transport_port_ssl` over `native_transport_port` when passed a config file with the property set (DB-4632)

## DSE 6.7.13 Build
* The version of DSBulk bundled with DSE has been updated to `1.7.0`. (DSP-21535)

## DSE 6.7.13 Cassandra
* Data export from cqlsh is now less noisy in the logs (DSP-21494)
* Fixed intermittent *ERROR: java.util.ConcurrentModificationException at org.apache.cassandra.transport.CBUtil.writeStringList* (DSP-21336)
* Fixed a bug where the slow query log would fill with queries that do not meet the slow query threshold (DSP-21417)
* Fix for `DESCRIBE TYPES` in CQLSH (DSP-21667)
* Add support for multiple authentication sources (LDAP + DSE Internal) (DSP-14233)
* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)
* Fix a bug in `cassandra.repair.mutation_repair_rows_per_batch` setting that caused sending all repair mutations at once (DSP-21429)
* Addressed several Jackson databind vulnerabilities by upgrading `jackson-databind` to version `2.9.10.8` in DSE 5.1.21, 6.0.15 and 6.7.13 and version 2.10.5.1 in DSP 6.8.10. (DSP-21503) (DSP-21503)

## DSE 6.7.13 Security
* When optimized group retrieval was used in `memberof_search` mode (`ldap_options.all_parent_groups_search_type` parameter in `dse.yaml`), DSE confused attributes specified by `ldap_options.user_memberof_attribute` and `ldap_options.all_parent_groups_memberof_attribute` making the optimized search work only in case both attributes were set to the same value. (DSP-21537)

## DSE 6.7.13 CVE
* Update Tomcat version 8.0.53 to 8.5.61 (DSP-21394)
* Update Jetty to 9.4.34.v20201102 and update SparkVersion (DSP-21506)

## DSE 6.7.13 Spark
* SCC by default enables direct join optimization only when size_estimates for both tables are available.  (DSP-21628)
* Fix: Spark Master fails to start if keystore (used by web UI) contains more than one certificate (DSP-21703)

## DSE 6.7.13 Search
* A system property `dse.solr.fuzzy.max.expansion` was added. The property allows to workaround a Solr limitation (DSP-21605)
* Search queries will no longer fail when querying clustering columns of certain types on which the order is reversed (DSP-21363)
* Fixed a bug where `FilterCache` warmup triggered by node health change can block `GossipStage-1` thread for several seconds (DSP-21674)

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

## DSE 6.7.12 core
* Fix  extreme local pauses on all nodes in the cluster on a node restart (DB-4657)

## DSE 6.7.12 TPC
* Fixes problem in the scheduling of materialized view updates. (DB-4782)

# DataStax Enterprise 6.7.11
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
* New system property to cap the maximum amount of memory used by bloom filters: `-Dcassandra.max_bf_memory_mb` (DSP-21371)
* (6.7 only) jackson-databind upgraded to 2.9.10.4  (DSP-21257)
* Fix node restart issue after dropping a `PointType` column. (DSP-21326)
* Fix New system property to cap the maximum amount of memory used by bloom filters: `-Dcassandra.max_bf_memory_mb`. By default, this is _unlimited_. (DSP-21344)

## DSE 6.7.11 Spark
* Fix Spark Application contacting Nodes in Non Local DC  (DSP-19961)

## DSE 6.7.11 Backup and Restore
* Snapshot `schema.cql` files will now contain `IF NOT EXISTS` clause for `CREATE TYPE` statements (DB-4685)

## DSE 6.7.11 Compaction
* Fix a problem where races in notifying compaction strategies of added and removed sstables can cause compaction to try to use non-existing sstables and repeatedly fail to make progress. (DB-4711)

## DSE 6.7.11 Local Write-Read Paths
* Improves performance of estimation of partition counts for subranges. (DB-3679)

## TinkerPop changes for DSE 6.7.11
DataStax Enterprise (DSE) 6.7.11 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.

# Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/6.7/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse

---
