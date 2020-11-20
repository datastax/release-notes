# Release notes for DataStax Studio 6.8.6
19 November 2020

## Studio 6.8.6 Client

* Cluster information is displayed in the top bar of a Notebook. (STUDIO-3138)
* Fixes broken documentation links in the Create Graph dialog. (STUDIO-3138)

## DataStax Studio 6.8.6 IDE

* Fixes a problem that can spam the log with 'No enum constant found for name' messages. (STUDIO-3174)
* Fixes a problem with detection of classic or core graph in Gremlin cells. (STUDIO-3138)

## DataStax Studio 6.8.6 Server

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
