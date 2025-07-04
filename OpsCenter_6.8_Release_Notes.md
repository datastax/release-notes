# Release notes for OpsCenter

# Release Notes for OpsCenter 6.8.45
17th June,2025

## Core
* Added the `node_ips` option to monitor nodes for alerts. Setting this field limits alerts monitoring to the nodes specified in the list. For example: ["127.0.0.1","127.0.0.2"]. (OPSC-17644)
* Enhanced Solr Core Retrieval and Configurable Solr Core Exclusion in Backups: (OPSC-17704)
  * Improved the Solr core fetching process to be more targeted.OpsCenter now optimizes the retrieval of Solr core information. Instead of fetching cores for all keyspaces and tables, OpsCenter now fetches only the cores associated with `selected keyspaces and tables`. This improves performance and reduces unnecessary data processing. 
  * Added support for the `ignore_solr_resources` Boolean option in the `backup_service` section of the `opscenterd.conf` configuration file. When enabled, this option skips fetching `Solr core` information during backup creation, allowing for faster and more efficient backups.
* Introduced the following enhancements to authentication configuration and user lockout management: (OPSC-15418)
  * Added the `permanent_lockout_limit` option to the `authentication` section of the `opscenterd.conf` configuration file. This option supports permanent user lockouts. You can configure the number of total failed login attempts before the system locks out the user permanently. By default, this option is disabled.
  * Introduced two new API endpoints to manage permanently locked out users:
    * `GET /users/permanent-lockouts`: This option retrieves a list of users who are permanently locked out.
    * `GET /users/**USERNAME**/reset-permanent-lockout`: This option resets the permanent lockout status of a specified user. Only administrators can perform this operation.
* Added new options to the `authentication` section of `opscenterd.conf` to allow users to use `password_db` and `passwd_db` alias. (OPSC-17701)
* Addressed an issue that could cause errors when saving user role password history with previously used credentials. OpsCenter now handles these cases gracefully, improving the reliability of user role management.(OPSC-17693)
* Upgraded the `org.json:json` library to version `20230227`. (OPSC-17628 OPSC-17629)

## Backup Service
* Revised the compression process. OpsCenter now compresses only the differential SSTables when you sync a snapshot to a destination and enable compression. The system applies compression after the differential SSTable calculation, significantly reducing temporary storage usage and preventing temporary storage runout issues. (OPSC-17694)

## UI
* Provided the ability within the OpsCenter UI to generate diagnostics reports selectively for specific datacenters or nodes. This feature reduces the report size and improves performance when working with large clusters. (OPSC-17610)

# Release Notes for OpsCenter 6.8.44
25 April 2025

## Core
* Added support for running OpsCenter on Amazon Linux 2023. (OPSC-17676)
* Added a new configuration option, `enable_curl`, in the `posturl.conf` file. This option enables alerts to use the `curl` command. The default setting is `False`, which disables this option. To enable this option, set `enable_curl` to `True`. (OPSC-17177)

## Monitoring
* Added cassandra log, agent log, and the cdc_raw as options to alerts by partition function. (OPSC-17650)
* Fixed an issue that made LDAP authentication unusable. (OPSC-17688)

# Release Notes for OpsCenter 6.8.43
31 March 2025

## Core
* Added new configuration options to the `Authentication` section of the `opscenterd.conf` configuration file to allow passwords to be handled in a more secure manner. (OPSC-16260)
  * `password_complexity_enabled` - Enables OpsCenter to check for password complexity. The default setting is `False` (disabled).
  * `new_user_password_change` - Requires new users to change their password upon first authentication. The default setting is `False` (disabled).
  * `failed_login_attempts_limit` - Sets the number of failed login attempts before OpsCenter locks out a user. The default setting is `5`.
  * `user_lockout_timeout_in_seconds` - Sets the amount of time that a user is locked out from OpsCenter after exceeding the failed login attempt limit. The default setting is `300` seconds (5 minutes).
  * `user_password_expiration_days` - Sets the user password expiration period in days. The default setting is `0` (disabled).
  * `password_history_limit` - Specifies the number of previous passwords to review when updating a password. The default setting is `0` (disabled).

## Best Practice Service
* Fixed numerous issues in the best practice service UI that were introduced when upgrading the UI framework version. (OPSC-17625)
* Fixed a problem with the backup service UI that sometimes caused the configuration window for a different rule to be displayed when clicking a rule. (OPSC-17658)

## Backup Service
* Fixed an issue that prevented the deletion of compressed commit logs from the backup staging directory. (OPSC-17075)
* Improved `opscenterd` error handling of backup status updates after the backup for an agent was marked as complete. (OPSC-17641)
* Added support for `HTTPS_PROXY` on Microsoft Azure by adding the `azure_proxy_host` and `azure_proxy_port` options in the `opscenterd.conf` configuration file. (OPSC-17645)
* Updated rolling restarts during the point in time restore for a single datacenter so that only the nodes in the specified datacenter are restarted. (OPSC-16542)
* Fixed an issue for handling special characters in dropped columns when restoring a table schema. (OPSC-17640)
* Enabled the compression option for Azure backup destinations. (OPSC-17654)
* Fixed an issue that prevented the backup and restore of tables using Storage-Attached Indexes (SAI) in DSE 6.9. (OPSC-17678)
* Introduced `azcopy_max_files`, an agent configuration option to control the maximum number of files that the azcopy utility uploads at the same time. (OPSC-17614)

## Monitoring
* Resolved an issue that caused HTML tags to appear in the description of triggered alerts. (OPSC-17624)
* Added Solr index searcher metrics for DSE Search (Solr)-enabled tables. (OPSC-17680)

## UI
* Fixed a UI issue where several keyspace lists did not display more than 25 items. (OPSC-17663)

# Release Notes for OpsCenter 6.8.42
31 January 2025

## Backup Service
* Added support for picking individual tables when creating a backup. (OPSC-17084)
* Updated the AWS SDK version to `aws-java-sdk-s3:1.12.779`. To use the AWS CLI for bucket validation, set the `use_s3_cli` option to `true`. This option resolves issues when using some generic S3 providers, such as Cloudian. (OPSC-17639)
* Fixed an issue with the restore dialog where clicking `All Keyspaces` before expanding the tree would result in no tables being selected. (OPSC-17669)

## Core
* Upgraded the Apache Directory LDAP API to version `1.0.3` and the Apache MINA core library to version `2.0.27` to address a potential security vulnerability. (OPSC-17655)

# Release Notes for OpsCenter 6.8.41
26 November 2024

## Backup Service
* Improved the rsync operation by getting the throttle value from destination dialog. (OPSC-17623)
* Addressed issue with error logging in backup service. (OPSC-17034)
* Fixed issue with s3 object store not getting cleaned up when backup.json file is missing (OPSC-17578)

## UI
* Added versioning for configuration profiles in LCM, enabled seamless comparison and tracking of changes across versions, Improved transparency and control over profile changes. (OPSC-17535)
* Fixed authentication failures, when no default value is provided for `restrict_session_to_ip_and_agent`. (OPSC-17616)

## Core
* Fixed bug in `datastax-agent` script to prevent a non-zero exit code when PIDFILE environment variable is not set. (OPSC-17634)

# Release Notes for OpsCenter 6.8.40
11 September 2024

## Backup Service
* Improved the performance of AzCopy, by introducing new customizable configuration options. Users can now use these options `azure_parallel_level`, `azure_cap_mbps`, `azcopy_concurrency_value`, `azcopy_buffer_gb` and `azcopy_log_level` to fine-tune CPU utilization, faster file transfers, and efficient memory usage of AzCopy. (OPSC-17579)
* Added `backup_reports_migrate_data_ttl` optional config in `[backup_service]` in `opscenterd.conf` file to delete data older than ttl days. Added `backup_reports_ttl` in the same section for setting ttl, when creating records in backup reports table. (OPSC-17531)

## Core
* Fixed issues in showing the status of nodes in the ring view after a failover. (OPSC-17583)
* Fixed issues while calculating free-space of the tmp directory when the device name contains hyphens.(OPSC-17563)

# Release Notes for OpsCenter 6.8.39
30 July 2024

## Backup Service
* Fixed the Azure SAS token expiry issue for scheduled backups with Azure as the destination. (OPSC-17565)

## Best Practice Service
* Fixed issue with best practices service for repair service that does not seem to be honoring the `ignore_keyspaces` or `ignore_tables` parameters in `[repair_service]` section. (OPSC-17195)

## Provisioning
* Fixed issue with LCM creating a certificate with a spurious backtick on the OU element. (OPSC-17510)

## Core
* Added support for DSE 6.9.x versions. (OPSC-17576)

# Release Notes for OpsCenter 6.8.38
28 June 2024

## CVE
* Upgraded several Node.js libraries and also upgraded Clojure version from 1.10.0 to 1.11.2. (OPSC-16083)
* Upgraded joda-time to v2.12.7. (OPSC-17519)

## UI
* Fixed a regression introduced in 6.8.37 with `restrict_session_to_ip_and_agent` configuration setting, which did not obey the setting specified by `restrict_session_to_ip_and_agent`. (OPSC-17539)

## Core
* Fixed intermittent "No Data" issue in Dashboards for Search-Related Metrics. (OPSC-17526)

# Release Notes for OpsCenter 6.8.37
14 May 2024

## Backup Service
* Upgraded Azcopy to v10; added new authentication methods for connecting Azure storage. (OPSC-16022)
* Upgraded Azure SDK to V12. (OPSC-16414)
* Fixed an error that could occur when syncing backup meta data from a destination to OpsCenter's backup table. (OPSC-17506)
* Improved backup activity API and upgraded backup_reports table schema. (OPSC-17511)
* Added Migration script to upgrade backup_reports table. Added new config `backup_reports_migrate_data` in the `[backup_service]` section of `opscenterd.conf` file.  Set this to `True` to start migration, reset to `False` after the migration is completed and restart opscenter.

## Monitoring
* Removed unnecessary error warnings while generating diagnostic tarball. (OPSC-17517)
* Revamped posturl header parsing logic. (OPSC-17493)

## Core
* Updated the code to auto-enable systemd scripts. (OPSC-17383)
* Fixed issues with user login, during session timeouts. (OPSC-17505)
* Upgraded Bouncy Castle and clj-ssh to latest versions. (OPSC-17530)

# Release Notes for OpsCenter 6.8.36
1 Apr 2024

## Monitoring,UI
* Fixed issue with installing datastax-agent. (OPSC-17503)

## Core
* Reverted the code changes made for limiting a session to a specific user agent and IP address. (OPSC-17278)

# Release Notes for OpsCenter 6.8.35
22 Mar 2024

:warning: Customers who are upgrading the OpsCenter to 6.8.35 from older versions may face issue with agent installation. Please use [version `6.8.36`](#release-notes-for-opscenter-6836) instead.

## Backup Service
* Fixed an issue with PIT restore when there is a schema mismatch. Added `force_schema` parameter to PIT Restore API to solve this issue. (OPSC-17486)
* Fixed the backup process to run post-backup script after the snapshot files are synchronised to the destinations. (OPSC-17483)
* Fixed backup activity API memory and timeout issues using parameter `backup_activity_query_batch_size` configurable in `[backup]` section. (OPSC-17496)

## Monitoring
* Fixed an issue in diagnostic tarball generation to use `dse client-tool` instead of `dsetool` to list output for `sparkmaster`. Removed the deprecated `listjt` file. (OPSC-11798)

## Provisioning
* Added option to configure truststore location through LCM. (OPSC-17395)

## UI
* Added Materialized View restoration progress in the restore dialog. (OPSC-17263)

## Core
* Fixed potential memory leak in the twisted library. (OPSC-17147)

# Release Notes for OpsCenter 6.8.34
22 Feb 2024

## Core
* Fixed OpsCenter startup failure for customers using a separate storage cluster. Added `alert_on_no_host_available` to the `[storage_cassandra]` section of the cluster configuration. A setting of `true`  triggers a message in the backup opscenter logs when *opscenterd* is unable to make a cql connection to the storage cluster. (OPSC-17488)
* Added `heartbeat_warn_window` to the `[failover]` section of the `opscenterd.conf`. When set to non zero integer value (seconds), Backup OpsCenter triggers a message in the backup opscenter logs if it does not receive heartbeat from Primary OpsCenter in the given window and added `heartbeat_log_level` to the `[failover]` section of the opscenterd conf. When set to one of these values in `info`, `debug`, `trace` primary and backup OpsCenter logs all the heartbeat communication activities at the set level. (OPSC-17388)

# Release Notes for OpsCenter 6.8.33
15 Feb 2024

:warning: Customers using a separate storage cluster for metrics are advised to not use this release as OpsCenter will fail to start. Please use [version `6.8.34`](#release-notes-for-opscenter-6834) instead.

## Backup Service
* Improved handling encryption keys in collision, keys from system tables will be ignored during restore. (OPSC-17115)

## Core
* Added gossip configuration files to diagnostics tarball. (OPSC-17480)
* Added `alert_on_no_host_available` to the `[cassandra]` section of the cluster conf. When set to true an alert will be triggered if opscenterd is unable to make a cql connection to the monitored cluster. (OPSC-17398)
* Added `redirect_host` config value to the `[webserver]` section of `opscenterd.conf` to force the hostname used in redirects. (OPSC-17265)

## Monitoring
* Fixed issue in diagnostic tarball generation when `diagnostic_tarball_skip_instance_check` parameter is True. (OPSC-17471)
* Added the `Swap` value to the os-metrics memory.json file to identify if `Swap` is enabled from a diagnostics generated using OpsCenter. (OPSC-17405)
* Fixed metrics computation causing alerts to be triggered when values were close but below their threshold. (OPSC-17446)

## Repair Service
* Improved repair service to automatically ignore tables using the time window compaction strategy. (OPSC-17449)

# Release Notes for OpsCenter 6.8.32
11 Jan 2024

## Backup Service
* Resolved an error when opscenterd encounters an unexpected key when processing backup status reports from nodes. (OPSC-17423)
* Resolved various errors that occurred after a backup sync was deleted. (OPSC-17419)
* Backup clean up code will now run after a sync retry. (OPSC-17186)
* Fixed bugs when running a backup using `allow_one_failure` when one agent is down. (OPSC-17421)
* Added Commitlog backups cache refresh button in commitlogs dialog. (OPSC-17403)

## Core
* Publish failover and missing heartbeat after `heartbeat_reply_period` through event service.(OPSC-17212)

## UI
* Limit a session to a specific user agent and IP address (OPSC-17278)

# Release Notes for OpsCenter 6.8.31
29 Nov 2023

## Backup Service
* Fixed a regression introduced in 6.8.29 that caused an Azure StorageException leading backups to fail on Azure blob storage. This fix applies to all regions and also includes specific fixes for Azure’s China region where backup store configuration was never possible. (OPSC-17401)
* Allow users to manually truncate tables when sstableloader is not being used and show warning message for confirmation. (OPSC-17402)
* Fixed an issue where opscenterd would error when trying to list snapshot syncs that had been cleaned up or manually deleted. When this happened the ui would display an error when trying to view the backup history. (OPSC-17414)

# Release Notes for OpsCenter 6.8.30
9 Nov 2023

## Backup Service
* Fixed bugs when running a backup using `allow_one_failure` when one agent is down. (OPSC-17371)
* Commitlog staging files will now always overwrite commitlog storage files in case of conflict. (OPSC-17375)

## Monitoring
* Added `action_text` to values available in the email and post URL templates to provide a human readable version of the event action. (OPSC-17267)
* Resolved subsequent ssl request failures when using posturl for alert notifications. (OPSC-17379)

## UI
* Removed banner about opscenter 6.7.0 that appears at startup (OPSC-17386)
* Add security headers when redirecting to index.html (OPSC-17376)

## Core
* Fixed node status logic when a single node is brought online after all nodes are taken offline. (OPSC-17372)

# Release Notes for 6.8.29
9 Oct 2023

## Backup Service
* Added way to configure a new Azure endpoint for destinations in Azure (OPSC-17365)

## Monitoring
* Added solr and hints as options to alerts by partition function. (OPSC-17350)

## Core
* Upgrades `clj-ssh` to latest `0.6.2` version. (OPSC-17344)
* Updated version of jackson-databind. (OPSC-17312)
* Added an [agents] 'diagnostic_tarball_skip_instance_check' config option to allow opscenterd to skip the instance data look up when creating a diagnostic tarball as it can hang in some situations. (OPSC-17368)

# Release notes for 6.8.28
3 Aug 2023

## 6.8.28 OpsCenter Core

* Fixed bug in DataStax Agent service causing failure to start on older platforms such as Ubuntu 18.04 or RHEL 8 (OPSC-17357).


# Release notes for 6.8.27
27 Jul 2023

:warning: There's a known bug when starting DataStax Agent service in 
Ubuntu 18.04 (Bionic Beaver), and in RHEL/Oracle/Rocky Linux 8 platforms.
Later OS versions are not affected.
Customers in those platforms are recommended to upgrade to OpsCenter 6.8.28.

## 6.8.27 OpsCenter Core

* Fixed usage of RSA keys in platforms where `rsa-sha` algorithm have been deprecated. (OPSC-17300)
* Fixed `datastax-agent.pid` creation/removal when starting/stopping datastax-agent service. (OPSC-17013)
* Added the ability for disk based alerts to operate based on the function of a partition. This will make the alerts more useful in clusters where the disks for nodes are not named in a uniform manner. (OPSC-17277)
* Added additional [SAI Per Query and Table Query metrics](https://docs.datastax.com/en/cql/astra/docs/developing/indexing/sai/monitoring.html). (OPSC-17330)
* Normalized IPv6 addresses which in some configurations could cause a mismatch between DataStax Agent and OpsCenter leading to metric dashboards not being populated. (OPSC-17205)
* Fixed bug that caused the cleanup of commit logs on remote destinations to fail. (OPSC-17305)
* Fixed bug when reporting for missing pluggable authentication method. (OPSC-17314)

## 6.8.27 OpsCenter Life Cycle Manager
* Added `additional-jvm-opts` to the `cassandra-env.sh` definitions file for DSE 6.8 configurations. (OPSC-17331)

## 6.8.27 OpsCenter Platforms
* Updated OpsCenter Docker image to be based on a more modern Ubuntu 20.04 (Focal Fossa). (OPSC-17341)

## 6.8.27 OpsCenter CVE // https://nvd.nist.gov/vuln/detail/
* Upgraded Jackson libraries to latest version. (OPSC-17336, [CVE-2021-46877](https://nvd.nist.gov/vuln/detail/CVE-2021-46877))
* Upgraded Bouncy Castle libraries to latest `1.75` version. (OPSC-17342, [CVE-2023-33201](https://nvd.nist.gov/vuln/detail/CVE-2023-33201))
* Upgraded Golang compiler to `1.16.15` version. (OPSC-17343, [CVE-2018-16875](https://nvd.nist.gov/vuln/detail/CVE-2018-16875), [CVE-2021-33195](https://nvd.nist.gov/vuln/detail/CVE-2021-33195), [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772), [CVE-2019-11888](https://nvd.nist.gov/vuln/detail/CVE-2019-11888), [CVE-2021-38297](https://nvd.nist.gov/vuln/detail/CVE-2021-38297))
* Upgraded JNR POSIX library to latest 3.1.17 version. (OPSC-17345, [CWE-416](https://cwe.mitre.org/data/definitions/416.html))
* Upgraded `jetty-server` to `9.4.51.v20230217` version. (OPSC-17346, [CVE-2021-28165](https://nvd.nist.gov/vuln/detail/CVE-2021-28165), [CVE-2019-10247](https://nvd.nist.gov/vuln/detail/CVE-2019-10247), [CVE-2020-27218](https://nvd.nist.gov/vuln/detail/CVE-2020-27218), [CVE-2020-27223](https://nvd.nist.gov/vuln/detail/CVE-2020-27223), [CVE-2021-28169](https://nvd.nist.gov/vuln/detail/CVE-2021-28169), [CVE-2019-10241](https://nvd.nist.gov/vuln/detail/CVE-2019-10241), [CVE-2021-34428](https://nvd.nist.gov/vuln/detail/CVE-2021-34428))
* Upgraded `jackson-datatype-jsr310` library to latest `2.9` version. (OPSC-17347, [CVE-2018-1000873](https://nvd.nist.gov/vuln/detail/CVE-2018-1000873))
* Upgraded logback libraries to latest 1.2.12 version. (OPSC-17348, [CVE-2021-42550](https://nvd.nist.gov/vuln/detail/CVE-2021-42550))
* Upgraded Apache Commons IO to version `2.7`. (OPSC-17349, [CVE-2021-29425](https://nvd.nist.gov/vuln/detail/CVE-2021-29425), [CWE-20](https://cwe.mitre.org/data/definitions/20.html), [CWE-22](https://cwe.mitre.org/data/definitions/22.html))
* Upgraded `xerial/snappy-java` to version `1.1.10.1`. (OPSC-17337, [CVE-2023-34453](https://nvd.nist.gov/vuln/detail/CVE-2023-34453), [CVE-2023-34454](https://nvd.nist.gov/vuln/detail/CVE-2023-34454), [CVE-2023-34455](https://nvd.nist.gov/vuln/detail/CVE-2023-34455))
* Upgraded `org.xerial:sqlite-jdbc` to latest version. (OPSC-17338, [CVE-2023-32697](https://nvd.nist.gov/vuln/detail/CVE-2023-32697))
* Upgraded SnakeYAML library to latest `2.0` version. (OPSC-17339, [CVE-2022-41854](https://nvd.nist.gov/vuln/detail/CVE-2022-41854), [CVE-2022-38752](https://nvd.nist.gov/vuln/detail/CVE-2022-38752), [CVE-2022-38751](https://nvd.nist.gov/vuln/detail/CVE-2022-38751), [CVE-2022-38750](https://nvd.nist.gov/vuln/detail/CVE-2022-38750), [CVE-2022-38749](https://nvd.nist.gov/vuln/detail/CVE-2022-38749), [CVE-2022-25857](https://nvd.nist.gov/vuln/detail/CVE-2022-25857), [CVE-2022-1471](https://nvd.nist.gov/vuln/detail/CVE-2022-1471), [CVE-2017-18640](https://nvd.nist.gov/vuln/detail/CVE-2017-18640))
* Upgraded `me.raynes:fs` library that is not longer maintained by its maintained fork `clj-commons:fs`. (OPSC-17301, [CWE-29](https://cwe.mitre.org/data/definitions/29.html))


# Release notes for 6.8.26
18 Apr 2023

:warning: In Operating Systems using OpenSSH 8+, (e.g. Ubuntu 20.04 Focal Fossa or RHEL 8),
where `ssh-rsa` signature schemes have been deprecated, using RSA keys in LCM will report authentication
failures (even when keys are perfectly valid). For OpsCenter 6.8.26 this issue can be work around by using
ECDSA or ED25519 keys (OPSC-17286), or re-enabling the deprecated `ssh-rsa` signature scheme (not recommended).
Customers are recommended to upgrade to OpsCenter 6.8.27.

## 6.8.26 OpsCenter Core
* Removed unnecessary files from OpsCenter tarball which was causing download failures in some environments due to presence of windows executables. (OPSC-17247)
* Removed SysV scripts used to start/stop OpsCenter and DataStax Agent services. (OPSC-17291)
* Fixed datastax-agent .deb package installation in Ubuntu 22.04. (OPSC-17295)
  Note: with this change, DataStax Agent package installation will no longer modify `/etc/sudoers` file to include `/etc/sudoers.d`. In systems where this configuration does not exist, sudoers permissions will *not* be created for DataStax Agent. 
* Updated Bouncy Castle to 1.73 version. (OPSC-17296)
* Updated JSch library which supports newer EdDSA (Ed25519) and ECDSA (nistp256) ssh keys. (OPSC-17297)
* Fixed missing default value for `force_https_redirects` for package installations which could cause an authentication failure. (OPSC-17287)
* Fixed redirect issue when using Pluggable Authentication with IPv6 addresses. (OPSC-17288)

## 6.8.26 OpsCenter Backup Service
* Fixed an issue with stalled backups. If OpsCenter does not receive a status update from an agent within a given timeout, OpsCenter will query the agent directly to see if the backup is complete. The backup will be marked as complete or failed based on the agent's response. The timeout can be specified in seconds using `opscenterd.conf` `[backup_service] stomp_status_update_timeout`. The default timeout is 5 minutes. (OPSC-17196)

## 6.8.26 OpsCenter Monitoring
* Fixed an issue in the email plugin that caused dates with non-ascii characters to display incorrectly. (OPSC-17258)
* Added a `ascii_body` config option in `email.conf` to allow the email to be reverted to plain text if needed. (OPSC-17282)
* Added the ability to suspend event notifications. The ui for this can be found on the alert rules management dialog. (OPSC-17067)
* Best practice failure notifications now include the details that are displayed in the UI. (OPSC-17256)

## 6.8.26 OpsCenter Life Cycle Manager
* LCM will no longer automatically fail when encountering an unknown operating system. (OPSC-17215)

## 6.8.26 OpsCenter Platforms
* Added support for Red Hat Enterprise Linux (RHEL) 8, Oracle Linux 8, and Rocky Linux 8 versions. (OPSC-17110, OPSC-17270)
* Added support for Red Hat Enterprise Linux (RHEL) 9, Oracle Linux 9, and Rocky Linux 9 versions. 


# Release notes for OpsCenter 6.8.25
9 Mar 2023

## 6.8.25 OpsCenter Core
* Fixed startup issue when enabling SSL in IPv6 configurations. (OPSC-17269)
* Fixed authentication and failover redirects in IPv6 configurations. (OPSC-17273)
* Added sudoers permissions to start/stop datastax-agent from cassandra user without requesting for password. (OPSC-17268)


# Release notes for OpsCenter 6.8.24
13 Feb 2023

## 6.8.24 OpsCenter Core
* Fixed failure to connect to existing cluster when PostURL plugin was enabled. (OPSC-17262)
* Modified PostURL plugin to accept as http success code anything in the range of 200 - 299. (OPSC-16144)


# Release notes for OpsCenter 6.8.23
16 Jan 2023

:warning: There's a known bug when enabling `posturl` causing OpsCenter failure to load properly.
Users relying on this feature should upgrade to the `6.8.24` release which addresses this issue (OPSC-17262).

## 6.8.23 OpsCenter Core
* Added stomp-setup-timeout to the address.yaml config options with a default of 30 seconds.
  This resolves issues around initializing agent stomp connections.
  We recommend increasing this setting to 120 seconds for large clusters. (OPSC-17235)


# Release notes for OpsCenter 6.8.22
14 Dec 2022

:warning: There's a known bug when enabling `posturl` causing OpsCenter failure to load properly.
Users relying on this feature should upgrade to the `6.8.24` release which addresses this issue (OPSC-17262).

## 6.8.22 OpsCenter Core
* Added support for Ubuntu 22.04 (Jammy Jellyfish) package installation. (OPSC-17213)
* Updated `sqlite-jdbc` to version 3.40.0.0. (OPSC-17237, [CVE-2019-19242](https://nvd.nist.gov/vuln/detail/CVE-2019-19242))


# Release notes for OpsCenter 6.8.21
22 Nov 2022

:warning: There's a known bug when enabling `posturl` causing OpsCenter failure to load properly. 
Users relying on this feature should upgrade to the `6.8.24` release which addresses this issue (OPSC-17262).

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

## OpsCenter 6.8.9 Platforms
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

## OpsCenter 6.8.0 Backup Service
* OpsCenter now uses sha256 instead of md5 to generate a unique identifier for backup files stored on a remote destination. Because of this change the first backup after upgrading may take significantly longer and more disk space as all files will be uploaded rather than only the files since the last backup.  (OPSC-14381)

# Release notes for previous versions
Release notes for previous OpsCenter patch releases can be found here:
https://docs.datastax.com/en/opscenter/6.8/opsc/release_notes/opscReleaseNotes_g.html

---
