# Release notes for OpsCenter

# Release notes for OpsCenter 6.8.23
16 Jan 2023

## 6.8.23 OpsCenter Core
* Added stomp-setup-timeout to the address.yaml config options with a default of 30 seconds.
  This resolves issues around initializing agent stomp connections.
  We recommend increasing this setting to 120 seconds for large clusters. (OPSC-17235)


# Release notes for OpsCenter 6.8.22
14 Dec 2022

## 6.8.22 OpsCenter Core
* Added support for Ubuntu 22.04 (Jammy Jellyfish) package installation. (OPSC-17213)
* Updated `sqlite-jdbc` to version 3.40.0.0. (OPSC-17237, [CVE-2019-19242](https://nvd.nist.gov/vuln/detail/CVE-2019-19242))


# Release notes for OpsCenter 6.8.21
22 Nov 2022

Maintenance release with no code changes from 6.8.20 version.
Created to address issue that some users would see 6.8.20-rc2 as latest version instead of the official 6.8.20 release.  


# Release notes for OpsCenter 6.8.20
18 Nov 2022

## 6.8.20 OpsCenter Core

* Fixed a problem where agents would sometimes just hang when trying to start the stomp connection to opscenterd. (OPSC-17209)
* Basic IPv6 support. OpsCenter can now connect to clusters using IPv6. When configuring opscenterd’s [webserver] or [stomp] to listen on IPv6 a specific ip address needs to be specified. opscenterd does not support listening on ::/0. (OPSC-16694)

## 6.8.20 OpsCenter Backup Service

* Implemented configuration that will allow agents use rsync to transfer files to a localfs destination. This is enabled through the new address.yaml config parameter ‘use_rsync_for_localfs’. It is recommended to enable this if there are problems with the agents spawning large numbers of sub-processes when backing up to a localfs destination. (OPSC-16925)
* Handled error when the agent moves a commit log from the staging directory to the storage directory and the file is already there. (OPSC-17089)

## 6.8.20 OpsCenter Monitoring

* Changed the library used for the post url alert functionality. This update allows the feature to work with IPv6. (OPSC-17202)

## 6.8.20 OpsCenter Life Cycle Manager 

* Basic IPv6 support for LCM. (OPSC-17225)


# Release notes for OpsCenter 6.8.19
30 May 2022

## 6.8.19 OpsCenter Backup Service

* When not using sstableloader for a point in time restore, opscenterd will no longer use the host id check to ensure the topology has not changed. Instead the point in time restore call relies on the topology check already done by restores not using sstableloader. (OPSC-17120)

## 6.8.19 OpsCenter Core

* Added secret reduction when including spark-alwayson-sql.conf in a diagnostic tarball. (OPSC-17141)

## 6.8.19 OpsCenter Monitoring

* Fixed an issue that prevented the collection of data center based metrics. (OPSC-17016)

# Release notes for 6.8.18
10 Mar 2022

## 6.8.18 OpsCenter Backup Service

* When restoring from other location a host id and backup tag can now be specified. This can dramatically speed up the process of scanning a destination for snapshots. (OPSC-16989)
* Fixed and issue that prevented the agent from retrying syncing files to a destination. (OPSC-17096)
* Fixed a restore issue where the table truncate during a restore either wouldn't happen at all or would happen asynchronously. (OPSC-17111)

## 6.8.18 OpsCenter Core

* Replaced log4j with reload4j and updated slf4j libraries to 1.7.36. (OPSC-17097)

# Release notes for OpsCenter 6.8.17
13 Jan 2022

## OpsCenter 6.8.17 Backup Service

* During a restore tables will not be truncated until after opscenterd verifies there is sufficient space in the agent tmp dirs for the restore. (OPSC-16991)
* Reintroduced agent config parameters remote_verify_initial_delay and remote_verify_max which specify an amount of time to wait before verifying file uploads during a backup to a destination. (OPSC-17040)
* Allow the agent to skip the schema verification check during a backup if the agent is unable to get the current schema from the cassandra driver. (OPSC-17061)

## OpsCenter 6.8.17 Monitoring

* Agent will now include rack and datacenter in the long interval node details sent to opscenterd. Rack and datacenter information will also be included in the information updated when viewing the node details dialog. (OPSC-17073)

## OpsCenter 6.8.17

* Updated version of guava, jackson-databind, and javassist to fix vulnerabilities. (OPSC-16922)

# Release notes for OpsCenter 6.8.16

## OpsCenter 6.8.16 Backup Service

* Fixed restore for a schema with restrict rows on condition is present. (OPSC-16924)
* Fixed the restore of solr index keyspaces having capitalized table name. (OPSC-16970)

## OpsCenter 6.8.16 

* If allow_one_failure under [backup_service] in opscenterd.conf is set to true, backups where a single node failed will now be marked as a success rather than a failure. (OPSC-16961)
* Added the new config parameter "cluster_name_restore_confirmation" to the "[ui]" section of opscenterd.conf. When set to True this will added a text field to the restore confirmation window where the user will have to type the name of the cluster before the restore will run. (OPSC-16994)
* Making the restore progress even when the dse version can't be determined.  (OPSC-17001)
* Removed config parameters remote_verify_initial_delay and remote_verify_max from address.yaml because they are no longer used by the code.  (OPSC-17023)
* Fixed a bug where default values took precedence over explicit values in the [agent_config] section of the cluster config file. (OPSC-17029)
* When downloading diagnostic tarballs with the diagnostic_tarball_lock_time feature, old diagnostic tarballs will be deleted from the disk before a new one is generated. (OPSC-16997)

# Release notes for OpsCenter 6.8.15
19 Aug 2021

## OpsCenter 6.8.15 Backup Service
* Fixed the restore of Transparent Data Encryption (TDE) enabled tables and keyspaces. (OPSC-16845)
* Improved communication between agents and Opscenter. (OPSC-16939)

## OpsCenter 6.8.15 Monitoring
* The solr query metrics - mbean data - update, merge, query, commit, search index pool, stall and filtercache metrics are added as opscenter metrics. (OPSC-14846)

## OpsCenter 6.8.15 NodeSync
* Disable the nodesync refresh by modifying environment requirements in the `[nodesync]` section. (OPSC-16968)

## OpsCenter 6.8.15 UI
* Fixed issue of unavailability of SAI related metrics. (OPSC-16903)

## OpsCenter 6.8.15
* Added new config `single_session_per_user` in authentication section so by setting it to `True` with `enabled` option will enable the single session per user under different browsers. (OPSC-16830)
* Improved the look up of snapshots from other locations to ensure all snapshots are listed when snapshots differ based on datacenter. (OPSC-16985)
* Added a template for sending messages over slack webhooks. (OPSC-16535)
* Introduced new config flag `ssl_redirect` to disable port 8888 when ssl is enabled. (OPSC-16928)
* Fixed DSE startup failure during PIT restore. (OPSC-16942)
* Added support for the `clusters/datacenters/nodes` with non-default ssh port while importing into the LCM. (OPSC-16953)
* Permissions to `/etc/opscenter/` path for other users is restricted. (OPSC-16976)
* Updated backup destination logic to be datacenter aware. (OPSC-16984)

# Release notes for OpsCenter 6.8.14
04 June 2021

## OpsCenter 6.8.14
*  Improvements in internal testing infrastructure. (OPSC-16945)

# Release notes for OpsCenter 6.8.13
20 May 2021

## OpsCenter 6.8.13 Backup Service
* Optimized communication between OpsCenter and agents for restores. (OPSC-16790)
* Fixed a bug preventing the backup of some tables using SAI. (OPSC-16919)

## OpsCenter 6.8.13 Best Practice Service
* Fixed a bug in the best practice rule "Require Oracle HotSpot or OpenJDK" that caused some versions of OpenJDK to be marked as invalid. (OPSC-16834)

## OpsCenter 6.8.13 Core 
* Added nodetool cfhistograms command to data collector. (OPSC-7376)
* Using the secret_key_file for the key while taking backup of tables with system_info_encryption is enabled. (OPSC-16198)
* Improve diagnostic tarball generation to prevent the creation of multiple diagnostic tarballs in concurrent requests. (OPSC-16684)
* Improved password obfuscation in the diagnostic tarball.  (OPSC-16786)
* Improved error handling in diagnostic tarball password obfuscation script. (OPSC-16846)
* Updated ring-jetty-adapter version from 1.5.0 to 1.9.1 so that Jetty version will be updated to 9.4.x (OPSC-16931)
* DataStax branding refresh on the OpsCenter landing page for login, dashboard and Life Cycle Manager (LCM) pages (OPSC-16851)

# Release notes for OpsCenter 6.8.12
22 March 2021

## OpsCenter 6.8.12 Core
* Updated Jackson Databind version from 2.10.2 to 2.10.5.1  (OPSC-16804)
* Systemd service files added for opscenterd and agents (OPSC-8299)
* Added the force_https_redirects config parameter in the authentication section of opscenterd.conf to force redirects from opscenterd to use https for situations where opscenterd is behind a proxy that handles encryption. (OPSC-16805)

## OpsCenter 6.8.12 NodeSync
* Changed the labels from Enabled to Activated and from Disabled to Deactivated (OPSC-14220)

## OpsCenter 6.8.12 Provisioning
* Removed default values from Inter-node-messaging options non-required fields in dse.yaml definitions (OPSC-16659)

# Release notes for 6.8.11
12 February 2021 

## OpsCenter 6.8.11 Core
* Added DSE 6.8.0 jvm files to the diagnostic tarball. (OPSC-16602)
* Update definition file for `10-statsd.conf` so the "host" field will now be treated as a string. (OPSC-16782)

## OpsCenter 6.8.11 Backup Service
* Added additional logging when transferring backup data to a destination fails. Also moved some verbose agent logging from debug to trace. (OPSC-16803)
* Updated OpsCenter to be aware of the new sstable format introduced in DSE 6.8.9 (OPSC-16815)

## OpsCenter 6.8.11 Best Practice Service
* DSE and Cassandra system keyspaces were removed from wide partition check best practice rule. (OPSC-12790)
* Provided a config value `ignore_allow_filtering_tables` in `opscenterd.conf` where a list of *keyspace.table* can be provided to make `ALLOW FILTERING` best practice rule ignore them. (OPSC-14785)
* Changed Best Practice Rule definition for "low" importance rules to change "alert-level" from *alert* to *warn*. This will reduce alert notifications for low importance best practice rules. (OPSC-16587)

## OpsCenter 6.8.11 Provisioning
* Introduced default value as `null` for `ldap_options.all_parent_groups_search_type` in `dse.yaml` (OPSC-16747)

## OpsCenter 6.8.11 Repair Service
* Introduced a new `ignore_schema_addition_events_for_repair_service` config parameter. When set to `True` schema change events will no longer cause the repair service to restart. (OPSC-15991)
* The `dse_perf` keyspace and it's tables ignored by the repair service will no longer be considered for `gc_grace_seconds` value calculation in the repair service UI. (OPSC-16249)

## OpsCenter 6.8.11 UI
* Changed label of the link from "Remove" to "Clear" on the notification when an activity completes. (OPSC-14823)

# Release notes for OpsCenter 6.8.10
15 January 2021

## OpsCenter Core 6.8.10
* Refactored the ssl parameters for connecting to Cassandra with client to node encryption. This fixed a bug for configurations where only the keystore was
specified. The `require_two_way_ssl` config parameter has been removed and the case it was introduced for will now be handled automatically. (OPSC-16802)

# Release notes for OpsCenter 6.8.9
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

## OpsCenter 6.8.9 Platfor
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

---
