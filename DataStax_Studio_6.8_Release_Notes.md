# Release notes for DataStax Studio 6.8

# Release notes for DataStax Studio 6.8.32
24 July 2023

## Studio 6.8.32 Client
* Fix a problem in which very large Number values inside JSON results were not displayed correctly in the CQL results Details view. (Studio-3244)

## Studio 6.8.32 Server
* Add support for Astra Vector Search databases. (Studio-3241, Studio-3242)
* Add the ability to use an Astra database token in a connection configuration. (Studio-3246)
* Add configuration setting to support displaying Date and Timestamp values in a specific timezone. (Studio-3237)
```
  # The timezone used to display Date and Timestamp values.
  # Examples: UTC, GMT, CET, America/Los_Angeles, America/New_York, Europe/Paris, Asia/Kolkata, etc
  # These zone ids are defined by Java in java.time.ZoneId 
  # Some special values are also supported:
  # * "SYSTEM" - use the default system timezone.
  # * "TIMESTAMP" - display as timestamp value (milliseconds since epoch) 
  # Default: UTC
  displayTimezone: UTC
```
* When using Astra Database for DSE, graph queries will automatically be executed with local quorum consistency level. A configuration setting can be used to enable/disable this capability. (Studio-3229)
```
  # Use LOCAL_QUORUM consistency level when connected to Astra Database for DSE (AD4D)
  # Default: true
  gremlinAD4DConsistencyLevelEnabled: true
```
* Fix a problem that caused Studio to fail to start while clearing notifications from previous releases. (Studio-3243)

# Release notes for DataStax Studio 6.8.26
06 January 2023

## Studio 6.8.26 IDE
* Studio editor now recognizes additional table encryption options (Studio-3232):
  * Compression classes: Encryptor, EncryptingLZ4Compressor, EncryptingDeflateCompressor, and EncryptingSnappyCompressor
  * cipher_algorithm
  * secret_key_strength
  * system_key_file

## Studio 6.8.26 Server
* Fix incorrect timezone adjustment for date and timestamp results from Spark SQL queries. (Studio-3133)
* Fix "keyspace not found" error executing a CQL statement with a mixed case keyspace name and in which Studio detects a syntax error. (Studio-3222)
* Makes startup more resilient to unexpected errors. (Studio-3223)
* Fix `NullPointerException` serializing notebooks due to uninitialized fields. (Studio-3224)
* Update to Spring library version 5.3.20 to address CVE-2022-22970 and CVE-2022-22971. (Studio-3227 and Studio-2009)

# Release notes for DataStax Studio 6.8.21
31 March 2022

## Studio 6.8.21 Client
* Javascript library updates: bootstrap-sass 3.4.1, node-sass 4.2.0, handlebars 4.7.7, lodash 4.17.21. (Studio-3214)

## Studio 6.8.21 Server
* Studio startup no longer automatically loads all notebooks to clear any cell "running" statuses remaining from before the Studio restart. Use the notebook menu action "Clear All Cell Results..." or the cell menu action "Clear Results..." to both clear cell results and the cell "running" status. A new configuration parameter, `resetRunningNotebookCellsOnStartupEnabled`, may be set to `true` or `false` (default) to control this behavior. (Studio-3215)
* Astra connections now work with Graph if it is available. (Studio-3212)

# Release notes for DataStax Studio 6.8.20
25 January 2022

## Studio 6.8.20 Client
* Improve Spark SQL CACHE/UNCACHE statement validation when prefixing a table with a database name with both persistent and temporary tables. (Studio-3198)

## Studio 6.8.20 Server
* Update to log4j library version 2.17.1 to address CVE-2021-44832. (Studio-3208)
* Remove unused log4j 1.x artifacts from Studio distribution. (Studio-3209)
* Fix issue with http headers running in K8s. (Studio-3210)

# Release notes for DataStax Studio 6.8.19
20 December 2021

## Studio 6.8.19 Server
* Update to log4j library version 2.17.0 to address CVE-2021-45105. (Studio-3207)
* Fix race condition that could lead to random Graph or Spark SQL connection terminations. (Studio-3206)

# Release notes for DataStax Studio 6.8.18
16 December 2021

## Studio 6.8.18 Server
* Update to log4j library version 2.16.0 to address CVE-2021-45046. (Studio-3205)

# Release notes for DataStax Studio 6.8.17
13 December 2021

## Studio 6.8.17 Client
* Adds an optional Gremlin Port field to the Connection configuration. (STUDIO-3195)

## Studio 6.8.17 Server
* Update to log4j library version 2.15.0 to address CVE-2021-44228. (Studio-3204)
* Improved detection of Spark SQL connection status to avoid premature connection termination. (STUDIO-3203)
* Add configuration settings to adjust Gremlin and Spark SQL connection heartbeat and idle timeout values. (STUDIO-3202)
```
  connectionManagement:
    # Graph (gremlin driver) connection heartbeat polling interval (milliseconds).
    # The connection status is tested at the given interval to ensure it is still working.
    # Default: 30000 (30 seconds)
    gremlinHeartbeatIntervalMillis: 30000

    # Graph (gremlin driver) connection timeout interval (milliseconds).
    # The time interval after which the connection will be terminated if there have been
    # no successful user or connection hearbeat queries executed.
    # Default: 90000 (90 seconds)
    gremlinIdleTimeoutMillis: 90000

    # Spark SQL (jdbc driver) connection heartbeat polling interval (milliseconds).
    # The connection status is tested at the given interval to ensure it is still working.
    # Default: 30000 (30 seconds)
    sparkHeartbeatIntervalMillis: 30000

    # Spark SQL (jdbc driver) connection timeout interval (milliseconds).
    # The time interval after which the connection will be terminated if there have been
    # no successful user or connection hearbeat queries executed.
    # Default: 300000 (5 minutes)
    sparkIdleTimeoutMillis: 300000
```
* Improve ability to troubleshoot Graph errors by logging the remote server stack trace when the Graph gremlin driver reports a ResponseException. (STUDIO-3201)
* Fix issue creating a Classic graph using the Create Graph dialog when connected to DSE versions 6.7 or earlier. (STUDIO-3200)
* Fix issue processing query results when CQL Timestamp values are used as the key value for a Map. The Studio server previously returned those Map key Timestamp values formatted only to seconds precision, which could lead to duplicate values and cause no results displayed in the client. Timestamp values used as Map keys are now formatted the same as other Timestamp values (ISO-8601: yyyy-MM-dd'T'HH:mm:ss.SSSZ). (STUDIO-3199)
* Fix error executing Spark SQL CACHE TABLE statements. (STUDIO-3198)
* Prevent relative file access on /images requests. (STUDIO-3196)
* Restrict notebook import URL's to use only http or https. (STUDIO-3167)
* Prevent internal stack traces appearing in http responses. (STUDIO-3010)

(:information_source: **Note**: there was no Studio 6.8.16 release)

# Release notes for DataStax Studio 6.8.15
10 September 2021

## Studio 6.8.15 Client
* Add Kerberos authentication support for CQL connections. (STUDIO-1685)
* Add ability to clone Notebooks and Connection Configurations. (STUDIO-2857)
* Correct filtering of system keyspaces that belong to DSE Classic Graphs. (STUDIO-3194)
* Remove warning about `SELECT` permissions on `system_auth.roles` when connected to Astra. (STUDIO-3191)

## Studio 6.8.15 Server
* Add a configuration option, `querySystemAuthEnabled`, that determines if the `system_auth.roles` table should be queried by the Studio server to get metadata information about user roles. When this option value is set `false`, Studio will not to query the table at all, eliminating DSE audit log entries when the connected Studio user does not have `SELECT` permission to `system_auth.roles`. (STUDIO-3192)

(:information_source: **Note**: there were no Studio 6.8.12, 6.8.13 or 6.1.14 releases)

# Release notes for DataStax Studio 6.8.11
03 May 2021

## Studio 6.8.11 Client
* Updates the Create/Edit Astra Connection dialog to use field names "Client ID" and "Client Secret". (STUDIO-3184)
* Add IDE support to recognize the "split_during_flush" option of the `TimeWindowCompactionStrategy` (TWCS). (STUDIO-3190)

## Studio 6.8.11 Server
* CVE updates to jackson-databind, guava, jetty, commons-compress and async-http-client libraries (STUDIO-3182)
* Add "Getting Started with Astra" tutorial notebook. (STUDIO-3183)
* Fix issue displaying the wrong DC value in the Notebook connection information bar; the DC value shown should always be the local datacenter based on the given contact points in the Connection configuration. (STUDIO-3187)
* Fix "Error Writing" exception when executing certain CQL GRANT statements. (STUDIO-3189)
* Fix `NullPointerException` when mixed case keyspace or table name is used with `DESCRIBE ACTIVE|PENDING SEARCH INDEX SCHEMA ON <keyspace>.<table>` statement. (STUDIO-3186)

(:information_source: **Note**: there was no Studio 6.8.10 release)

# Release notes for DataStax Studio 6.8.9
29 January 2021

## Studio 6.8.9 Client
* Increases the display width of graph names in drop down menus, and adds a tooltip with the full graph name to the Notebook graph drop down menu. (STUDIO-3178)

## Studio 6.8.9 Server
* Fixes a startup bash script issue when the Java path contains spaces, which may happen after macOS upgrade to Big Sur. (STUDIO-3179)

(note: there was no Studio 6.8.7 or 6.8.8 release)

# Release notes for DataStax Studio 6.8.6
19 November 2020

## Studio 6.8.6 Client
* Cluster information is displayed in the top bar of a Notebook. (STUDIO-3138)
* Fixes broken documentation links in the Create Graph dialog. (STUDIO-3138)

## Studio 6.8.6 IDE
* Fixes a problem that can spam the log with 'No enum constant found for name' messages. (STUDIO-3174)
* Fixes a problem with detection of classic or core graph in Gremlin cells. (STUDIO-3138)

## Studio 6.8.6 Server
* Reduces advanced workload connection attempts when those workloads are not present in the cluster. (STUDIO-3138)
* Fixes possible errors if multiple CQL or Spark SQL cells are executed at the same time. (STUDIO-3175)

(note: there was no Studio 6.8.5 release)

# Release notes for DataStax Studio 6.8.4
24 September 2020

## Studio 6.8.4 Client
* Storage-attached indexes (SAI) are displayed in the schema viewer. (STUDIO-3162)

## Studio 6.8.4 Schema
* Storage-attached indexes (SAI) are displayed in the schema viewer. (STUDIO-3162)

## Studio 6.8.4 Server
* Storage-attached indexes (SAI) are displayed in the schema viewer. (STUDIO-3162)
* Notebook import accepts .zip files. (STUDIO-3157)
* Fixes a problem starting Studio on Windows if the java path contains a space. (STUDIO-3161)

## Older Release Notes
[Release notes for prior versions of DataStax Studio](https://docs.datastax.com/en/studio/6.8/studio/releaseNotes/RelNotesstudio.html) are available on the DataStax website.  

---
