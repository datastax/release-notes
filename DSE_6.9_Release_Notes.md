# Release notes for DataStax Enterprise 6.9
DSE 6.9.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any.
Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

# Release notes for 6.9.11
25 June 2025

## Components versions for DSE 6.9.11
 * Apache Solr™ 6.0.1.5.2977
 * Apache Spark™ 2.5.0.6
 * Apache TinkerPop™ 3.4.15-20250603-0956e859
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.119.1.dse
 * Spark JobServer 0.8.0.57

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.11 DSE Docker
* Updated DSE 6.9 UBI 8 images Python 3 version to 3.9 required by `cqlsh`. (DSP-24707)

# Release notes for 6.9.10
12 June 2025

## Components versions for DSE 6.9.10
 * Apache Solr™ 6.0.1.5.2977
 * Apache Spark™ 2.5.0.6
 * Apache TinkerPop™ 3.4.15-20250603-0956e859&ast;
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.119.1.dse&ast;
 * Spark JobServer 0.8.0.57&ast;

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.10 DSE Core
* Updated the Java Development Kit (JDK) versions to `8u452` and `11.0.27`. These JDKs help build and test DSE, and are available in DSE Docker images. (DSP-24710) The following exceptions for DSE UBI images apply: (DSP-24710)
  * The DSE 6.9 UBI images use JDK version `11.0.25` (from registry.access.redhat.com/ubi8/ubi-minimal:8.10-1255).
  * The DSE 6.8 UBI images use JDK versions `11.0.23` and `8u412` (from the deprecated registry.redhat.io/ubi7/ubi:7.9-1445).

## 6.9.10 DSE Cassandra
* Removed non-supported Java 8 configuration files. (DSP-24845)

## 6.9.10 DSE CVE
* Upgraded the `net.minidev:json-smart` Java JSON parser package to version `2.5.2`. (DSP-24851, [CVE-2024-57699](https://nvd.nist.gov/vuln/detail/CVE-2024-57699))
* Upgraded Jetty to version `9.4.57.v20241219` and Apache Commons IO to version `2.19.0`. (DSP-24855, [CVE-2024-6763](https://nvd.nist.gov/vuln/detail/CVE-2024-6763), [CVE-2024-47554](https://nvd.nist.gov/vuln/detail/CVE-2024-47554))
* Upgraded the Apache Commons BeanUtils library to version `1.11.0` to resolve a vulnerability. (DSP-24857, [CVE-2025-48734](https://nvd.nist.gov/vuln/detail/CVE-2025-48734))
* Upgraded Netty to version `4.1.119.1.dse`, which is based on version `4.1.119.Final`. (DSP-24850, [CVE-2025-24970](https://nvd.nist.gov/vuln/detail/CVE-2025-24970))
* Upgraded the protocol buffers (protobuf) to version `4.29.4` to support DSE core workloads. (DSP-24853, [CVE-2024-7254](https://nvd.nist.gov/vuln/detail/CVE-2024-7254))
* Added a fix for [HADOOP-19031](https://issues.apache.org/jira/browse/HADOOP-19031) into the DSE Hadoop software codebase. (DSP-24859, [CVE-2024-23454](https://nvd.nist.gov/vuln/detail/CVE-2024-23454))

# Release notes for 6.9.9
12 May 2025

## Components versions for DSE 6.9.9
 * Apache Solr™ 6.0.1.5.2977
 * Apache Spark™ 2.5.0.6&ast;
 * Apache TinkerPop™ 3.4.15-20250129-bd39a459
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.9 DSE Cassandra
* Fixed an issue to prevent a deadlock for some operator commands. (DSP-24701)
* Added expert-level system properties to work around invalid list keys. Contact DataStax Support to set these properties in DSE or in DSE client tools (such as `sstabledump`). (DSP-24819)
* Added `--address-config`, an `sstableloader` option to configure IP addresses from a `cassandra.yaml` file. (DSP-24826)

## 6.9.9 DSE CVE
* Upgraded the Apache Parquet and Apache Avro libraries used by Apache Spark to version `1.15.1`. (DSP-24802, [CVE-2025-30065](https://nvd.nist.gov/vuln/detail/CVE-2025-30065))

# Release notes for 6.9.8
7 April 2025

## Components versions for DSE 6.9.8
 * Apache Solr™ 6.0.1.5.2977&ast;
 * Apache Spark™ 2.5.0.5
 * Apache TinkerPop™ 3.4.15-20250129-bd39a459
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.8 DSE Indexing
* Fixed a hybrid vector query issue that occurred when sstable had rows containing null vectors. (DSP-24798)

## 6.9.8 DSE CVE
* Improved permissions checking on system keyspaces to limit user privileges appropriately. (DSP-24657, [CVE-2025-23015](https://nvd.nist.gov/vuln/detail/CVE-2025-23015))
* Removed Apache MINA from the DataStax Agent bundled with DSE Docker images. (DSP-24697, [CVE-2024-52046](https://nvd.nist.gov/vuln/detail/CVE-2024-52046))
* Removed an old jquery library from Apache Solr. (DSP-24777, [CVE-2020-11022](https://nvd.nist.gov/vuln/detail/CVE-2020-11022), [CVE-2020-11023](https://nvd.nist.gov/vuln/detail/CVE-2020-11023))
* Removed demonstration code from Docker images that was being used for testing purposes, and resolved some potential vulnerabilities. (DSP-24782, [CVE-2024-52046](https://nvd.nist.gov/vuln/detail/CVE-2024-52046))

# Release notes for 6.9.7
10 February 2025

## Components versions for DSE 6.9.7
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.5
 * Apache TinkerPop™ 3.4.15-20250129-bd39a459&ast;
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.7 DSE Core
* Updated the node startup process so that it verifies the minimum supported version of the Java Virtual Machine (JVM). If the current JVM version is not supported, the node startup process ends and notifies you of the minimum supported version. To view the latest recommended JVM patch version, see the DataStax Enterprise Release notes.  To disable the node startup JVM verification check,  set the `CASSANDRA_JDK_UNSUPPORTED` environment variable. (DSP-24659)
* Improved handling of 64-bit values defined in `/proc/self/limits` to prevent displaying an exception. Before the fix, if you set the `Max locked memory` field in `/proc/self/limits`  to a value larger than 2 GB, the DSE logs might report an exception in the description. (DSP-24705)

## 6.9.7 DSE Cassandra
* Introduced a transitional mode that enables both encrypted and unencrypted connections between nodes. This feature facilitates a seamless transition of node-to-node traffic from unencrypted to encrypted within a live cluster. 
**CAUTION**: To enable the cluster to continue to function during an upgrade, edit the `cassandra.yaml` file.
In the `server_encryption_options` section, set the `enable_legacy_ssl_storage_port` option to `true`. This setting enables listening on the original `ssl_storage_port`. When you complete the upgrade for the cluster, disable listening by setting the `enable_legacy_ssl_storage_port` option to `false`. For more information, see [Configure transitional mode for node-to-node connections](https://docs.datastax.com/en/dse/6.9/securing/internode-transitional-mode.html)). (DSP-24610)
* Fixed an issue where index entries were duplicated for tables with static columns and storage-attached indexing (SAI) on primary key components. Before the fix, the duplicated index entries would produce duplicated rows in SELECT queries using SAI indexes. After the fix, DSE prevents the creation of new duplicated index entries, but it doesn't remove the existing ones. If your tables contain duplicated index entries, rebuild the indexes in the affected tables. (DSP-24709)

## 6.9.7 DSE CVE
* Updated the Java Development Kit (JDK) versions to `8u432` and `11.0.25`. These JDKs help build and test DSE, and are available in DSE Docker images. For DSE versions that use JDK 8, this update also fixes known security vulnerabilities. (DSP-24611, [CVE-2024-21147](https://nvd.nist.gov/vuln/detail/CVE-2024-21147), [](https://nvd.nist.gov/vuln/detail/))
* Added a redaction flag for Apache Solr to improve security.  (DSP-24474, [CVE-2023-50291](https://nvd.nist.gov/vuln/detail/CVE-2023-50291))

# Release notes for 6.9.6
16 January 2025

## Components versions for DSE 6.9.6
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.5
 * Apache TinkerPop™ 3.4.15-20241206-b7790fff
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.6 DSE Cassandra
* Added functionality to compress the index status messages that the gossip protocol shares with other nodes. This enhancement ensures that the gossip message size guardrail allows an appropriate number of secondary indexes. (DSP-24654)

## 6.9.6 DSE SparkConnector
* Improved the reliability of the DataStax Connector for Apache Spark to Apache Cassandra. The connector now retries queries when it receives connectivity errors and timeouts. (DSP-24651)

## 6.9.6 DSE Miscellaneous
* Replaced the x86 System Information Gatherer And Reporter (Sigar) library with a Java-native Operating System and Hardware Information (OSHI) library. To provide compatibility with the OSHI library, this change also updates the Java Native Access (JNA) library version from `5.11.0` to `5.14.0`. (DSP-24647)

## 6.9.6 DSE CVE
* Upgraded the `ch.qos.logback` library to version `1.2.13`. (DSP-24016, [CVE-2023-6378](https://nvd.nist.gov/vuln/detail/CVE-2023-6378))
* Upgraded the Apache MINA core library to version `2.0.27`. (DSP-24667, [CVE-2024-52046](https://nvd.nist.gov/vuln/detail/CVE-2024-52046))

# Release notes for 6.9.5
16 December 2024

## Components versions for DSE 6.9.5
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.5
 * Apache TinkerPop™ 3.4.15-20241206-b7790fff&ast;
 * Apache Tomcat® 8.5.100
 * DSE Java Driver 1.10.0-dse-20241015 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.5 DSE Cassandra
* Improved `libjemalloc` implementation to detect `libmalloc2` in Amazon Linux 2023 and RedHat-based platforms. This is a subsequent fix from `DSP-24402`. (DSP-24632)
* Added configuration to warn or reject on wrong-topology single-partition local requests. These yaml configuration options are `log_out_of_token_range_requests` and `reject_out_of_token_range_requests`. They are not initially present in `cassandra.yaml` but can be added as desired. The defaults are `log_out_of_token_range_requests:true` and `reject_out_of_token_range_requests:false`. Enabling `reject_out_of_token_range_requests` is mutually exclusive with nodesync. That is, NodeSync must be disabled before enabling `reject_out_of_token_range_requests`. (DSP-24437)
* Fixed gossip issue with gossip-only and bootstrapping nodes missing DC/Rack/Host ID endpoint state. (DSP-24567)
* Added a new `nodetool` command: `nodetool checktokenmetadata`. This command verifies if the `TokenMetadata` is in sync with the Gossip `endpointState`.  To fix a node with `TokenMetadata` that is out of sync, restart the node. (DSP-24597)
* Fixed an issue where the outbound connection pending messages counter, `numPendingMessages`, did not reset correctly. This fix prevents the connection from stalling, and keeps a node in a reachable state. (DSP-24617)

## 6.9.5 DSE Platform
* Added support for Amazon Linux 2023 (DSP-23827).

## 6.9.5 DSE CVE
* Removed some Apache ZooKeeper JAR files from the tarball to remove potential security vulnerabilities. (DSP-24531, [CVE-2023-44981](https://nvd.nist.gov/vuln/detail/CVE-2023-44981))

# Release notes for 6.9.4
13 November 2024

## Components versions for DSE 6.9.4
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.5&ast;
 * Apache TinkerPop™ 3.4.15-20241028-a6bf761d&ast;
 * Apache Tomcat® 8.5.100&ast;
 * DSE Java Driver 1.10.0-dse-20241015&ast; (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.4 DSE Core
* Updated the JDK used to build DSE to versions `8u422` and `11.0.24`. (DSP-23997)
* Changed the MAX_HEAP_SIZE to avoid OOM errors with new Java 11 Garbage Collector. The change is done in the following scrips: `bin/dse`, `bin/dsetool`, `resources/cassandra/bin/nodetool`. (DSP-24431)

## 6.9.4 DSE Docker
* Changed DSE 6.9 images to load the OSS Management API as a Java Agent. As of DSE 6.9.3, the outdated in-tree Management API has been removed, and the OSS Management API has been bundled to replace it. (DSP-24564)

## 6.9.4 DSE Driver
* Updated DSE Java Driver with fix for JAVA-3125. (DSP-24556)

## 6.9.4 DSE CVE
* Updated the spark version to `2.4.0.31` to pull in the latest ivy library (vs 2.5.2) for a vulnerability fix. (DSP-23685, [CVE-2022-46751](https://nvd.nist.gov/vuln/detail/CVE-2022-46751))
* Upgraded tomcat-embed-core to version `8.5.100`. (DSP-24013, [CVE-2023-46589](https://nvd.nist.gov/vuln/detail/CVE-2023-46589))
* Upgraded nimbus-jose-jwt to `9.41.2`, json-smart to `2.5.1`, commons-lang3 to `3.17.0`, commons-io to `2.17.0`, and Azure SDK BOM to `1.2.28`. (DSP-24015, [CVE-2023-52428](https://nvd.nist.gov/vuln/detail/CVE-2023-52428))
* Updated aws-java-sdk library from `1.12.549` to `1.12.774` to address CVE 2024-21634. (DSP-24018, [CVE-2024-21634](https://nvd.nist.gov/vuln/detail/CVE-2024-21634))
* Upgraded orc-core from version `1.5.2` to `1.9.4`. (DSP-24538, [CVE-2024-36114](https://nvd.nist.gov/vuln/detail/CVE-2024-36114))
* Upgraded Apache Avro to version `1.11.4`. (DSP-24540, [CVE-2024-47561](https://nvd.nist.gov/vuln/detail/CVE-2024-47561), [CVE-2023-39410](https://nvd.nist.gov/vuln/detail/CVE-2023-39410))
* Upgraded reload4j to version `1.2.25`. (DSP-24551, [CWE-611](https://nvd.nist.gov/vuln/detail/CWE-611))
* Upgraded tika-core to version `1.28.5`. (DSP-23425, [CVE-2022-30126](https://nvd.nist.gov/vuln/detail/CVE-2022-30126), [CVE-2022-30973](https://nvd.nist.gov/vuln/detail/CVE-2022-30973))

# Release notes for 6.9.3
14 October 2024

## Components versions for DSE 6.9.3
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.2&ast;
 * Apache TinkerPop™ 3.4.15-20240705-ffb48eb3
 * Apache Tomcat® 8.5.94
 * DSE Java Driver 1.10.0-dse-20240930&ast; (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/java-drivers.html) to choose an appropriate version.

## 6.9.3 DSE Cassandra
* Fixed sstablescrub to run with `-t` disabled by default. (DSP-24501)
* Added guardrail warning for large columns in `cassandra.yaml` file. The new field is called `column_value_size_warn_threshold_in_kb` can can be used to get warned when a column is larger than a given value. By default this field is not used. (DSP-24384)
* Replaced the out-dated in-tree Management API code with the updated OSS version from GitHub [k8ssandra/management-api-for-apache-cassandra](https://github.com/k8ssandra/management-api-for-apache-cassandra). This should not affect any DSE 6.9 users except for situations where DSE 6.9 Docker images are being used with Management API enabled. Those cases will be fixed in a future DSE 6.9.x release.

## 6.9.3 DSE Graph
* Fixed count() query in classic graph. (DSP-24336)
* Fixed Spark default JVM options (resources/spark/conf/java-opts) to work with Java 11. (DSP-24512)

## 6.9.3 DSE Driver
* Updated DSE Java Driver with fix for JAVA-2738. (DSP-24514)

## 6.9.3 DSE Performance
* Changed the default location of the histogram aggregation work, offloading it by default to a thread pool different than the main one. This unblocks the TPC threads when large numbers of tables exist. (DSP-24520)

## 6.9.3 DSE Node/DseTool
* Updated Debian package dependencies on `libaio1` so that it can be installed on Ubuntu 24.04 (Noble Numbat). (DSP-24359)

## 6.9.3 DSE CVE
* Upgraded jetty to version `9.4.56.v20240826`. (DSP-24447, [CVE-2024-22201](https://nvd.nist.gov/vuln/detail/CVE-2024-22201))
* Upgraded Spotify DNS Wrapper Library to version 3.3.2 and dnsjava library to version 3.4.2. (DSP-24545, [CVE-2024-25638](https://nvd.nist.gov/vuln/detail/CVE-2024-25638), [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868), [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387))


# Release notes for 6.9.2
30 August 2024

## Components versions for DSE 6.9.2
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.1
 * Apache TinkerPop™ 3.4.15-20240705-ffb48eb3
 * Apache Tomcat® 8.5.94
 * DSE Java Driver 1.10.0-dse-20240621 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.2 DSE Cassandra
* Improved `libjemalloc` detection to detect `libmalloc2` in systems where this package is present. (DSP-24402)

## 6.9.2 DSE Upgrade
* Fixed a bug in 6.9 upgrade caused by DSE nodes in mixed-version mode choosing non-compatible checksum algorithms. (DSP-24364)


# Release notes for 6.9.1
14 August 2024

## Components versions for DSE 6.9.1
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.1
 * Apache TinkerPop™ 3.4.15-20240705-ffb48eb3
 * Apache Tomcat® 8.5.94
 * DSE Java Driver 1.10.0-dse-20240621 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.1 DSE Cassandra
* Improved memory footprint of `ORDER BY` queries. (DSP-24375)
* Fixed a bug in SAI filtering intersection for map types. (DSP-24389)
* Fixed a race condition in disabling of in-progress compactions when interrupting compaction types are initiated. Added debug logging to help identify in-progress and interrupting compactions. (DSP-24318)
* Made Kerberos authentication provider for `cqlsh` pluggable so customers can plug in and/or customize how it works in their environment. (DSP-24129)
* Fixed `OR` operator when using `ANALYZER_MATCHES` with n-grams. (DSP-24357)
* Fixed a bug in scheduling that resulted in searches resuming execution on different threads then when initialized. It resulted in invalid query results. (DSP-24385)
* Fixed a bug in backup error handling that led to backups being stuck indefinitely in the running state, resulting in snapshots not getting cleaned up. (DSP-24390)
* Fixed SSBR to prevent dropping not used UDTs on restore. (DSP-24376)

## 6.9.1 DSE CVE
* Upgraded commons-compress to version 1.26.2. (DSP-24380, [CVE-2024-25710](https://nvd.nist.gov/vuln/detail/CVE-2024-25710))


# Release notes for 6.9.0
10 July 2024

This is the first version of DSE 6.9 having Java 11 and Vector support.

## Components versions for DSE 6.9.0
 * Apache Solr™ 6.0.1.5.2973
 * Apache Spark™ 2.5.0.1
 * Apache TinkerPop™ 3.4.15-20240705-ffb48eb3
 * Apache Tomcat® 8.5.94
 * DSE Java Driver 1.10.0-dse-20240621 (DSE *internal-only* version)
 * Netty 4.1.100.1.dse
 * Spark JobServer 0.8.0.56

**NOTE**: above-listed DSE Java Driver is an _internal-version_ only.
If you're developing applications, please refer to the [Java Driver documentation](https://docs.datastax.com/en/driver-matrix/doc/java-drivers.html) to choose an appropriate version.

## 6.9.0 DSE Upgrade

* To upgrade to DSE 6.9 from an earlier release, you need to install the Java Development Kit (JDK) version `11.0.2` or later, and Python `3.8` to `3.11`. In general, follow the guidance listed in the Release Notes and upgrade to the JDK and Python versions recommended for a specific DSE 6.9 release. For more information, see [Preparing to upgrade](https://docs.datastax.com/en/upgrading/datastax-enterprise/dse-68-to-69.html#preparing-to-upgrade).
