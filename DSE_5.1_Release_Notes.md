# Release notes for DataStax Enterprise 5.1
DSE 5.1.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any. Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.


# Release notes for 5.1.32
18 July 2022

## Components versions for DSE 5.1.32
 * Apache Solr™ 6.0.1.0.2939&ast;
 * Apache Spark™ 2.0.2.43&ast;
 * Apache TinkerPop™ 3.2.11-20210716-faea8d16
 * Apache Tomcat® 8.5.75
 * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
 * Netty 4.0.54.1.dse
 * Spark JobServer 0.6.2.241&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.32 DSE Core
* Implemented ability to replace the THREE consistency level with an ALL_BUT_ONE consistency level. (DSP-22366)
* Replaced `1.9.13` version of `jackson-core-asl` and `jackson-mapper-asl` to be `1.9.13.1.dse` which contains the security fix. (DSP-22389, [CVE-2019-10172](https://nvd.nist.gov/vuln/detail/CVE-2019-10172))
* Removed dependency to Xerces2 Java XML Parser library. (DSP-22391, [CVE-2012-0881](https://nvd.nist.gov/vuln/detail/CVE-2012-0881), [CVE-2013-4002](https://nvd.nist.gov/vuln/detail/CVE-2013-4002))
* Removed the PMD plugin from gradle config. (DSP-22575, [CVE-2019-7722](https://nvd.nist.gov/vuln/detail/CVE-2019-7722))
* Fixed the cqlsh tool to restore the ability to use the EXECUTE AS command. (DSP-22417)
* Fixed bug with overriding customer limits.d file if there are new values in the package upgrade. Complementary to DSP-21928. (DSP-22594)

## 5.1.32 DSE Cassandra
* Updated outdated `nofile` parameter value to `1048576` in `/etc/security/limits.d/cassandra.conf`. (DSP-21947)
* Ported CASSANDRA-16987 and fixed python version check bug in cqlsh. (DSP-22517)

## 5.1.32 DSE Search
* Upgraded Solr libraries `metadata-extractor` to `2.18.0` and `XmpCore` to `6.1.11`. (DSP-22406, [CVE-2019-14262](https://nvd.nist.gov/vuln/detail/CVE-2019-14262))
* Fixed parsing range queries on DSE Search indexed columns of CQL types Date and Time. (DSP-22548)
* Changed Tomcat {{showServerInfo}} configuration parameter to {{false}} for not exposing Tomcat version in error pages. (DSP-22561)

## 5.1.32 DSE Spark
* Upgraded spark library version containing change to sanitize passwords when printing spark commands to `stderr`. (DSP-22481)

## 5.1.32 DSE CVE
* Upgraded apache-shiro used by spark-jobserver to version 1.8.0. (DSP-22579, [CVE-2021-41303](https://nvd.nist.gov/vuln/detail/CVE-2021-41303))


# Release notes for 5.1.31
11 May 2022

## Components versions for DSE 5.1.31
 * Apache Solr™ 6.0.1.0.2882
 * Apache Spark™ 2.0.2.42
 * Apache TinkerPop™ 3.2.11-20210716-faea8d16
 * Apache Tomcat® 8.5.75&ast;
 * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
 * Netty 4.0.54.1.dse
 * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.31 DSE Core
* Improved reading logic to ensure that sstables are not unnecessarily read for columns that are not selected. See CASSANDRA-16737. (Previously DB-4974). (DSP-22478)
* Fixed the `URISyntaxException: Malformed IPv6 address` when using `nodetool` or `dsetool` with Java 8u331 or 11.0.15. This is due to the recent changes of JDK-8278972, in which parsing of URL Strings in Built-in JNDI Providers is more strict. (DSP-22474)

## 5.1.31 DSE Cassandra
* Greater than '>' and less than '<' operators are swapped in the slow query log for a table with DESC clustering keys (port CASSANDRA-15503). (DSP-22369)
* Fixed a rare race condition where attempting to read from a sstable would fail with an assertion error. (DSP-22431)

## 5.1.31 DSE Security
* Upgraded Bouncy Castle to the latest 1.70 version. (DSP-22352)

## 5.1.31 DSE CVE
* Upgraded apache-commons compress library to 1.21 version. This version upgrade fixed several vulnerabilities that could be used to mount a denial of service attack against specially-crafted services that use a compress or decompress sevenz, tar, or zip package. (DSP-22383, [CVE-2021-35515](https://nvd.nist.gov/vuln/detail/CVE-2021-35515), [CVE-2021-35516](https://nvd.nist.gov/vuln/detail/CVE-2021-35516), [CVE-2021-35517](https://nvd.nist.gov/vuln/detail/CVE-2021-35517), [CVE-2021-36090](https://nvd.nist.gov/vuln/detail/CVE-2021-36090))
* Upgraded snakeyaml version to 1.30. (DSP-22386, [CVE-2017-18640](https://nvd.nist.gov/vuln/detail/CVE-2017-18640))
* Upgraded logback version to 1.2.11. This fixes a vulnerability affecting logback-classic and logback-core. (DSP-22237, [CVE-2021-42550](https://nvd.nist.gov/vuln/detail/CVE-2021-42550))
* Upgraded version of Apache Tomcat from 8.5.72 to 8.5.75. (DSP-22360, [CVE-2022-23181](https://nvd.nist.gov/vuln/detail/CVE-2022-23181))


# Release notes for 5.1.30
7 March 2022

## Components versions for DSE 5.1.30
 * Apache Solr™ 6.0.1.0.2882
 * Apache Spark™ 2.0.2.42
 * Apache TinkerPop™ 3.2.11-20210716-faea8d16
 * Apache Tomcat® 8.5.72
 * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
 * Netty 4.0.54.1.dse
 * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.30 DSE Core
* Introduces system property "cassandra.commitlog.skip_file_advice" that allows to skip the native call to "fadvise" with "FADV_DONTNEED" argument after the commit log is flushed. The native call is not skipped by default and therefore has no effect. (DSP-22315)
* MemoryOnlyStrategy tables will always use mmap disk access mode, the cassandra.yaml setting will be ignored for those tables. (DSP-22246)

## 5.1.30 DSE Cassandra
* With disk_access_mode ‘auto’ (default value) DSE will map only index files on 64-bit JVM unless there is no limit for `-Djdk.nio.maxCachedBufferSize` or `-XX:+DisableExcplicitGC` is set for the DSE JVM. (DSP-22079)
* Lower commitlog replay sstable origin warning to info. (DSP-22270)

## 5.1.30 DSE CVE
* Removed log4j 1.2.x dependency from dse-spark/client/lib and replace it with reload4j 1.2.19. (DSP-22279, [CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228), [CVE-2019-17571](https://nvd.nist.gov/vuln/detail/CVE-2019-17571), [CVE-2022-23305](https://nvd.nist.gov/vuln/detail/CVE-2022-23305), [CVE-2022-23302](https://nvd.nist.gov/vuln/detail/CVE-2022-23302), [CVE-2021-4104](https://nvd.nist.gov/vuln/detail/CVE-2021-4104))
* Upgraded version of Bouncy Castle to 1.67. (DSP-22301, [CVE-2018-1000613](https://nvd.nist.gov/vuln/detail/CVE-2018-1000613), [CVE-2018-1000180](https://nvd.nist.gov/vuln/detail/CVE-2018-1000180), [CVE-2020-28052](https://nvd.nist.gov/vuln/detail/CVE-2020-28052))


# Release notes for 5.1.29
17 February 2022

## Components versions for DSE 5.1.29
 * Apache Solr™ 6.0.1.0.2882
 * Apache Spark™ 2.0.2.42
 * Apache TinkerPop™ 3.2.11-20210716-faea8d16
 * Apache Tomcat® 8.5.72
 * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
 * Netty 4.0.54.1.dse
 * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.29 DSE Cassandra
* Ported fix from CASSANDRA-17352: Remote code execution for scripted UDFs (DSP-22321, [CVE-2021-44521](https://nvd.nist.gov/vuln/detail/CVE-2021-44521))

# Release notes for 5.1.28
18 January 2022

## Components versions for DSE 5.1.28
 * Apache Solr™ 6.0.1.0.2882
 * Apache Spark™ 2.0.2.42
 * Apache TinkerPop™ 3.2.11-20210716-faea8d16
 * Apache Tomcat® 8.5.72&ast;
 * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
 * Netty 4.0.54.1.dse
 * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.28 DSE Cassandra
* Await timeout for shutting down non periodic tasks is now configurable with the new jvm option `cassandra.non_periodic_tasks_shutdown_timeout_in_minutes`. When timeout is reached, force shutdown those tasks. (DSP-22241)

## 5.1.28 DSE Upgrade
* Retain changes to /etc/security/limits.d/cassandra.conf on yum upgrade. (DSP-21928)

## 5.1.28 DSE CVE
* Upgraded version of Apache Tomcat from 8.5.70 to 8.5.72 to fix CVE-2021-42340. (DSP-22098, [CVE-2021-42340](https://nvd.nist.gov/vuln/detail/CVE-2021-42340))


# DataStax Enterprise 5.1.27
26 November 2021

# Components versions for DSE 5.1.27
   * Apache Solr™ 6.0.1.0.2882
   * Apache Spark™ 2.0.2.42
   * Apache TinkerPop™ 3.2.11-20210716-faea8d16
   * Apache Tomcat® 8.5.70
   * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.27 DSE Cassandra
* Enables periodic logging of system status (default every 5 minutes, configurable). (DSP-22039)
* Fix a possible issue that shell tool could break with `-h`/`--help` in package install. (DSP-20375)

## 5.1.27 DSE core
* Port CASSANDRA-16671: Cassandra can return no row when the row columns have been deleted. Issue not reproduced on 5.1 but brings code to parity with OSS version. (DB-5008)
* Port CASSANDRA-16712: DROP COMPACT STORAGE does not invalidate prepared statements as it should. (DB-5044)

## 5.1.27 DSE CQL
* Prints TLS protocol information when running cqlsh with `--debug` parameter. (DB-4981)

## 5.1.27 DSE Spark
* Storing and revoking permissions for the application owner is removed. The application owner is explicitly assumed to have these permissions (backported DSP-19393). (DSP-21740)
* Fixed and updated javax.mail dependency to com.sun.mail. (DSP-22085)

## 5.1.27 DSE Security
* Storing and revoking permissions for the application owner is removed. The application owner is explicitly assumed to have these permissions (backported DSP-19393). (DSP-21740)


# DataStax Enterprise 5.1.26
21 September 2021

## Components versions for DSE 5.1.26
   * Apache Solr™ 6.0.1.0.2882&ast;
   * Apache Spark™ 2.0.2.42
   * Apache TinkerPop™ 3.2.11-20210716-faea8d16&ast;
   * Apache Tomcat® 8.5.70&ast;
   * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.26 DSE core
* Added check against the negative value in local stream throughput (stream_throughput_outbound_megabits_per_sec) and inter dc stream throughput (inter_dc_stream_throughput_outbound_megabits_per_sec) (DB-5010)

## 5.1.26 DSE SSTables
* Backported fixes from CASSANDRA-15595 that prevent IllegalBound exceptions in tables with huge data and CASSANDRA-15869 that fixes MemoryOutputStream overflow on large bloom filters. (DB-5035)

## 5.1.26 DSE CVE
* Upgraded Tomcat version from 8.5.65 to 8.5.70 to fix CVE-2021-33037. (DSP-21996)
* Upgraded Bootstrap version from 3.1.1 to 3.4.1 and Flask from 0.10.1 to 1.1.4 to fix CVE-2019-8331, CVE-2016-10735, CVE-2018-1000656, and CVE-2019-1010083. (DSP-21682)
* Ported fix from SOLR-12514 to dse lucene-Solr to fix CVE-2018-11802. (DSP-21685)
* Upgraded version of PDFBox and FontBox to 2.0.24, and version of JempBox to 1.8.16 to fix CVE-2018-8036 and CVE-2018-11797. (DSP-21688)
* Upgraded version of directory-ldap-api from DSE 1.0.0.2.dse to OSS 1.0.3 to fix CVE-2018-1337. (DSP-21758)
* Upgraded version of groovy to 2.4.21 (DSE 5.1/6.0/67) and to 2.5.14 (DSE 6.8) to fix CVE-2020-17521. (DSP-21767)

# DataStax Enterprise 5.1.25
16 July 2021

## 5.1.25 DSE Platform
* Provide DSE support for Ubuntu 20.04 (Focal) (DSP-21330). Please note that certification was done using Python 2.7 and Python 2.7 needs to be available on the target system.

## Components versions for DSE 5.1.25
   * Apache Solr™ 6.0.1.0.2841
   * Apache Spark™ 2.0.2.42
   * Apache TinkerPop™ 3.2.11-20210601-6b27fbde
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 5.1.25 DSE Auth
* Removed a possible false-positive error message in the log that would cause confusion when multiple authentication schemes are defined.
 (DB-5015)

## 5.1.25 DSE CQL
* Added unit test cases for logic cqlsh TLS version. (DB-4979)

## 5.1.25 DSE Cassandra
* Added warning message in case of cases where dse was started with duplicated -Xmx options when used in jvm-server.options (DSP-21795)

## 5.1.25 DSE CVE
* Upgraded jetty version from `9.4.34.v20201102` to `9.4.41.v20210516` (DSP-21684, DSP-21687)

## 5.1.25 DSE Search
* Fixed a bug where in rare cases search query routing might start to spin endlessly for a particular query (DSP-21838)

## 5.1.25 DSE Security
* Fixed an issue in the LDAP `group_search_filter` default value that meant that group hierarchies were not being loaded if the `group_search_filter` was not explicitly set in the dse.yaml. (DSP-21874)

# DataStax Enterprise 5.1.24
6 May 2021

## Components versions for DSE 5.1.24
   * Apache Solr™ 6.0.1.0.2841
   * Apache Spark™ 2.0.2.42
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 5.1.24 Core
* Fixed a potential issue that users may have tombstone deletion time in the future updated to the current time if they run `nodetool scrub`. (DB-4982)
* Fixed an issue with DSE daemon unable to stop after the default timeout expired. The issue only happened in the systems that use package install and init.d, such as centos. (DSP-21804)

# DataStax Enterprise 5.1.23
3 May 2021

:warning: **NOTE**: Due to a bug which affects DSE `5.1.23`, this release has been retracted.  We recommend against upgrading to this version at this time. This bug is already addressed in DSE `5.1.24`. All features and fixes for `5.1.23` are present in `5.1.24`.

## Components versions for DSE 5.1.23
   * Apache Solr™ 6.0.1.0.2841&ast;
   * Apache Spark™ 2.0.2.42&ast;
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.5.65&ast;
   * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 5.1.23 Core
* Adds a new flag -t <number of days> for sstablescrub to update deletion times which are in the future. It accepts a command-line argument: -t <number of days>. All deletion times further in the future than the given number of days will be reset to the current time. (DB-4912)
* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)

## DSE 5.1.23 CQL
* Fix an error in cqlsh encoding unicode in multi-line statements (DB-4855)
* Make cqlsh prefer newer TLS versions. (DB-4966)

## DSE 5.1.23 Schema
* CDC property per table is now propagated regardless CDC is enabled in yaml or not. CDC property is not propagated when there are nodes running C&ast; 3.0 or DSE 5.0 in the cluster (upgrade state). During the upgrade we also prohibit toggling CDC property on per-table basis. (DB-4926

## DSE 5.1.23 SSTables
* Fixes a problem with nulls in tuples in the byte-comparable translation (i.e. sstables in `bti` format) as well as the comparator (i.e. sstables in `big` format, see CASSANDRA-19538). (DB-4813)

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
* A new jvm option is added: “dse.search.fc.warmup”: AUTO, ALWAYS & NEVER.  Warmup will be disabled for cases when it’s either set to NEVER or set to AUTO with Non-Static type for cover finder & Vnodes are enabled. For all other scenarios, it will be enabled. (DSP-21813)

# DataStax Enterprise 5.1.22
12 February 2021

## Components versions for DSE 5.1.22
   * Apache Solr™ 6.0.1.0.2810
   * Apache Spark™ 2.0.2.38
   * Apache TinkerPop™ 3.2.11-20200603-0524f70f
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.8.3-dse+20201217 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

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
   * DSE Java Driver 1.8.3-dse+20201217&ast; (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

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
   * DSE Java Driver 1.2.8 (DSE *internal-only* version)
   * Netty 4.0.54.1.dse
   * Spark JobServer 0.6.2.240

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

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
