# Release notes for DataStax Enterprise 6.8
DSE 6.8.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any.
Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

# Release notes for 6.8.37
10 July 2023

## Components versions for DSE 6.8.37
 * Apache Solr™ 6.0.1.4.2959
 * Apache Spark™ 2.4.0.28
 * Apache TinkerPop™ 3.4.14-20230523-37856751
 * Apache Tomcat® 8.5.89
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse
 * Spark JobServer 0.8.0.54

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.37 DSE Core
* Allowed to encrypt `kmip_host` passwords in the `dse.yaml` file. New optional parameter `password_encryption_key_name` was added to the `kmip_hosts` items. DSP-23326 enabled password encryption before placing them in `dse.yaml`. (DSP-23313)
* Fixed the issue with dropping the UDT column, which potentially leads to a problem accessing data from the affected table after the node is restarted. (DSP-23337)

## 6.8.37 DSE Cassandra
* Fixed race condition causing sstableloader to hang when the Connections Per Host (`-cph`) value is greater than one (1). (DSP-23117)

## 6.8.37 DSE Docker
* Updated official DSE Docker image, basing it on a more current Ubuntu 20.04 (Focal Fossa) that is FIPS certified and handles multiple known CVEs. (DSP-23397)

## 6.8.37 DSE Indexing
* Improved SAI index-building process when reloading SSTables by building the indexes in parallel. (DSP-23415)
* Reduced allocations by removing some unnecessary autoboxing from SAI range iterators. (DSP-23419)
* Improved SAI exact match queries performance on the memtable index data by skipping unnecessary size calculations. (DSP-23280)
* Fixed a bug in the SAI intersection comparison. (DSP-23375)

## 6.8.37 DSE CVE
* Upgraded Apache mina-core library to version 2.0.24. (DSP-23378, [CVE-2021-41973](https://nvd.nist.gov/vuln/detail/CVE-2021-41973))
* Upgraded Azure SDK client libraries to be based on BOM 1.2.13. (DSP-23382, [CVE-2023-1370](https://nvd.nist.gov/vuln/detail/CVE-2023-1370))
* Updated aws-java-sdk to version 1.12.486. (DSP-23383, [CVE-2022-31159](https://nvd.nist.gov/vuln/detail/CVE-2022-31159))
* Upgraded Apache Commons libraries to recently available versions: `commons-io` to `2.11.0`, `commons-lang3` to `3.12.0`, `commons-math3` to `3.6.1`, and `commons-collection4` to `4.4`. (DSP-23384, [CVE-2021-29425](https://nvd.nist.gov/vuln/detail/CVE-2021-29425))
* Upgraded `xerial/snappy-java` library to version `1.1.10.1`. (DSP-23391, DSP-23433, [CVE-2023-34453](https://nvd.nist.gov/vuln/detail/CVE-2023-34453), [CVE-2023-34454](https://nvd.nist.gov/vuln/detail/CVE-2023-34454), [CVE-2023-34455](https://nvd.nist.gov/vuln/detail/CVE-2023-34455))
* Upgraded Jetty to version `9.4.51.v20230217`. (DSP-23428, [CVE-2023-26048](https://nvd.nist.gov/vuln/detail/CVE-2023-26048))
* Removed all dependencies on Netty 3 known to have security vulnerabilities. (DSP-22562, [CVE-2019-16869](https://nvd.nist.gov/vuln/detail/CVE-2019-16869))


# Release notes for 6.8.36
12 June 2023

## Components versions for DSE 6.8.36
 * Apache Solr™ 6.0.1.4.2959
 * Apache Spark™ 2.4.0.28&ast;
 * Apache TinkerPop™ 3.4.14-20230523-37856751&ast;
 * Apache Tomcat® 8.5.89&ast;
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse
 * Spark JobServer 0.8.0.54&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.36 DSE Core
* Fixed compaction to ensure tombstones are not pruned for data in SSTables that are excluded from the compaction due to limited disk space. This fixes CASSANDRA-18507. (DSP-23305)

## 6.8.36 DSE Cassandra
* Improved logging around index summary building. Introduced rounding that effectively uses the `min_index_interval` option set to a multiple of 128 in the index summary building process. (DSP-23317)

## 6.8.36 DSE Search
* Fixed the bug in the Solr UI permissions when accessing segments information. It was not working with authorization enabled by implementing a  segments view when granting the `SELECT` permission on the Solr-indexed table. (DSP-22295)

## 6.8.36 DSE Node/DseTool
* Added `--key` option to dsetool encryptconfigvalue command to allow using different key than the default one. (DSP-23326)

## 6.8.36 DSE Miscellaneous
* Fixed memory leak in the chunk cache metadata caching. (DSP-23316)

## 6.8.36 DSE CVE
* Upgraded commons-net library used in Hadoop and Tinkerpop. Removed old Hadoop `1.0.3` dependency and replaced it with version universally used in DSE (`2.7.1.x` for 5.1  and `2.10.2.x` for 6.8). (DSP-23327, [CVE-2021-37533](https://nvd.nist.gov/vuln/detail/CVE-2021-37533), [CVE-2012-4449](https://nvd.nist.gov/vuln/detail/CVE-2012-4449))
* Upgraded Apache Tomcat to version `8.5.89`. (DSP-23329, [CVE-2023-28709](https://nvd.nist.gov/vuln/detail/CVE-2023-28709))


# Release notes for 6.8.35
10 May 2023

## Components versions for DSE 6.8.35
 * Apache Solr™ 6.0.1.4.2959
 * Apache Spark™ 2.4.0.27
 * Apache TinkerPop™ 3.4.14-20230215-3db1ca33
 * Apache Tomcat® 8.5.87
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse
 * Spark JobServer 0.8.0.53

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.35 DSE Core
* Fixed regression in KMIP encryption introduced in DSP-22164. Moved the logic required for using old HashiVault KMIP under the feature flag `experimental_custom_attributes_mode` in dse.yaml, defined per kmip_hosts.per-kmip-group section. (DSP-23278)

## 6.8.35 DSE Indexing
* Fixed SAI numeric index validation on SSTables with over 2 billion rows. (DSP-23255)

## 6.8.35 DSE Other
* Improved CQLSH to support Python 3.11 and changed preferred interpreter from python2 to python3. Introduced CQLSH_PYTHON environment variable to allow users to specify the python interpreter used by CQLSH. (DSP-23257)

## 6.8.35 DSE CVE
* Upgraded org.codehaus.jettison:jettison library to version 1.5.4. (DSP-23254, [CVE-2023-1436](https://nvd.nist.gov/vuln/detail/CVE-2023-1436))
* Upgraded com.google.auto.factory:auto-factory to version 1.0.1 to remove the dependency on org.eclipse.equinox. (DSP-22864, [CVE-2021-41033](https://nvd.nist.gov/vuln/detail/CVE-2021-41033))


# Release notes for 6.8.34
11 April 2023

## Components versions for DSE 6.8.34
 * Apache Solr™ 6.0.1.4.2959&ast;
 * Apache Spark™ 2.4.0.27
 * Apache TinkerPop™ 3.4.14-20230215-3db1ca33
 * Apache Tomcat® 8.5.87&ast;
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse
 * Spark JobServer 0.8.0.53

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.34 DSE Core
* Set default systemd dse.service startup timeout to 7 minutes. (DSP-23225)

## 6.8.34 DSE Cassandra
* Fixed memory leak that can happen while handling inbound large messages. (DSP-23156)

## 6.8.34 DSE Search
* Fixed race condition occurring in DSE Search with enabled real-time (RT) indexing that was causing client-side failures under query-heavy workload. (DSP-23184)

## 6.8.34 DSE Build
* Updated OS versions used to create DSE packages (Ubuntu 12.04 for `.deb` packages, and CentOS 7.9 for `.rpm` packages). (DSP-22750)

## 6.8.34 DSE Security
* Fixed regression scenario where DSE was not using keys on the KMIP server that were created either by a previous DSE version or outside of DSE. Regression was introduced in DSE v6.8.22. (DSP-23182)

## 6.8.34 DSE CVE
* Upgraded `org.json:json` to `20230227` to resolve a Denial of Service (DoS) vulnerability. In addition, upgraded `esri-geometry-api` to `2.2.4`. (DSP-23187, [CWE-400](https://nvd.nist.gov/vuln/detail/CWE-400))
* Upgraded commons-fileupload to 1.5. Added a solrconfig.xml setting that limits the number of files allowed in multipart update requests. (DSP-23188, [CVE-2023-24998](https://nvd.nist.gov/vuln/detail/CVE-2023-24998))
* Upgraded Apache Tomcat to version 8.5.87. (DSP-23205, [CVE-2023-24998](https://nvd.nist.gov/vuln/detail/CVE-2023-24998))


# Release notes for 6.8.33
6 March 2023

## Components versions for DSE 6.8.33
 * Apache Solr™ 6.0.1.4.2951&ast;
 * Apache Spark™ 2.4.0.27&ast;
 * Apache TinkerPop™ 3.4.14-20230215-3db1ca33&ast;
 * Apache Tomcat® 8.5.84
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse
 * Spark JobServer 0.8.0.53&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.33 DSE Core
* Exposed two configuration properties: `-Dcassandra.counter_locks_per_core` and `-Dcassandra.lwt_locks_per_core` to be tuned for intensive counter batch workloads when observing WriteTimeoutExceptions.  For example, update the default of 1024 to `-Dcassandra.lwt_locks_per_core=16384`. (DSP-23163)
* Fixed SAI index metrics initialization potentially causing dse start failure due to NullPointerException. (DSP-23192)

## 6.8.33 DSE Platform
* Added support for Rocky Linux 9. (DSP-22732)
* Added support for Rocky Linux 8. (DSP-23170)

## 6.8.33 DSE Miscellaneous
* Fixed RPM package install for platforms requiring systemd services. (DSP-23146)

## 6.8.33 DSE CVE
* Upgraded libthrift to v0.9.3-1. (DSP-18096, [CVE-2018-1320](https://nvd.nist.gov/vuln/detail/CVE-2018-1320))
* Upgraded groovy-sandbox to 1.20.1.DSE, which is a DataStax version based on OSS v1.20 that contains additional fixes. (DSP-21677, [CVE-2018-1000865](https://nvd.nist.gov/vuln/detail/CVE-2018-1000865))
* Ported a security fix from Spark 2.4.6 that prevents RCE on unauthenticated Spark resource manager. (DSP-21782, [CVE-2020-9480](https://nvd.nist.gov/vuln/detail/CVE-2020-9480))
* Removed Postgresql driver from spark-jobserver. (DSP-22894, [CVE-2022-21724](https://nvd.nist.gov/vuln/detail/CVE-2002-21724), [CVE-2020-13692](https://nvd.nist.gov/vuln/detail/CVE-2020-13692), [CVE-2018-10936](https://nvd.nist.gov/vuln/detail/CVE-2018-10936))
* Upgraded insights-collectd to version 0.1.5 that removed libmodbus.so. (DSP-22809, [CVE-2022-0367](https://nvd.nist.gov/vuln/detail/CVE-2022-0367))
* Upgraded Gson that is used in Solr to v2.10.1. (DSP-22798, [CVE-2022-25647](https://nvd.nist.gov/vuln/detail/CVE-2022-25647))
* Upgraded Apache Derby used in Spark to v10.14.2.0. (DSP-23008, [CVE-2018-1313](https://nvd.nist.gov/vuln/detail/CVE-2018-1313))
* Removed unused, outdated org.mortbay.jetty libraries. (DSP-23004, [CVE-2011-4461](https://nvd.nist.gov/vuln/detail/CVE-2011-4461))
* Upgraded Jettison to 1.5.3, Xerces to 2.12.2, and Gson Hadoop to 2.10.1. Enforced the same Hadoop 2.10.2.x version for all DSE components. (DSP-23120, [CVE-2022-40149](https://nvd.nist.gov/vuln/detail/CVE-2022-40149), [CVE-2022-40150](https://nvd.nist.gov/vuln/detail/CVE-2022-40150), [CVE-2013-4002](https://nvd.nist.gov/vuln/detail/CVE-2013-4002))
* Upgraded Jcommander used in SJK to v1.82. (DSP-21783, [SRCCLR-SID-22555](https://nvd.nist.gov/vuln/detail/SRCCLR-SID-22555))


# Release notes for 6.8.32
7 February 2023

## Components versions for DSE 6.8.32
 * Apache Solr™ 6.0.1.4.2947&ast;
 * Apache Spark™ 2.4.0.24&ast;
 * Apache TinkerPop™ 3.4.14-20230124-b2e47e9a&ast;
 * Apache Tomcat® 8.5.84
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse
 * Spark JobServer 0.8.0.52

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.32 DSE Core
* Added logging of unexpected failures in asynchronous reactive code. (DSP-23111)

## 6.8.32 DSE Cassandra
* Fixed incorrect count(*) results when hitting guardrail paging limits. (DSP-22813)

## 6.8.32 DSE Search
* Allow the use of date with time in Solr range queries on SimpleDateField fields (time will be truncated). (DSP-23085)

## 6.8.32 DSE Node/DseTool
* Fixed the CLI usage of namespace filtering in the dsetool utility. (DSP-23064)
* Fixed the dsetool utility ‘managekmip revoke’ command to correctly set the ‘compromiseOccurrenceDate’ field. (DSP-23110)

## 6.8.32 DSE Miscellaneous
* Fixed error preventing cqlsh COPY from Mac M1 hardware. (DSP-22996)

## 6.8.32 DSE CVE
* Upgraded httpclient version to 4.5.14 version. (DSP-22831, [CVE-2020-13956](https://nvd.nist.gov/vuln/detail/CVE-2020-13956))
* Upgraded Spark to version that is based on Hadoop 2.10.2. (DSP-22923, [CVE-2016-6811](https://nvd.nist.gov/vuln/detail/CVE-2016-6811), [CVE-2017-3162](https://nvd.nist.gov/vuln/detail/CVE-2017-3162))
* Upgraded TinkerPop to a version that uses Hadoop 2.10.2. (DSP-23092, [CVE-2022-25168](https://nvd.nist.gov/vuln/detail/CVE-2022-25168), [CVE-2021-33036](https://nvd.nist.gov/vuln/detail/CVE-2021-33036), [CVE-2021-37404](https://nvd.nist.gov/vuln/detail/CVE-2021-37404), [CVE-2020-9492](https://nvd.nist.gov/vuln/detail/CVE-2020-9492), [CVE-2018-8009](https://nvd.nist.gov/vuln/detail/CVE-2018-8009), [CVE-2016-3086](https://nvd.nist.gov/vuln/detail/CVE-2016-3086), [CVE-2016-6811](https://nvd.nist.gov/vuln/detail/CVE-2016-6811), [CVE-2016-5393](https://nvd.nist.gov/vuln/detail/CVE-2016-5393))


# Release notes for 6.8.31
9 January 2023

## Components versions for DSE 6.8.31
 * Apache Solr™ 6.0.1.4.2943
 * Apache Spark™ 2.4.0.23
 * Apache TinkerPop™ 3.4.14-20221125-fd3c10f9
 * Apache Tomcat® 8.5.84&ast;
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.86.1.dse&ast;
 * Spark JobServer 0.8.0.52&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.31 DSE Core
* Added a guarding exception that prevents the creation of an invalid range tombstone. Improved range tombstone addition by skipping the creation of a tombstone for the empty range. (DSP-23075)

## 6.8.31 DSE Hadoop
* Upgraded Hadoop direct dependency to 2.10.2.1, a new version that is based on OSS 2.10.2. (DSP-22922)

## 6.8.31 DSE CVE
* Upgraded apache-shiro used by spark-jobserver to version 1.10.1. (DSP-23019, [CVE-2022-32532](https://nvd.nist.gov/vuln/detail/CVE-2022-32532), [CVE-2022-40664](https://nvd.nist.gov/vuln/detail/CVE-2022-40664))
* Upgraded Netty to version 4.1.86.Final. (DSP-23062, [CVE-2022-41915](https://nvd.nist.gov/vuln/detail/CVE-2022-41915), [CVE-2022-41881](https://nvd.nist.gov/vuln/detail/CVE-2022-41881))
* Upgraded Tomcat to version 8.5.84. (DSP-23017, [CVE-2022-34305](https://nvd.nist.gov/vuln/detail/CVE-2022-34305))


# Release notes for 6.8.30
12 December 2022

## Components versions for DSE 6.8.30
 * Apache Solr™ 6.0.1.4.2943&ast;
 * Apache Spark™ 2.4.0.23&ast;
 * Apache TinkerPop™ 3.4.14-20221125-fd3c10f9&ast;
 * Apache Tomcat® 8.5.79
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.78.1.dse
 * Spark JobServer 0.8.0.51

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.30 DSE Insights
* Changed log messages added when Insights functionality cannot be started from ERROR to WARN. (DSP-22962)

## 6.8.30 DSE Installer: Debian
* Fixed Debian package dependencies on Python so that it can be installed on Ubuntu 22.04. (DSP-22961)

## 6.8.30 DSE CVE
* Use `com.google.cloud:libraries-bom:26.1.3` libraries for GCE backup and restore functionality. Upgraded Guava from 19.0 to 31.1-jre. (DSP-22904, [CVE-2020-8908](https://nvd.nist.gov/vuln/detail/CVE-2020-8908), [CVE-2018-10237](https://nvd.nist.gov/vuln/detail/CVE-2018-10237), [CVE-2020-7692](https://nvd.nist.gov/vuln/detail/CVE-2020-7692))
* Updated Apache Ivy of DSE Spark to version 2.5.1. (DSP-22949, [CVE-2022-37865](https://nvd.nist.gov/vuln/detail/CVE-2022-37865), [CVE-2022-37866](https://nvd.nist.gov/vuln/detail/CVE-2022-37866))
* Removed `lucene-benchmark` from `lucene-solr` as it contained unnecessary vulnerable library: `nekohtml:1.9.17`. (DSP-22902, [CVE-2022-28366](https://nvd.nist.gov/vuln/detail/CVE-2022-28366), [CVE-2022-24839](https://nvd.nist.gov/vuln/detail/CVE-2022-24839), [CVE-2022-29546](https://nvd.nist.gov/vuln/detail/CVE-2022-29546))


# Release notes for 6.8.29
14 November 2022

## Components versions for DSE 6.8.29
* Apache Solr™ 6.0.1.4.2940
* Apache Spark™ 2.4.0.21&ast;
* Apache TinkerPop™ 3.4.5-20220728-e115ab9a
* Apache Tomcat® 8.5.79
* DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
* Netty 4.1.78.1.dse
* Spark JobServer 0.8.0.51

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.29 DSE Spark
* Fixed an issue in DSE Spark which was unable to read S3 objects with $ and = characters in the path. Updated aws-java-sdk to 1.11.892 and hadoop to 2.7.1.5. Dropped support of s3n, which is no longer undergoing active maintenance from the OSS Hadoop. (https://hadoop.apache.org/docs/current2/hadoop-aws/tools/hadoop-aws/index.html#S3N) Users are recommended to migrate to s3a instead. (DSP-22737)

## 6.8.29 DSE CVE
* Upgraded `jackson-databind` to version `2.13.4.2`. (DSP-22905, [CVE-2022-42003](https://nvd.nist.gov/vuln/detail/CVE-2022-42003))
* Replaced the vulnerable `woodstox-core` library used by `jackson-dataformat-xml` with version 6.4.0. (DSP-22914, [CVE-2022-40151](https://nvd.nist.gov/vuln/detail/CVE-2022-40151), [CVE-2022-40152](https://nvd.nist.gov/vuln/detail/CVE-2022-40152), [CVE-2022-40153](https://nvd.nist.gov/vuln/detail/CVE-2022-40153), [CVE-2022-40154](https://nvd.nist.gov/vuln/detail/CVE-2022-40154), [CVE-2022-40155](https://nvd.nist.gov/vuln/detail/CVE-2022-40155), [CVE-2022-40156](https://nvd.nist.gov/vuln/detail/CVE-2022-40156))


# Release notes for 6.8.28
28 October 2022

## Components versions for DSE 6.8.28
 * Apache Solr™ 6.0.1.4.2940
 * Apache Spark™ 2.4.0.20&ast;
 * Apache TinkerPop™ 3.4.5-20220728-e115ab9a
 * Apache Tomcat® 8.5.79&ast;
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.78.1.dse&ast;
 * Spark JobServer 0.8.0.51

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.28 DSE Management API
* Fixed regression in management api in 6.8.27 by ensuring that epoll netty libraries are included. (DSP-22895)


# Release notes for 6.8.27
25 October 2022

**NOTE**: DSE 6.8.27 has a regression that hinders the use of the management api used in kubernetes. Use of DSE 6.8.27 is not adviced. DSE 6.8.28 resolves this regression.

## Components versions for DSE 6.8.27
 * Apache Solr™ 6.0.1.4.2940
 * Apache Spark™ 2.4.0.20&ast;
 * Apache TinkerPop™ 3.4.5-20220728-e115ab9a
 * Apache Tomcat® 8.5.79&ast;
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.78.1.dse&ast;
 * Spark JobServer 0.8.0.51

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.27 DSE Cassandra
* Fixed nodetool flush assertion failure on TWCS tables with split_during_flush=true. (DSP-20708)

## 6.8.27 DSE Search
* Fixed `dsetool core_indexing_status` to show consistent indexing status between calls with and without `--all` parameter. (DSP-21594)

## 6.8.27 DSE Graph
* Fixed GraphOLAP spark connection problem in the multi-network cloud environments when GossipingPropertyFileSnitch (GPFS) is not used. (DSP-22707)
* Fixed permission issue in classic graph where DROP permissions were erroneously required for creating and altering a graph schema. (DSP-22024)

## 6.8.27 DSE Insights
* Upgraded insightsCollectd to 0.1.4. (DSP-22739)

## 6.8.27 DSEFS
* Fixed an issue where EMPTY_LAST_CONTENT would no be written to the stream when the connection was closed. (DSP-22671)

## 6.8.27 DSE Security
Fixed an issue during DSE Spark cluster upgrade where InClusterAuthenticator would fail to compose and decode a token if it receives an old version token. (DSP-22723)

## 6.8.27 DSE CVE
* Upgraded `jackson-databind` to 2.13.4. (DSP-22780, [CVE-2022-42004](https://nvd.nist.gov/vuln/detail/CVE-2022-42004))
* Upgraded Netty to version 4.1.78. (DSP-22511, [CVE-2019-9512](https://nvd.nist.gov/vuln/detail/CVE-2019-9512), [CVE-2019-9514](https://nvd.nist.gov/vuln/detail/CVE-2019-9514), [CVE-2019-9515](https://nvd.nist.gov/vuln/detail/CVE-2019-9515), [CVE-2019-20444](https://nvd.nist.gov/vuln/detail/CVE-2019-20444), [CVE-2019-20445](https://nvd.nist.gov/vuln/detail/CVE-2019-20445), [CVE-2020-7238](https://nvd.nist.gov/vuln/detail/CVE-2020-7238), [CVE-2020-11612](https://nvd.nist.gov/vuln/detail/CVE-2020-11612), [CVE-2021-37136](https://nvd.nist.gov/vuln/detail/CVE-2021-37136), [CVE-2021-37137](https://nvd.nist.gov/vuln/detail/CVE-2021-37137))
* Upgraded version of Apache Tomcat from 8.5.75 to 8.5.79. (DSP-22746, [CVE-2022-34305](https://nvd.nist.gov/vuln/detail/CVE-2022-34305), [CVE-2022-29885](https://nvd.nist.gov/vuln/detail/CVE-2022-29885))
* Upgraded org.apache.commons:commons-text to version 1.10.0. (DSP-22816, [CVE-2022-42889](https://nvd.nist.gov/vuln/detail/CVE-2022-42889))
* Upgraded SnakeYAML to 1.33. (DSP-22773, [CVE-2022-25857](https://nvd.nist.gov/vuln/detail/CVE-2022-25857))
* Upgraded jetty to 9.4.49.v20220914. (DSP-22774, [CVE-2022-2048](https://nvd.nist.gov/vuln/detail/CVE-2022-2048))


# Release notes for 6.8.26
12 September 2022

## Components versions for DSE 6.8.26
 * Apache Solr™ 6.0.1.4.2940
 * Apache Spark™ 2.4.0.19
 * Apache TinkerPop™ 3.4.5-20220728-e115ab9a&ast;
 * Apache Tomcat® 8.5.75
 * DSE Java Driver 1.10.0-dse-20220616 (DSE *internal-only* version)
 * Netty 4.1.34.3.dse
 * Spark JobServer 0.8.0.51

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.26 DSE Core
* Fixed a bug in streaming that could connect back using the wrong address under a specific network setup. (DSP-22585)

## 6.8.26 DSE Cassandra
* Ported CASSANDRA-15271 to make CLUSTERING ORDER validation less strict. (DSP-21801)
* Fixed ArrayIndexOutOfBoundsException during indexing SAI with ascii option enabled. (DSP-22601)

## 6.8.26 DSE Spark
* Fixed the logic that orders columns in the SELECT list to maintain the given order of the column headers. (DSP-22420)

## 6.8.26 DSE Management API
* Fixed command injection vulnerability in management-api. (DSP-22272)

## 6.8.26 DSE Miscellaneous
* Made ‘nodetool status’ report the state of unreachable nodes in order to allow knowing why they are unreachable. (DSP-22648)


# Release notes for 6.8.25
18 July 2022

## Components versions for DSE 6.8.25
* Apache Solr™ 6.0.1.4.2940
* Apache Spark™ 2.4.0.19&ast;
* Apache TinkerPop™ 3.4.5-20220405-a52bbe2c
* Apache Tomcat® 8.5.75
* DSE Java Driver 1.10.0-dse-20220616&ast; (DSE *internal-only* version)
* Netty 4.1.34.3.dse
* Spark JobServer 0.8.0.51&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.25 DSE Core
* Upgraded internally used DSE Java driver to `1.10.0-dse-20220616`. (DSP-22380) **NOTE**:
* Replaced `1.9.13` version of `jackson-core-asl` and `jackson-mapper-asl` to be `1.9.13.1.dse` which contains the security fix. (DSP-22389, [CVE-2019-10172](https://nvd.nist.gov/vuln/detail/CVE-2019-10172))
* Removed the PMD plugin from gradle config. (DSP-22575, [CVE-2019-7722](https://nvd.nist.gov/vuln/detail/CVE-2019-7722))
* Fixed the cqlsh tool to restore the ability to use the EXECUTE AS command. (DSP-22417)
* Fixed bug with overriding customer limits.d file if there are new values in the package upgrade. Complementary to DSP-21928. (DSP-22594)

## 6.8.25 DSE Cassandra
* Changed outdated `nofile` parameter value to `1048576` in `/etc/security/limits.d/cassandra.conf`. (DSP-21947)

## 6.8.25 DSE Search
* Fixed parsing range queries on DSE Search indexed columns of CQL types Date and Time. (DSP-22548)
* Added `SolrCore` index size metric. (DSP-22546)
* Added `SolrCore` `numDocs`, `maxDoc`, and `deletedDocs` metrics. (DSP-22587)
* Added per core DSE Search indexing status as a metric. (DSP-22592)
* Changed Tomcat {{showServerInfo}} configuration parameter to {{false}} for not exposing Tomcat version in error pages. (DSP-22561)

## 6.8.25 DSE Spark
* Upgraded jackson and jackson-databind to 2.13.3. (DSP-22452, [CVE-2020-36518](https://nvd.nist.gov/vuln/detail/CVE-2020-36518))
* Upgraded Spark library version containing change to sanitize passwords when printing spark commands to `stderr`. (DSP-22481)

## 6.8.25 DSE Graph
* Fixed an error when using the search index and traversing with an inequality operator such as gt or gte against Date or Time data types. (DSP-21279)

## 6.8.25 DSE Management API
* Improved Management API logic to reduce the likelihood of resource leaks when DSE is starting up. (DSP-22539)

## 6.8.25 DSE Security
* Fixed `EXECUTE AS` functionality to work with RLAC. (DSP-22508)

## 6.8.25 DSE CVE
* Upgraded apache-shiro used by spark-jobserver to version 1.8.0. (DSP-22557, [CVE-2021-41303](https://nvd.nist.gov/vuln/detail/CVE-2021-41303))


# Release notes for 6.8.24
15 June 2022

## Components versions for DSE 6.8.24
 * Apache Solr™ 6.0.1.4.2940&ast;
 * Apache Spark™ 2.4.0.18
 * Apache TinkerPop™ 3.4.5-20220405-a52bbe2c
 * Apache Tomcat® 8.5.75
 * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
 * Netty 4.1.34.3.dse
 * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.24 DSE Core
* Implemented ability to replace the `THREE` consistency level with an `ALL_BUT_ONE` consistency level. (DSP-22366)
* Removed Netty 3.6.2 and 3.7.0. (DSP-22381, [CVE-2015-2156](https://nvd.nist.gov/vuln/detail/CVE-2015-2156))
* Upgraded Jetty All Core to latest version (9.4.46.v20220331). (DSP-22491, [CVE-2009-4611](https://nvd.nist.gov/vuln/detail/CVE-2009-4611), [CVE-2020-27216](https://nvd.nist.gov/vuln/detail/CVE-2020-27216))
* Upgraded Azure SDK client libraries to be based on BOM 1.2.2 to remove [CVE-2020-36518](https://nvd.nist.gov/vuln/detail/CVE-2020-36518) and [CVE-2020-5404](https://nvd.nist.gov/vuln/detail/CVE-2020-5404). (DSP-22528, DSP-21781)
* Fixed the `TIMING` feature in cqlsh which throws a message "global name 'request_start' is not defined" when enabled. (DSP-22435)

## 6.8.24 DSE Cassandra
* Added two configurable variables `stream_outbound_permits_in_mb` and `input_stream_channel_timeout_in_ms` to allow streaming of high density of data by using [ZCS](https://docs.datastax.com/en/dse/6.8/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse__whatsNew). (DSP-22362)
* Fixed releasing of resources (including heap memory) for metrics removed from the registry (e.g. after table is dropped). (DSP-22516)
* Ported [CASSANDRA-16987](https://issues.apache.org/jira/browse/CASSANDRA-16987) and fixed python version check bug in cqlsh. (DSP-22517)

## 6.8.24 DSE Search
* Upgraded solr version which uses upgraded metadata-extractor 2.18.0 and XmpCore 6.1.11 libraries. (DSP-22406, [CVE-2019-14262](https://nvd.nist.gov/vuln/detail/CVE-2019-14262))

## 6.8.24 DSE Security
* Fixed dsetool expirekey/revoke commands by using KMIP custom attributes. (DSP-22421)


# Release notes for 6.8.23
11 May 2022

## Components versions for DSE 6.8.23
 * Apache Solr™ 6.0.1.4.2919&ast;
 * Apache Spark™ 2.4.0.18
 * Apache TinkerPop™ 3.4.5-20220405-a52bbe2c
 * Apache Tomcat® 8.5.75
 * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
 * Netty 4.1.34.3.dse
 * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.23 DSE Core
* Improved reading logic to ensure that sstables are not unnecessarily read for columns that are not selected. See [CASSANDRA-16737](https://issues.apache.org/jira/browse/CASSANDRA-16737). (Previously DB-4974). (DSP-22478)
* Fixed the `URISyntaxException: Malformed IPv6 address` when using `nodetool` or `dsetool` with Java 8u331 or 11.0.15. This is due to the recent changes of JDK-8278972, in which parsing of URL Strings in Built-in JNDI Providers is more strict. (DSP-22474)

## 6.8.23 DSE Cassandra
* Greater than '>' and less than '<' operators are swapped in the slow query log for a table with DESC clustering keys (port CASSANDRA-15503). (DSP-22369)
* Fixed a rare race condition where attempting to read from a sstable would fail with an assertion error. (DSP-22431)

## 6.8.23 DSE Search
* Upgraded xmlbeans version to 4.0.0. (DSP-22379, [CVE-2021-23926](https://nvd.nist.gov/vuln/detail/CVE-2021-23926))
* Upgraded Rome Library to `1.17.0` that uses JDOM `2.0.6.1` version. (DSP-22405, [CVE-2021-33813](https://nvd.nist.gov/vuln/detail/CVE-2021-33813))

## 6.8.23 DSE Upgrade
* Do not skip 5.1.x format sstables when running `nodetool upgradesstables` without `--include-all-sstables`. (DSP-22424)


# Release notes for 6.8.22
11 April 2022

## 6.8.22 DSE Platform
* Introduced DSE support for Java 11 for core Cassandra workloads. Please note that DSE does not currently provide support for advanced workloads (Search, Spark and Graph) for Java 11.

## Components versions for DSE 6.8.22
 * Apache Solr™ 6.0.1.4.2887
 * Apache Spark™ 2.4.0.18
 * Apache TinkerPop™ 3.4.5-20220405-a52bbe2c&ast;
 * Apache Tomcat® 8.5.75&ast;
 * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
 * Netty 4.1.34.3.dse&ast;
 * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.22 DSE Core
* Added a startup check that prevents starting DSE with advanced workloads on Java 11. (DSP-22358)
* Upgraded netty to 4.1.34 from 4.1.25. (DSP-22363)
* Removed `disk_cal.py` and `compaction-metrics.ipynb` Python 2 tools. (DSP-22382)
* Used azure sdk client libraries from bill of materials 1.2.0 for Azure Blob Storage backup and restore. Used okhttp based azure code http client instead of the netty based one. (DSP-22401)
* Reduced node bootstrapping and rebuild operation time by improving the algorithm that calculates the map of streaming candidates. (DSP-22339)

## 6.8.22 DSE Cassandra
* Limited heap pressure during mutation repair for tables with materialized views by throttling number of concurrent batches (default 10). Number of batches can be controlled by new system property `cassandra.repair.mutation_repair_max_concurrent_batches`. Setting to 0 (zero) disables throttling and reverts behavior before this change. (DSP-22344)

## 6.8.22 DSE Graph
* Replaced log4j with reload4j in TinkerPop and bumped the version of TinkerPop. (DSP-22326)

## 6.8.22 DSE NodeSync
* Changed heap size to 512M for command line tools on Azul Zing if `MAX_HEAP_SIZE` is not specified. (DSP-22313)

## 6.8.22 DSE Security
* Upgraded Bouncy Castle to the latest 1.70 version. (DSP-22352)

## 6.8.22 DSE Miscellaneous
* Ported fix from DSP-22315: Option to disable call to `NativeLibrary.trySkipCache`. (DSP-22343)

## 6.8.22 DSE CVE
* Upgraded azure-storage-blob from 12.4.0 to 12.15.0 version. (DSP-22377, [CVE-2020-5403](https://nvd.nist.gov/vuln/detail/CVE-2020-5403))
* Upgraded apache-commons compress library to 1.21 version. (DSP-22383, [CVE-2021-35515](https://nvd.nist.gov/vuln/detail/CVE-2021-35515), [CVE-2021-35516](https://nvd.nist.gov/vuln/detail/CVE-2021-35516), [CVE-2021-35517](https://nvd.nist.gov/vuln/detail/CVE-2021-35517), [CVE-2021-36090](https://nvd.nist.gov/vuln/detail/CVE-2021-36090))
* Upgraded snakeyaml version to 1.30. (DSP-22386, [CVE-2017-18640](https://nvd.nist.gov/vuln/detail/CVE-2017-18640))
* Upgraded ApacheVelocity to 2.3 version. (DSP-22387, [CVE-2020-13936](https://nvd.nist.gov/vuln/detail/CVE-2020-13936))
* Upgraded commons-beanutils version to 1.9.4 version. (DSP-22388, [CVE-2019-10086](https://nvd.nist.gov/vuln/detail/CVE-2019-10086))
* Upgraded Hazelcast to 5.1.1 version. (DSP-22390, [CVE-2022-0265](https://nvd.nist.gov/vuln/detail/CVE-2022-0265))
* Upgraded logback version to 1.2.11. (DSP-22237, [CVE-2021-42550](https://nvd.nist.gov/vuln/detail/CVE-2021-42550))
* Upgraded version of Apache Tomcat from 8.5.72 to 8.5.75. (DSP-22360, [CVE-2022-23181](https://nvd.nist.gov/vuln/detail/CVE-2022-23181))
* Upgraded version of azure-identity from 1.1.0 to 1.4.6. (DSP-22194, [CVE-2017-1000190](https://nvd.nist.gov/vuln/detail/CVE-2017-1000190))

# Release notes for 6.8.21
7 March 2022

## Components versions for DSE 6.8.21
 * Apache Solr™ 6.0.1.4.2887
 * Apache Spark™ 2.4.0.18
 * Apache TinkerPop™ 3.4.5-20210816-c28c0de2
 * Apache Tomcat® 8.5.72
 * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
 * Netty 4.1.25.7.dse
 * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.21 DSE Core
* Changes reading logic of compressed chunk offsets that are loaded from compression info for zero copied partial sstables. It results in smaller off-heap usage. (DSP-22247)
* Adds configurable snapshot size cache speeding up the retrieval of snapshot information. (DSP-22338)
* PKCS#11 needs Signature algorithms to be configured on some versions of Java 11 (see [https://bugs.openjdk.java.net/browse/JDK-8217611|https://bugs.openjdk.java.net/browse/JDK-8217611|smart-link]). In order to work with TLSv1.3, RSA keys in PKCS#11 key stores must have a key size of at least 4096 bits. (DSP-22276)
* RSA Certificates for SSL on Java 11 require larger keypairs than on Java 8. Testing on Java 11 is done with 1024 bit keys instead of 512 bit keys. (DSP-22277)
* Clean up ClientWarn State when message sending expired. (DSP-22290)

## 6.8.21 DSE Graph
* fix deletion of a dropped vertex’s incoming edges when the far side of those edges involves multiple vertex labels. (DSP-22218)

## 6.8.21 DSE NodeSync
* Fix validation age in the belated incremental NodeSync log warning. (DSP-22300)

## 6.8.21 DSE CVE
* Removed log4j 1.2.x dependency from dse-spark/client/lib and replace it with reload4j 1.2.19. (DSP-22279, [CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228), [CVE-2019-17571](https://nvd.nist.gov/vuln/detail/CVE-2019-17571), [CVE-2022-23305](https://nvd.nist.gov/vuln/detail/CVE-2022-23305), [CVE-2022-23302](https://nvd.nist.gov/vuln/detail/CVE-2022-23302), [CVE-2021-4104](https://nvd.nist.gov/vuln/detail/CVE-2021-4104))
* Upgraded version of Bouncy Castle to 1.67. (DSP-22301, [CVE-2018-1000613](https://nvd.nist.gov/vuln/detail/CVE-2018-1000613), [CVE-2018-1000180](https://nvd.nist.gov/vuln/detail/CVE-2018-1000180), [CVE-2020-28052](https://nvd.nist.gov/vuln/detail/CVE-2020-28052))


# Release notes for 6.8.20
17 February 2022

## Components versions for DSE 6.8.20
 * Apache Solr™ 6.0.1.4.2887
 * Apache Spark™ 2.4.0.18
 * Apache TinkerPop™ 3.4.5-20210816-c28c0de2
 * Apache Tomcat® 8.5.72
 * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
 * Netty 4.1.25.7.dse
 * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.20 DSE Cassandra
* Ported fix from CASSANDRA-17352: Remote code execution for scripted UDFs (DSP-22321, [CVE-2021-44521](https://nvd.nist.gov/vuln/detail/CVE-2021-44521))

# Release notes for 6.8.19
24 January 2022

## Components versions for DSE 6.8.19
 * Apache Solr™ 6.0.1.4.2887
 * Apache Spark™ 2.4.0.18
 * Apache TinkerPop™ 3.4.5-20210816-c28c0de2
 * Apache Tomcat® 8.5.72
 * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
 * Netty 4.1.25.7.dse
 * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.19 DSE Core
* Fix a possible overflow with elapsed nano-time calculation in messaging queue timeout. (DSP-22011)

## 6.8.19 DSE Cassandra
* Await timeout for shutting down non periodic tasks is now configurable with the new jvm option `cassandra.non_periodic_tasks_shutdown_timeout_in_minutes`. When timeout is reached, force shutdown those tasks. (DSP-22241)
* Lower commitlog replay sstable origin warning to info. (DSP-22270)
* Fix the miscalculation of totalCDCSizeOnDisk. (DSP-22135)

## 6.8.19 DSE Upgrade
* Retain changes to /etc/security/limits.d/cassandra.conf on yum upgrade. (DSP-21928)

## 6.8.19 DSE CVE
* Removed unused log4j dependency to avoid false positives in vulnerability scans. (DSP-22234, [CVE-2019-17571](https://nvd.nist.gov/vuln/detail/CVE-2019-17571), [CVE-2021-4104](https://nvd.nist.gov/vuln/detail/CVE-2021-4104), [CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228), [CVE-2021-45105](https://nvd.nist.gov/vuln/detail/CVE-2021-45105))
* Upgraded version of json-smart library used by Azure blob store access from 2.3 to 2.4.7 to fix CVE-2021-27568 and CVE-2021-31684. (DSP-22186, [CVE-2021-27568](https://nvd.nist.gov/vuln/detail/CVE-2021-27568), [CVE-2021-31684](https://nvd.nist.gov/vuln/detail/CVE-2021-31684))


# Release notes for 6.8.18
8 December 2021

## Components versions for DSE 6.8.18
* Apache Solr™ 6.0.1.4.2887
* Apache Spark™ 2.4.0.18
* Apache TinkerPop™ 3.4.5-20210816-c28c0de2
* Apache Tomcat® 8.5.72&ast;
* DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
* Netty 4.1.25.7.dse
* Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.18 DSE Cassandra
* Fix calculation of `CompressionMetadataOffHeapMemoryUsed` metric accessible via `nodetool tablestats` command. (DSP-22181)

## 6.8.18 DSE core
* Port and adjust CASSANDRA-16686 for DSE. (DB-5022)

## 6.8.18 DSE Search
* Upgraded version of Apache Tomcat from 8.5.70 to 8.5.72 to fix CVE-2021-42340. (DSP-22098)

## 6.8.18 DSE Spark
* Fixed and updated javax.mail dependency to com.sun.mail. (DSP-22085)

## 6.8.18 DSE CVE
* Upgraded version of Apache Tomcat from 8.5.70 to 8.5.72 to fix [CVE-2021-42340](https://nvd.nist.gov/vuln/detail/CVE-2021-42340). (DSP-22098)


# Release notes for 6.8.17
4 November 2021

## Components versions for DSE 6.8.17
* Apache Solr™ 6.0.1.4.2887
* Apache Spark™ 2.4.0.18
* Apache TinkerPop™ 3.4.5-20210816-c28c0de2
* Apache Tomcat® 8.5.70
* DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
* Netty 4.1.25.7.dse
* Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.17 DSE Cassandra
* Enables periodic logging of system status (default every 5 minutes, configurable). (DSP-22039)
* Fix a possible issue that shell tool could break with `-h`/`--help` in package install. (DSP-20375)

## 6.8.17 DSE Core
* Fixed a bug in the authenticator that would use the default management mode instead of the defined mode by authentication when authenticating. (DSP-22067)
* Fixes stack overflow with secondary indexes on collections. (DSP-22070)
* Fixed an issue in preloading prepared statements that queries static columns. (DB-5012)

## 6.8.17 DSE Security
* Fixes issue that when disabling `system_info_encryption` configuration in `dse.yaml`, encryption for tables in the `system_backups` keyspace would not turn off. (DSP-22078)

## 6.8.17 DSE CQL
* Prints TLS protocol information when running `cqlsh` with `--debug` parameter. (DB-4981)

## 6.8.17 DSE Spark/Hive
* Fixes broken partition filtering in hive metastore leading to missing data in the spark-sql queries results for queries involving numeric partition keys or complex conditions. (DSP-21651)


# Release notes for 6.8.16
7 October 2021

## Components versions for DSE 6.8.16
   * Apache Solr™ 6.0.1.4.2887&ast;
   * Apache Spark™ 2.4.0.18
   * Apache TinkerPop™ 3.4.5-20210816-c28c0de2&ast;
   * Apache Tomcat® 8.5.70&ast;
   * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.16 DSE Cassandra
* The Change Data Capture (CDC) is now near real time as in Cassandra 4.x. Active commitlog segments can be processed from the CDC raw directory defined in your `cassandra.yaml` without flushing tables. It also allows you to read the last mutation form the most recent commitlog file. See the [Datastax Change Data Capture documentation page](https://docs.datastax.com/en/dse/6.8/dse-admin/datastax_enterprise/config/configCDCLogging.html) for more details. (DSP-21992)

## 6.8.16 DSE core
* Added check against the negative value in local stream throughput `stream_throughput_outbound_megabits_per_sec` and inter dc stream throughput `inter_dc_stream_throughput_outbound_megabits_per_sec` (DB-5010)
* Fixes output of compaction file progress. (DB-5028)

## 6.8.16 DSE Local Write-Read Paths
* Resolves a TPC weakness with large rows and collections, where DSE 6 would repeatedly attempt to read the same row and create a lot of on-heap garbage. (DB-3962)

## 6.8.16 DSE CVE
* Ported fix from SOLR-12514 to dse lucene-Solr to fix CVE-2018-11802. (DSP-21685)
* Upgraded version of PDFBox and FontBox to 2.0.24, and version of JempBox to 1.8.16 to fix CVE-2018-8036 and CVE-2018-11797. (DSP-21688)
* Upgraded version of groovy to 2.4.21 (DSE 5.1/6.0/67) and to 2.5.14 (DSE 6.8) to fix CVE-2020-17521. (DSP-21767)
* Upgraded version of Tomcat from 8.5.65 to 8.5.70 to fix CVE-2021-33037. (DSP-21996)

# Addition to Release Notes for 6.8.15
31 August 2021

## 6.8.15 DSE Platform
* Provide DSE support for Centos8, Red Hat Enterprise Linux 8 and Oracle Linux (DSP-19104). Please note that certification was done using Python 2.7 and Python 2.7 needs to be available on the target system. SparkR version included in DSE 6.8.15 is not compatible with the default R version >= 4.0.0.

# Release notes for 6.8.15
26 August 2021

## Components versions for DSE 6.8.15
   * Apache Solr™ 6.0.1.4.2840
   * Apache Spark™ 2.4.0.18
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.15 DSE CVE

* upgraded Bootstrap version from 3.1.1 to 3.4.1, upgraded Flask from 0.10.1 to 1.1.4. (DSP-21682)
* Upgraded version of directory-ldap-api from DSE 1.0.0.2.dse to OSS 1.0.3 (DSP-21758)

## 6.8.15 DSE Spark

* Spark had an unused dependency on azure-storage-blob jar files version 12.4.0 which was removed from Azure repos. This fix removes the dependency. (DSP-21978)

## 6.8.15 DSE TPC

Execution of the back pressure task can be rejected in TPC, leading to the back pressure job being dropped entirely and then deadlocking. This was fixed by properly rescheduling the task. (DB-5027)

# Release notes for 6.8.14
07 July 2021

## 6.8.14 DSE Platform
* Provide DSE support for Ubuntu 20.04 (Focal) (DSP-21330). Please note that certification was done using Python 2.7 and Python 2.7 needs to be available on the target system.

## Components versions for DSE 6.8.14
   * Apache Solr™ 6.0.1.4.2840
   * Apache Spark™ 2.4.0.18
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.8.14 DSE Cassandra
* Added warning message in case of dse start failure due to this issue (DSP-21795)

## 6.8.14 DSE Core
* Fixed concurrent modification exception in consistent replace (DSP-21836)

## 6.8.14 DSE CVE
* Upgraded version of resteasy to `4.6.0.Final` (DSP-21683)
* Upgraded jetty version from `9.4.34.v20201102` to `9.4.41.v20210516` (DSP-21684, DSP-21687)

## 6.8.14 DSE Search
* Fixed a bug where in rare cases search query routing might start to spin endlessly for a particular query (DSP-21838)

## 6.8.14 DSE Security
* Fixed an issue in the LDAP `group_search_filter` default value that meant that group hierarchies were not being loaded if the `group_search_filter` was not explicitly set in the dse.yaml. (DSP-21874)

## 6.8.14 DSE Auth
* Removed a possible false-positive error message in the log that would cause confusion when multiple authentication schemes are defined.
 (DB-5015)

## 6.8.14 DSE CQL
* Added unit Testcases for logic cqlsh TLS version. (DB-4979)

## 6.8.14 DSE SSTables
* When the Bloom filter is recreated due to FP chance change, sstable metadata is loaded and re-written in order to update validation metadata with the new fp chance. However, the loaded metadata lacked compaction metadata, so when rewritten, compaction metadata got truncated.  (DB-5005)

## 6.8.14 DSE Streaming
* Fixed nodetool not able to `setstreamthroughput` and `setinterdcstreamthroughput` (DB-4940)

## 6.8.14 DSE Tools
* Updated the python driver version used by cqlsh from `3.24.0` to `3.25.0` (DB-4978)

# Release notes for DSE 6.8.13
18 May 2021

## Components versions for DSE 6.8.13
   * Apache Solr™ 6.0.1.4.2840
   * Apache Spark™ 2.4.0.18
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.5.65
   * DSE Java Driver 1.10.0-dse+20210424 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.13 AOSS
* AOSS returns additional parameter in `status` `endpoint: "connection_hostname"`. The new parameter is a FQDN of the node hosting AOSS, it may be used for connections (instead of connection_address) if needed. (DSP-21811)

## DSE 6.8.13 Core
* Fixed an issue with DSE daemon being unable to stop after the default timeout expired. This issue only affected systems that use package install and init.d, such as centos. (DSP-21804)

## DSE 6.8.13 Graph
* Fixed a problem where the Gremlin `phrase()` predicate may not match Solr results for equivalent search. (DSP-21724)

## DSE 6.8.13 Search
* A new JVM option is added: `dse.search.fc.warmup`: `AUTO`, `ALWAYS` & `NEVER`.  (DSP-21813)

# Release notes for DSE 6.8.12
26 April 2021

## Components versions for DSE 6.8.12
   * Apache Solr™ 6.0.1.4.2840&ast;
   * Apache Spark™ 2.4.0.18
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.5.65&ast;
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.50

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.12 CQL
* Fixed an error in cqlsh encoding unicode in multi-line statements (DB-4855)
* Make cqlsh prefer newer TLS versions. (DB-4966)

## DSE 6.8.12 Cassandra
* Address a problem where new or rebooted nodes may not be able to gossip with peers. (DSP-21753)

## DSE 6.8.12 CVE
* Upgrade apache commons-compress to address CVE-2019-12402 (DSP-21679)
* Update tomcat version 8.5.61 to 8.5.65 (DSP-21798)

## DSE 6.8.12 Search
* Fixed a bug where under heavy load solr query worker threads would use 100% CPU due to contention on thread local map
 (DSP-21746)

# Release notes for DSE 6.8.11
9 April 2021

## Components versions for DSE 6.8.11
   * Apache Solr™ 6.0.1.4.2814
   * Apache Spark™ 2.4.0.18
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.5.61&ast;
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.50&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.11 Auth
* Fixes an issue where a login attempt with missing credentials logged a misleading warning message with stack trace instead of an error message about the missing username or password. (DB-4806)

## DSE 6.8.11 Legacy Repair
* Fixes a bug when in rare cases a terminated repair session would leak on-heap memory (DB-4833)

## DSE 6.8.11 Streaming
* Print a timestamp when nodetool exits due to an error (DB-4826)

## DSE 6.8.11 Cassandra
* Data export from cqlsh is now less noisy in the logs (DSP-21494)
* Fixes intermittent ERROR: java.util.ConcurrentModificationException at org.apache.cassandra.transport.CBUtil.writeStringList (DSP-21336)
* Fix for DESCRIBE TYPES in cqlsh (DSP-21667)
* Add asynchronous update to KMIP key cache to fix blocking of commit log (DSP-20582)
* Fixes CVE-2020-1945 affecting Apache Ant (DSP-21716)
* Fixes SRCCLR-SID-22742: Insecure Input Validation Vulnerability in the Apache Commons Codec library (DSP-21747)
* Update Tomcat version 8.0.53 to 8.5.61 (fixes CVE-2002-0493 CVE-2009-3548 CVE-2013-2185 CVE-2016-1240 CVE-2016-5018 CVE-2016-5388 CVE-2016-6796 CVE-2016-6797 CVE-2016-8745 CVE-2016-9774 CVE-2016-9775 CVE-2020-8022) (DSP-21394)

## DSE 6.8.11 Indexing
* Fixes a severe issue where flushing an empty MemtableIndex causes the index to not be queryable (DB-4934)

## DSE 6.8.11 Search
* Fixes a bug where FilterCache warmup triggered by node health change can block GossipStage-1 thread for several seconds (DSP-21674)

## DSE 6.8.11 Spark
* Fixes CVE-2014-0114, CVE-2014-0114 (DSP-21668)

# Release notes for DSE 6.8.10
11 March 2021

## Components versions for DSE 6.8.10
   * Apache Solr™ 6.0.1.4.2814
   * Apache Spark™ 2.4.0.18&ast;
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.10 Auth
* Works around a bug in JDK 1.8u282 (JDK-8260018) (DB-4884)

## DSE 6.8.10 Bootstrap
* Fixes a Null Pointer Excpetion in Gossip when upgrading from 5.1 to 6.8.6 (DB-4810)

## DSE 6.8.10 Configuration
* During package upgrade yum and apt managers overwrite unedited old jvm.options file. (DB-4705)

## DSE 6.8.10 core
* Fixes a problem where *FSReadError* during streaming could causes DSE to shutdown (DB-4878)

## DSE 6.8.10 Distributed Read/Write
* Port fix of CVE-2020-17516 onto DSE 6.8 (DB-4923)

## DSE 6.8.10 Local Write-Read Paths

* Dropped messages metrics calculation doesn't cause assertion errors when dropped messages contain remote batch mutation. (DB-3905)

## DSE 6.8.10 Tools
* SSTablePartitions tool will no longer fail with "histogram overflowed" when its working for the server code (DB-2952)

## DSE 6.8.10 Cassandra
* Fixes a problem where sstablescrub could not fix a corrupted file (DSP-21672)

## DSE 6.8.10 Core
* Addressed several Jackson databind vulnerabilities by upgrading jackson-databind to version 2.9.10.8 in DSE 5.1.21, 6.0.15 and 6.7.13 and version 2.10.5.1 in DSP 6.8.10. (DSP-21503) (DSP-21503)
* Fixes a problem where nodetool rebuild could fail intermittently with zerocopy streaming enabled (DSP-21564)

## DSE 6.8.10 Spark
* Update Jetty to 9.4.34.v20201102 and update Spark Versions: DSE 5.1: 2.0.2.38; DSE 6.0: 2.2.3.16; DSE 6.7: 2.2.3.16; DSE 6.8: 2.4.0.17 (DSP-21506)
* SCC by default enables direct join optimization only when size_estimates for both tables are available.  (DSP-21628)
* Fix: Spark Master fails to start if keystore (used by web UI) contains more than one certificate (DSP-21703)

## DSE 6.8.10 Graph
* Both graph engines now accept either `byte[]` or `ByteBuffer` for blob-typed property values. (DSP-21643)

## DSE 6.8.10 Indexing
* Index segments are now merged into a single segment, after the index build. (DSP-19608)

## DSE 6.8.10 Search

* Fixes a problem where lucene threads were getting interrupted, causing problems with solr cores (DSP-21339)
* Search queries will no longer fail when querying clustering columns of certain types on which the order is reversed (DSP-21363)

## DSE 6.8.10 SparkConnector
* Spark Cassandra Connector supports Storage Attached Indexes (SAI). The connector pushes down predicates defined on columns with SAI indexes.  (DSP-21655)
* DSE Spark supports connections to Astra clusters  (DSP-21510)

# Release notes for DSE 6.8.9
7 January 2021

## Component versions for DSE 6.8.9
   * Apache Solr™ 6.0.1.4.2814
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.9 Streaming
* Addresses a severe issue where streaming an older file format to a new node could crash sending and receiving nodes. (DB-4846)

## DSE 6.8.9 Core
* Add support for multiple authorization sources (LDAP + DSE Internal) (DSP-14233)

## DSE 6.8.9 SparkConnector
* Fixed direct join optimization for spark sql. (DSP-21498)

# Release notes for DSE 6.8.8
15 December 2020

:warning: **NOTE**: Due to a serious bug which affects DSE `6.8.7` and DSE `6.8.8`, these releases have been retracted.  We recommend against upgrading to these versions at this time.  If you have already upgraded to these versions, please _EITHER_ set `zerocopy_streaming_enabled=false` in the `cassandra.yaml` and perform a rolling restart AND/OR run `upgradesstables` on all nodes in your cluster before adding new nodes, running repair, or restoring from backups.  This bug has been addressed in DSE `6.8.9`. All features and fixes for `6.8.8` and `6.8.7` are present in `6.8.9`.

## Components versions for DSE 6.8.8
   * Apache Solr™ 6.0.1.4.2814&ast;
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.8 Backup and Restore
* During Backup Service startup, to avoid stalling during service initialization, check cluster readiness in response to endpoint "on alive" events. (DB-4818)

## DSE 6.8.8 Management API
* Fixed an issue in DSE that prevented the Management API to work with DSE versions 6.8.5 - 6.8.7 (DSP-21607)

## DSE 6.8.8 Indexing
* The issue: When flushing text column indexes, the internal ordering of terms can be processed out of order causing an "&ast;java.lang.AssertionError: Incremental trie requires sorted keys&ast;" error. When this happens, all flushing of indexes involved in this transaction is aborted and the indexes are marked non-queryable. Recovering from this issue involves either rebuilding the indexes or restarting the nodes. (DSP-21580)
* Fixes a performance regression in SAI for versions 6.8.6 and 6.8.7 regarding &ast;MultiRangeReadCommand&ast;. (DSP-21601)

## DSE 6.8.8 Search
* A system property `dse.solr.fuzzy.max.expansion` was added which allows the user to define a custom number of fuzzy query expansions. The maximal possible value is 1024. When unset, the default number of max expansions is 50. (DSP-21605)

## DSE 6.8.8 Spark
* Adjust available framework values for `--framework` parameter. (DSP-21500)

# Release notes for DSE 6.8.7
23 November 2020

:warning: **NOTE**: Due to a serious bug which affects DSE `6.8.7` and DSE `6.8.8`, these releases have been retracted.  We recommend against upgrading to these versions at this time.  If you have already upgraded to these versions, please _EITHER_ set `zerocopy_streaming_enabled=false` in the `cassandra.yaml` and perform a rolling restart AND/OR run `upgradesstables` on all nodes in your cluster before adding new nodes, running repair, or restoring from backups.  This bug has been addressed in DSE `6.8.9`. All features and fixes for `6.8.8` and `6.8.7` are present in `6.8.9`.

## Components versions for DSE 6.8.7
   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.7 Cassandra
* Fixed a bug where the slow query log would fill with queries that do not meet the slow query threshold (DSP-21417)

## DSE 6.8.7 Core
* Fixed a bug where a single partition read might fail if the following conditions were true:
    1) several sstables had the same partition level deletion info
    2) some of the sstables had wide rows whereas others had not
    3) the sstables in question contained range tombstone markers (DSP-21346)
* Fixed a bug in `cassandra.repair.mutation_repair_rows_per_batch` setting that caused sending all repair mutations at once (DSP-21429)
* There is a change in SSTable format and/or version. Please refer to the [compatibility documentation](https://docs.datastax.com/en/landing_page/doc/landing_page/compatibility.html#compatibility__current-software) for more details.

## DSE 6.8.7 Indexing
* On the CQLSH `CREATE CUSTOM INDEX ... WITH OPTIONS` statement, SAI adds support for an ascii option. If set to `true`, converts alphabetic, numeric, and symbolic characters that are not in the Basic Latin Unicode block (first 127 ASCII characters) to their ASCII equivalent, if one exists. For example, the filter changes à to a. The default is `false`. (DSP-21409)
* Make the SAI read path synchronous. (DSP-21451)
* Fixed "java.lang.ArithmeticException: integer overflow" printing in `system.log` when retrieving the SAI index `segmentRowID` (DSP-21522

## DSE 6.8.7 Graph
* A meaningful error message is logged when two properties with the same name but different types are used in a single core graph. Classic graph was not affected. (DSP-21490)

## DSE 6.8.7 Security
* Optimized retrieval when `memberof_search` used the wrong attribute to retrieve groups of the user. (DSP-21537)

## DSE 6.8.7 Backup and Restore
* Multi-datacenter backup and restore, new `CompositeStore` type of backup store. (DB-4489)
* Adds the possibility to restore a backup marked as `INCOMPLETE` by using the new `FORCE RESTORE` statement.

## DSE 6.8.7 CommitLog
* Addressed a bug where a "CommitLogReplayException" is caused by a bad header but correct CRC after restart (DB-3996)
* Fixed a bug where some part of the commit log might not be replayed after injecting a foreign sstable to a node or, on 6.8, after zero-copy streaming of an sstable (DB-4629)

## DSE 6.8.7 Streaming
* Fixed an issue where zero copy streaming could cause file descriptor leakage (DB-4594)

## DSE 6.8.7 Tools
* SStableloader now uses `native_transport_port_ssl` over `native_transport_port` when passed a config file with the property set (DB-4632)

## DSE 6.8.7 TPC
* Fixed memory leak in Netty resulting in OOM. (DB-4664)
* Fixed a problem in the scheduling and counting of active materialized view updates that could cause too many to be executed concurrently, overwhelming the node. (DB-4782)

# Release notes for DataStax Enterprise version 6.8.6
12 November 2020

## Components versions for DSE 6.8.6
   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.6 Bootstrap
* A node may be stuck in repair while joining the cluster if broadcast_address is set differently than local_address (DB-4786)

# Release notes for DataStax Enterprise version 6.8.5
20 October 2020

## Components versions for DSE 6.8.5
   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.5 Backup and Restore
* Server side backup and restore now supports Microsoft Azure cloud storage as a backup target. (DB-3894)
* snapshot `schema.cql` files will now contain `IF NOT EXISTS` clause for `CREATE TYPE` statements (DB-4685)

## DSE 6.8.5 Compaction
* Fixes a problem where races in notifying compaction strategies of added and removed sstables can cause compaction to try to use non-existing sstables and repeatedly fail to make progress. (DB-4711)

## DSE 6.8.5 Core
* Fixed node restart issue after dropping a PointType column. (DSP-21326)
* Fixed extreme local pauses on all nodes in the cluster on a node restart. (DB-4657)

## DSE 6.8.5 Local Write-Read Paths
* Improves performance of estimation of partition counts for subranges. (DB-3679)

## DSE 6.8.5 Virtual Tables
* Fsync nodes metadata to prevent FSReadError issues on startup. (DB-4672)

## DSE 6.8.5 Cassandra
* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)

## DSE 6.8.5 Security
* Fixes LDAP user permissions problem following LDAP server restart. (DSP-21284)

## DSE 6.8.5 Graph
* Escape single-quotes in certain graph-search query predicates. (DSP-21450)

## DSE 6.8.5 Spark
* Fix: Spark Application contacting Nodes in Non Local DC  (DSP-19961)

## TinkerPop changes for DSE 6.8.5
DataStax Enterprise (DSE) 6.8.4 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.

# Release notes for DataStax Enterprise version 6.8.4
17 September 2020

## Component versions for DSE 6.8.4
   * Apache Solr™ 6.0.1.4.2794
   * Apache Spark™ 2.4.0.16
   * Apache TinkerPop™ 3.4.5-20200107-6cec00d8
   * Apache Tomcat® 8.0.53
   * DSE Java Driver 1.10.0-dse+20200217 (DSE *internal-only* version)
   * Netty 4.1.25.7.dse
   * Spark JobServer 0.8.0.49

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## DSE 6.8.4 Compaction
* Fixes compaction getting stuck on acquiring references for non-existing sstables. (DB-4290)

## DSE 6.8.4 CQL
* Distributes Netty connections more uniformly across TPC cores (DB-4683)

## DSE 6.8.4 MessagingService
* Distributes Netty connections more uniformly across TPC cores (DB-4683)

## DSE 6.8.4 Core
* Adds TTL and TimeWindowCompactionStrategy (TWCS) to `system_distributed.repair_history` and `system_distributed.parent_repair_history` tables.  (DB-2009)
* DNS Service Discovery is now a part of the DSE/LDAP integration. (DSP-11450)
* New system property to cap the maximum amount of memory used by bloom filters: `-Dcassandra.max_bf_memory_mb}`. By default, this is _unlimited_. (DSP-21344)

## DSE 6.8.4 Security
* DNS Service Discovery is now a part of the DSE/LDAP integration. (DSP-11450)

## DSE 6.8.4 DSEFS
*  DSEFS waits for a schema agreement before starting and issuing the first CQL query. (DSP-20743)

## DSE 6.8.4 Indexing
* Storage-Attached Indexing (SAI) adds support for creating multiple SAI indexes on the same collection map column.
See [SAI collection map examples with keys, values, and entries](https://docs.datastax.com/en/storage-attached-index/6.8/sai/saiUsing.html#saiUsing__saiUsingCollectionsExamples). (DSP-21306)

## TinkerPop changes for DSE 6.8.4
DataStax Enterprise (DSE) 6.8.4 includes all changes from previous DSE versions. See TinkerPop [upgrade documentation](http://tinkerpop.apache.org/docs/3.4.5/upgrade/#_upgrading_for_users) for all changes.

# Release notes for previous versions
Release notes for previous DSE patch releases can be found here:
https://docs.datastax.com/en/dse/6.8/dse-admin/datastax_enterprise/releaseNotes/RNdse.html#RNdse

---
