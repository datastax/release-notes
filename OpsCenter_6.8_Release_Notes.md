# Release notes for OpsCenter

## OpsCenter 6.8.5

* Fixed a problem preventing point in time restores using a snapshot on a destination. (OPSC-16739)

## OpsCenter 6.8.4 

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
* Added chrony output to the diagnostic tarball. (OPSC-16560)
* Fixed an issue where the diagnostic tarball download link would be incorrect when behind a proxy with a subpath. (OPSC-15566)
* Fixed check-2i-cardinality warning caused by OpsCenter backup_reports index. (OPSC-15895)
* Fixed an issue that could cause OpsCenter to failover during a diagnostics tarball collection. (OPSC-16228)
* Improved the performance of the metric fetcher when querying values from the storage cluster. (OPSC-16559)


## OpsCenter 6.8.4 Provisioning

* Fixed OpsCenter and LCM workflows that resulted in seemingly identical clusters. (OPSC-16520)
* Fixed LCM config rendering for dse-env.sh when using custom-env-vars. (OPSC-16629)


## OpsCenter 6.8.4 Repair Service

* When DSR isn't in use don't open connection pool just to close it. (OPSC-16351)
* Only count unique repair scopes when calculating repair backpressure (OPSC-16592)


## OpsCenter 6.8.4 UI

* OpsCenter now cleans up directories created during a diagnostic. (OPSC-16300)
