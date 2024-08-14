# Release notes for DataStax Enterprise 6.9
DSE 6.9.x is compatible with Apache Cassandra&trade; 3.11 and adds additional production-certified changes, if any.
Components that are indicated with an asterisk (&ast;) (if any) are known to be updated since the prior patch version.

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
