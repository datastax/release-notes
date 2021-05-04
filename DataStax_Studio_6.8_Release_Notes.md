# Release notes for DataStax Studio 6.8

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