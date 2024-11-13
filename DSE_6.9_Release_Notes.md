# Release notes for DataStax Enterprise 6.9
DSE 6.9.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any.
Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

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
