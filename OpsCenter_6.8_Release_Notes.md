# Release notes for OpsCenter

# Release notes for 6.8.11
12 February 2021 

## 6.8.11 OpsCenter Core

* Added DSE 6.8.0 jvm files to the diagnostic tarball. (OPSC-16602)
* Update definition file for 10-statsd.conf so the "host" field will now be treated as a string. (OPSC-16782)


## 6.8.11 OpsCenter Backup Service

* Added additional logging when transferring backup data to a destination fails. Also moved some verbose agent logging from debug to trace. (OPSC-16803)
* Updated OpsCenter to be aware of the new stable format introduced in DSE 6.8.9 (OPSC-16815)


## 6.8.11 OpsCenter Best Practice Service

* DSE and Cassandra system keyspaces were removed from wide partition check best practice rule. (OPSC-12790)
* Provided a config value ignore_allow_filtering_tables in opscenterd.conf where a list of keyspace.table can be provided to make ALLOW FILTERING best practice rule ignore them. (OPSC-14785)
* Changed Best Practice Rule definition for "low" importance rules to change "alert-level" from alert to warn. This will reduce alert notifications for low importance best practice rules. (OPSC-16587)

## 6.8.11 OpsCenter Provisioning

*  Introduced default value as null for ldap_options.all_parent_groups_search_type in dse.yaml (OPSC-16747)


## 6.8.11 OpsCenter Repair Service

* Introduced a new ignore_schema_addition_events_for_repair_service config parameter. When set to True schema change events will no longer cause the repair service to restart. (OPSC-15991)
* The dse_perf keyspace and keyspaces ignored by the repair service will no longer be considered for gc_grace_seconds value calculation in the repair service ui. (OPSC-16249)


## 6.8.11 OpsCenter UI

* Changed label of the link from "Remove" to "Clear" on the notification when an activity completes. (OPSC-14823)


# Release notes for 6.8.10
15 January 2021

## OpsCenter Core 6.8.10

* Refactored the ssl parameters for connecting to Cassandra with client to node encryption. This fixed a bug for configurations where only the keystore was
specified. The `require_two_way_ssl` config parameter has been removed and the case it was introduced for will now be handled automatically. (OPSC-16802)

# Release notes for 6.8.9
7 January 2021

## OpsCenter Core 6.8.9 

* Introduced a new `require_two_way_ssl` config option in the cluster conf file indicating if one-way or two-way SSL / host certificate validation has been enabled for client to node encryption. Default value is "False" which indicates one-way SSL certificate validation. (OPSC-14627)
* Fixed an issue preventing the update of cluster display name when authentication is enabled. (OPSC-16555)
* Increased the default diagnostic tarball download timeout from 2 minutes to 10 minutes. (OPSC-16679)
* Fixed an issue with ssl communication between opscenterd and the agents in newer versions of Java 8. (OPSC-16778)

## OpsCenter 6.8.9 Backup Service

* Updated backup of commit logs while the agent is running to be batched instead of transferring one at a time. (OPSC-15890)
* Fixed a bug that sometimes caused commit logs to be moved from staging to storage even though the transfer to the destination failed. (OPSC-15897)
* Improved messaging between the agent and OpsCenter during backups to reduce the memory usage. (OPSC-16772)

## OpsCenter 6.8.9 Core

* Upgraded the logic for redaction of sensitive information in the diagnostic tarball to provide better coverage. (OPSC-16765)
* Corrected an issue were using LCM to edit dse.yaml would sometimes result in a missing closing bracket. (OPSC-16636)

## OpsCenter 6.8.9 Platform

* Added an entry "7.8.x" for RedHat Enterprise in the platforms definition file. (OPSC-16710)

## OpsCenter 6.8.9 Repair Service

* Changed repair service property incremental_repair_tables default to be empty. (OPSC-15858)

## OpsCenter 6.8.9 UI

* Fixed Repair service status under Repair Service settings tab after re-enabling the repair service (OPSC-16723)

# Release notes for OpsCenter 6.8.6
06 November 2020

## OpsCenter 6.8.6 Backup Service

* Fixed a bug where opscenterd was not correctly waiting for schema agreement after recreating tables during a restore. (OPSC-16272)
* Fixed issue with recreating materialized views during restore if the name needed to be in quotes. (OPSC-16476)

## OpsCenter 6.8.6 Best Practice Service

* Updated the bad filter cache size best practice rule to use new default values for search nodes. (OPSC-13688)

## OpsCenter 6.8.6 Nodes

* When creating a diagnostic tarball OpsCenter agent now passes the SSL flag to nodetool and dsetool when SSL communication has been enabled for JMX on the DSE node. (OPSC-15818)

## OpsCenter 6.8.5
19 October 2020

* Fixed a problem preventing point in time restores using a snapshot on a destination. (OPSC-16739)

## OpsCenter 6.8.4
18 September 2020

* Restored support for DSE 5.1. (OPSC-16640)
* Added support for SAI metrics. (OPSC-16650)
* Fixed an issue that could cause the incorrect metric definition file to be used for DSE 6.0.10. (OPSC-16608)
* Removed code that prevented the use of PEM certificates for ssl. (OPSC-16615)

## OpsCenter 6.8.4 Backup Service

* Added datacenter selection to restore. (OPSC-16369)
* Performance improvements to restores that do not use sstableloader. (OPSC-16429)
* Changed the restore process to store size information with the backup to a destination so it no longer has to be queried before starting a restore. (OPSC-16430)
* Added support for renaming a keyspace during a restore. (OPSC-16540)
* File transfers from destinations during a restore can now be configured to run in parallel using [agents] restore_parallel_factor. This property defaults to 1 to remain compatible in behavior with older releases. (OPSC-16541)
* Added a config parameter to allow the specification of the parallel-level parameter for azcopy when using an azure destination. (OPSC-16676)
* Preventing logging of sstableloader parsing of blank lines. (OPSC-12755)
* Fixed several issues that could prevent destinations from getting cleaned up from the cluster configuration file after a restore. (OPSC-13253)
* Removed the need for host-ids to match when doing a restore without sstableloader. (OPSC-16528)
* Updated generic s3 destinations to allow the specification of region and path style access. Previously 'us-east-1' was the region used for generic s3 and that value must be used when editing preexisting generic s3 destinations. (OPSC-16639)
* Added a config parameter to skip verification of files after a backup completes. (OPSC-16656)
* Fixed an issue that prevented the backup and restore of tables using storage attached indexes. (OPSC-16673)

## OpsCenter 6.8.4 Core

* Permissions are now more restrictive on the SSL directory for package installs. (OPSC-16136)
* Changed rpc address logging from info to debug. (OPSC-16456)
* New LDAP authentication options which also enable support for multiple authentication sources.  (OPSC-16464)
* Removed IP constraint on '[agents] reported_interface' to allow use of hostnames for failover. (OPSC-16470)
* Added LCM definition entries to jvm.options to assist with capturing thread dumps. (OPSC-16599)
* Added back_track_device_lookup_path to the address.yaml agent config. Setting this value to true corrects problems encountered by the agent when collecting device information in some scenarios. (OPSC-12536)
* Improved failover logging. (OPSC-13463)
* Changed OpsCenter "disconnect cluster" so that it does not automatically remove the associated LCM cluster. (OPSC-15026)
* DataStax Agent now cleans up diagnostic tarball files on disk after transfer. (OPSC-16507)
* Fixed an issue where OpsCenter user interface session caches were invalidated but not cleaned up properly. (OPSC-16572)

## OpsCenter 6.8.4 CVE

* Fixed issues in how OpsCenter generates redirect responses during login. (OPSC-16011)

## OpsCenter 6.8.4 Monitoring

* Added support for DataStax Graph. (OPSC-14700)
* Added chrony output to the diagnostic tarball.
 (OPSC-16560)
* Fixed an issue where the diagnostic tarball download link would be incorrect when behind a proxy with a subpath. (OPSC-15566)
* Fixed check-2i-cardinality warning caused by OpsCenter backup_reports index. (OPSC-15895)
* Fixed an issue that could cause OpsCenter to failover during a diagnostics tarball collection. (OPSC-16228)
* Improved the performance of the metric fetcher when querying values from the storage cluster. (OPSC-16559)

## OpsCenter 6.8.4 Provisioning

* Fixed OpsCenter and LCM workflows that resulted in seemingly identical clusters.
 (OPSC-16520)
* Fixed LCM config rendering for dse-env.sh when using custom-env-vars. (OPSC-16629)

## OpsCenter 6.8.4 Repair Service

* When DSR isn't in use don't open connection pool just to close it. (OPSC-16351)
* Only count unique repair scopes when calculating repair backpressure (OPSC-16592)

## OpsCenter 6.8.4 UI

* OpsCenter now cleans up directories created during a diagnostic. (OPSC-16300)

# Release notes for previous versions
Release notes for previous OpsCenter patch releases can be found here:
https://docs.datastax.com/en/opscenter/6.8/opsc/release_notes/opscReleaseNotes_g.html