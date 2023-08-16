# Release notes for DataStax Luna Streaming Distribution

## About DataStax Luna Streaming Distribution

Luna Streaming Distribution 2.10 is compatible with Apache Pulsar&TRADE; 2.10.0
and subsequent releases.

### Components

- [DataStax Luna Streaming](https://github.com/datastax/pulsar) (Apache Pulsar
  2.10 fork)
- [DataStax BookKeeper](https://github.com/datastax/bookkeeper) (Apache
  BookKeeper fork)
- DataStax Burnell
- DataStax Pulsar Admin Console
- DataStax Pulsar Heartbeat
- DataStax Apache Pulsar Cassandra Sink
- DataStax Apache Pulsar Cassandra Source
- DataStax Starlight For Kafka
- DataStax Starlight For RabbitMQ
- DataStax Starlight For JMS Broker filter
- DataStax Snowflake connector

This release adds these features to the original Apache Pulsar 2.10 release:

- Stability improvements
- Third party libraries updates for security fixes
- Dependency upgrades (for security, stability and performances)
- An enhanced ElasticSearch Pulsar IO Sink
- An enhanced version of Apache BookKeeper with security fixes
- Apache ZooKeeper 3.8.0

*Note:* The DataStax Luna Streaming Distribution is designed for Java 11.
However, because the product releases Docker images, you do not need to install
Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

### Security

Luna Streaming is developed with great attention to security.

Since it is based on Apache Pulsar&TRADE;, Luna Streaming Pulsar distribution
has all the security processes and requirements required by the Apache Software
Foundation&TRADE;, such as:

- Peer to peer code reviews.
- Clear process for handling possible security vulnerabilities.

On top of that, Luna Streaming development processes are enhanced with
additional security best practices for all the components involved:

- Robust Continuous Integration and reproducible Release pipeline in a secure
  monitored environment. Such monitoring improves the overall security of the
  application.
- Reactivity to third-party vulnerabilities. Every component is scanned and
  monitored daily, ensuring quick fixes in case of vulnerability disclosure.
- Regular docker images vulnerability scans on latest Luna Streaming releases,
  with a well-defined release procedure.

At the time of the creation of the release, all the components included in the
*[all](#packaging)* packages are scanned by [Sonatype IQ Server
service](https://help.sonatype.com/iqserver) and they don't have any critical
(severity 8 or higher) security issues.

### Upgrade considerations for Luna Streaming Distribution 2.10

As with Luna Streaming 2.7, this release uses non-root containers for enhanced
security. When upgrading from a previous version (for example, 2.6.2_1.0.1),
files created while running that version will have root permissions and will not
be readable by containers running the new version.

To fix this, manually log into the ZooKeeper, BookKeeper, and Function Worker
containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs`
directories are owned by UID 10000 (user pulsar). The group ID of the files
should also be set to GID 10001 (group pulsar). Here is an example command:

    chown -R 10000:10001 /pulsar/data

If you are using the Luna Streaming Helm chart, you can enable automatic repair
of the permissions using the `fixRootlessPermissions` setting to solve this
problem. For more details on this setting, go
[here](https://github.com/datastax/pulsar-helm-chart).

If you are upgrading from Luna Streaming Distribution 2.8.0 or 2.8.3, you don't
have to do any particular action.

### Upgrade considerations for custom Pulsar Functions and Pulsar IO Connectors

If you are upgrading from Apache Pulsar 2.7.0 or Luna Streaming 2.7.2 you may
need to recompile your Pulsar Functions or Pulsar IO Connectors using Apache
Pulsar 2.8.0 as a dependency. This is because there is a breaking API change in
Apache Pulsar 2.8.0 (and therefore in Luna Streaming 2.8.0) related to the
`SchemaInfo` java class. More context
[here](https://github.com/apache/pulsar/issues/11338).

If you are upgrading from Luna Streaming Distribution 2.8.0 or 2.8.3, you don't
have to do any particular action.

### Packaging

Luna Streaming Distribution comes with different packages tooled for different
purposes. The distributions are available as Docker images and tarballs, and
both methods follow the same packaging patterns.

#### Patterns

- **lunastreaming**: the basic Luna Streaming Distribution **including Pulsar
  SQL** feature.
- **lunastreaming-core**: the basic Luna Streaming Distribution **without Pulsar
  SQL** feature. Pick this distribution if you don't need Pulsar SQL features.
- **lunastreaming-all**: contains the Core Luna Streaming Distribution,
  including **Pulsar Offloaders** and the **DataStax Pulsar IO Connectors**
  listed above. Pick this distribution if you want the DataStax connectors or
  the offloading feature.
- \[DEPRECATED\] **lunastreaming-experimental**: extends the **all**
  distribution with experimental features and connectors. This distribution is
  only available as a Docker image.

# Releases

## Luna Streaming Distribution 2.10 5.1
This release only contains plugins update.


### `lunastreaming-all` distribution
<details><summary>Sinks</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.5.1 | pulsar-io-data-generator-2.10.5.1.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.5.1 | pulsar-io-elastic-search-2.10.5.1.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.5.1 | pulsar-io-http-2.10.5.1.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.5.1 | pulsar-io-jdbc-clickhouse-2.10.5.1.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.5.1 | pulsar-io-jdbc-mariadb-2.10.5.1.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.5.1 | pulsar-io-jdbc-postgres-2.10.5.1.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.5.1 | pulsar-io-jdbc-sqlite-2.10.5.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.5.1 | pulsar-io-kafka-2.10.5.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.5.1 | pulsar-io-kinesis-2.10.5.1.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.5.1 | pulsar-io-data-generator-2.10.5.1.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.5.1 | pulsar-io-debezium-mongodb-2.10.5.1.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.5.1 | pulsar-io-debezium-mssql-2.10.5.1.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.5.1 | pulsar-io-debezium-mysql-2.10.5.1.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.5.1 | pulsar-io-debezium-oracle-2.10.5.1.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.5.1 | pulsar-io-debezium-postgres-2.10.5.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.5.1 | pulsar-io-kafka-2.10.5.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.5.1 | pulsar-io-kinesis-2.10.5.1.nar |
</details>
<details><summary>Proxy extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.10 | pulsar-kafka-proxy-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.10 | pulsar-protocol-handler-kafka-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>CLI extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>
<details><summary>Filters</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.1.7 | pulsar-ai-tools-3.1.7.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.1 | pulsar-transformations-3.1.1.nar |
</details>


## Luna Streaming Distribution 2.10 5.0
This is a maintenance release containing important stability and security updates.

### Most notable commits

* [8b4791a2fa4](https://github.com/datastax/pulsar/commit/8b4791a2fa4) [fix] [broker] Can not receive any messages after switch to standby cluster (#20767)
* [814702f5531](https://github.com/datastax/pulsar/commit/814702f5531) [improve] [broker] Add consumer-id into the log when doing subscribe. (#20568)
* [7a634b61737](https://github.com/datastax/pulsar/commit/7a634b61737) Fix breaking change of the deprecated constructor of PersistentMessageExpiryMonitor
* [1057fa1adcd](https://github.com/datastax/pulsar/commit/1057fa1adcd) [fix][broker][branch-2.10] Fix NPE when reset Replicator's cursor by position. (#20597) (#20781)
* [f6248d3f5cc](https://github.com/datastax/pulsar/commit/f6248d3f5cc) Revert "[fix][broker] Fix NPE when reset Replicator's cursor by position. (#20597)"
* [cedcbd7739d](https://github.com/datastax/pulsar/commit/cedcbd7739d) [fix][broker] Fix test and checkstyle
* [91db71037ea](https://github.com/datastax/pulsar/commit/91db71037ea) [fix] [client] Messages lost when consumer reconnect (#20695)
* [4d735f4e23c](https://github.com/datastax/pulsar/commit/4d735f4e23c) [fix][client] Make the whole grabCnx() progress atomic (#20595)
* [2f40424a61a](https://github.com/datastax/pulsar/commit/2f40424a61a) [fix][meta] Bookie Info lost by notification race condition. (#20642)
* [115105f6e33](https://github.com/datastax/pulsar/commit/115105f6e33) [fix][schema] Only handle exception when there has (#20730)
* [ffe393dd24f](https://github.com/datastax/pulsar/commit/ffe393dd24f) [fix][broker] Topic policy can not be work well if replay policy message has any exception. (#20613)
* [b8b576289ca](https://github.com/datastax/pulsar/commit/b8b576289ca) [fix][test] Fix the compilation issue introduced in #20597
* [0b03570e499](https://github.com/datastax/pulsar/commit/0b03570e499) [fix][broker] Fix NPE when reset Replicator's cursor by position. (#20597)
* [fa8bef95414](https://github.com/datastax/pulsar/commit/fa8bef95414) [fix][broker] Fix return the earliest position when query position by timestamp. (#20457)
* [42302aaf5b2](https://github.com/datastax/pulsar/commit/42302aaf5b2) [fix][offload] Filesystem offloader class not found hadoop-hdfs-client (#20365)
* [036dbf2a1e0](https://github.com/datastax/pulsar/commit/036dbf2a1e0) [improve][admin] Return BAD_REQUEST on cluster data is null for createCluster (#20346)
* [9a9b1355b1c](https://github.com/datastax/pulsar/commit/9a9b1355b1c) [fix] [meta]Switch to the metadata store thread after zk operation (#20303)
* [7e25ea96d75](https://github.com/datastax/pulsar/commit/7e25ea96d75) [fix][fn] Make KubernetesRuntime translate characters in function tenant, namespace, and name during function removal to avoid label errors (#19584)
* [ffc29c29743](https://github.com/datastax/pulsar/commit/ffc29c29743) [fix][fn] Fix JavaInstanceStarter inferring type class name error (#19896)
* [63ffd8d35cd](https://github.com/datastax/pulsar/commit/63ffd8d35cd) [fix] [txn] fix consumer can receive aborted txn message when readType is replay (#19815)
* [2a93e8c7b5a](https://github.com/datastax/pulsar/commit/2a93e8c7b5a) [broker] clean inactive bundle from bundleData in loadData and bundlesCache (#13974)
* [6e4863145f3](https://github.com/datastax/pulsar/commit/6e4863145f3) fix: bundle-data metadata leak because of bundlestats was not clean (#17095)
* [75f0d53545d](https://github.com/datastax/pulsar/commit/75f0d53545d) [fix] [Perf] PerformanceProducer do not produce expected number of messages. (#19775)
* [318a2e8b5bc](https://github.com/datastax/pulsar/commit/318a2e8b5bc) [improve][broker] Save createIfMissing in TopicLoadingContext (#19993)
* [ba7f03e5615](https://github.com/datastax/pulsar/commit/ba7f03e5615) [fix][broker] Invalidate metadata children cache after key deleted (#20363)
* [9f396883d03](https://github.com/datastax/pulsar/commit/9f396883d03) [improve] [broker] Avoid `PersistentSubscription.expireMessages` logic check backlog twice. (#20416)
* [f99a67ec623](https://github.com/datastax/pulsar/commit/f99a67ec623) [fix][meta] Adding the missed bookie id in the registration manager. (#20641)
* [fa43cf76f94](https://github.com/datastax/pulsar/commit/fa43cf76f94) [fix][io] Close the kafka source connector got stuck (#20698)
* [b94990a5259](https://github.com/datastax/pulsar/commit/b94990a5259) [fix][fn] Pulsar Function Kubernetes Runtime fails to start function that contains parenthesis in original jar filename (#20790)
* [cd3d0b7d2ab](https://github.com/datastax/pulsar/commit/cd3d0b7d2ab) [fix] Ignore openIDTokenIssuerTrustCertsFilePath conf when blank (#20745)
* [68b3d8fc9df](https://github.com/datastax/pulsar/commit/68b3d8fc9df) [fix][ws] Remove unnecessary ping/pong implementation  (#20733)


### `lunastreaming-all` distribution

<details><summary>Sinks</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.5.0 | pulsar-io-data-generator-2.10.5.0.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.5.0 | pulsar-io-elastic-search-2.10.5.0.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.5.0 | pulsar-io-http-2.10.5.0.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.5.0 | pulsar-io-jdbc-clickhouse-2.10.5.0.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.5.0 | pulsar-io-jdbc-mariadb-2.10.5.0.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.5.0 | pulsar-io-jdbc-postgres-2.10.5.0.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.5.0 | pulsar-io-jdbc-sqlite-2.10.5.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.5.0 | pulsar-io-kafka-2.10.5.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.5.0 | pulsar-io-kinesis-2.10.5.0.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.5.0 | pulsar-io-data-generator-2.10.5.0.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.5.0 | pulsar-io-debezium-mongodb-2.10.5.0.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.5.0 | pulsar-io-debezium-mssql-2.10.5.0.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.5.0 | pulsar-io-debezium-mysql-2.10.5.0.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.5.0 | pulsar-io-debezium-oracle-2.10.5.0.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.5.0 | pulsar-io-debezium-postgres-2.10.5.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.5.0 | pulsar-io-kafka-2.10.5.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.5.0 | pulsar-io-kinesis-2.10.5.0.nar |
</details>
<details><summary>Proxy extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.10 | pulsar-kafka-proxy-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.10 | pulsar-protocol-handler-kafka-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>CLI extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>
<details><summary>Filters</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.1.1 | pulsar-ai-tools-3.1.1.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.1 | pulsar-transformations-3.1.1.nar |
</details>



## Luna Streaming Distribution 2.10 4.9

This is a maintenance release containing important stability and security updates.

### Most notable commits
* [51585c285af](https://github.com/datastax/pulsar/commit/51585c285af) [fix][sec] Upgrade snappy-java to address multiple CVEs (#20604)
* [ae960408ed8](https://github.com/datastax/pulsar/commit/ae960408ed8) [fix][broker]fix the publish latency spike issue with large number of producers (#20607)
* [6ec35730e9e](https://github.com/datastax/pulsar/commit/6ec35730e9e) Optimize conusmer pause (#14566)
* [34401aaa92d](https://github.com/datastax/pulsar/commit/34401aaa92d) [fix][broker] Fix the publish latency spike from the contention of MessageDeduplication (#20647)
* [2cd0c501664](https://github.com/datastax/pulsar/commit/2cd0c501664) [fix][client]Fix deadlock issue of consumer while using multiple IO threads (#20669)
* [736d853979c](https://github.com/datastax/pulsar/commit/736d853979c) [fix][broker] release orphan replicator after topic closed (#20567)
* [3ca44af4f81](https://github.com/datastax/pulsar/commit/3ca44af4f81) [fix][broker] REST Client Producer fails with TLS only (#20535)
* [ec27d173f51](https://github.com/datastax/pulsar/commit/ec27d173f51) [fix][fn] Exit JVM when main thread throws exception (#20689)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.9 | pulsar-io-data-generator-2.10.4.9.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.9 | pulsar-io-elastic-search-2.10.4.9.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.9 | pulsar-io-http-2.10.4.9.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.9 | pulsar-io-jdbc-clickhouse-2.10.4.9.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.9 | pulsar-io-jdbc-mariadb-2.10.4.9.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.9 | pulsar-io-jdbc-postgres-2.10.4.9.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.9 | pulsar-io-jdbc-sqlite-2.10.4.9.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.9 | pulsar-io-kafka-2.10.4.9.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.9 | pulsar-io-kinesis-2.10.4.9.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.9 | pulsar-io-data-generator-2.10.4.9.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.9 | pulsar-io-debezium-mongodb-2.10.4.9.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.9 | pulsar-io-debezium-mssql-2.10.4.9.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.9 | pulsar-io-debezium-mysql-2.10.4.9.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.9 | pulsar-io-debezium-oracle-2.10.4.9.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.9 | pulsar-io-debezium-postgres-2.10.4.9.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.9 | pulsar-io-kafka-2.10.4.9.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.9 | pulsar-io-kinesis-2.10.4.9.nar |
</details>
<details><summary>Proxy extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.10 | pulsar-kafka-proxy-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.10 | pulsar-protocol-handler-kafka-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>CLI extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>
<details><summary>Filters</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | AI tools | 3.1.0 | pulsar-ai-tools-3.1.0.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.0 | pulsar-transformations-3.1.0.nar |
</details>



## Luna Streaming Distribution 2.10 4.8
This is a maintenance release containing important stability updates.

### Most notable commits

* [4cda264b397](https://github.com/datastax/pulsar/commit/4cda264b397) [cleanup][broker] Validate authz earlier in delete subscription logic (#20549)
* [10dae3b2177](https://github.com/datastax/pulsar/commit/10dae3b2177) [improve][broker] Backport Linux metrics changes from master branch to branch-2.10 (#188)


### `lunastreaming-all` distribution
<details><summary>Sinks</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.8 | pulsar-io-data-generator-2.10.4.8.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.8 | pulsar-io-elastic-search-2.10.4.8.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.8 | pulsar-io-http-2.10.4.8.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.8 | pulsar-io-jdbc-clickhouse-2.10.4.8.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.8 | pulsar-io-jdbc-mariadb-2.10.4.8.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.8 | pulsar-io-jdbc-postgres-2.10.4.8.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.8 | pulsar-io-jdbc-sqlite-2.10.4.8.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.8 | pulsar-io-kafka-2.10.4.8.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.8 | pulsar-io-kinesis-2.10.4.8.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.8 | pulsar-io-data-generator-2.10.4.8.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.8 | pulsar-io-debezium-mongodb-2.10.4.8.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.8 | pulsar-io-debezium-mssql-2.10.4.8.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.8 | pulsar-io-debezium-mysql-2.10.4.8.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.8 | pulsar-io-debezium-oracle-2.10.4.8.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.8 | pulsar-io-debezium-postgres-2.10.4.8.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.8 | pulsar-io-kafka-2.10.4.8.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.8 | pulsar-io-kinesis-2.10.4.8.nar |
</details>
<details><summary>Proxy extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.10 | pulsar-kafka-proxy-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.10 | pulsar-protocol-handler-kafka-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>CLI extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>
<details><summary>Filters</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | AI tools | 3.0.1 | pulsar-ai-tools-3.0.1.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.0.1 | pulsar-transformations-3.0.1.nar |
</details>

## Luna Streaming Distribution 2.10 4.7
This is a maintenance release containing important updates.

### Most notable commits

* [7db320b10c6](https://github.com/datastax/pulsar/commit/7db320b10c6) [fix][monitor] topic/subscription with slash breaks the prometheus format (#187)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.7 | pulsar-io-data-generator-2.10.4.7.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.7 | pulsar-io-elastic-search-2.10.4.7.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.7 | pulsar-io-http-2.10.4.7.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.7 | pulsar-io-jdbc-clickhouse-2.10.4.7.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.7 | pulsar-io-jdbc-mariadb-2.10.4.7.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.7 | pulsar-io-jdbc-postgres-2.10.4.7.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.7 | pulsar-io-jdbc-sqlite-2.10.4.7.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.7 | pulsar-io-kafka-2.10.4.7.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.7 | pulsar-io-kinesis-2.10.4.7.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.7 | pulsar-io-data-generator-2.10.4.7.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.7 | pulsar-io-debezium-mongodb-2.10.4.7.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.7 | pulsar-io-debezium-mssql-2.10.4.7.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.7 | pulsar-io-debezium-mysql-2.10.4.7.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.7 | pulsar-io-debezium-oracle-2.10.4.7.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.7 | pulsar-io-debezium-postgres-2.10.4.7.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.7 | pulsar-io-kafka-2.10.4.7.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.7 | pulsar-io-kinesis-2.10.4.7.nar |
</details>
<details><summary>Proxy extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.10 | pulsar-kafka-proxy-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.10 | pulsar-protocol-handler-kafka-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>CLI extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>
<details><summary>Filters</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.1.2 | pulsar-transformations-2.1.2.nar |
</details>


## Luna Streaming Distribution 2.10 4.6

This is a maintenance release containing important stability and security updates.

### Most notable commits

- [c370cfece99](https://github.com/datastax/pulsar/commit/c370cfece99)
  \[improve\]\[sink\]add metrics to elastic search sink
- [c8d7cc6cec6](https://github.com/datastax/pulsar/commit/c8d7cc6cec6)
  \[improve\]\[es-sink\] Add error log for failed bulk records in ES sink
  (#16177)
- [0c612c2f10f](https://github.com/datastax/pulsar/commit/0c612c2f10f)
  \[fix\]\[fn\] TLS args admin download command use zero arity (#20513)
- [a144970d843](https://github.com/datastax/pulsar/commit/a144970d843)
  \[fix\]\[fn\] Support customizing TLS config for function download command
  (#20482)
- [20ea481c2dc](https://github.com/datastax/pulsar/commit/20ea481c2dc)
  \[fix\]\[broker\] Restore solution for certain topic unloading race conditions
  (#20527)
- [6597e18da5d](https://github.com/datastax/pulsar/commit/6597e18da5d)
  \[fix\]\[ml\] There are two same-named managed ledgers in the one broker
  (#18688)
- [a2c33fe4f11](https://github.com/datastax/pulsar/commit/a2c33fe4f11)
  \[feat\]\[fn\] Add stateStorageURL and pulsarWebService URL to go
  InstanceConfig (#20443)
- [6b6b6f9a3ed](https://github.com/datastax/pulsar/commit/6b6b6f9a3ed)
  \[fix\]\[fn\] enable Go function token auth and TLS (#20468)
- [0c40723c121](https://github.com/datastax/pulsar/commit/0c40723c121) Fix
  license header with missing \*
- [fd67e96c759](https://github.com/datastax/pulsar/commit/fd67e96c759)
  \[fix\]\[fn\] Go functions must retrieve consumers by non-particioned topic ID
  (#20413)
- [039f9ccc3a6](https://github.com/datastax/pulsar/commit/039f9ccc3a6)
  \[fix\]\[broker\] Fix skip message API when hole messages exists (#20326)
- [a27da8dd5fa](https://github.com/datastax/pulsar/commit/a27da8dd5fa)
  \[fix\]\[sec\] Upgrade Guava to 32.0.0 to address CVE-2023-2976 (#20459)
- [c02ecfcb6d8](https://github.com/datastax/pulsar/commit/c02ecfcb6d8)
  \[fix\]\[client\] Cache empty schema version in ProducerImpl schemaCache.
  (#19929)
- [4f39556c26e](https://github.com/datastax/pulsar/commit/4f39556c26e)
  \[fix\]\[broker\] If ledger lost, cursor mark delete position can not forward
  (#18620)
- [db4a6958d94](https://github.com/datastax/pulsar/commit/db4a6958d94)
  \[improve\]\[monitor\] Add JVM start time metric (#20381)
- [ba1904bd423](https://github.com/datastax/pulsar/commit/ba1904bd423)
  \[fix\]\[ml\] Fix ledger left in OPEN state when enable
  `inactiveLedgerRollOverTimeMs` (#20276)
- [f6254d1068f](https://github.com/datastax/pulsar/commit/f6254d1068f)
  \[fix\]\[broker\] Fix default bundle size used while setting bookie affinity
  (#20250)
- [4cead08d57e](https://github.com/datastax/pulsar/commit/4cead08d57e)
  \[fix\]\[broker\] Fix the behavior of delayed message in Key_Shared mode
  (#20233)
- [917343dba74](https://github.com/datastax/pulsar/commit/917343dba74)
  \[improve\]\[broker\] Get lowest PositionImpl from NavigableSet (#18278)
- [a00e8af2c59](https://github.com/datastax/pulsar/commit/a00e8af2c59) \[fix\]
  \[broker\] error TimeUnit to record publish latency (#20074)
- [968838ce671](https://github.com/datastax/pulsar/commit/968838ce671)
  \[fix\]\[fn\] Go functions need to use static grpcPort in k8s runtime (#20404)
- [479ddfe1398](https://github.com/datastax/pulsar/commit/479ddfe1398)
  \[fix\]\[fn\]Reset idle timer correctly (#20450)
- [649586a0fdd](https://github.com/datastax/pulsar/commit/649586a0fdd)
  \[improve\]\[misc\] Upgrade Netty to 4.1.93.Final (#20423)
- [6ea70d3f821](https://github.com/datastax/pulsar/commit/6ea70d3f821) \[fix\]
  \[broker\] In Key_Shared mode: remove unnecessary mechanisms of message skip
  to avoid unnecessary consumption stuck (#20335)
- [75f380a59f2](https://github.com/datastax/pulsar/commit/75f380a59f2)
  \[fix\]\[sec\] Upgrade sqlite-jdbc to resolve CVE-2023-32697 (#20411)
- [444ce53c8d0](https://github.com/datastax/pulsar/commit/444ce53c8d0)
  \[fix\]\[ci\] Update nar maven plugin version to fix excessive downloads
  (#20410)
- [ce8008e8550](https://github.com/datastax/pulsar/commit/ce8008e8550)
  \[fix\]\[broker\] partitioned \_\_change_events topic is policy topic (#20392)
- [9dfe4bc3833](https://github.com/datastax/pulsar/commit/9dfe4bc3833)
  \[fix\]\[fn\] Make pulsar-admin support update py/go with package url (#19897)
- [df4ce260212](https://github.com/datastax/pulsar/commit/df4ce260212)
  \[fix\]\[broker\]Fix deadlock of metadata store (#20189)
- [189e18c85c3](https://github.com/datastax/pulsar/commit/189e18c85c3) \[feat\]
  OIDC: support JWKS refresh for missing Key ID (#20338)


### `lunastreaming-all` distribution

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.10 | cassandra-enhanced-pulsar-sink-1.6.10-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.6 | pulsar-io-data-generator-2.10.4.6.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.6 | pulsar-io-elastic-search-2.10.4.6.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.6 | pulsar-io-http-2.10.4.6.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.6 | pulsar-io-jdbc-clickhouse-2.10.4.6.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.6 | pulsar-io-jdbc-mariadb-2.10.4.6.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.6 | pulsar-io-jdbc-postgres-2.10.4.6.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.6 | pulsar-io-jdbc-sqlite-2.10.4.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.6 | pulsar-io-kafka-2.10.4.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.6 | pulsar-io-kinesis-2.10.4.6.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.6 | pulsar-io-data-generator-2.10.4.6.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.6 | pulsar-io-debezium-mongodb-2.10.4.6.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.6 | pulsar-io-debezium-mssql-2.10.4.6.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.6 | pulsar-io-debezium-mysql-2.10.4.6.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.6 | pulsar-io-debezium-oracle-2.10.4.6.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.6 | pulsar-io-debezium-postgres-2.10.4.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.6 | pulsar-io-kafka-2.10.4.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.6 | pulsar-io-kinesis-2.10.4.6.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.10 | pulsar-kafka-proxy-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.10 | pulsar-protocol-handler-kafka-2.10.3.10.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.1.2 | pulsar-transformations-2.1.2.nar |
</details>


## Luna Streaming Distribution 2.10 4.5

This is a maintenance release containing important stability and security
updates.

### Most notable commits

- [9c7f2191d60](https://github.com/datastax/pulsar/commit/9c7f2191d60)
  \[improve\] \[broker\] Skip split boundle if only one broker (#20190)
- [0e039e8b86a](https://github.com/datastax/pulsar/commit/0e039e8b86a) Exclude
  bouncy-castle from oidc module
- [ec41594509b](https://github.com/datastax/pulsar/commit/ec41594509b) \[fix\]
  \[broker\] \[branch-2.10\] Upgrade rocksDB version to 6.16.4 to keep sync with
  BookKeeper 4.14.7 (#20312)
- [95bc8ef242c](https://github.com/datastax/pulsar/commit/95bc8ef242c)
  \[fix\]\[monitor\] topic with double quote breaks the prometheus format
  (#20230)
- [e0065b56a8f](https://github.com/datastax/pulsar/commit/e0065b56a8f)
  \[fix\]\[broker\] Fix `RoaringBitmap.contains` can't check value 65535
  (#20176)
- [c00eaa676e6](https://github.com/datastax/pulsar/commit/c00eaa676e6)
  \[fix\]\[broker\] Fix the reason label of authentication metrics (#20030)
- [e1245b9b8c7](https://github.com/datastax/pulsar/commit/e1245b9b8c7)
  \[fix\]\[txn\] Fix transaction is not aborted when send or ACK failed (#20240)
- [9fefcbae513](https://github.com/datastax/pulsar/commit/9fefcbae513) \[fix\]
  \[broker\] Fix infinite ack of Replicator after topic is closed (#20232)
- [8de3ba40106](https://github.com/datastax/pulsar/commit/8de3ba40106)
  \[fix\]\[monitor\] Fix the partitioned publisher topic stat aggregation bug
  (#18807)
- [491bb42b195](https://github.com/datastax/pulsar/commit/491bb42b195)
  \[cleanup\]\[test\] fix incorrect license-header of java file
- [26f8cffe19d](https://github.com/datastax/pulsar/commit/26f8cffe19d) \[fix\]
  \[broker\] Producer created by replicator is not displayed in topic stats
  (#20229)
- [2b9e1c61470](https://github.com/datastax/pulsar/commit/2b9e1c61470)
  \[fix\]\[client\] Release the orphan producers after the primary consumer is
  closed (#19858)
- [af0bbb2fcf5](https://github.com/datastax/pulsar/commit/af0bbb2fcf5)
  \[fix\]\[client\] Fix ReconsumeLater will hang up if retryLetterProducer
  exception (#16655)
- [62681fb7234](https://github.com/datastax/pulsar/commit/62681fb7234) \[fix\]
  \[ml\] make the result of delete cursor is success if cursor is deleted
  (#19825)
- [c3aed87c418](https://github.com/datastax/pulsar/commit/c3aed87c418) \[fix\]
  \[broker\] Fast fix infinite HTTP call getSubscriptions caused by wrong
  topicName (#20131)
- [f9f535639fe](https://github.com/datastax/pulsar/commit/f9f535639fe)
  \[fix\]\[broker\] Fix issue where msgRateExpired may not refresh forever
  (#19759)
- [569d0b2c7aa](https://github.com/datastax/pulsar/commit/569d0b2c7aa)
  \[fix\]\[broker\] Fix can't send ErrorCommand when message is null value
  (#19899)
- [289a3f5d34f](https://github.com/datastax/pulsar/commit/289a3f5d34f)
  \[fix\]\[client\] Fix DeadLetterProducer creation callback blocking client io
  thread. (#19930)
- [50dbe98463f](https://github.com/datastax/pulsar/commit/50dbe98463f)
  \[fix\]\[broker\] Fix Return value of getPartitionedStats doesn't contain
  subscription type (#20210)
- [44258e004b6](https://github.com/datastax/pulsar/commit/44258e004b6)
  \[branch-2.10\]\[fix\]\[build\] Upgrade swagger version to fix CVE-2022-1471
  (#20172)
- [a6e213c332b](https://github.com/datastax/pulsar/commit/a6e213c332b)
  \[fix\]\[meta\] deadlock of zkSessionWatcher when zkConnection loss (#20122)
- [23443696ed8](https://github.com/datastax/pulsar/commit/23443696ed8)
  \[fix\]\[broker\] Fix getPartitionedStats miss subscription's messageAckRate
  (#19870)
- [e20944351a2](https://github.com/datastax/pulsar/commit/e20944351a2) \[fix\]
  Use scheduled executor in BinaryProtoLookupService (#20043)
- [8be2ab46e28](https://github.com/datastax/pulsar/commit/8be2ab46e28)
  \[branch-2.10\]\[improve\]\[build\] Upgrade snakeyaml version to 2.0 (#20118)
- [1a0e54b2a8d](https://github.com/datastax/pulsar/commit/1a0e54b2a8d)
  \[improve\] \[broker\] Fix broker restart logic (#20113)
- [0ab34c2eb65](https://github.com/datastax/pulsar/commit/0ab34c2eb65) \[fix\]
  \[cli\] Fix Broker crashed by too much memory usage of pulsar tools (#20031)
- [415017e5d64](https://github.com/datastax/pulsar/commit/415017e5d64)
  \[improve\]\[txn\] Cleanup how superusers abort txns (#19976)
- [327aae590ce](https://github.com/datastax/pulsar/commit/327aae590ce)
  \[fix\]\[broker\] Only validate superuser access if authz enabled (#19989)
- [77190cea10c](https://github.com/datastax/pulsar/commit/77190cea10c)
  \[fix\]\[broker\] Ignore and remove the replicator cursor when the remote
  cluster is absent (#19972)
- [a27f27e87d0](https://github.com/datastax/pulsar/commit/a27f27e87d0)
  \[branch-2.10\] \[fix\] \[auth\] fix not forward compatible config
  saslJaasServerRoleTokenSignerSecretPath after cherry-pick \#15121 (#19971)
- [081d5bfc9fd](https://github.com/datastax/pulsar/commit/081d5bfc9fd) \[Build\]
  Make the test JVM exit if OOME occurs (#14509)
- [fc3415c9a99](https://github.com/datastax/pulsar/commit/fc3415c9a99)
  \[branch-2.10\]\[fix\]\[broker\] Fix index generator is not rollback after
  entries are failed added (#19980)
- [71f062dfc00](https://github.com/datastax/pulsar/commit/71f062dfc00)
  \[fix\]\[ci\]\[branch-2.10\] Fix the release tools (#19711)
- [270582d455a](https://github.com/datastax/pulsar/commit/270582d455a)
  \[Authenticate\] fix Invalid signature error when use Kerberos Authentication
  (#15121)
- [afcbed303a0](https://github.com/datastax/pulsar/commit/afcbed303a0)
  \[improve\]\[misc\] Upgrade Netty to 4.1.89.Final (#19649)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.10 | cassandra-enhanced-pulsar-sink-1.6.10-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.5 | pulsar-io-data-generator-2.10.4.5.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.5 | pulsar-io-elastic-search-2.10.4.5.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.5 | pulsar-io-http-2.10.4.5.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.5 | pulsar-io-jdbc-clickhouse-2.10.4.5.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.5 | pulsar-io-jdbc-mariadb-2.10.4.5.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.5 | pulsar-io-jdbc-postgres-2.10.4.5.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.5 | pulsar-io-jdbc-sqlite-2.10.4.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.5 | pulsar-io-kafka-2.10.4.5.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.5 | pulsar-io-kinesis-2.10.4.5.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.5 | pulsar-io-data-generator-2.10.4.5.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.5 | pulsar-io-debezium-mongodb-2.10.4.5.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.5 | pulsar-io-debezium-mssql-2.10.4.5.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.5 | pulsar-io-debezium-mysql-2.10.4.5.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.5 | pulsar-io-debezium-oracle-2.10.4.5.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.5 | pulsar-io-debezium-postgres-2.10.4.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.5 | pulsar-io-kafka-2.10.4.5.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.5 | pulsar-io-kinesis-2.10.4.5.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.9 | pulsar-kafka-proxy-2.10.3.9.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.9 | pulsar-protocol-handler-kafka-2.10.3.9.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.1.2 | pulsar-transformations-2.1.2.nar |
</details>


## Luna Streaming Distribution 2.10 4.4

This is a maintenance release containing important updates.

### Most notable commits

- [02d6c16230c](https://github.com/datastax/pulsar/commit/02d6c16230c)
  \[feat\]\[ws\] Use async auth method to support OIDC (#20238)
- [e2e2c4ac097](https://github.com/datastax/pulsar/commit/e2e2c4ac097)
  \[improve\]\[io\] Add ElasticSearch Sink bulk debug logs (#179)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.10 | cassandra-enhanced-pulsar-sink-1.6.10-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.4 | pulsar-io-data-generator-2.10.4.4.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.4 | pulsar-io-elastic-search-2.10.4.4.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.4 | pulsar-io-http-2.10.4.4.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.4 | pulsar-io-jdbc-clickhouse-2.10.4.4.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.4 | pulsar-io-jdbc-mariadb-2.10.4.4.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.4 | pulsar-io-jdbc-postgres-2.10.4.4.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.4 | pulsar-io-jdbc-sqlite-2.10.4.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.4 | pulsar-io-kafka-2.10.4.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.4 | pulsar-io-kinesis-2.10.4.4.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13-alpha.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.7 | pulsar-cassandra-source-2.2.7.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.4 | pulsar-io-data-generator-2.10.4.4.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.4 | pulsar-io-debezium-mongodb-2.10.4.4.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.4 | pulsar-io-debezium-mssql-2.10.4.4.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.4 | pulsar-io-debezium-mysql-2.10.4.4.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.4 | pulsar-io-debezium-oracle-2.10.4.4.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.4 | pulsar-io-debezium-postgres-2.10.4.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.4 | pulsar-io-kafka-2.10.4.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.4 | pulsar-io-kinesis-2.10.4.4.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.8 | pulsar-kafka-proxy-2.10.3.8.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.8 | pulsar-protocol-handler-kafka-2.10.3.8.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.1.2 | pulsar-transformations-2.1.2.nar |
</details>


## Luna Streaming Distribution 2.10 4.3

This is a maintenance release containing important stability updates.

### Most notable commits

- [175cf7afc48](https://github.com/datastax/pulsar/commit/175cf7afc48)
  \[improve\]\[fn\] Allow unknown fields in connectors config (#20116)
- [6b07892eda7](https://github.com/datastax/pulsar/commit/6b07892eda7)
  \[fix\]\[authentication\] Store the original authentication data (#19519)
- [5c7ec68ab31](https://github.com/datastax/pulsar/commit/5c7ec68ab31)
  \[fix\]\[broker\] Add missing catches for AssertionError
- [8eb96c8f324](https://github.com/datastax/pulsar/commit/8eb96c8f324)
  \[fix\]\[fn\] Supply download auth params when provided for k8s runtime
  (#20144)
- [9f841a83628](https://github.com/datastax/pulsar/commit/9f841a83628)
  \[improve\] AuthenticationProviderOpenID k8s error logs (#20135)
- [fb2c96a1ed3](https://github.com/datastax/pulsar/commit/fb2c96a1ed3)
  \[fix\]\[broker\] Implement authenticateAsync for AuthenticationProviderList
  (#20132)
- [139209a9ab3](https://github.com/datastax/pulsar/commit/139209a9ab3)
  \[fix\]\[proxy\] Refresh auth data if ProxyLookupRequests (#20067)
- [6332aa4ddf0](https://github.com/datastax/pulsar/commit/6332aa4ddf0)
  \[improve\]\[proxy\] Only create ConnectionPool when needed (#20062)
- [f8370926504](https://github.com/datastax/pulsar/commit/f8370926504) \[feat\]
  PIP-257: Add AuthenticationProviderOpenID (#19849)
- [c2a93ec2181](https://github.com/datastax/pulsar/commit/c2a93ec2181)
  \[feat\]\[fn\] PIP-257: Support mounting k8s ServiceAccount for OIDC auth
  (#19888)
- [a1450f8c1d2](https://github.com/datastax/pulsar/commit/a1450f8c1d2)
  \[feat\]\[broker\] PIP 97: Implement for ServerCnx (#19409)
- [b5b252bc6b8](https://github.com/datastax/pulsar/commit/b5b252bc6b8)
  \[feat\]\[proxy\] PIP 97: Implement for ProxyConnection (#19292)
- [3d2839d4a3c](https://github.com/datastax/pulsar/commit/3d2839d4a3c)
  \[fix\]\[broker\] TokenAuthenticationState: authenticate token only once
  (#19314)
- [d7d38d7ab1d](https://github.com/datastax/pulsar/commit/d7d38d7ab1d)
  \[improve\]\[broker\] ServerCnx: go to Failed state when auth fails (#19312)
- [a347f7fe441](https://github.com/datastax/pulsar/commit/a347f7fe441)
  \[improve\]\[broker\] Replace authenticate with authenticateAsync (#19313)
- [82fe8a957c5](https://github.com/datastax/pulsar/commit/82fe8a957c5)
  \[feat\]\[broker\] OneStageAuth State: move authn out of constructor (#19295)
- [6b0a78e8657](https://github.com/datastax/pulsar/commit/6b0a78e8657)
  \[fix\]\[broker\] Let TokenAuthState update authenticationDataSource (#19282)
- [5e99e8add97](https://github.com/datastax/pulsar/commit/5e99e8add97)
  \[improve\]\[broker\] Documentation for AuthenticationState contract (#19283)
- [7b7ee933d45](https://github.com/datastax/pulsar/commit/7b7ee933d45)
  \[cleanup\]\[proxy\] Remove unused AuthenticationDataSource variable (#19278)
- [9645bc48442](https://github.com/datastax/pulsar/commit/9645bc48442)
  \[feat\]\[broker\] Update AuthenticationProvider to simplify HTTP Authn
  (#19197)
- [cf0f459952c](https://github.com/datastax/pulsar/commit/cf0f459952c)
  \[improve\]\[broker\] Unreasonable AuthenticationException reference (#18502)
- [f4c2d9dd292](https://github.com/datastax/pulsar/commit/f4c2d9dd292)
  \[fix\]\[broker\] Fix token expiration (#16016)
- [7e87e9dba0c](https://github.com/datastax/pulsar/commit/7e87e9dba0c)
  \[broker\]\[authentication\]Support pass http auth status (#14044)
- [1502a7db17a](https://github.com/datastax/pulsar/commit/1502a7db17a) \[PIP
  97\] Update Authentication Interfaces to Include Async Authentication Methods
  (#12104)
- [b47d8c63e1c](https://github.com/datastax/pulsar/commit/b47d8c63e1c)
  \[fix\]\[io\] KCA: handle kafka sources that use commitRecord (#176 )

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.9 | cassandra-enhanced-pulsar-sink-1.6.9-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.3 | pulsar-io-data-generator-2.10.4.3.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.4.3 | pulsar-io-elastic-search-2.10.4.3.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 2.10.4.3 | pulsar-io-http-2.10.4.3.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.4.3 | pulsar-io-jdbc-clickhouse-2.10.4.3.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.4.3 | pulsar-io-jdbc-mariadb-2.10.4.3.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.4.3 | pulsar-io-jdbc-postgres-2.10.4.3.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.4.3 | pulsar-io-jdbc-sqlite-2.10.4.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.3 | pulsar-io-kafka-2.10.4.3.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.3 | pulsar-io-kinesis-2.10.4.3.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13-alpha.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.5 | pulsar-cassandra-source-2.2.5.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.4.3 | pulsar-io-data-generator-2.10.4.3.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.4.3 | pulsar-io-debezium-mongodb-2.10.4.3.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.4.3 | pulsar-io-debezium-mssql-2.10.4.3.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.4.3 | pulsar-io-debezium-mysql-2.10.4.3.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.4.3 | pulsar-io-debezium-oracle-2.10.4.3.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.4.3 | pulsar-io-debezium-postgres-2.10.4.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.4.3 | pulsar-io-kafka-2.10.4.3.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.4.3 | pulsar-io-kinesis-2.10.4.3.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.3.7 | pulsar-kafka-proxy-2.10.3.7.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.3.7 | pulsar-protocol-handler-kafka-2.10.3.7.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.2.5 | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0 | pulsar-jms-admin-3.1.0-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0 | pulsar-jms-3.1.0-nar.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.1.2 | pulsar-transformations-2.1.2.nar |
</details>


## Luna Streaming Distribution 2.10 4.2

This is a maintenance release containing important stability updates.

### Most notable commits

- [167ff8b84ef](https://github.com/datastax/pulsar/commit/167ff8b84ef)
  \[improve\]\[broker\] Prevent range conflicts with Key Shared sticky consumers
  when TCP/IP connections get orphaned (#174)
- [ecbcb812d13](https://github.com/datastax/pulsar/commit/ecbcb812d13) Revert
  "\[test\] Fix ServerCnxTest failing after merge of \#19830"
- [51add4bae52](https://github.com/datastax/pulsar/commit/51add4bae52)
  \[improve\]\[broker\] Test AuthorizationService to cover proxyRoles behavior
  (#19845)
- [a9b193bf700](https://github.com/datastax/pulsar/commit/a9b193bf700) Revert
  "\[improve\]\[broker\] Authorize originalPrincipal when provided (#19830)"
- [f8ee97d3b71](https://github.com/datastax/pulsar/commit/f8ee97d3b71)
  \[improve\]\[pulsar-shell\] Use singleton custom command factories (#20064)
- [ef8dad02e9c](https://github.com/datastax/pulsar/commit/ef8dad02e9c)
  \[refactor\]\[broker\] Use AuthenticationParameters for rest producer (#20046)
- [bb044be51b7](https://github.com/datastax/pulsar/commit/bb044be51b7)
  \[refactor\]\[fn\] Use AuthorizationServer more in Function Worker API
  (#19975)
- [b94d560bd1b](https://github.com/datastax/pulsar/commit/b94d560bd1b)
  \[improve\]\[proxy\] Implement graceful shutdown for Pulsar Proxy (#20011)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.9 \|
cassandra-enhanced-pulsar-sink-1.6.9-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.0 \| pulsar-io-cloud-storage-2.10.0.nar
\| \| [data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
data generator source \| 2.10.4.2 \| pulsar-io-data-generator-2.10.4.2.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.4.2 \| pulsar-io-elastic-search-2.10.4.2.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.4.2 \| pulsar-io-http-2.10.4.2.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.4.2 \| pulsar-io-jdbc-clickhouse-2.10.4.2.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.4.2 \| pulsar-io-jdbc-mariadb-2.10.4.2.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.4.2 \| pulsar-io-jdbc-postgres-2.10.4.2.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.4.2 \| pulsar-io-jdbc-sqlite-2.10.4.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.2 \| pulsar-io-kafka-2.10.4.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.2 \| pulsar-io-kinesis-2.10.4.2.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.5 \| pulsar-cassandra-source-2.2.5.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.2 \| pulsar-io-data-generator-2.10.4.2.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.4.2 \| pulsar-io-debezium-mongodb-2.10.4.2.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.4.2 \| pulsar-io-debezium-mssql-2.10.4.2.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.4.2 \| pulsar-io-debezium-mysql-2.10.4.2.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.4.2 \| pulsar-io-debezium-oracle-2.10.4.2.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.4.2 \| pulsar-io-debezium-postgres-2.10.4.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.2 \| pulsar-io-kafka-2.10.4.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.2 \| pulsar-io-kinesis-2.10.4.2.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.6 \| pulsar-kafka-proxy-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.6 \| pulsar-protocol-handler-kafka-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) \|
Cassandra CDC - Pulsar Admin Custom Commands \| 2.2.5 \|
pulsar-cassandra-admin-2.2.5-nar.nar \| \|
[jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.9 \|
cassandra-enhanced-pulsar-sink-1.6.9-nar.nar \| \|
[camel-aws-s3-source](https://github.com/datastax/pulsar-3rdparty-connector) \|
camel-aws-s3-source Connector \| 2.10.1.5 \|
pulsar-3rdparty-camel-aws-s3-source-2.10.1.5.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.6 \|
pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.6-alpha2.nar \| \|
[coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \| \|
[couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \| Couchbase
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.4.2 \| pulsar-io-aerospike-2.10.4.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.4.2 \|
pulsar-io-batch-data-generator-2.10.4.2.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.0 \| pulsar-io-cloud-storage-2.10.0.nar
\| \| [data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
data generator source \| 2.10.4.2 \| pulsar-io-data-generator-2.10.4.2.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.4.2 \| pulsar-io-elastic-search-2.10.4.2.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.4.2 \| pulsar-io-flume-2.10.4.2.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.4.2 \| pulsar-io-hbase-2.10.4.2.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.4.2 \| pulsar-io-hdfs2-2.10.4.2.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.4.2 \| pulsar-io-hdfs3-2.10.4.2.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.4.2 \| pulsar-io-http-2.10.4.2.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.4.2 \| pulsar-io-influxdb-2.10.4.2.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.4.2 \| pulsar-io-jdbc-clickhouse-2.10.4.2.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.4.2 \| pulsar-io-jdbc-mariadb-2.10.4.2.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.4.2 \| pulsar-io-jdbc-postgres-2.10.4.2.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.4.2 \| pulsar-io-jdbc-sqlite-2.10.4.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.2 \| pulsar-io-kafka-2.10.4.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.2 \| pulsar-io-kinesis-2.10.4.2.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.4.2 \| pulsar-io-mongo-2.10.4.2.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.4.2 \| pulsar-io-rabbitmq-2.10.4.2.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.4.2 \| pulsar-io-redis-2.10.4.2.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.4.2 \| pulsar-io-solr-2.10.4.2.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[camel-aws-s3-source](https://github.com/datastax/pulsar-3rdparty-connector) \|
camel-aws-s3-source Connector \| 2.10.1.5 \|
pulsar-3rdparty-camel-aws-s3-source-2.10.1.5.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.6 \|
pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.6-alpha2.nar \| \|
[coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \| \|
[couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \| Couchbase
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.5 \| pulsar-cassandra-source-2.2.5.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.4.2 \|
pulsar-io-batch-data-generator-2.10.4.2.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.4.2 \| pulsar-io-canal-2.10.4.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.2 \| pulsar-io-data-generator-2.10.4.2.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.4.2 \| pulsar-io-debezium-mongodb-2.10.4.2.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.4.2 \| pulsar-io-debezium-mssql-2.10.4.2.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.4.2 \| pulsar-io-debezium-mysql-2.10.4.2.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.4.2 \| pulsar-io-debezium-oracle-2.10.4.2.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.4.2 \| pulsar-io-debezium-postgres-2.10.4.2.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.4.2 \| pulsar-io-dynamodb-2.10.4.2.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.4.2 \| pulsar-io-file-2.10.4.2.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.4.2 \| pulsar-io-flume-2.10.4.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.2 \| pulsar-io-kafka-2.10.4.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.2 \| pulsar-io-kinesis-2.10.4.2.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.4.2 \| pulsar-io-mongo-2.10.4.2.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.4.2 \| pulsar-io-netty-2.10.4.2.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.4.2 \| pulsar-io-nsq-2.10.4.2.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.4.2 \| pulsar-io-rabbitmq-2.10.4.2.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.4.2 \| pulsar-io-twitter-2.10.4.2.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.6 \| pulsar-kafka-proxy-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.6 \| pulsar-protocol-handler-kafka-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) \|
Cassandra CDC - Pulsar Admin Custom Commands \| 2.2.5 \|
pulsar-cassandra-admin-2.2.5-nar.nar \| \|
[jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


## Luna Streaming Distribution 2.10 4.1

This is a maintenance release containing important stability and security
updates.

### Most notable commits

- [19c6d68b71b](https://github.com/datastax/pulsar/commit/19c6d68b71b)
  \[fix\]\[sec\] Fix transitive critical CVEs in file-system tiered storage
  (#19957)
- [f41b3776c08](https://github.com/datastax/pulsar/commit/f41b3776c08)
  \[improve\]\[io\] KCA: flag to force optional primitive schemas (#19951)
- [867a763c79c](https://github.com/datastax/pulsar/commit/867a763c79c)
  \[improve\]\[io\] KCA: option to collapse partitioned topics (#19923)
- [be7c237abb2](https://github.com/datastax/pulsar/commit/be7c237abb2) \[fix\]
  \[admin\] fix incorrect state replication.connected on API partitioned-topic
  stat (#19942)
- [d68a99816b2](https://github.com/datastax/pulsar/commit/d68a99816b2) \[fix\]
  \[proxy\] Used in proxyConf file when configuration is missing in the command
  line (#15938)
- [42584f7afb1](https://github.com/datastax/pulsar/commit/42584f7afb1) \[fix\]
  \[broker\] Counter of pending send messages in Replicator incorrect if schema
  future not complete (#19242)
- [a52202346fd](https://github.com/datastax/pulsar/commit/a52202346fd) \[fix\]
  \[admin\] Make response code to 400 instead of 500 when delete topic fails due
  to enabled geo-replication (#19879)
- [6a9a22c9b3a](https://github.com/datastax/pulsar/commit/6a9a22c9b3a) \[test\]
  Fix ServerCnxTest failing after merge of \#19830
- [0c365e206f4](https://github.com/datastax/pulsar/commit/0c365e206f4)
  \[improve\]\[broker\] Authorize originalPrincipal when provided (#19830)
- [a56c9e45fb8](https://github.com/datastax/pulsar/commit/a56c9e45fb8)
  \[fix\]\[broker\] Fix potential exception cause the policy service init fail.
  (#19746)
- [a7e4837c473](https://github.com/datastax/pulsar/commit/a7e4837c473)
  \[fix\]\[client\]\[branch-2.10\]Return local thread for the `newThread`
  (#19779)
- [0104c0d26b6](https://github.com/datastax/pulsar/commit/0104c0d26b6)
  \[fix\]\[io\] KCA sink: handle null values with KeyValue\<Avro,Avro\> schema
  (#19861) (#169)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.9 \|
cassandra-enhanced-pulsar-sink-1.6.9-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.0 \| pulsar-io-cloud-storage-2.10.0.nar
\| \| [data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
data generator source \| 2.10.4.1 \| pulsar-io-data-generator-2.10.4.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.4.1 \| pulsar-io-elastic-search-2.10.4.1.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.4.1 \| pulsar-io-http-2.10.4.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.4.1 \| pulsar-io-jdbc-clickhouse-2.10.4.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.4.1 \| pulsar-io-jdbc-mariadb-2.10.4.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.4.1 \| pulsar-io-jdbc-postgres-2.10.4.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.4.1 \| pulsar-io-jdbc-sqlite-2.10.4.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.1 \| pulsar-io-kafka-2.10.4.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.1 \| pulsar-io-kinesis-2.10.4.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.4 \| pulsar-cassandra-source-2.2.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.1 \| pulsar-io-data-generator-2.10.4.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.4.1 \| pulsar-io-debezium-mongodb-2.10.4.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.4.1 \| pulsar-io-debezium-mssql-2.10.4.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.4.1 \| pulsar-io-debezium-mysql-2.10.4.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.4.1 \| pulsar-io-debezium-oracle-2.10.4.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.4.1 \| pulsar-io-debezium-postgres-2.10.4.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.1 \| pulsar-io-kafka-2.10.4.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.1 \| pulsar-io-kinesis-2.10.4.1.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.6 \| pulsar-kafka-proxy-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.6 \| pulsar-protocol-handler-kafka-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) \|
Cassandra CDC - Pulsar Admin Custom Commands \| 2.2.4 \|
pulsar-cassandra-admin-2.2.4-nar.nar \| \|
[jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.9 \|
cassandra-enhanced-pulsar-sink-1.6.9-nar.nar \| \|
[camel-aws-s3-source](https://github.com/datastax/pulsar-3rdparty-connector) \|
camel-aws-s3-source Connector \| 2.10.1.5 \|
pulsar-3rdparty-camel-aws-s3-source-2.10.1.5.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.6 \|
pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.6-alpha2.nar \| \|
[coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \| \|
[couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \| Couchbase
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.4.1 \| pulsar-io-aerospike-2.10.4.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.4.1 \|
pulsar-io-batch-data-generator-2.10.4.1.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.0 \| pulsar-io-cloud-storage-2.10.0.nar
\| \| [data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
data generator source \| 2.10.4.1 \| pulsar-io-data-generator-2.10.4.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.4.1 \| pulsar-io-elastic-search-2.10.4.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.4.1 \| pulsar-io-flume-2.10.4.1.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.4.1 \| pulsar-io-hbase-2.10.4.1.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.4.1 \| pulsar-io-hdfs2-2.10.4.1.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.4.1 \| pulsar-io-hdfs3-2.10.4.1.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.4.1 \| pulsar-io-http-2.10.4.1.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.4.1 \| pulsar-io-influxdb-2.10.4.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.4.1 \| pulsar-io-jdbc-clickhouse-2.10.4.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.4.1 \| pulsar-io-jdbc-mariadb-2.10.4.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.4.1 \| pulsar-io-jdbc-postgres-2.10.4.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.4.1 \| pulsar-io-jdbc-sqlite-2.10.4.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.1 \| pulsar-io-kafka-2.10.4.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.1 \| pulsar-io-kinesis-2.10.4.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.4.1 \| pulsar-io-mongo-2.10.4.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.4.1 \| pulsar-io-rabbitmq-2.10.4.1.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.4.1 \| pulsar-io-redis-2.10.4.1.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.4.1 \| pulsar-io-solr-2.10.4.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[camel-aws-s3-source](https://github.com/datastax/pulsar-3rdparty-connector) \|
camel-aws-s3-source Connector \| 2.10.1.5 \|
pulsar-3rdparty-camel-aws-s3-source-2.10.1.5.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.6 \|
pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.6-alpha2.nar \| \|
[coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \| \|
[couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \| Couchbase
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.4 \| pulsar-cassandra-source-2.2.4.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.4.1 \|
pulsar-io-batch-data-generator-2.10.4.1.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.4.1 \| pulsar-io-canal-2.10.4.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.1 \| pulsar-io-data-generator-2.10.4.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.4.1 \| pulsar-io-debezium-mongodb-2.10.4.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.4.1 \| pulsar-io-debezium-mssql-2.10.4.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.4.1 \| pulsar-io-debezium-mysql-2.10.4.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.4.1 \| pulsar-io-debezium-oracle-2.10.4.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.4.1 \| pulsar-io-debezium-postgres-2.10.4.1.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.4.1 \| pulsar-io-dynamodb-2.10.4.1.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.4.1 \| pulsar-io-file-2.10.4.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.4.1 \| pulsar-io-flume-2.10.4.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.1 \| pulsar-io-kafka-2.10.4.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.1 \| pulsar-io-kinesis-2.10.4.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.4.1 \| pulsar-io-mongo-2.10.4.1.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.4.1 \| pulsar-io-netty-2.10.4.1.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.4.1 \| pulsar-io-nsq-2.10.4.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.4.1 \| pulsar-io-rabbitmq-2.10.4.1.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.4.1 \| pulsar-io-twitter-2.10.4.1.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.6 \| pulsar-kafka-proxy-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.6 \| pulsar-protocol-handler-kafka-2.10.3.6.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) \|
Cassandra CDC - Pulsar Admin Custom Commands \| 2.2.4 \|
pulsar-cassandra-admin-2.2.4-nar.nar \| \|
[jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


## Luna Streaming Distribution 2.10 4.0

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [eacedf95f9c](https://github.com/datastax/pulsar/commit/eacedf95f9c) Upgrade
  BookKeeper to 4.14.7.1.0.1
- [7a5079a5978](https://github.com/datastax/pulsar/commit/7a5079a5978)
  \[cherry-pick\]\[branch-2.10\] KCA: picking fixes from master (#19788)
- [27800ffbd32](https://github.com/datastax/pulsar/commit/27800ffbd32)
  \[fix\]\[sec\] Upgrade kafka client to 3.4.0 to fix CVE-2023-25194 (#19527)
- [e707c493c80](https://github.com/datastax/pulsar/commit/e707c493c80) Upgrade
  DataStax BookKeeper to 4.14.7.1.0.0
- [335ab8abd57](https://github.com/datastax/pulsar/commit/335ab8abd57)
  \[improve\]\[offloaders\] Automatically evict Offloaded Ledgers from memory
  (#168)
- [b7a6883b532](https://github.com/datastax/pulsar/commit/b7a6883b532)
  \[fix\]\[broker\] Fix LedgerOffloaderStatsImpl singleton close method (#19666)
- [142f2d84e3b](https://github.com/datastax/pulsar/commit/142f2d84e3b)
  \[cherry-pick\]\[branch-2.10\] Fix deadlock causes session notification not to
  work (#19754) (#19768)
- [bbfaa1e9971](https://github.com/datastax/pulsar/commit/bbfaa1e9971)
  \[fix\]\[io\] KCA: 'desanitize' topic name for the pulsar's ctx calls (#19756)
- [c8e1d1a395c](https://github.com/datastax/pulsar/commit/c8e1d1a395c) \[fix\]
  \[broker\] Topic close failure leaves subscription in a permanent fence state
  (#19692)
- [e57ef2a9849](https://github.com/datastax/pulsar/commit/e57ef2a9849) \[fix\]
  \[client\] fix memory leak if enabled pooled messages (#19585)
- [d2066636a83](https://github.com/datastax/pulsar/commit/d2066636a83)
  \[improve\] Simplify enabling Broker, WS Proxy hostname verification (#19674)
- [872094ffe65](https://github.com/datastax/pulsar/commit/872094ffe65)
  \[branch-2.10\]\[broker\] Support zookeeper read-only config. (#19156)
  (#19637)
- [3ffd5197fc3](https://github.com/datastax/pulsar/commit/3ffd5197fc3) \[fix\]
  \[ml\] topic load fail by ledger lost (#19444)

### `lunastreaming-all` distribution

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.8 \|
cassandra-enhanced-pulsar-sink-1.6.8-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.0 \| pulsar-io-data-generator-2.10.4.0.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.4.0 \| pulsar-io-elastic-search-2.10.4.0.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.4.0 \| pulsar-io-http-2.10.4.0.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.4.0 \| pulsar-io-jdbc-clickhouse-2.10.4.0.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.4.0 \| pulsar-io-jdbc-mariadb-2.10.4.0.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.4.0 \| pulsar-io-jdbc-postgres-2.10.4.0.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.4.0 \| pulsar-io-jdbc-sqlite-2.10.4.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.0 \| pulsar-io-kafka-2.10.4.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.0 \| pulsar-io-kinesis-2.10.4.0.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.0 \| pulsar-io-data-generator-2.10.4.0.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.4.0 \| pulsar-io-debezium-mongodb-2.10.4.0.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.4.0 \| pulsar-io-debezium-mssql-2.10.4.0.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.4.0 \| pulsar-io-debezium-mysql-2.10.4.0.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.4.0 \| pulsar-io-debezium-oracle-2.10.4.0.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.4.0 \| pulsar-io-debezium-postgres-2.10.4.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.0 \| pulsar-io-kafka-2.10.4.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.0 \| pulsar-io-kinesis-2.10.4.0.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.5 \| pulsar-kafka-proxy-2.10.3.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.5 \| pulsar-protocol-handler-kafka-2.10.3.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.8 \|
cassandra-enhanced-pulsar-sink-1.6.8-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.4 \|
pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.4-alpha1.nar \| \|
[coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \| \|
[couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \| Couchbase
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.4.0 \| pulsar-io-aerospike-2.10.4.0.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.4.0 \|
pulsar-io-batch-data-generator-2.10.4.0.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.0 \| pulsar-io-data-generator-2.10.4.0.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.4.0 \| pulsar-io-elastic-search-2.10.4.0.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.4.0 \| pulsar-io-flume-2.10.4.0.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.4.0 \| pulsar-io-hbase-2.10.4.0.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.4.0 \| pulsar-io-hdfs2-2.10.4.0.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.4.0 \| pulsar-io-hdfs3-2.10.4.0.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.4.0 \| pulsar-io-http-2.10.4.0.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.4.0 \| pulsar-io-influxdb-2.10.4.0.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.4.0 \| pulsar-io-jdbc-clickhouse-2.10.4.0.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.4.0 \| pulsar-io-jdbc-mariadb-2.10.4.0.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.4.0 \| pulsar-io-jdbc-postgres-2.10.4.0.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.4.0 \| pulsar-io-jdbc-sqlite-2.10.4.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.0 \| pulsar-io-kafka-2.10.4.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.0 \| pulsar-io-kinesis-2.10.4.0.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.4.0 \| pulsar-io-mongo-2.10.4.0.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.4.0 \| pulsar-io-rabbitmq-2.10.4.0.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.4.0 \| pulsar-io-redis-2.10.4.0.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.4.0 \| pulsar-io-solr-2.10.4.0.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.4 \|
pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.4-alpha1.nar \| \|
[coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \| \|
[couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \| Couchbase
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.4.0 \|
pulsar-io-batch-data-generator-2.10.4.0.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.4.0 \| pulsar-io-canal-2.10.4.0.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.4.0 \| pulsar-io-data-generator-2.10.4.0.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.4.0 \| pulsar-io-debezium-mongodb-2.10.4.0.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.4.0 \| pulsar-io-debezium-mssql-2.10.4.0.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.4.0 \| pulsar-io-debezium-mysql-2.10.4.0.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.4.0 \| pulsar-io-debezium-oracle-2.10.4.0.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.4.0 \| pulsar-io-debezium-postgres-2.10.4.0.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.4.0 \| pulsar-io-dynamodb-2.10.4.0.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.4.0 \| pulsar-io-file-2.10.4.0.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.4.0 \| pulsar-io-flume-2.10.4.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.4.0 \| pulsar-io-kafka-2.10.4.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.4.0 \| pulsar-io-kinesis-2.10.4.0.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.4.0 \| pulsar-io-mongo-2.10.4.0.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.4.0 \| pulsar-io-netty-2.10.4.0.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.4.0 \| pulsar-io-nsq-2.10.4.0.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.4.0 \| pulsar-io-rabbitmq-2.10.4.0.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.4.0 \| pulsar-io-twitter-2.10.4.0.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.5 \| pulsar-kafka-proxy-2.10.3.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.5 \| pulsar-protocol-handler-kafka-2.10.3.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


## Luna Streaming Distribution 2.10 3.4.1

This is a hotfix release containing the upgrade of the BigQuery Sink connector.
Only the `-experimental` docker image has been updated.

## Luna Streaming Distribution 2.10 3.4

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [62f86e9fd62](https://github.com/datastax/pulsar/commit/62f86e9fd62) Add
  support for custom proxy lookup handler (#163)
- [9e66f0e937d](https://github.com/datastax/pulsar/commit/9e66f0e937d)
  \[improve\]\[CI\] Remove cmd-line level test retries (#16524)
- [1fd8e6cc193](https://github.com/datastax/pulsar/commit/1fd8e6cc193)
  \[improve\] Upgrade lombok to 1.8.26 (#19426)
- [b7bae70faff](https://github.com/datastax/pulsar/commit/b7bae70faff)
  \[improve\]\[misc\] Upgrade Netty to 4.1.87.Final (#19417)
- [4cc97d0e386](https://github.com/datastax/pulsar/commit/4cc97d0e386)
  \[improve\]\[broker\] Follow up \#19230 to tighten the validation scope
  (#19234)
- [467bfa9f3af](https://github.com/datastax/pulsar/commit/467bfa9f3af)
  \[fix\]\[client\] Set authentication when using loadConf in client and admin
  client (#18358)
- [1dae02eca7c](https://github.com/datastax/pulsar/commit/1dae02eca7c)
  \[improve\]\[broker\] Add UncaughtExceptionHandler for every thread pool
  (#18211)
- [b30b2244ce5](https://github.com/datastax/pulsar/commit/b30b2244ce5)
  \[feature\]\[txn\] Fix individual ack batch message with transaction abort
  redevlier duplicate messages (#14327)
- [465431f1d46](https://github.com/datastax/pulsar/commit/465431f1d46)
  \[fix\]\[client\] Fix authentication not update after changing the serviceUrl
  (#19510)
- [4a1bf35a649](https://github.com/datastax/pulsar/commit/4a1bf35a649)
  \[improve\]\[broker\] Use shrink map for trackerCache (#19534)
- [652754605f4](https://github.com/datastax/pulsar/commit/652754605f4) \[fix\]
  \[broker\] Incorrect service name selection logic (#19505)
- [1af1c7f6925](https://github.com/datastax/pulsar/commit/1af1c7f6925)
  \[Improve\]\[Broker\]Reduce GetReplicatedSubscriptionStatus local REST call
  (#16946)
- [e8b2d79688b](https://github.com/datastax/pulsar/commit/e8b2d79688b)
  \[fix\]\[broker\] PulsarRegistrationClient - implement getAllBookies and
  follow BookieServiceInfo updates (#18133)
- [2f1df06dd72](https://github.com/datastax/pulsar/commit/2f1df06dd72)
  \[fix\]\[admin\] Fix `validatePersistencePolicies` that Namespace/Topic
  persistent policies cannot set to \< 0 (#18999)
- [c00ac619e86](https://github.com/datastax/pulsar/commit/c00ac619e86)
  \[fix\]\[broker\]\[branch-2.10\] Fix geo-replication admin (#19608)
- [12f61edb9d5](https://github.com/datastax/pulsar/commit/12f61edb9d5)
  \[fix\]\[broker\] Copy command fields and fix potential thread-safety in
  ServerCnx (#19517)
- [525517fbca5](https://github.com/datastax/pulsar/commit/525517fbca5)
  \[fix\]\[client\] Broker address resolution wrong if connect through a
  multi-dns names proxy (#19597)
- [32dfda9ec65](https://github.com/datastax/pulsar/commit/32dfda9ec65)
  \[branch-2.10\]\[fix\]\[proxy\] Fix using wrong client version in pulsar proxy
  (#19576)
- [9fda5cc6dbb](https://github.com/datastax/pulsar/commit/9fda5cc6dbb)
  \[fix\]\[proxy\] Fix refresh client auth (#17831)
- [8de0609c7d5](https://github.com/datastax/pulsar/commit/8de0609c7d5) \[fix\]
  \[ml\] messagesConsumedCounter of NonDurableCursor was initialized incorrectly
  (#19355)
- [11a67f37adf](https://github.com/datastax/pulsar/commit/11a67f37adf)
  \[fix\]\[broker\] Fix loadbalance score caculation problem (#19420)
- [f42dd413ee3](https://github.com/datastax/pulsar/commit/f42dd413ee3)
  \[fix\]\[client\] Fix async completion in ConsumerImpl#processPossibleToDLQ
  (#19392)
- [6a491981652](https://github.com/datastax/pulsar/commit/6a491981652)
  \[fix\]\[ml\] Reset individualDeletedMessagesSerializedSize after acked all
  messages. (#19428)
- [d26add6afc3](https://github.com/datastax/pulsar/commit/d26add6afc3)
  \[fix\]\[authorization\] Fix the return value of canConsumeAsync (#19412)
- [90188eaaee8](https://github.com/datastax/pulsar/commit/90188eaaee8)
  \[Improve\]\[broker\] Support clear old bookie data for BKCluster (#16744)
- [902b442da77](https://github.com/datastax/pulsar/commit/902b442da77)
  \[fix\]\[broker\] Remove timestamp from broker metrics (#17419)
- [11a35649d79](https://github.com/datastax/pulsar/commit/11a35649d79)
  \[fix\]\[broker\] Fix race condition while updating partition number (#19199)
- [7e2d0b503cf](https://github.com/datastax/pulsar/commit/7e2d0b503cf)
  \[fix\]\[txn\] fix txn coordinator recover handle committing and aborting txn
  race condition. (#19201)
- [fc449868b12](https://github.com/datastax/pulsar/commit/fc449868b12)
  \[improve\]\[txn\] Handle changeToReadyState failure correctly in TC client
  (#19308)
- [731fc5e619b](https://github.com/datastax/pulsar/commit/731fc5e619b) \[fix\]
  \[ml\] The atomicity of multiple fields of ml is broken (#19346)
- [83dc9d3726b](https://github.com/datastax/pulsar/commit/83dc9d3726b)
  \[fix\]\[ml\] Fix potential NPE cause future never complete. (#19415)
- [1c5f02302e4](https://github.com/datastax/pulsar/commit/1c5f02302e4)
  \[fix\]\[broker\] Fix PulsarRegistrationClient and ZkRegistrationClient not
  aware rack info problem. (#18672)
- [7f81fbcb62f](https://github.com/datastax/pulsar/commit/7f81fbcb62f)
  \[revert\]\[misc\] "modify check waitingForPingResponse with volatile
  (#12615)" (#19439)
- [8b003f9451d](https://github.com/datastax/pulsar/commit/8b003f9451d)
  \[cherry-pick\]\[branch-2.10\] Close TransactionBuffer when create persistent
  topic timeout (#19454)
- [9ad4925883e](https://github.com/datastax/pulsar/commit/9ad4925883e)
  \[improve\]\[broker\] Copy subscription properties during updating the topic
  partition number. (#19223)
- [89f6ac67f33](https://github.com/datastax/pulsar/commit/89f6ac67f33)
  \[improve\]\[broker\] Added isActive in ManagedCursorImpl (#19341)
- [9877210f097](https://github.com/datastax/pulsar/commit/9877210f097)
  \[improve\]\[broker\] Added isActive in ManagedCursorImpl (#19341)
- [efec058bd70](https://github.com/datastax/pulsar/commit/efec058bd70)
  \[fix\]\[txn\] Catch and log runtime exceptions in async operations (#19258)
- [72bf32eb04a](https://github.com/datastax/pulsar/commit/72bf32eb04a) \[fix\]
  \[ml\] Fix the incorrect total size if use ML interceptor (#19404)
- [ac75bc7ea23](https://github.com/datastax/pulsar/commit/ac75bc7ea23)
  \[fix\]\[broker\] Support deleting partitioned topics with the keyword
  `-partition-` (#19230)
- [669ff922ae7](https://github.com/datastax/pulsar/commit/669ff922ae7)
  \[improve\]\[client\] Change the get lastMessageId to debug level (#18421)
- [8e349631931](https://github.com/datastax/pulsar/commit/8e349631931) \[fix\]
  \[broker\] getLastMessageId returns a wrong batch index of last message if
  enabled read compacted (#18877)
- [f3dd2f5792b](https://github.com/datastax/pulsar/commit/f3dd2f5792b)
  \[fix\]\[broker\]fix multi invocation for ledger createComplete (#18975)
- [7e95b661133](https://github.com/datastax/pulsar/commit/7e95b661133)
  \[fix\]\[txn\] Correct the prompt message (#17009)
- [5733157ab28](https://github.com/datastax/pulsar/commit/5733157ab28)
  \[fix\]\[broker\]optimize the shutdown sequence of broker service when it
  close (#16756)
- [c2719ece1b2](https://github.com/datastax/pulsar/commit/c2719ece1b2) Close
  TransactionBuffer when MessageDeduplication#checkStatus failed (#19288)
- [ae25a364445](https://github.com/datastax/pulsar/commit/ae25a364445)
  \[fix\]\[proxy\] Only go to connecting state once (#19331)
- [31aac760b63](https://github.com/datastax/pulsar/commit/31aac760b63)
  \[fix\]\[client\] Set fields earlier for correct ClientCnx initialization
  (#19327)
- [ed965d550a9](https://github.com/datastax/pulsar/commit/ed965d550a9)
  \[fix\]\[client\] Prevent DNS reverse lookup when physical address is an IP
  address (#19028)
- [f214d674c73](https://github.com/datastax/pulsar/commit/f214d674c73)
  \[fix\]\[broker\] fixed the build error for pattern matching variable in lower
  JVM versions (#19362)
- [6adf0739a48](https://github.com/datastax/pulsar/commit/6adf0739a48)
  \[fix\]\[client\] Fix reader listener can't auto ack with pooled message.
  (#19354)
- [f4044db8d88](https://github.com/datastax/pulsar/commit/f4044db8d88)
  \[improve\]\[broker\] Replaced checkBackloggedCursors with
  checkBackloggedCursor(single subscription check) upon subscription (#19343)
- [99a0b0d5bbe](https://github.com/datastax/pulsar/commit/99a0b0d5bbe)
  \[fix\]\[cli\]\[branch-2.10\] Fix mbeans to json (#19294)
- [52d9075d0f2](https://github.com/datastax/pulsar/commit/52d9075d0f2)
  \[improve\]\[broker\] Added isActive in ManagedCursorImpl (#19341)
- [8a279fb5a61](https://github.com/datastax/pulsar/commit/8a279fb5a61) \[fix\]
  \[ml\] Topics stats shows msgBacklog but there reality no backlog (#19275)
- [0d6beace8b8](https://github.com/datastax/pulsar/commit/0d6beace8b8)
  \[fix\]\[broker\] Fix open cursor with null-initialPosition result with
  earliest position (#18416)
- [839125df136](https://github.com/datastax/pulsar/commit/839125df136)
  \[improve\]\[sec\] Suppress false positive OWASP reports (#19105)
- [68acff7781f](https://github.com/datastax/pulsar/commit/68acff7781f)
  \[improve\]\[broker\] Add ref count for sticky hash to optimize the
  performance of Key_Shared subscription (#19167)
- [dab085ec915](https://github.com/datastax/pulsar/commit/dab085ec915)
  \[improve\]\[websocket\]\[branch-2.10\] Add ping support (#19254)
- [47267602575](https://github.com/datastax/pulsar/commit/47267602575)
  \[fix\]\[flaky-test\]LedgerOffloaderMetricsTest (#17106)
- [b613e8de966](https://github.com/datastax/pulsar/commit/b613e8de966)
  \[bugfix\] Fix race condition that leads to caching failed CompletableFutures
  in ConnectionPool
- [73254640ced](https://github.com/datastax/pulsar/commit/73254640ced) Use
  spyWithClassAndConstructorArgsRecordingInvocations in ServerCnxTest
- [d33987c50c6](https://github.com/datastax/pulsar/commit/d33987c50c6)
  \[fix\]\[broker\] Allow proxy to pass same role for authRole and originalRole
  (#19557)
- [5605b919768](https://github.com/datastax/pulsar/commit/5605b919768)
  \[fix\]\[broker\] Make authentication refresh threadsafe (#19506)
- [ca1beb24282](https://github.com/datastax/pulsar/commit/ca1beb24282)
  \[fix\]\[test\] ProxyWithAuthorizationTest remove SAN from test certs (#19594)
- [5d123fa68cb](https://github.com/datastax/pulsar/commit/5d123fa68cb)
  \[fix\]\[broker\] Call originalAuthState.authenticate in ServerCnx
- [b57280db403](https://github.com/datastax/pulsar/commit/b57280db403)
  \[improve\]\[broker\] Add test to verify authRole cannot change (#19430)
- [936273b41d0](https://github.com/datastax/pulsar/commit/936273b41d0)
  \[feat\]\[broker\] Cherry-pick tests from (#19409)
- [9f14fcd7940](https://github.com/datastax/pulsar/commit/9f14fcd7940)
  \[improve\]\[broker\] ServerCnx: go to Failed state when auth fails (#19312)
- [f9ae3098ae4](https://github.com/datastax/pulsar/commit/f9ae3098ae4)
  \[improve\]\[broker\] Require authRole is proxyRole to set originalPrincipal
  (#19455)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.4 \| pulsar-io-data-generator-2.10.3.4.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.4 \| pulsar-io-elastic-search-2.10.3.4.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.4 \| pulsar-io-http-2.10.3.4.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.4 \| pulsar-io-jdbc-clickhouse-2.10.3.4.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.4 \| pulsar-io-jdbc-mariadb-2.10.3.4.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.4 \| pulsar-io-jdbc-postgres-2.10.3.4.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.4 \| pulsar-io-jdbc-sqlite-2.10.3.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.4 \| pulsar-io-kafka-2.10.3.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.4 \| pulsar-io-kinesis-2.10.3.4.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.4 \| pulsar-io-data-generator-2.10.3.4.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.4 \| pulsar-io-debezium-mongodb-2.10.3.4.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.4 \| pulsar-io-debezium-mssql-2.10.3.4.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.4 \| pulsar-io-debezium-mysql-2.10.3.4.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.4 \| pulsar-io-debezium-oracle-2.10.3.4.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.4 \| pulsar-io-debezium-postgres-2.10.3.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.4 \| pulsar-io-kafka-2.10.3.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.4 \| pulsar-io-kinesis-2.10.3.4.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.4 \| pulsar-kafka-proxy-2.10.3.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.4 \| pulsar-protocol-handler-kafka-2.10.3.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.3.4 \| pulsar-io-aerospike-2.10.3.4.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.4 \|
pulsar-io-batch-data-generator-2.10.3.4.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.4 \| pulsar-io-data-generator-2.10.3.4.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.4 \| pulsar-io-elastic-search-2.10.3.4.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.4 \| pulsar-io-flume-2.10.3.4.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.3.4 \| pulsar-io-hbase-2.10.3.4.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.3.4 \| pulsar-io-hdfs2-2.10.3.4.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.3.4 \| pulsar-io-hdfs3-2.10.3.4.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.4 \| pulsar-io-http-2.10.3.4.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.3.4 \| pulsar-io-influxdb-2.10.3.4.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.4 \| pulsar-io-jdbc-clickhouse-2.10.3.4.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.4 \| pulsar-io-jdbc-mariadb-2.10.3.4.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.4 \| pulsar-io-jdbc-postgres-2.10.3.4.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.4 \| pulsar-io-jdbc-sqlite-2.10.3.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.4 \| pulsar-io-kafka-2.10.3.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.4 \| pulsar-io-kinesis-2.10.3.4.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.4 \| pulsar-io-mongo-2.10.3.4.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.4 \| pulsar-io-rabbitmq-2.10.3.4.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.3.4 \| pulsar-io-redis-2.10.3.4.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.3.4 \| pulsar-io-solr-2.10.3.4.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.4 \|
pulsar-io-batch-data-generator-2.10.3.4.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.3.4 \| pulsar-io-canal-2.10.3.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.4 \| pulsar-io-data-generator-2.10.3.4.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.4 \| pulsar-io-debezium-mongodb-2.10.3.4.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.4 \| pulsar-io-debezium-mssql-2.10.3.4.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.4 \| pulsar-io-debezium-mysql-2.10.3.4.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.4 \| pulsar-io-debezium-oracle-2.10.3.4.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.4 \| pulsar-io-debezium-postgres-2.10.3.4.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.3.4 \| pulsar-io-dynamodb-2.10.3.4.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.3.4 \| pulsar-io-file-2.10.3.4.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.4 \| pulsar-io-flume-2.10.3.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.4 \| pulsar-io-kafka-2.10.3.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.4 \| pulsar-io-kinesis-2.10.3.4.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.4 \| pulsar-io-mongo-2.10.3.4.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.3.4 \| pulsar-io-netty-2.10.3.4.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.3.4 \| pulsar-io-nsq-2.10.3.4.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.4 \| pulsar-io-rabbitmq-2.10.3.4.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.3.4 \| pulsar-io-twitter-2.10.3.4.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.4 \| pulsar-kafka-proxy-2.10.3.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.4 \| pulsar-protocol-handler-kafka-2.10.3.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


## Luna Streaming Distribution 2.10 3.3

This is a maintenance release containing important stability updates.

### Most notable commits

- [4a5079d7b25](https://github.com/datastax/pulsar/commit/4a5079d7b25)
  \[fix\]\[broker\]\[branch-2.10\] Replace sync method call in async call chain
  to prevent ZK event thread deadlock (#19539)
- [f389356db4a](https://github.com/datastax/pulsar/commit/f389356db4a)
  \[fix\]\[broker\] ServerCnx broken after recent cherry-picks (#19521)
- [5b0a5641245](https://github.com/datastax/pulsar/commit/5b0a5641245)
  \[cleanup\]\[broker\] Validate originalPrincipal earlier in ServerCnx (#19270)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.3 \| pulsar-io-data-generator-2.10.3.3.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.3 \| pulsar-io-elastic-search-2.10.3.3.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.3 \| pulsar-io-http-2.10.3.3.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.3 \| pulsar-io-jdbc-clickhouse-2.10.3.3.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.3 \| pulsar-io-jdbc-mariadb-2.10.3.3.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.3 \| pulsar-io-jdbc-postgres-2.10.3.3.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.3 \| pulsar-io-jdbc-sqlite-2.10.3.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.3 \| pulsar-io-kafka-2.10.3.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.3 \| pulsar-io-kinesis-2.10.3.3.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.3 \| pulsar-io-data-generator-2.10.3.3.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.3 \| pulsar-io-debezium-mongodb-2.10.3.3.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.3 \| pulsar-io-debezium-mssql-2.10.3.3.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.3 \| pulsar-io-debezium-mysql-2.10.3.3.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.3 \| pulsar-io-debezium-oracle-2.10.3.3.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.3 \| pulsar-io-debezium-postgres-2.10.3.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.3 \| pulsar-io-kafka-2.10.3.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.3 \| pulsar-io-kinesis-2.10.3.3.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.2 \| pulsar-kafka-proxy-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.2 \| pulsar-protocol-handler-kafka-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.3.3 \| pulsar-io-aerospike-2.10.3.3.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.3 \|
pulsar-io-batch-data-generator-2.10.3.3.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.3 \| pulsar-io-data-generator-2.10.3.3.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.3 \| pulsar-io-elastic-search-2.10.3.3.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.3 \| pulsar-io-flume-2.10.3.3.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.3.3 \| pulsar-io-hbase-2.10.3.3.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.3.3 \| pulsar-io-hdfs2-2.10.3.3.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.3.3 \| pulsar-io-hdfs3-2.10.3.3.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.3 \| pulsar-io-http-2.10.3.3.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.3.3 \| pulsar-io-influxdb-2.10.3.3.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.3 \| pulsar-io-jdbc-clickhouse-2.10.3.3.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.3 \| pulsar-io-jdbc-mariadb-2.10.3.3.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.3 \| pulsar-io-jdbc-postgres-2.10.3.3.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.3 \| pulsar-io-jdbc-sqlite-2.10.3.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.3 \| pulsar-io-kafka-2.10.3.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.3 \| pulsar-io-kinesis-2.10.3.3.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.3 \| pulsar-io-mongo-2.10.3.3.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.3 \| pulsar-io-rabbitmq-2.10.3.3.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.3.3 \| pulsar-io-redis-2.10.3.3.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.3.3 \| pulsar-io-solr-2.10.3.3.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.3 \|
pulsar-io-batch-data-generator-2.10.3.3.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.3.3 \| pulsar-io-canal-2.10.3.3.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.3 \| pulsar-io-data-generator-2.10.3.3.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.3 \| pulsar-io-debezium-mongodb-2.10.3.3.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.3 \| pulsar-io-debezium-mssql-2.10.3.3.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.3 \| pulsar-io-debezium-mysql-2.10.3.3.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.3 \| pulsar-io-debezium-oracle-2.10.3.3.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.3 \| pulsar-io-debezium-postgres-2.10.3.3.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.3.3 \| pulsar-io-dynamodb-2.10.3.3.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.3.3 \| pulsar-io-file-2.10.3.3.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.3 \| pulsar-io-flume-2.10.3.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.3 \| pulsar-io-kafka-2.10.3.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.3 \| pulsar-io-kinesis-2.10.3.3.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.3 \| pulsar-io-mongo-2.10.3.3.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.3.3 \| pulsar-io-netty-2.10.3.3.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.3.3 \| pulsar-io-nsq-2.10.3.3.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.3 \| pulsar-io-rabbitmq-2.10.3.3.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.3.3 \| pulsar-io-twitter-2.10.3.3.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.2 \| pulsar-kafka-proxy-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.2 \| pulsar-protocol-handler-kafka-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.1 \| pulsar-transformations-2.1.1.nar \|

</details>


## Luna Streaming Distribution 2.10 3.2

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [b1000712f9e](https://github.com/datastax/pulsar/commit/b1000712f9e)
  \[improve\] Upgrade wildfly-eytron (used by debezium) to fix CVE-2022-3143
  (#19333)
- [04100389db7](https://github.com/datastax/pulsar/commit/04100389db7)
  \[cherry-pick\]\[branch-2.10\] Allow superusers to abort transactions (#19467)
  (#19473)
- [1ba48c07989](https://github.com/datastax/pulsar/commit/1ba48c07989)
  \[fix\]\[broker\] Make ServerCnx#originalAuthData volatile (#19507)
- [f559d8d46a5](https://github.com/datastax/pulsar/commit/f559d8d46a5)
  \[improve\] PIP-241: add TopicEventListener / topic events for the
  BrokerService (#19153) (#161)
- [b4f8a835de1](https://github.com/datastax/pulsar/commit/b4f8a835de1)
  \[fix\]\[fn\] Fix k8s merge runtime opts bug (#19481)
- [4579052fa3c](https://github.com/datastax/pulsar/commit/4579052fa3c)
  \[fix\]\[io\] Update Elasticsearch sink idle cnx timeout to 30s (#19377)
- [f538502a6cd](https://github.com/datastax/pulsar/commit/f538502a6cd)
  \[fix\]\[broker\] Expect msgs after server initiated CloseProducer (#19446)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.2 \| pulsar-io-data-generator-2.10.3.2.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.2 \| pulsar-io-elastic-search-2.10.3.2.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.2 \| pulsar-io-http-2.10.3.2.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.2 \| pulsar-io-jdbc-clickhouse-2.10.3.2.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.2 \| pulsar-io-jdbc-mariadb-2.10.3.2.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.2 \| pulsar-io-jdbc-postgres-2.10.3.2.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.2 \| pulsar-io-jdbc-sqlite-2.10.3.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.2 \| pulsar-io-kafka-2.10.3.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.2 \| pulsar-io-kinesis-2.10.3.2.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.2 \| pulsar-io-data-generator-2.10.3.2.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.2 \| pulsar-io-debezium-mongodb-2.10.3.2.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.2 \| pulsar-io-debezium-mssql-2.10.3.2.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.2 \| pulsar-io-debezium-mysql-2.10.3.2.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.2 \| pulsar-io-debezium-oracle-2.10.3.2.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.2 \| pulsar-io-debezium-postgres-2.10.3.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.2 \| pulsar-io-kafka-2.10.3.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.2 \| pulsar-io-kinesis-2.10.3.2.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.2 \| pulsar-kafka-proxy-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.2 \| pulsar-protocol-handler-kafka-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.0 \| pulsar-transformations-2.1.0.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.3.2 \| pulsar-io-aerospike-2.10.3.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.2 \|
pulsar-io-batch-data-generator-2.10.3.2.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.2 \| pulsar-io-data-generator-2.10.3.2.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.2 \| pulsar-io-elastic-search-2.10.3.2.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.2 \| pulsar-io-flume-2.10.3.2.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.3.2 \| pulsar-io-hbase-2.10.3.2.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.3.2 \| pulsar-io-hdfs2-2.10.3.2.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.3.2 \| pulsar-io-hdfs3-2.10.3.2.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.2 \| pulsar-io-http-2.10.3.2.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.3.2 \| pulsar-io-influxdb-2.10.3.2.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.2 \| pulsar-io-jdbc-clickhouse-2.10.3.2.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.2 \| pulsar-io-jdbc-mariadb-2.10.3.2.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.2 \| pulsar-io-jdbc-postgres-2.10.3.2.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.2 \| pulsar-io-jdbc-sqlite-2.10.3.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.2 \| pulsar-io-kafka-2.10.3.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.2 \| pulsar-io-kinesis-2.10.3.2.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.2 \| pulsar-io-mongo-2.10.3.2.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.2 \| pulsar-io-rabbitmq-2.10.3.2.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.3.2 \| pulsar-io-redis-2.10.3.2.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.3.2 \| pulsar-io-solr-2.10.3.2.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.3 \| pulsar-cassandra-source-2.2.3.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.2 \|
pulsar-io-batch-data-generator-2.10.3.2.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.3.2 \| pulsar-io-canal-2.10.3.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.2 \| pulsar-io-data-generator-2.10.3.2.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.2 \| pulsar-io-debezium-mongodb-2.10.3.2.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.2 \| pulsar-io-debezium-mssql-2.10.3.2.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.2 \| pulsar-io-debezium-mysql-2.10.3.2.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.2 \| pulsar-io-debezium-oracle-2.10.3.2.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.2 \| pulsar-io-debezium-postgres-2.10.3.2.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.3.2 \| pulsar-io-dynamodb-2.10.3.2.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.3.2 \| pulsar-io-file-2.10.3.2.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.2 \| pulsar-io-flume-2.10.3.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.2 \| pulsar-io-kafka-2.10.3.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.2 \| pulsar-io-kinesis-2.10.3.2.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.2 \| pulsar-io-mongo-2.10.3.2.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.3.2 \| pulsar-io-netty-2.10.3.2.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.3.2 \| pulsar-io-nsq-2.10.3.2.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.2 \| pulsar-io-rabbitmq-2.10.3.2.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.3.2 \| pulsar-io-twitter-2.10.3.2.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.2 \| pulsar-kafka-proxy-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.2 \| pulsar-protocol-handler-kafka-2.10.3.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.0 \| pulsar-transformations-2.1.0.nar \|

</details>


## Luna Streaming Distribution 2.10 3.1

This is a maintenance release containing important stability updates.

### Most notable commits

- [ae3670cd27d](https://github.com/datastax/pulsar/commit/ae3670cd27d) Upgrade
  BookKeeper to 4.14.6.1.0.1
- [6b9967fb928](https://github.com/datastax/pulsar/commit/6b9967fb928)
  \[fix\]\[broker\] AbstractBatchedMetadataStore - use AlreadyClosedException
  instead of IllegalStateException (#19284)
- [addb66454db](https://github.com/datastax/pulsar/commit/addb66454db)
  \[fix\]\[cli\] Shell syntax (#19188)
- [3b363ac0470](https://github.com/datastax/pulsar/commit/3b363ac0470)
  \[fix\]\[cli\] Fix mbeans to json (#17676)
- [ad4795be1e6](https://github.com/datastax/pulsar/commit/ad4795be1e6)
  \[Fix\]\[broker\] Fix JDK17 compatibility issues. (#15540)
- [1813d08c1bf](https://github.com/datastax/pulsar/commit/1813d08c1bf) Support
  JAVA_HOME in env file when check java version (#14711)
- [79956a7096c](https://github.com/datastax/pulsar/commit/79956a7096c)
  \[fix\]\[env\]Fix potential incompatible java opts caused by IS_JAVA_8
  (#15444)
- [a51682f3219](https://github.com/datastax/pulsar/commit/a51682f3219)
  \[fix\]\[jdk17\] Enable Netty and BookKeeper IO optimizations on jdk17
  (#15256)
- [9a145382d91](https://github.com/datastax/pulsar/commit/9a145382d91)
  \[fix\]\[jdk17\] remove illegal access warning and enable reads optimization
  on jdk17 (#14999)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.1 \| pulsar-io-data-generator-2.10.3.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.1 \| pulsar-io-elastic-search-2.10.3.1.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.1 \| pulsar-io-http-2.10.3.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.1 \| pulsar-io-jdbc-clickhouse-2.10.3.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.1 \| pulsar-io-jdbc-mariadb-2.10.3.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.1 \| pulsar-io-jdbc-postgres-2.10.3.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.1 \| pulsar-io-jdbc-sqlite-2.10.3.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.1 \| pulsar-io-kafka-2.10.3.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.1 \| pulsar-io-kinesis-2.10.3.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.1 \| pulsar-io-data-generator-2.10.3.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.1 \| pulsar-io-debezium-mongodb-2.10.3.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.1 \| pulsar-io-debezium-mssql-2.10.3.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.1 \| pulsar-io-debezium-mysql-2.10.3.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.1 \| pulsar-io-debezium-oracle-2.10.3.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.1 \| pulsar-io-debezium-postgres-2.10.3.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.1 \| pulsar-io-kafka-2.10.3.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.1 \| pulsar-io-kinesis-2.10.3.1.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.0 \| pulsar-kafka-proxy-2.10.3.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.0 \| pulsar-protocol-handler-kafka-2.10.3.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.0 \| pulsar-transformations-2.1.0.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.3.1 \| pulsar-io-aerospike-2.10.3.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.1 \|
pulsar-io-batch-data-generator-2.10.3.1.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.1 \| pulsar-io-data-generator-2.10.3.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.1 \| pulsar-io-elastic-search-2.10.3.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.1 \| pulsar-io-flume-2.10.3.1.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.3.1 \| pulsar-io-hbase-2.10.3.1.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.3.1 \| pulsar-io-hdfs2-2.10.3.1.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.3.1 \| pulsar-io-hdfs3-2.10.3.1.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.1 \| pulsar-io-http-2.10.3.1.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.3.1 \| pulsar-io-influxdb-2.10.3.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.1 \| pulsar-io-jdbc-clickhouse-2.10.3.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.1 \| pulsar-io-jdbc-mariadb-2.10.3.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.1 \| pulsar-io-jdbc-postgres-2.10.3.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.1 \| pulsar-io-jdbc-sqlite-2.10.3.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.1 \| pulsar-io-kafka-2.10.3.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.1 \| pulsar-io-kinesis-2.10.3.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.1 \| pulsar-io-mongo-2.10.3.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.1 \| pulsar-io-rabbitmq-2.10.3.1.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.3.1 \| pulsar-io-redis-2.10.3.1.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.3.1 \| pulsar-io-solr-2.10.3.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.1 \|
pulsar-io-batch-data-generator-2.10.3.1.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.3.1 \| pulsar-io-canal-2.10.3.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.1 \| pulsar-io-data-generator-2.10.3.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.1 \| pulsar-io-debezium-mongodb-2.10.3.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.1 \| pulsar-io-debezium-mssql-2.10.3.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.1 \| pulsar-io-debezium-mysql-2.10.3.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.1 \| pulsar-io-debezium-oracle-2.10.3.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.1 \| pulsar-io-debezium-postgres-2.10.3.1.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.3.1 \| pulsar-io-dynamodb-2.10.3.1.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.3.1 \| pulsar-io-file-2.10.3.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.1 \| pulsar-io-flume-2.10.3.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.1 \| pulsar-io-kafka-2.10.3.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.1 \| pulsar-io-kinesis-2.10.3.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.1 \| pulsar-io-mongo-2.10.3.1.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.3.1 \| pulsar-io-netty-2.10.3.1.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.3.1 \| pulsar-io-nsq-2.10.3.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.1 \| pulsar-io-rabbitmq-2.10.3.1.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.3.1 \| pulsar-io-twitter-2.10.3.1.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.3.0 \| pulsar-kafka-proxy-2.10.3.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.3.0 \| pulsar-protocol-handler-kafka-2.10.3.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.1.0 \| pulsar-transformations-2.1.0.nar \|

</details>

## Luna Streaming Distribution 2.10 3.0

This release is the first release based on Apache Pulsar 2.10.3. However, this
doesn't change the compatibility guarantee with older releases (2.10 2.x)

Most relevant changes:

- BookKeeper upgrade to 4.14.6.1.0.0 which is based on [Apache BookKeeper
  4.14.6](https://bookkeeper.apache.org/release-notes#4146).
- Group prometheus metrics: the metrics are displayed in a different order and
  the grouped by type.
- Starlight for Kafka upgrade with Kafka transactions support. See the [release
  notes](https://github.com/datastax/starlight-for-kafka/releases/tag/v2.10.0.8).

### Most notable commits

- [2ee664660af](https://github.com/datastax/pulsar/commit/2ee664660af)
  \[fix\]\[broker\] Pass subName for subscription operations in ServerCnx
  (#19184)
- [9920b081254](https://github.com/datastax/pulsar/commit/9920b081254)
  \[fix\]\[broker\]optimize the shutdown sequence of broker service when it
  close (#16756)
- [f6859e6b8d0](https://github.com/datastax/pulsar/commit/f6859e6b8d0)
  \[fix\]\[broker\] Remove timestamp from Promtheus metrics (#17419) - reapply
- [bf1729f9916](https://github.com/datastax/pulsar/commit/bf1729f9916) Upgrade
  DataStax BookKeeper to 4.14.6.1.0.0
- [4febb562dc9](https://github.com/datastax/pulsar/commit/4febb562dc9) Bump
  snappy zstd version to fix CompressorCodecBackwardCompatTest on apple m1
  (#15698)
- [cc5af4f8712](https://github.com/datastax/pulsar/commit/cc5af4f8712) Debezium
  sources: Support loading config from secrets (#19163)
- [32304aac9c1](https://github.com/datastax/pulsar/commit/32304aac9c1)
  \[improve\]\[broker\] Add logs for why namespace bundle been split (#19003)
- [e2dbee21be0](https://github.com/datastax/pulsar/commit/e2dbee21be0)
  \[fix\]\[broker\] Fix deadlock in PendingAckHandleImpl (#18989)
- [5052ac64c03](https://github.com/datastax/pulsar/commit/5052ac64c03)
  \[fix\]\[broker\] Branch-2.10 Avoid endless blocking call. (#18914)
- [39c0fa26de8](https://github.com/datastax/pulsar/commit/39c0fa26de8)
  \[branch-2.10\] Group prometheus metrics (#18941)
- [46d9d6f9ea7](https://github.com/datastax/pulsar/commit/46d9d6f9ea7)
  \[fix\]\[broker\]Update interceptor handler exception (#18940)
- [1921c46f961](https://github.com/datastax/pulsar/commit/1921c46f961) \[fix\]
  \[tx\] \[branch-2.10\] Transaction buffer recover blocked by readNext (#18971)
- [7c5fcf67b6d](https://github.com/datastax/pulsar/commit/7c5fcf67b6d)
  \[fix\]\[txn\] transaction pending ack store future not completely problem
  (#18943)
- [57b51dc7901](https://github.com/datastax/pulsar/commit/57b51dc7901)
  \[cherry-pick\] \[branch-2.10\] Better Python garbage collection management
  for C++-owned objects (#16535) (#18921)
- [dd0fd46733b](https://github.com/datastax/pulsar/commit/dd0fd46733b)
  \[cherry-pick\]\[branch-2.10\]wrong metrics text generated when label_cluster
  specified (#17704) (#18919)
- [a4f9949479d](https://github.com/datastax/pulsar/commit/a4f9949479d)
  \[cherry-pick\]\[branch-2.10\] Fix issue where unexpected ack timeout (#18906)
- [297caf3eab8](https://github.com/datastax/pulsar/commit/297caf3eab8)
  \[fix\]\[fn\] Typo in method name (#18844)
- [5399b13dfdd](https://github.com/datastax/pulsar/commit/5399b13dfdd) Revert
  "\[fix\]\[load-balancer\] skip mis-configured resource usage(\>100%) in load
  computation (#16937)"
- [73aa2d16c04](https://github.com/datastax/pulsar/commit/73aa2d16c04)
  \[fix\]\[broker\] Fix incorrect bundle split count metric (#17970)
- [6cb3e524718](https://github.com/datastax/pulsar/commit/6cb3e524718)
  \[fix\]\[client\] For exclusive subscriptions, if two consumers are created
  repeatedly, the second consumer will block (#18633)
- [b51e24fb0cd](https://github.com/datastax/pulsar/commit/b51e24fb0cd)
  \[fix\]\[client\] Fixes batch_size not checked in
  MessageId#fromByteArrayWithTopic (#18405)
- [20a38ae4a8e](https://github.com/datastax/pulsar/commit/20a38ae4a8e)
  \[fix\]\[broker\] Avoid OOM not trigger PulsarByteBufAllocator
  outOfMemoryListener when use ByteBufAllocator.DEFAULT.heapBuffer in
  PrometheusMetricsGeneratorUtils (#18747)
- [5591dc2c264](https://github.com/datastax/pulsar/commit/5591dc2c264)
  \[fix\]\[txn\] Fix PendingAckHandleImpl when
  `pendingAckStoreProvider.checkInitializedBefore` failed (#18859)
- [d8b951b3d25](https://github.com/datastax/pulsar/commit/d8b951b3d25)
  \[improve\]\[broker\] Make Consumer#equals more effective (#18662)
- [e4ac214891a](https://github.com/datastax/pulsar/commit/e4ac214891a)
  \[fix\]\[client\] Fix possible npe (#18406)
- [56a16903f74](https://github.com/datastax/pulsar/commit/56a16903f74)
  \[fix\]\[client\] Fix exception when calling loadConf on a ConsumerBuilder
  that has a KeySharedPolicy (#18345)
- [32450a7052a](https://github.com/datastax/pulsar/commit/32450a7052a)
  \[fix\]\[broker\] In the trimDeletedEntries method, release the removed entry
  (#18305)
- [6c632e42ee4](https://github.com/datastax/pulsar/commit/6c632e42ee4)
  \[fix\]\[cli\] Fix CLI client produce don't able to use multiple -m send
  multiple messages (#18238)
- [610c540f644](https://github.com/datastax/pulsar/commit/610c540f644)
  \[improve\]\[broker\] Remove locallyAcquiredLock when removeOwnership (#18197)
- [5fe35d594c6](https://github.com/datastax/pulsar/commit/5fe35d594c6)
  \[fix\]\[meta\] fix getChildren in MemoryMetadataStore and EtcdMetadataStore
  (#18172)
- [985e58d3fa0](https://github.com/datastax/pulsar/commit/985e58d3fa0)
  \[fix\]\[function\] Fix invalid metric type `gauge ` (#18129)
- [d03e7461ffc](https://github.com/datastax/pulsar/commit/d03e7461ffc) \[fix\]
  \[pulsar-client\] Fix pendingLookupRequestSemaphore leak when Ser&mldr;
  (#18219)
- [8bab173e95e](https://github.com/datastax/pulsar/commit/8bab173e95e)
  \[fix\]\[client\] Fix failover/exclusive consumer with batch cumulate ack
  issue. (#18454)
- [ca87df94df0](https://github.com/datastax/pulsar/commit/ca87df94df0) Avoid
  unnecessary creation of BitSetRecyclable objects (#17998)
- [f67b878a9bc](https://github.com/datastax/pulsar/commit/f67b878a9bc)
  \[fix\]\[broker\] add return for
  PersistentMessageExpiryMonitor#findEntryFailed
- [1e86ecf6d32](https://github.com/datastax/pulsar/commit/1e86ecf6d32)
  \[improve\]\[java-client\]Add init capacity for messages in
  BatchMessageContainerImpl (#17822)
- [2f1390b20d1](https://github.com/datastax/pulsar/commit/2f1390b20d1)
  \[fix\]\[ml\] Persist correct markDeletePosition to prevent message loss
  (#18237)
- [843fe6e7706](https://github.com/datastax/pulsar/commit/843fe6e7706)
  \[fix\]\[cpp\] Use weak ptr avoid circular references. (#17481)
- [471cea6f14a](https://github.com/datastax/pulsar/commit/471cea6f14a) Fix wrong
  consumers size: execute `callback` before executing `readerCreatedCallback_`.
  (#17325)
- [5f06c93dec3](https://github.com/datastax/pulsar/commit/5f06c93dec3)
  \[improve\]\[broker\] Support setting forceDeleteTenantAllowed dynamically
  (#18192)
- [52e30163373](https://github.com/datastax/pulsar/commit/52e30163373) Make
  BookieId work with PulsarRegistrationDriver (second take) (#17922)
- [25d8042ac8e](https://github.com/datastax/pulsar/commit/25d8042ac8e)
  \[Improve\]\[Auth\]Update authentication failed metrics report (#17787)
- [d89abe09b0c](https://github.com/datastax/pulsar/commit/d89abe09b0c)
  \[fix\]\[broker\] Extract additional servlets to the default directory
  by&mldr; (#17477)
- [bf0fc84de55](https://github.com/datastax/pulsar/commit/bf0fc84de55)
  \[improve\]\[schema\] Change update schema auth from tenant to produce
  (#18074)
- [191a6a663d9](https://github.com/datastax/pulsar/commit/191a6a663d9)
  \[improve\]\[broker\]Improve PersistentMessageExpiryMonitor expire speed when
  ledger not existed (#17842)
- [237da0ed594](https://github.com/datastax/pulsar/commit/237da0ed594)
  \[fix\]\[broker\]Fix mutex never released when trimming (#17911)
- [e2c30f72423](https://github.com/datastax/pulsar/commit/e2c30f72423)
  \[cherry-pick\]\[branch-2.10\] Check numMessages after incrementing counter
  and NPE cause (#18885)
- [38230b1fd3a](https://github.com/datastax/pulsar/commit/38230b1fd3a)
  \[fix\]\[broker\] Fix system service namespace create internal event topic.
  (#17867)
- [a1e94ffcd8b](https://github.com/datastax/pulsar/commit/a1e94ffcd8b)
  \[refactor\]\[java\] Improve docs and code quality about KeyValueSchema usages
  (#17256)
- [376b68b24f6](https://github.com/datastax/pulsar/commit/376b68b24f6) Skip
  creating a subscription replication snapshot if no messages have been
  published after the topic gets activated on a broker (#16618)
- [0fe3879d3d0](https://github.com/datastax/pulsar/commit/0fe3879d3d0)
  \[improve\]\[admin\] Fix NPE in admin-CLI topic stats command (#18326)
- [fef6c7febd6](https://github.com/datastax/pulsar/commit/fef6c7febd6)
  \[fix\]\[broker\] Fix uncompleted future when get the topic policies of a
  deleted topic (#18824)
- [6e6c61419ef](https://github.com/datastax/pulsar/commit/6e6c61419ef)
  \[fix\]\[broker\] Fix delete system topic clean topic policy (#18823)
- [cf3e3e24137](https://github.com/datastax/pulsar/commit/cf3e3e24137)
  \[cherry-pick\]\[branch-2.10\] make getList async (#18819)
- [51d26adf49e](https://github.com/datastax/pulsar/commit/51d26adf49e)
  \[fix\]\[test\]\[branch-2.10\] Remove testGetTopic method (#18829)
- [b7a3e7b730a](https://github.com/datastax/pulsar/commit/b7a3e7b730a)
  \[improve\]\[broker\] System topic writer/reader connection not counted
  (#18603)
- [e39c3701226](https://github.com/datastax/pulsar/commit/e39c3701226)
  \[improve\]\[broker\] System topic writer/reader connection not counted.
  (#18369)
- [d97593708e7](https://github.com/datastax/pulsar/commit/d97593708e7)
  \[cherry-pick\]\[branch-2.10\] cherry-pick \#17957 (unify time unit at
  dropping the backlog on a topic)
- [9518891beb7](https://github.com/datastax/pulsar/commit/9518891beb7)
  \[fix\]\[broker\]unify time unit at dropping the backlog on a topic (#17957)
- [0849468fce3](https://github.com/datastax/pulsar/commit/0849468fce3)
  \[improve\]\[broker\] Support setting `ForceDeleteNamespaceAllowed`
  dynamically (#18181)
- [cabbb1ab98b](https://github.com/datastax/pulsar/commit/cabbb1ab98b)
  \[fix\]\[sql\] Fix message without schema issue. (#18745)
- [da66185972d](https://github.com/datastax/pulsar/commit/da66185972d)
  \[cherry-pick\]\[branch-2.10\]Add fix cherry-pick \#17907 duplicated
  configuration.
- [33048cdcef5](https://github.com/datastax/pulsar/commit/33048cdcef5) Allow to
  configure and disable the size of lookahead for detecting fixed delays in
  messages (#17907)
- [62c64ee01db](https://github.com/datastax/pulsar/commit/62c64ee01db)
  \[fix\]\[broker\] Fix `getPositionAfterN` infinite loop. (#17971)
- [8e81236f8af](https://github.com/datastax/pulsar/commit/8e81236f8af)
  \[fix\]\[broker\] Update the log print content of createSubscriptions (#18024)
- [b4c29058d91](https://github.com/datastax/pulsar/commit/b4c29058d91) \[fix\]
  \[pulsar-client\] Fix pendingLookupRequestSemaphore leak when channel inactive
  (#17856)
- [aa7f4467fa3](https://github.com/datastax/pulsar/commit/aa7f4467fa3)
  \[cherry-pick\]\[branch-2.10\] Make
  PersistentTopicsBase#internalGetPartitionedMetadata async (#18749)
- [cce065045d0](https://github.com/datastax/pulsar/commit/cce065045d0)
  \[branch-2.10\]\[fix\]\[broker\] Fix duplicated schemas creation (#18760)
- [3119b6ec02f](https://github.com/datastax/pulsar/commit/3119b6ec02f)
  \[improve\]\[broker\] Using `handle` instead of `handleAsync` to avoid using
  common pool thread (#17403)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.0 \| pulsar-io-data-generator-2.10.3.0.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.0 \| pulsar-io-elastic-search-2.10.3.0.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.0 \| pulsar-io-http-2.10.3.0.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.0 \| pulsar-io-jdbc-clickhouse-2.10.3.0.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.0 \| pulsar-io-jdbc-mariadb-2.10.3.0.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.0 \| pulsar-io-jdbc-postgres-2.10.3.0.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.0 \| pulsar-io-jdbc-sqlite-2.10.3.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.0 \| pulsar-io-kafka-2.10.3.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.0 \| pulsar-io-kinesis-2.10.3.0.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.0 \| pulsar-io-data-generator-2.10.3.0.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.0 \| pulsar-io-debezium-mongodb-2.10.3.0.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.0 \| pulsar-io-debezium-mssql-2.10.3.0.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.0 \| pulsar-io-debezium-mysql-2.10.3.0.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.0 \| pulsar-io-debezium-oracle-2.10.3.0.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.0 \| pulsar-io-debezium-postgres-2.10.3.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.0 \| pulsar-io-kafka-2.10.3.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.0 \| pulsar-io-kinesis-2.10.3.0.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.9 \| pulsar-kafka-proxy-2.10.0.9.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.9 \| pulsar-protocol-handler-kafka-2.10.0.9.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.3.0 \| pulsar-io-aerospike-2.10.3.0.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.0 \|
pulsar-io-batch-data-generator-2.10.3.0.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.0 \| pulsar-io-data-generator-2.10.3.0.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.3.0 \| pulsar-io-elastic-search-2.10.3.0.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.0 \| pulsar-io-flume-2.10.3.0.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.3.0 \| pulsar-io-hbase-2.10.3.0.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.3.0 \| pulsar-io-hdfs2-2.10.3.0.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.3.0 \| pulsar-io-hdfs3-2.10.3.0.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.3.0 \| pulsar-io-http-2.10.3.0.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.3.0 \| pulsar-io-influxdb-2.10.3.0.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.3.0 \| pulsar-io-jdbc-clickhouse-2.10.3.0.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.3.0 \| pulsar-io-jdbc-mariadb-2.10.3.0.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.3.0 \| pulsar-io-jdbc-postgres-2.10.3.0.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.3.0 \| pulsar-io-jdbc-sqlite-2.10.3.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.0 \| pulsar-io-kafka-2.10.3.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.0 \| pulsar-io-kinesis-2.10.3.0.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.0 \| pulsar-io-mongo-2.10.3.0.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.0 \| pulsar-io-rabbitmq-2.10.3.0.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.3.0 \| pulsar-io-redis-2.10.3.0.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.3.0 \| pulsar-io-solr-2.10.3.0.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.3.0 \|
pulsar-io-batch-data-generator-2.10.3.0.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.3.0 \| pulsar-io-canal-2.10.3.0.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.3.0 \| pulsar-io-data-generator-2.10.3.0.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.3.0 \| pulsar-io-debezium-mongodb-2.10.3.0.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.3.0 \| pulsar-io-debezium-mssql-2.10.3.0.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.3.0 \| pulsar-io-debezium-mysql-2.10.3.0.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.3.0 \| pulsar-io-debezium-oracle-2.10.3.0.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.3.0 \| pulsar-io-debezium-postgres-2.10.3.0.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.3.0 \| pulsar-io-dynamodb-2.10.3.0.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.3.0 \| pulsar-io-file-2.10.3.0.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.3.0 \| pulsar-io-flume-2.10.3.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.3.0 \| pulsar-io-kafka-2.10.3.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.3.0 \| pulsar-io-kinesis-2.10.3.0.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.3.0 \| pulsar-io-mongo-2.10.3.0.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.3.0 \| pulsar-io-netty-2.10.3.0.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.3.0 \| pulsar-io-nsq-2.10.3.0.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.3.0 \| pulsar-io-rabbitmq-2.10.3.0.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.3.0 \| pulsar-io-twitter-2.10.3.0.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.9 \| pulsar-kafka-proxy-2.10.0.9.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.9 \| pulsar-protocol-handler-kafka-2.10.0.9.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.11

This release only contains an important revert for a breaking change introduced
in 2.10 2.4. In releases \>= 2.10 2.4 and \<= 2.10 2.10, when a topic is deleted
the associated schema is always deleted and there's no way to avoid it.

Upgrading to 2.10 2.11 will bring back the usual flag needed to enforce the
schema deletion, which is NOT checked by default. More details [in the Apache
Pulsar project](https://github.com/apache/pulsar/pull/14608) and [mailing list
discussion](https://lists.apache.org/thread/wbny8x0b31jdkgoc9cjlc29gt9fdsm6v).

### Most notable commits

- [fa6553e5b2b](https://github.com/datastax/pulsar/commit/fa6553e5b2b) Revert
  "Ensure the deletion consistency of topic and schema (#14608)"

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.11 \| pulsar-io-data-generator-2.10.2.11.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.11 \| pulsar-io-elastic-search-2.10.2.11.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.11 \| pulsar-io-http-2.10.2.11.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.11 \| pulsar-io-jdbc-clickhouse-2.10.2.11.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.11 \| pulsar-io-jdbc-mariadb-2.10.2.11.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.11 \| pulsar-io-jdbc-postgres-2.10.2.11.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.11 \| pulsar-io-jdbc-sqlite-2.10.2.11.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.11 \| pulsar-io-kafka-2.10.2.11.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.11 \| pulsar-io-kinesis-2.10.2.11.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.11 \| pulsar-io-data-generator-2.10.2.11.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.11 \| pulsar-io-debezium-mongodb-2.10.2.11.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.11 \|
pulsar-io-debezium-mssql-2.10.2.11.nar \| \|
[debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium MySql
Source \| 2.10.2.11 \| pulsar-io-debezium-mysql-2.10.2.11.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.11 \| pulsar-io-debezium-oracle-2.10.2.11.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.11 \| pulsar-io-debezium-postgres-2.10.2.11.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.11 \| pulsar-io-kafka-2.10.2.11.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.11 \| pulsar-io-kinesis-2.10.2.11.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.11 \| pulsar-io-aerospike-2.10.2.11.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.11 \|
pulsar-io-batch-data-generator-2.10.2.11.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.11 \| pulsar-io-data-generator-2.10.2.11.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.11 \| pulsar-io-elastic-search-2.10.2.11.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.11 \| pulsar-io-flume-2.10.2.11.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.11 \| pulsar-io-hbase-2.10.2.11.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.11 \| pulsar-io-hdfs2-2.10.2.11.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.11 \| pulsar-io-hdfs3-2.10.2.11.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.11 \| pulsar-io-http-2.10.2.11.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.11 \| pulsar-io-influxdb-2.10.2.11.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.11 \| pulsar-io-jdbc-clickhouse-2.10.2.11.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.11 \| pulsar-io-jdbc-mariadb-2.10.2.11.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.11 \| pulsar-io-jdbc-postgres-2.10.2.11.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.11 \| pulsar-io-jdbc-sqlite-2.10.2.11.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.11 \| pulsar-io-kafka-2.10.2.11.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.11 \| pulsar-io-kinesis-2.10.2.11.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.11 \| pulsar-io-mongo-2.10.2.11.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.11 \| pulsar-io-rabbitmq-2.10.2.11.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.11 \| pulsar-io-redis-2.10.2.11.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.11 \| pulsar-io-solr-2.10.2.11.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.11 \|
pulsar-io-batch-data-generator-2.10.2.11.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.11 \| pulsar-io-canal-2.10.2.11.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.11 \| pulsar-io-data-generator-2.10.2.11.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.11 \| pulsar-io-debezium-mongodb-2.10.2.11.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.11 \|
pulsar-io-debezium-mssql-2.10.2.11.nar \| \|
[debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium MySql
Source \| 2.10.2.11 \| pulsar-io-debezium-mysql-2.10.2.11.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.11 \| pulsar-io-debezium-oracle-2.10.2.11.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.11 \| pulsar-io-debezium-postgres-2.10.2.11.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.11 \| pulsar-io-dynamodb-2.10.2.11.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.11 \| pulsar-io-file-2.10.2.11.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.11 \| pulsar-io-flume-2.10.2.11.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.11 \| pulsar-io-kafka-2.10.2.11.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.11 \| pulsar-io-kinesis-2.10.2.11.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.11 \| pulsar-io-mongo-2.10.2.11.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.11 \| pulsar-io-netty-2.10.2.11.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.11 \| pulsar-io-nsq-2.10.2.11.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.11 \| pulsar-io-rabbitmq-2.10.2.11.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.11 \| pulsar-io-twitter-2.10.2.11.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>

## Luna Streaming Distribution 2.10 2.10
This is a maintenance release containing important security and stability updates.

### Most notable commits

- [3ab23403d7d](https://github.com/datastax/pulsar/commit/3ab23403d7d)
  \[fix\]\[broker\] Topic could be in fenced state forever if deletion fails
  (#19129)
- [63ccd740dac](https://github.com/datastax/pulsar/commit/63ccd740dac)
  \[fix\]\[sec\] Upgrade woodstox to 5.4.0 (#19041)
- [647649333f3](https://github.com/datastax/pulsar/commit/647649333f3)
  \[fix\]\[sec\] Upgrade jettison to 1.5.3 (#19038)
- [b9b8536d5b4](https://github.com/datastax/pulsar/commit/b9b8536d5b4)
  \[fix\]\[admin\] Keep new inputSpecs when updating sink configs (#19082)
  (#158)
- [c8ff466649b](https://github.com/datastax/pulsar/commit/c8ff466649b)
  \[improve\]\[broker\] Omit making a copy of CommandAck when there are no
  broker interceptors (#18997)
- [7a4ff02096a](https://github.com/datastax/pulsar/commit/7a4ff02096a)
  \[fix\]\[broker\] Copy proto command fields into final variables in ServerCnx
  (#18987)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.10 \| pulsar-io-data-generator-2.10.2.10.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.10 \| pulsar-io-elastic-search-2.10.2.10.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.10 \| pulsar-io-http-2.10.2.10.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.10 \| pulsar-io-jdbc-clickhouse-2.10.2.10.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.10 \| pulsar-io-jdbc-mariadb-2.10.2.10.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.10 \| pulsar-io-jdbc-postgres-2.10.2.10.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.10 \| pulsar-io-jdbc-sqlite-2.10.2.10.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.10 \| pulsar-io-kafka-2.10.2.10.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.10 \| pulsar-io-kinesis-2.10.2.10.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.10 \| pulsar-io-data-generator-2.10.2.10.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.10 \| pulsar-io-debezium-mongodb-2.10.2.10.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.10 \|
pulsar-io-debezium-mssql-2.10.2.10.nar \| \|
[debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium MySql
Source \| 2.10.2.10 \| pulsar-io-debezium-mysql-2.10.2.10.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.10 \| pulsar-io-debezium-oracle-2.10.2.10.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.10 \| pulsar-io-debezium-postgres-2.10.2.10.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.10 \| pulsar-io-kafka-2.10.2.10.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.10 \| pulsar-io-kinesis-2.10.2.10.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.10 \| pulsar-io-aerospike-2.10.2.10.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.10 \|
pulsar-io-batch-data-generator-2.10.2.10.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.10 \| pulsar-io-data-generator-2.10.2.10.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.10 \| pulsar-io-elastic-search-2.10.2.10.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.10 \| pulsar-io-flume-2.10.2.10.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.10 \| pulsar-io-hbase-2.10.2.10.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.10 \| pulsar-io-hdfs2-2.10.2.10.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.10 \| pulsar-io-hdfs3-2.10.2.10.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.10 \| pulsar-io-http-2.10.2.10.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.10 \| pulsar-io-influxdb-2.10.2.10.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.10 \| pulsar-io-jdbc-clickhouse-2.10.2.10.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.10 \| pulsar-io-jdbc-mariadb-2.10.2.10.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.10 \| pulsar-io-jdbc-postgres-2.10.2.10.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.10 \| pulsar-io-jdbc-sqlite-2.10.2.10.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.10 \| pulsar-io-kafka-2.10.2.10.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.10 \| pulsar-io-kinesis-2.10.2.10.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.10 \| pulsar-io-mongo-2.10.2.10.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.10 \| pulsar-io-rabbitmq-2.10.2.10.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.10 \| pulsar-io-redis-2.10.2.10.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.10 \| pulsar-io-solr-2.10.2.10.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.10 \|
pulsar-io-batch-data-generator-2.10.2.10.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.10 \| pulsar-io-canal-2.10.2.10.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.10 \| pulsar-io-data-generator-2.10.2.10.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.10 \| pulsar-io-debezium-mongodb-2.10.2.10.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.10 \|
pulsar-io-debezium-mssql-2.10.2.10.nar \| \|
[debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium MySql
Source \| 2.10.2.10 \| pulsar-io-debezium-mysql-2.10.2.10.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.10 \| pulsar-io-debezium-oracle-2.10.2.10.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.10 \| pulsar-io-debezium-postgres-2.10.2.10.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.10 \| pulsar-io-dynamodb-2.10.2.10.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.10 \| pulsar-io-file-2.10.2.10.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.10 \| pulsar-io-flume-2.10.2.10.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.10 \| pulsar-io-kafka-2.10.2.10.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.10 \| pulsar-io-kinesis-2.10.2.10.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.10 \| pulsar-io-mongo-2.10.2.10.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.10 \| pulsar-io-netty-2.10.2.10.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.10 \| pulsar-io-nsq-2.10.2.10.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.10 \| pulsar-io-rabbitmq-2.10.2.10.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.10 \| pulsar-io-twitter-2.10.2.10.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.1.0 \|
starlight-rabbitmq-2.10.1.0.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.1.0 \| starlight-rabbitmq-2.10.1.0.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.9

This is a maintenance release containing:

- Security updates
- Stability improvements about Transactions
- Netty upgrades

### Most notable commits

- [fc5f13c0bcd](https://github.com/datastax/pulsar/commit/fc5f13c0bcd)
  \[fix\]\[sec\] Upgrade scala-library to get rid of CVE-2022-36944
- [cbeadc2cbe2](https://github.com/datastax/pulsar/commit/cbeadc2cbe2)
  \[fix\]\[io\] Only bundle kafka schema registry client (#18931)
- [63f66f68e75](https://github.com/datastax/pulsar/commit/63f66f68e75)
  \[fix\]\[misc\] do not require encryption on system topics (#18898)
- [7144b56dffe](https://github.com/datastax/pulsar/commit/7144b56dffe) Flag to
  block transactions in replicated namespaces (#156)
- [8a65d256651](https://github.com/datastax/pulsar/commit/8a65d256651)
  \[fix\]\[txn\] Fix replication of transactional messages (#18896)
- [3963ccc2e1c](https://github.com/datastax/pulsar/commit/3963ccc2e1c)
  \[fix\]\[broker\] Fix namespace deletion if \_\_change_events has not been
  created yet
- [775379480e4](https://github.com/datastax/pulsar/commit/775379480e4)
  \[improve\]\[misc\] Upgrade Netty to 4.1.86.Final and Netty Tcnative to
  2.0.54.Final (#18599)
- [f4bec73c54e](https://github.com/datastax/pulsar/commit/f4bec73c54e)
  \[improve\]\[build\] Remove versions that are handled by netty-bom (#18629)
- [f5ed178c2cf](https://github.com/datastax/pulsar/commit/f5ed178c2cf)
  \[fix\]\[cli\] Pulsar shell: allow absolute config file (#18805)
- [fbfb58811a2](https://github.com/datastax/pulsar/commit/fbfb58811a2)
  \[fix\]\[broker\] Fix can not delete namespace by force (#18307)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.9 \| pulsar-io-data-generator-2.10.2.9.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.9 \| pulsar-io-elastic-search-2.10.2.9.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.9 \| pulsar-io-http-2.10.2.9.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.9 \| pulsar-io-jdbc-clickhouse-2.10.2.9.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.9 \| pulsar-io-jdbc-mariadb-2.10.2.9.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.9 \| pulsar-io-jdbc-postgres-2.10.2.9.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.9 \| pulsar-io-jdbc-sqlite-2.10.2.9.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.9 \| pulsar-io-kafka-2.10.2.9.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.9 \| pulsar-io-kinesis-2.10.2.9.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.9 \| pulsar-io-data-generator-2.10.2.9.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.9 \| pulsar-io-debezium-mongodb-2.10.2.9.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.9 \| pulsar-io-debezium-mssql-2.10.2.9.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.9 \| pulsar-io-debezium-mysql-2.10.2.9.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.9 \| pulsar-io-debezium-oracle-2.10.2.9.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.9 \| pulsar-io-debezium-postgres-2.10.2.9.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.9 \| pulsar-io-kafka-2.10.2.9.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.9 \| pulsar-io-kinesis-2.10.2.9.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.9 \| pulsar-io-aerospike-2.10.2.9.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.9 \|
pulsar-io-batch-data-generator-2.10.2.9.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.9 \| pulsar-io-data-generator-2.10.2.9.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.9 \| pulsar-io-elastic-search-2.10.2.9.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.9 \| pulsar-io-flume-2.10.2.9.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.9 \| pulsar-io-hbase-2.10.2.9.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.9 \| pulsar-io-hdfs2-2.10.2.9.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.9 \| pulsar-io-hdfs3-2.10.2.9.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.9 \| pulsar-io-http-2.10.2.9.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.9 \| pulsar-io-influxdb-2.10.2.9.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.9 \| pulsar-io-jdbc-clickhouse-2.10.2.9.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.9 \| pulsar-io-jdbc-mariadb-2.10.2.9.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.9 \| pulsar-io-jdbc-postgres-2.10.2.9.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.9 \| pulsar-io-jdbc-sqlite-2.10.2.9.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.9 \| pulsar-io-kafka-2.10.2.9.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.9 \| pulsar-io-kinesis-2.10.2.9.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.9 \| pulsar-io-mongo-2.10.2.9.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.9 \| pulsar-io-rabbitmq-2.10.2.9.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.9 \| pulsar-io-redis-2.10.2.9.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.9 \| pulsar-io-solr-2.10.2.9.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.9 \|
pulsar-io-batch-data-generator-2.10.2.9.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.9 \| pulsar-io-canal-2.10.2.9.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.9 \| pulsar-io-data-generator-2.10.2.9.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.9 \| pulsar-io-debezium-mongodb-2.10.2.9.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.9 \| pulsar-io-debezium-mssql-2.10.2.9.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.9 \| pulsar-io-debezium-mysql-2.10.2.9.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.9 \| pulsar-io-debezium-oracle-2.10.2.9.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.9 \| pulsar-io-debezium-postgres-2.10.2.9.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.9 \| pulsar-io-dynamodb-2.10.2.9.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.9 \| pulsar-io-file-2.10.2.9.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.9 \| pulsar-io-flume-2.10.2.9.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.9 \| pulsar-io-kafka-2.10.2.9.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.9 \| pulsar-io-kinesis-2.10.2.9.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.9 \| pulsar-io-mongo-2.10.2.9.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.9 \| pulsar-io-netty-2.10.2.9.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.9 \| pulsar-io-nsq-2.10.2.9.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.9 \| pulsar-io-rabbitmq-2.10.2.9.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.9 \| pulsar-io-twitter-2.10.2.9.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>

## Luna Streaming Distribution 2.10 2.8
This is a maintenance release containing important stability updates.

### Most notable commits

- [03074ba4769](https://github.com/datastax/pulsar/commit/03074ba4769)
  \[fix\]\[broker\] Fix dispatch duplicated messages with `Exclusive` mode.
  (#17237)
- [2a82a1f2b6f](https://github.com/datastax/pulsar/commit/2a82a1f2b6f)
  \[fix\]\[broker\] Fix the order of resource close in the
  InMemoryDelayedDeliveryTracker (#18000)
- [81bee7f2164](https://github.com/datastax/pulsar/commit/81bee7f2164)
  \[improve\]\[broker\] reduce code duplication to avoid endless wait
  `CompletableFuture` (#14853)
- [ea98d5ad4d9](https://github.com/datastax/pulsar/commit/ea98d5ad4d9) Remove
  invalid Netty system property which never was valid for Netty 4.1.x (#13563)
- [9fc3f1197f6](https://github.com/datastax/pulsar/commit/9fc3f1197f6)
  \[improve\]\[ML\] Print log when delete empty ledger. (#17859)
- [dc27da49ad3](https://github.com/datastax/pulsar/commit/dc27da49ad3)
  \[fix\]\[admin\] returns 4xx error when pulsar-worker-service is disabled and
  trying to access it (#17901)
- [f174276f611](https://github.com/datastax/pulsar/commit/f174276f611) Pulsar
  Admin: grab contextual stacktrace for sync methods (#14620)
- [de7fd6af281](https://github.com/datastax/pulsar/commit/de7fd6af281)
  \[fix\]\[client\] Unwrap completion exception for Lookup Services (#17717)
- [9aac483a99b](https://github.com/datastax/pulsar/commit/9aac483a99b)
  \[improve\] clean the empty topicAuthenticationMap in zk when revoke
  permission (#16815)
- [e83ef25cc87](https://github.com/datastax/pulsar/commit/e83ef25cc87)
  \[fix\]\[broker\] fix can not revoke permission after update topic partition
  (#17393)
- [f29e5bb3f54](https://github.com/datastax/pulsar/commit/f29e5bb3f54)
  \[fix\]\[broker\] Fix Npe thrown by splitBundle (#17370)
- [2339beb094a](https://github.com/datastax/pulsar/commit/2339beb094a)
  \[fix\]\[admin\] Fix NPE when get OffloadThreshold on namespace (#18061)
- [3e65e9f4695](https://github.com/datastax/pulsar/commit/3e65e9f4695)
  \[improve\]\[txn\] Add getState in transaction for client API (#17423)
- [c3747d81b67](https://github.com/datastax/pulsar/commit/c3747d81b67)
  \[improve\]\[txn\] Implementation of Delayed Transaction Messages (#17548)
- [71c3b25af28](https://github.com/datastax/pulsar/commit/71c3b25af28) \[fix\]
  Avoid redelivering duplicated messages when batching is enabled (#18486)
- [5e65536594f](https://github.com/datastax/pulsar/commit/5e65536594f)
  \[refactor\]\[java\] Unify the acknowledge process for batch and non-batch
  message IDs (#17833)
- [94b89b2107d](https://github.com/datastax/pulsar/commit/94b89b2107d)
  \[fix\]\[flaky-test\]BatchMessageWithBatchIndexLevelTest.testBatchMessageAck
  (#17436)
- [5cf3a32d1b9](https://github.com/datastax/pulsar/commit/5cf3a32d1b9)
  \[fix\]\[broker\] Fix executeWithRetry result is null (#17694)
- [4b1cb668038](https://github.com/datastax/pulsar/commit/4b1cb668038)
  \[fix\]\[broker\] Fix SystemTopicBasedTopicPoliciesService NPE issue (#17602)
- [2195a193e4f](https://github.com/datastax/pulsar/commit/2195a193e4f)
  \[fix\]\[common\] Fix parsing partitionedKey with Base64 encode issue.
  (#17687)
- [e951e472051](https://github.com/datastax/pulsar/commit/e951e472051)
  \[fix\]\[client\] Fix multi-topic consumer stuck after redeliver messages
  (#18491)
- [f51c82a5bac](https://github.com/datastax/pulsar/commit/f51c82a5bac)
  \[fix\]\[client\] Fix IllegalThreadStateException when using newThread in
  ExecutorProvider.ExtendedThreadFactory
- [3fb197169eb](https://github.com/datastax/pulsar/commit/3fb197169eb) Rename
  PulsarTransactionsAuthorizationProvider to
  AllowSystemTransactionTopicLookupAuthorizationProvider
- [26ef2f8eb29](https://github.com/datastax/pulsar/commit/26ef2f8eb29)
  \[fix\]\[txn\] Enable client without system topics permission to use
  transactions - Move to PulsarTransactionsAuthorizationProvider
- [6ecfcb29ea3](https://github.com/datastax/pulsar/commit/6ecfcb29ea3)
  \[fix\]\[txn\] Enable client without system topics permission to use
  transactions
- [1bb6ff483ac](https://github.com/datastax/pulsar/commit/1bb6ff483ac)
  \[fix\]\[monitor\] Fix reporting
  pulsar_subscription_blocked_on_unacked_m&mldr; (#154)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.8 \| pulsar-io-data-generator-2.10.2.8.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.8 \| pulsar-io-elastic-search-2.10.2.8.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.8 \| pulsar-io-http-2.10.2.8.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.8 \| pulsar-io-jdbc-clickhouse-2.10.2.8.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.8 \| pulsar-io-jdbc-mariadb-2.10.2.8.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.8 \| pulsar-io-jdbc-postgres-2.10.2.8.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.8 \| pulsar-io-jdbc-sqlite-2.10.2.8.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.8 \| pulsar-io-kafka-2.10.2.8.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.8 \| pulsar-io-kinesis-2.10.2.8.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.8 \| pulsar-io-data-generator-2.10.2.8.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.8 \| pulsar-io-debezium-mongodb-2.10.2.8.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.8 \| pulsar-io-debezium-mssql-2.10.2.8.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.8 \| pulsar-io-debezium-mysql-2.10.2.8.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.8 \| pulsar-io-debezium-oracle-2.10.2.8.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.8 \| pulsar-io-debezium-postgres-2.10.2.8.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.8 \| pulsar-io-kafka-2.10.2.8.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.8 \| pulsar-io-kinesis-2.10.2.8.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.8 \| pulsar-io-aerospike-2.10.2.8.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.8 \|
pulsar-io-batch-data-generator-2.10.2.8.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.8 \| pulsar-io-data-generator-2.10.2.8.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.8 \| pulsar-io-elastic-search-2.10.2.8.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.8 \| pulsar-io-flume-2.10.2.8.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.8 \| pulsar-io-hbase-2.10.2.8.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.8 \| pulsar-io-hdfs2-2.10.2.8.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.8 \| pulsar-io-hdfs3-2.10.2.8.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.8 \| pulsar-io-http-2.10.2.8.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.8 \| pulsar-io-influxdb-2.10.2.8.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.8 \| pulsar-io-jdbc-clickhouse-2.10.2.8.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.8 \| pulsar-io-jdbc-mariadb-2.10.2.8.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.8 \| pulsar-io-jdbc-postgres-2.10.2.8.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.8 \| pulsar-io-jdbc-sqlite-2.10.2.8.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.8 \| pulsar-io-kafka-2.10.2.8.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.8 \| pulsar-io-kinesis-2.10.2.8.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.8 \| pulsar-io-mongo-2.10.2.8.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.8 \| pulsar-io-rabbitmq-2.10.2.8.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.8 \| pulsar-io-redis-2.10.2.8.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.8 \| pulsar-io-solr-2.10.2.8.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.8 \|
pulsar-io-batch-data-generator-2.10.2.8.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.8 \| pulsar-io-canal-2.10.2.8.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.8 \| pulsar-io-data-generator-2.10.2.8.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.8 \| pulsar-io-debezium-mongodb-2.10.2.8.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.8 \| pulsar-io-debezium-mssql-2.10.2.8.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.8 \| pulsar-io-debezium-mysql-2.10.2.8.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.8 \| pulsar-io-debezium-oracle-2.10.2.8.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.8 \| pulsar-io-debezium-postgres-2.10.2.8.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.8 \| pulsar-io-dynamodb-2.10.2.8.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.8 \| pulsar-io-file-2.10.2.8.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.8 \| pulsar-io-flume-2.10.2.8.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.8 \| pulsar-io-kafka-2.10.2.8.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.8 \| pulsar-io-kinesis-2.10.2.8.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.8 \| pulsar-io-mongo-2.10.2.8.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.8 \| pulsar-io-netty-2.10.2.8.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.8 \| pulsar-io-nsq-2.10.2.8.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.8 \| pulsar-io-rabbitmq-2.10.2.8.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.8 \| pulsar-io-twitter-2.10.2.8.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.7 \| pulsar-kafka-proxy-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.7 \| pulsar-protocol-handler-kafka-2.10.0.7.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.7

This is a maintenance release containing important bugfixes.

### Most notable commits

- [09504017526](https://github.com/datastax/pulsar/commit/09504017526)
  \[improve\]\[io\] ElasticSearch sink: conditional id hashing (#18668)
- [ee28850664a](https://github.com/datastax/pulsar/commit/ee28850664a)
  \[fix\]\[broker\] Create replicated subscriptions for new partitions when
  needed (#18659)
- [605a809e74b](https://github.com/datastax/pulsar/commit/605a809e74b)
  \[fix\]\[offload\] Fix numerical overflow bug while reading data from tiered
  storage (#18595)
- [5fa44db20f8](https://github.com/datastax/pulsar/commit/5fa44db20f8)
  \[fix\]\[cli\] Pulsar shell: do not exit on user interrupt during commands
  (#18615)
- [cdd434dd705](https://github.com/datastax/pulsar/commit/cdd434dd705)
  \[improve\]\[cli\] Pulsar shell: allow cloning an existing config (#18608)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.7 \| pulsar-io-data-generator-2.10.2.7.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.7 \| pulsar-io-elastic-search-2.10.2.7.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.7 \| pulsar-io-http-2.10.2.7.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.7 \| pulsar-io-jdbc-clickhouse-2.10.2.7.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.7 \| pulsar-io-jdbc-mariadb-2.10.2.7.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.7 \| pulsar-io-jdbc-postgres-2.10.2.7.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.7 \| pulsar-io-jdbc-sqlite-2.10.2.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.7 \| pulsar-io-kafka-2.10.2.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.7 \| pulsar-io-kinesis-2.10.2.7.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.7 \| pulsar-io-data-generator-2.10.2.7.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.7 \| pulsar-io-debezium-mongodb-2.10.2.7.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.7 \| pulsar-io-debezium-mssql-2.10.2.7.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.7 \| pulsar-io-debezium-mysql-2.10.2.7.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.7 \| pulsar-io-debezium-oracle-2.10.2.7.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.7 \| pulsar-io-debezium-postgres-2.10.2.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.7 \| pulsar-io-kafka-2.10.2.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.7 \| pulsar-io-kinesis-2.10.2.7.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.7 \| pulsar-io-aerospike-2.10.2.7.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.7 \|
pulsar-io-batch-data-generator-2.10.2.7.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.7 \| pulsar-io-data-generator-2.10.2.7.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.7 \| pulsar-io-elastic-search-2.10.2.7.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.7 \| pulsar-io-flume-2.10.2.7.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.7 \| pulsar-io-hbase-2.10.2.7.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.7 \| pulsar-io-hdfs2-2.10.2.7.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.7 \| pulsar-io-hdfs3-2.10.2.7.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.7 \| pulsar-io-http-2.10.2.7.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.7 \| pulsar-io-influxdb-2.10.2.7.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.7 \| pulsar-io-jdbc-clickhouse-2.10.2.7.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.7 \| pulsar-io-jdbc-mariadb-2.10.2.7.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.7 \| pulsar-io-jdbc-postgres-2.10.2.7.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.7 \| pulsar-io-jdbc-sqlite-2.10.2.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.7 \| pulsar-io-kafka-2.10.2.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.7 \| pulsar-io-kinesis-2.10.2.7.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.7 \| pulsar-io-mongo-2.10.2.7.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.7 \| pulsar-io-rabbitmq-2.10.2.7.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.7 \| pulsar-io-redis-2.10.2.7.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.7 \| pulsar-io-solr-2.10.2.7.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.7 \|
pulsar-io-batch-data-generator-2.10.2.7.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.7 \| pulsar-io-canal-2.10.2.7.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.7 \| pulsar-io-data-generator-2.10.2.7.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.7 \| pulsar-io-debezium-mongodb-2.10.2.7.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.7 \| pulsar-io-debezium-mssql-2.10.2.7.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.7 \| pulsar-io-debezium-mysql-2.10.2.7.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.7 \| pulsar-io-debezium-oracle-2.10.2.7.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.7 \| pulsar-io-debezium-postgres-2.10.2.7.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.7 \| pulsar-io-dynamodb-2.10.2.7.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.7 \| pulsar-io-file-2.10.2.7.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.7 \| pulsar-io-flume-2.10.2.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.7 \| pulsar-io-kafka-2.10.2.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.7 \| pulsar-io-kinesis-2.10.2.7.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.7 \| pulsar-io-mongo-2.10.2.7.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.7 \| pulsar-io-netty-2.10.2.7.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.7 \| pulsar-io-nsq-2.10.2.7.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.7 \| pulsar-io-rabbitmq-2.10.2.7.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.7 \| pulsar-io-twitter-2.10.2.7.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.6

This is a maintenance release containing important stability updates.

### Most notable commits

- [6b65c9df461](https://github.com/datastax/pulsar/commit/6b65c9df461)
  \[improve\]\[test\] Upgrade testcontainers to 1.17.2 (#16161)
- [aea73786745](https://github.com/datastax/pulsar/commit/aea73786745)
  \[fix\]\[io\] ElasticSearch sink: align null fields behaviour
- [22a5682c7cc](https://github.com/datastax/pulsar/commit/22a5682c7cc)
  \[improve\]\[test\] Remove WhiteBox for ElasticSearchSinkTests (#17582)
- [b9d3d6f3a1e](https://github.com/datastax/pulsar/commit/b9d3d6f3a1e)
  \[fix\]\[broker\] DnsResolverUtil.TTL should be greater than zero (#18565)
- [a7d5981ca80](https://github.com/datastax/pulsar/commit/a7d5981ca80)
  \[fix\]\[broker\] Correctly set byte and message out totals per subscription
  (#18451)
- [a12d5186995](https://github.com/datastax/pulsar/commit/a12d5186995)
  \[fix\]\[fn\] fix function failed to start if no `typeClassName` provided in
  `FunctionDetails` (#18111)

### Connectors upgrades

- cloud-storage: 2.10.2.1. It's highly suggested to set the config
  `partitionerUseIndexAsOffset=true`, more details in
  <https://github.com/streamnative/pulsar-io-cloud-storage/pull/470>.

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.6 \| pulsar-io-data-generator-2.10.2.6.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.6 \| pulsar-io-elastic-search-2.10.2.6.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.6 \| pulsar-io-http-2.10.2.6.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.6 \| pulsar-io-jdbc-clickhouse-2.10.2.6.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.6 \| pulsar-io-jdbc-mariadb-2.10.2.6.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.6 \| pulsar-io-jdbc-postgres-2.10.2.6.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.6 \| pulsar-io-jdbc-sqlite-2.10.2.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.6 \| pulsar-io-kafka-2.10.2.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.6 \| pulsar-io-kinesis-2.10.2.6.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.6 \| pulsar-io-data-generator-2.10.2.6.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.6 \| pulsar-io-debezium-mongodb-2.10.2.6.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.6 \| pulsar-io-debezium-mssql-2.10.2.6.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.6 \| pulsar-io-debezium-mysql-2.10.2.6.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.6 \| pulsar-io-debezium-oracle-2.10.2.6.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.6 \| pulsar-io-debezium-postgres-2.10.2.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.6 \| pulsar-io-kafka-2.10.2.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.6 \| pulsar-io-kinesis-2.10.2.6.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.6 \| pulsar-io-aerospike-2.10.2.6.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.6 \|
pulsar-io-batch-data-generator-2.10.2.6.nar \| \|
[cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) \|
Writes data into cloud storage \| 2.10.2.1 \|
pulsar-io-cloud-storage-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.6 \| pulsar-io-data-generator-2.10.2.6.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.6 \| pulsar-io-elastic-search-2.10.2.6.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.6 \| pulsar-io-flume-2.10.2.6.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.6 \| pulsar-io-hbase-2.10.2.6.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.6 \| pulsar-io-hdfs2-2.10.2.6.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.6 \| pulsar-io-hdfs3-2.10.2.6.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.6 \| pulsar-io-http-2.10.2.6.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.6 \| pulsar-io-influxdb-2.10.2.6.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.6 \| pulsar-io-jdbc-clickhouse-2.10.2.6.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.6 \| pulsar-io-jdbc-mariadb-2.10.2.6.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.6 \| pulsar-io-jdbc-postgres-2.10.2.6.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.6 \| pulsar-io-jdbc-sqlite-2.10.2.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.6 \| pulsar-io-kafka-2.10.2.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.6 \| pulsar-io-kinesis-2.10.2.6.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.6 \| pulsar-io-mongo-2.10.2.6.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.6 \| pulsar-io-rabbitmq-2.10.2.6.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.6 \| pulsar-io-redis-2.10.2.6.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.6 \| pulsar-io-solr-2.10.2.6.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.6 \|
pulsar-io-batch-data-generator-2.10.2.6.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.6 \| pulsar-io-canal-2.10.2.6.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.6 \| pulsar-io-data-generator-2.10.2.6.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.6 \| pulsar-io-debezium-mongodb-2.10.2.6.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.6 \| pulsar-io-debezium-mssql-2.10.2.6.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.6 \| pulsar-io-debezium-mysql-2.10.2.6.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.6 \| pulsar-io-debezium-oracle-2.10.2.6.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.6 \| pulsar-io-debezium-postgres-2.10.2.6.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.6 \| pulsar-io-dynamodb-2.10.2.6.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.6 \| pulsar-io-file-2.10.2.6.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.6 \| pulsar-io-flume-2.10.2.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.6 \| pulsar-io-kafka-2.10.2.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.6 \| pulsar-io-kinesis-2.10.2.6.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.6 \| pulsar-io-mongo-2.10.2.6.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.6 \| pulsar-io-netty-2.10.2.6.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.6 \| pulsar-io-nsq-2.10.2.6.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.6 \| pulsar-io-rabbitmq-2.10.2.6.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.6 \| pulsar-io-twitter-2.10.2.6.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>CLI extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- Pulsar Admin Custom Commands \| 3.1.0 \| pulsar-jms-admin-3.1.0-nar.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.5

This is a maintenance release containing important stability updates.

### Most notable commits

- [018d4fa03df](https://github.com/datastax/pulsar/commit/018d4fa03df)
  \[fix\]\[offload\] Fix memory leak while Offloading ledgers (#18500)

### Connectors upgrades

- cloud-storage: 2.9.3.0

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.9.3.0 \| pulsar-io-cloud-storage-2.9.3.0-rc-daily.nar \|
\| [data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.5 \| pulsar-io-data-generator-2.10.2.5.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.5 \| pulsar-io-elastic-search-2.10.2.5.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.5 \| pulsar-io-http-2.10.2.5.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.5 \| pulsar-io-jdbc-clickhouse-2.10.2.5.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.5 \| pulsar-io-jdbc-mariadb-2.10.2.5.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.5 \| pulsar-io-jdbc-postgres-2.10.2.5.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.5 \| pulsar-io-jdbc-sqlite-2.10.2.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.5 \| pulsar-io-kafka-2.10.2.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.5 \| pulsar-io-kinesis-2.10.2.5.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.5 \| pulsar-io-data-generator-2.10.2.5.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.5 \| pulsar-io-debezium-mongodb-2.10.2.5.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.5 \| pulsar-io-debezium-mssql-2.10.2.5.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.5 \| pulsar-io-debezium-mysql-2.10.2.5.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.5 \| pulsar-io-debezium-oracle-2.10.2.5.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.5 \| pulsar-io-debezium-postgres-2.10.2.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.5 \| pulsar-io-kafka-2.10.2.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.5 \| pulsar-io-kinesis-2.10.2.5.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.5 \| pulsar-io-aerospike-2.10.2.5.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.5 \|
pulsar-io-batch-data-generator-2.10.2.5.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.9.3.0 \| pulsar-io-cloud-storage-2.9.3.0-rc-daily.nar \|
\| [data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.5 \| pulsar-io-data-generator-2.10.2.5.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.5 \| pulsar-io-elastic-search-2.10.2.5.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.5 \| pulsar-io-flume-2.10.2.5.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.5 \| pulsar-io-hbase-2.10.2.5.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.5 \| pulsar-io-hdfs2-2.10.2.5.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.5 \| pulsar-io-hdfs3-2.10.2.5.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.5 \| pulsar-io-http-2.10.2.5.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.5 \| pulsar-io-influxdb-2.10.2.5.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.5 \| pulsar-io-jdbc-clickhouse-2.10.2.5.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.5 \| pulsar-io-jdbc-mariadb-2.10.2.5.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.5 \| pulsar-io-jdbc-postgres-2.10.2.5.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.5 \| pulsar-io-jdbc-sqlite-2.10.2.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.5 \| pulsar-io-kafka-2.10.2.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.5 \| pulsar-io-kinesis-2.10.2.5.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.5 \| pulsar-io-mongo-2.10.2.5.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.5 \| pulsar-io-rabbitmq-2.10.2.5.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.5 \| pulsar-io-redis-2.10.2.5.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.5 \| pulsar-io-solr-2.10.2.5.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.5 \|
pulsar-io-batch-data-generator-2.10.2.5.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.5 \| pulsar-io-canal-2.10.2.5.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.5 \| pulsar-io-data-generator-2.10.2.5.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.5 \| pulsar-io-debezium-mongodb-2.10.2.5.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.5 \| pulsar-io-debezium-mssql-2.10.2.5.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.5 \| pulsar-io-debezium-mysql-2.10.2.5.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.5 \| pulsar-io-debezium-oracle-2.10.2.5.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.5 \| pulsar-io-debezium-postgres-2.10.2.5.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.5 \| pulsar-io-dynamodb-2.10.2.5.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.5 \| pulsar-io-file-2.10.2.5.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.5 \| pulsar-io-flume-2.10.2.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.5 \| pulsar-io-kafka-2.10.2.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.5 \| pulsar-io-kinesis-2.10.2.5.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.5 \| pulsar-io-mongo-2.10.2.5.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.5 \| pulsar-io-netty-2.10.2.5.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.5 \| pulsar-io-nsq-2.10.2.5.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.5 \| pulsar-io-rabbitmq-2.10.2.5.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.5 \| pulsar-io-twitter-2.10.2.5.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.4

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [21a609af122](https://github.com/datastax/pulsar/commit/21a609af122)
  \[improve\]\[io\] Upgrade Debezium to 1.9.7
- [684b4eb6959](https://github.com/datastax/pulsar/commit/684b4eb6959)
  \[improve\]\[transactions\] Add command to list transaction coordinators
  (#17522)
- [cf3ae19f1c8](https://github.com/datastax/pulsar/commit/cf3ae19f1c8)
  InflightReadsLimiter - address upstream review comments: Rename onDeallocate
- [3e44119e506](https://github.com/datastax/pulsar/commit/3e44119e506)
  \[fix\]\[sec\] Upgrade jackson-databind to 2.13.4.2 to get rid of
  CVE-2022-42003 (#18394)
- [18d138a2821](https://github.com/datastax/pulsar/commit/18d138a2821)
  \[fix\]\[client\] Support LocalDateTime Conversion (#18334)
- [90b6c21f808](https://github.com/datastax/pulsar/commit/90b6c21f808)
  \[fix\]\[io\] KCA connectors: fix missing runtime dependencies (#18370)
- [22371c22b39](https://github.com/datastax/pulsar/commit/22371c22b39)
  \[improve\]\[broker\]consumer backlog eviction policy should not reset read
  position for consumer (#18037)
- [6a7c5a5fb3c](https://github.com/datastax/pulsar/commit/6a7c5a5fb3c)
  \[fix\]\[client\] Fix NPE of MultiTopicsConsumerImpl due to race condition
  (#18287)
- [558cce2d04f](https://github.com/datastax/pulsar/commit/558cce2d04f)
  \[fix\]\[monitor\] fix metrics string encoding (#18138)
- [6e0a7772073](https://github.com/datastax/pulsar/commit/6e0a7772073) \[fix\]
  Combination of autocreate + forced delete of partitioned topic with active
  consumer leaves topic metadata inconsistent. (#18193)
- [87a33237b1d](https://github.com/datastax/pulsar/commit/87a33237b1d) Ensure
  the deletion consistency of topic and schema (#14608)
- [675f230f724](https://github.com/datastax/pulsar/commit/675f230f724) Clean
  unsed methods in BrokerService (#15257)
- [7ae14562c0d](https://github.com/datastax/pulsar/commit/7ae14562c0d) Make
  TopicLookupBase#internalLookupTopicAsync pure async (#14188)
- [c6af153951b](https://github.com/datastax/pulsar/commit/c6af153951b)
  \[improve\]\[admin\] Make deleteNamesapce api async (#17230)
- [0c9373fbda3](https://github.com/datastax/pulsar/commit/0c9373fbda3)
  \[PIP-143\] Support split bundle by specified boundaries (#13796)
- [d54efc369d4](https://github.com/datastax/pulsar/commit/d54efc369d4)
  \[improve\]\[broker\]\[PIP-149\]make deletePersistence method async in
  Namespaces (#17206)
- [059f444dc3f](https://github.com/datastax/pulsar/commit/059f444dc3f)
  \[Fix\]\[Tiered Storage\] Eagerly Delete Offloaded Segments On Topic Deletion
  (#17915) (#152)
- [79d958b6153](https://github.com/datastax/pulsar/commit/79d958b6153) cleaned
  up dependencies (#18255)
- [270b86a776f](https://github.com/datastax/pulsar/commit/270b86a776f) Add HTTP
  Sink (#17581)
- [b1a699832c7](https://github.com/datastax/pulsar/commit/b1a699832c7)
  \[improve\]\[broker\]prevent partitioned metadata lookup request when broker
  is closing (#17315)
- [c2f7230e663](https://github.com/datastax/pulsar/commit/c2f7230e663)
  \[improve\]\[broker\]prevent new connection request when broker is closing
  (#17314)
- [3197132150d](https://github.com/datastax/pulsar/commit/3197132150d)
  \[improve\]\[broker\]add ServerCnx state check before server handle request
  (#17084)
- [a428bc0df1f](https://github.com/datastax/pulsar/commit/a428bc0df1f)
  \[improve\]\[broker\] fix broker irrational behavior when it is closing
  (#17085)
- [1841990237a](https://github.com/datastax/pulsar/commit/1841990237a) Fix NPE
  when ResourceGroupService execute scheduled task. (#17840)
- [8efc9bba3b9](https://github.com/datastax/pulsar/commit/8efc9bba3b9)
  \[branch-2.10\]\[cpp\] Fix zlib dowload path. (#18136)
- [43867ec6882](https://github.com/datastax/pulsar/commit/43867ec6882)
  \[fix\]\[storage\] Autorecovery default reppDnsResolverClass to
  ZkBookieRackAffinityMapping (#15640)
- [49130915c38](https://github.com/datastax/pulsar/commit/49130915c38)
  \[fix\]\[broker\]Cache invalidation due to concurrent access (#18076)
- [2a3c3ca9585](https://github.com/datastax/pulsar/commit/2a3c3ca9585)
  PendingReadsManager - release the used memory count on Entry.deallocate
- [76f2fa95646](https://github.com/datastax/pulsar/commit/76f2fa95646)
  \[broker\] Fixed delayed delivery after read operation error (#18098)
- [5ab45e988ac](https://github.com/datastax/pulsar/commit/5ab45e988ac)
  \[improve\]\[fn\] Run connectors extraction in parallel (#17902)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.4 \| pulsar-io-data-generator-2.10.2.4.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.4 \| pulsar-io-elastic-search-2.10.2.4.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.4 \| pulsar-io-http-2.10.2.4.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.4 \| pulsar-io-jdbc-clickhouse-2.10.2.4.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.4 \| pulsar-io-jdbc-mariadb-2.10.2.4.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.4 \| pulsar-io-jdbc-postgres-2.10.2.4.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.4 \| pulsar-io-jdbc-sqlite-2.10.2.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.4 \| pulsar-io-kafka-2.10.2.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.4 \| pulsar-io-kinesis-2.10.2.4.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.4 \| pulsar-io-data-generator-2.10.2.4.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.4 \| pulsar-io-debezium-mongodb-2.10.2.4.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.4 \| pulsar-io-debezium-mssql-2.10.2.4.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.4 \| pulsar-io-debezium-mysql-2.10.2.4.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.4 \| pulsar-io-debezium-oracle-2.10.2.4.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.4 \| pulsar-io-debezium-postgres-2.10.2.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.4 \| pulsar-io-kafka-2.10.2.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.4 \| pulsar-io-kinesis-2.10.2.4.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.7 \|
cassandra-enhanced-pulsar-sink-1.6.7-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.4 \| pulsar-io-aerospike-2.10.2.4.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.4 \|
pulsar-io-batch-data-generator-2.10.2.4.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.4 \| pulsar-io-data-generator-2.10.2.4.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.4 \| pulsar-io-elastic-search-2.10.2.4.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.4 \| pulsar-io-flume-2.10.2.4.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.4 \| pulsar-io-hbase-2.10.2.4.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.4 \| pulsar-io-hdfs2-2.10.2.4.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.4 \| pulsar-io-hdfs3-2.10.2.4.nar \| \|
[http](https://pulsar.apache.org/docs/io-connectors) \| Writes data to an HTTP
server (Webhook) \| 2.10.2.4 \| pulsar-io-http-2.10.2.4.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.4 \| pulsar-io-influxdb-2.10.2.4.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.4 \| pulsar-io-jdbc-clickhouse-2.10.2.4.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.4 \| pulsar-io-jdbc-mariadb-2.10.2.4.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.4 \| pulsar-io-jdbc-postgres-2.10.2.4.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.4 \| pulsar-io-jdbc-sqlite-2.10.2.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.4 \| pulsar-io-kafka-2.10.2.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.4 \| pulsar-io-kinesis-2.10.2.4.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.4 \| pulsar-io-mongo-2.10.2.4.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.4 \| pulsar-io-rabbitmq-2.10.2.4.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.4 \| pulsar-io-redis-2.10.2.4.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.4 \| pulsar-io-solr-2.10.2.4.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.13 \| pulsar-snowflake-connector-0.1.13-alpha.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.2 \| pulsar-cassandra-source-2.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.4 \|
pulsar-io-batch-data-generator-2.10.2.4.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.4 \| pulsar-io-canal-2.10.2.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.4 \| pulsar-io-data-generator-2.10.2.4.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.4 \| pulsar-io-debezium-mongodb-2.10.2.4.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.4 \| pulsar-io-debezium-mssql-2.10.2.4.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.4 \| pulsar-io-debezium-mysql-2.10.2.4.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.4 \| pulsar-io-debezium-oracle-2.10.2.4.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.4 \| pulsar-io-debezium-postgres-2.10.2.4.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.4 \| pulsar-io-dynamodb-2.10.2.4.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.4 \| pulsar-io-file-2.10.2.4.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.4 \| pulsar-io-flume-2.10.2.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.4 \| pulsar-io-kafka-2.10.2.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.4 \| pulsar-io-kinesis-2.10.2.4.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.4 \| pulsar-io-mongo-2.10.2.4.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.4 \| pulsar-io-netty-2.10.2.4.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.4 \| pulsar-io-nsq-2.10.2.4.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.4 \| pulsar-io-rabbitmq-2.10.2.4.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.4 \| pulsar-io-twitter-2.10.2.4.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.5 \| pulsar-kafka-proxy-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.2 \|
starlight-rabbitmq-2.10.0.2.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.5 \| pulsar-protocol-handler-kafka-2.10.0.5.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.2 \| starlight-rabbitmq-2.10.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.1.0 \| pulsar-jms-3.1.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.2 \| pulsar-transformations-2.0.2.nar \|

</details>


## Luna Streaming Distribution 2.10 2.3

This is a maintenance release containing important security updates.

### Most notable commits

- [8738cdb5263](https://github.com/datastax/pulsar/commit/8738cdb5263)
  \[fix\]\[sec\] Upgrade protobuf to 3.19.6 to get rid of CVE-2022-3171 (#18086)
- [87d89e1e120](https://github.com/datastax/pulsar/commit/87d89e1e120)
  \[fix\]\[sec\] Upgrade commons-text to 1.10.0 in the kinesis-sink (#18093)
- [1d2c003c232](https://github.com/datastax/pulsar/commit/1d2c003c232)
  \[improve\]\[io\] JDBC Sink: add flag to exclude non declared fields (#18008)
- [201d70fb88f](https://github.com/datastax/pulsar/commit/201d70fb88f)
  \[feature\]\[pulsar-io\] Support transactions for JDBC connector (#16468)
- [3e2bb0a2c6e](https://github.com/datastax/pulsar/commit/3e2bb0a2c6e)
  \[fix\]\[connector\] JDBC sinks: verify key and nonKey fields are set with
  insertMode=UPSERT (#17950)
- [3f84f157026](https://github.com/datastax/pulsar/commit/3f84f157026)
  \[improve\]\[connector\] JDBC sink: allow any jdbc driver (#17951)
- [55f80c52c05](https://github.com/datastax/pulsar/commit/55f80c52c05) Bump
  commons-text to 1.10.0 (#18053)
- [4119e549322](https://github.com/datastax/pulsar/commit/4119e549322)
  \[fix\]\[sec\] File tiered storage: upgrade jettison to get rid of
  CVE-2022-40149 (#18022)
- [2405cb320b5](https://github.com/datastax/pulsar/commit/2405cb320b5)
  \[fix\]\[sec\] Upgrade JacksonXML to 2.13.4 (#18020)
- [b4d05d91d67](https://github.com/datastax/pulsar/commit/b4d05d91d67) Bump
  jackson version from 2.13.2 to 2.13.3 (#16508)
- [a2080693596](https://github.com/datastax/pulsar/commit/a2080693596)
  \[fix\]\[broker\] Make full async call in PulsarAuthorizationProvider (#18050)
- [65aea80f728](https://github.com/datastax/pulsar/commit/65aea80f728)
  \[fix\]\[metrics\] fixed ProxyStats to use common.stats.JvmMetrics (#15692)
- [c3dba744313](https://github.com/datastax/pulsar/commit/c3dba744313)
  \[fix\]\[io\] Fix builtin connector/function download filename (#18044)
- [764f60f9e1c](https://github.com/datastax/pulsar/commit/764f60f9e1c)
  \[fix\]\[connectors\] Fix builtin sink transformation on k8s
- [79d794cd11a](https://github.com/datastax/pulsar/commit/79d794cd11a)
  PendingReadsLimiter - address some review comments
- [bfd3b85dfa9](https://github.com/datastax/pulsar/commit/bfd3b85dfa9)
  \[fix\]\[broker\] Fix system service namespace create internal event topic.
  (#17867)
- [c3c473ee616](https://github.com/datastax/pulsar/commit/c3c473ee616) Limit the
  number of pending requests to BookKeeper to save the broker from OODM (#146)
- [06da3b8590c](https://github.com/datastax/pulsar/commit/06da3b8590c)
  \[improve\]\[client\] Refactor SchemaHash to reduce call of hashFunction in
  SchemaHash (#17948)
- [15c1fe903d9](https://github.com/datastax/pulsar/commit/15c1fe903d9)
  \[broker\] ServerCnx: log at warning level when topic not found (#16225)
- [035aeb45c2f](https://github.com/datastax/pulsar/commit/035aeb45c2f)
  \[fix\]\[bookie\] Correctly handle list configuration values (#17661)
- [afa95cc96d5](https://github.com/datastax/pulsar/commit/afa95cc96d5) Allow to
  configure and disable the size of lookahead for detecting fixed delays in
  messages (#17907)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.3 \| pulsar-io-data-generator-2.10.2.3.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.3 \| pulsar-io-elastic-search-2.10.2.3.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.3 \| pulsar-io-jdbc-clickhouse-2.10.2.3.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.3 \| pulsar-io-jdbc-mariadb-2.10.2.3.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.3 \| pulsar-io-jdbc-postgres-2.10.2.3.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.3 \| pulsar-io-jdbc-sqlite-2.10.2.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.3 \| pulsar-io-kafka-2.10.2.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.3 \| pulsar-io-kinesis-2.10.2.3.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.12 \| pulsar-snowflake-connector-0.1.12.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.3 \| pulsar-io-data-generator-2.10.2.3.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.3 \| pulsar-io-debezium-mongodb-2.10.2.3.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.3 \| pulsar-io-debezium-mssql-2.10.2.3.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.3 \| pulsar-io-debezium-mysql-2.10.2.3.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.3 \| pulsar-io-debezium-oracle-2.10.2.3.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.3 \| pulsar-io-debezium-postgres-2.10.2.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.3 \| pulsar-io-kafka-2.10.2.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.3 \| pulsar-io-kinesis-2.10.2.3.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.1 \| pulsar-transformations-2.0.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.3 \| pulsar-io-aerospike-2.10.2.3.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.3 \|
pulsar-io-batch-data-generator-2.10.2.3.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.3 \| pulsar-io-data-generator-2.10.2.3.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.3 \| pulsar-io-elastic-search-2.10.2.3.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.3 \| pulsar-io-flume-2.10.2.3.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.3 \| pulsar-io-hbase-2.10.2.3.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.3 \| pulsar-io-hdfs2-2.10.2.3.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.3 \| pulsar-io-hdfs3-2.10.2.3.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.3 \| pulsar-io-influxdb-2.10.2.3.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.3 \| pulsar-io-jdbc-clickhouse-2.10.2.3.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.3 \| pulsar-io-jdbc-mariadb-2.10.2.3.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.3 \| pulsar-io-jdbc-postgres-2.10.2.3.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.3 \| pulsar-io-jdbc-sqlite-2.10.2.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.3 \| pulsar-io-kafka-2.10.2.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.3 \| pulsar-io-kinesis-2.10.2.3.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.3 \| pulsar-io-mongo-2.10.2.3.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.3 \| pulsar-io-rabbitmq-2.10.2.3.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.3 \| pulsar-io-redis-2.10.2.3.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.3 \| pulsar-io-solr-2.10.2.3.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.12 \| pulsar-snowflake-connector-0.1.12.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.3 \|
pulsar-io-batch-data-generator-2.10.2.3.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.3 \| pulsar-io-canal-2.10.2.3.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.3 \| pulsar-io-data-generator-2.10.2.3.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.3 \| pulsar-io-debezium-mongodb-2.10.2.3.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.3 \| pulsar-io-debezium-mssql-2.10.2.3.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.3 \| pulsar-io-debezium-mysql-2.10.2.3.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.3 \| pulsar-io-debezium-oracle-2.10.2.3.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.3 \| pulsar-io-debezium-postgres-2.10.2.3.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.3 \| pulsar-io-dynamodb-2.10.2.3.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.3 \| pulsar-io-file-2.10.2.3.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.3 \| pulsar-io-flume-2.10.2.3.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.3 \| pulsar-io-kafka-2.10.2.3.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.3 \| pulsar-io-kinesis-2.10.2.3.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.3 \| pulsar-io-mongo-2.10.2.3.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.3 \| pulsar-io-netty-2.10.2.3.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.3 \| pulsar-io-nsq-2.10.2.3.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.3 \| pulsar-io-rabbitmq-2.10.2.3.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.3 \| pulsar-io-twitter-2.10.2.3.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.1 \| pulsar-transformations-2.0.1.nar \|

</details>


## Luna Streaming Distribution 2.10 2.2

This is a maintenance release containing important stability updates.

### Most notable commits

- [75b7f1f2a62](https://github.com/datastax/pulsar/commit/75b7f1f2a62)
  \[bug\]\[broker\] fix memory leak in case of error conditions in
  PendingReadsManager
- [efcffe54ec3](https://github.com/datastax/pulsar/commit/efcffe54ec3) Add
  option to flatten JSON with FULL_MESSAGE_IN_JSON_EXPAND_VALUE format (#14993)
- [b4834e99178](https://github.com/datastax/pulsar/commit/b4834e99178)
  \[fix\]\[connector\] Kinesis sink: fix NPE with KeyValue schema and no value
  (#17959)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.2 \| pulsar-io-data-generator-2.10.2.2.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.2 \| pulsar-io-elastic-search-2.10.2.2.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.2 \| pulsar-io-jdbc-clickhouse-2.10.2.2.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.2 \| pulsar-io-jdbc-mariadb-2.10.2.2.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.2 \| pulsar-io-jdbc-postgres-2.10.2.2.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.2 \| pulsar-io-jdbc-sqlite-2.10.2.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.2 \| pulsar-io-kafka-2.10.2.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.2 \| pulsar-io-kinesis-2.10.2.2.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.12 \| pulsar-snowflake-connector-0.1.12.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.2 \| pulsar-io-data-generator-2.10.2.2.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.2 \| pulsar-io-debezium-mongodb-2.10.2.2.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.2 \| pulsar-io-debezium-mssql-2.10.2.2.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.2 \| pulsar-io-debezium-mysql-2.10.2.2.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.2 \| pulsar-io-debezium-oracle-2.10.2.2.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.2 \| pulsar-io-debezium-postgres-2.10.2.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.2 \| pulsar-io-kafka-2.10.2.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.2 \| pulsar-io-kinesis-2.10.2.2.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.2 \| pulsar-io-aerospike-2.10.2.2.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.2 \|
pulsar-io-batch-data-generator-2.10.2.2.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.2 \| pulsar-io-data-generator-2.10.2.2.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.2 \| pulsar-io-elastic-search-2.10.2.2.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.2 \| pulsar-io-flume-2.10.2.2.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.2 \| pulsar-io-hbase-2.10.2.2.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.2 \| pulsar-io-hdfs2-2.10.2.2.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.2 \| pulsar-io-hdfs3-2.10.2.2.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.2 \| pulsar-io-influxdb-2.10.2.2.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.2 \| pulsar-io-jdbc-clickhouse-2.10.2.2.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.2 \| pulsar-io-jdbc-mariadb-2.10.2.2.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.2 \| pulsar-io-jdbc-postgres-2.10.2.2.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.2 \| pulsar-io-jdbc-sqlite-2.10.2.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.2 \| pulsar-io-kafka-2.10.2.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.2 \| pulsar-io-kinesis-2.10.2.2.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.2 \| pulsar-io-mongo-2.10.2.2.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.2 \| pulsar-io-rabbitmq-2.10.2.2.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.2 \| pulsar-io-redis-2.10.2.2.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.2 \| pulsar-io-solr-2.10.2.2.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.12 \| pulsar-snowflake-connector-0.1.12.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.2.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.2.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.2.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.2.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.2.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.2.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.2.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.2.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.2.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.2.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.2.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.2.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.2.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.2.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.2.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.2.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.2.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.2.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.2.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.2.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.2.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.2 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.2.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.2.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.2.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.2 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.2.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.2 \|
pulsar-io-batch-data-generator-2.10.2.2.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.2 \| pulsar-io-canal-2.10.2.2.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.2 \| pulsar-io-data-generator-2.10.2.2.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.2 \| pulsar-io-debezium-mongodb-2.10.2.2.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.2 \| pulsar-io-debezium-mssql-2.10.2.2.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.2 \| pulsar-io-debezium-mysql-2.10.2.2.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.2 \| pulsar-io-debezium-oracle-2.10.2.2.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.2 \| pulsar-io-debezium-postgres-2.10.2.2.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.2 \| pulsar-io-dynamodb-2.10.2.2.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.2 \| pulsar-io-file-2.10.2.2.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.2 \| pulsar-io-flume-2.10.2.2.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.2 \| pulsar-io-kafka-2.10.2.2.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.2 \| pulsar-io-kinesis-2.10.2.2.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.2 \| pulsar-io-mongo-2.10.2.2.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.2 \| pulsar-io-netty-2.10.2.2.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.2 \| pulsar-io-nsq-2.10.2.2.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.2 \| pulsar-io-rabbitmq-2.10.2.2.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.2 \| pulsar-io-twitter-2.10.2.2.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


## Luna Streaming Distribution 2.10 2.1

This is a maintenance release containing important stability updates.

### Most notable commits

- [424b950f8d3](https://github.com/datastax/pulsar/commit/424b950f8d3)
  \[fix\]\[metadata\] Handle session events in separate thread (#17638)
- [f1e697d4ff4](https://github.com/datastax/pulsar/commit/f1e697d4ff4)
  \[fix\]\[broker\] Fix the broker shutdown issue after Zookeeper node crashed
  (#17909)
- [95494b4f42e](https://github.com/datastax/pulsar/commit/95494b4f42e) Revert
  "Make BookieId work with PulsarRegistrationDriver (#138)"

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.1 \| pulsar-io-data-generator-2.10.2.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.1 \| pulsar-io-elastic-search-2.10.2.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.1 \| pulsar-io-jdbc-clickhouse-2.10.2.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.1 \| pulsar-io-jdbc-mariadb-2.10.2.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.1 \| pulsar-io-jdbc-postgres-2.10.2.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.1 \| pulsar-io-jdbc-sqlite-2.10.2.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.1 \| pulsar-io-kafka-2.10.2.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.1 \| pulsar-io-kinesis-2.10.2.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.1 \| pulsar-io-data-generator-2.10.2.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.1 \| pulsar-io-debezium-mongodb-2.10.2.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.1 \| pulsar-io-debezium-mssql-2.10.2.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.1 \| pulsar-io-debezium-mysql-2.10.2.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.1 \| pulsar-io-debezium-oracle-2.10.2.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.1 \| pulsar-io-debezium-postgres-2.10.2.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.1 \| pulsar-io-kafka-2.10.2.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.1 \| pulsar-io-kinesis-2.10.2.1.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.1 \| pulsar-io-aerospike-2.10.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.1 \|
pulsar-io-batch-data-generator-2.10.2.1.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.1 \| pulsar-io-data-generator-2.10.2.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.1 \| pulsar-io-elastic-search-2.10.2.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.1 \| pulsar-io-flume-2.10.2.1.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.1 \| pulsar-io-hbase-2.10.2.1.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.1 \| pulsar-io-hdfs2-2.10.2.1.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.1 \| pulsar-io-hdfs3-2.10.2.1.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.1 \| pulsar-io-influxdb-2.10.2.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.1 \| pulsar-io-jdbc-clickhouse-2.10.2.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.1 \| pulsar-io-jdbc-mariadb-2.10.2.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.1 \| pulsar-io-jdbc-postgres-2.10.2.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.1 \| pulsar-io-jdbc-sqlite-2.10.2.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.1 \| pulsar-io-kafka-2.10.2.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.1 \| pulsar-io-kinesis-2.10.2.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.1 \| pulsar-io-mongo-2.10.2.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.1 \| pulsar-io-rabbitmq-2.10.2.1.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.1 \| pulsar-io-redis-2.10.2.1.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.1 \| pulsar-io-solr-2.10.2.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.1 \|
pulsar-io-batch-data-generator-2.10.2.1.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.1 \| pulsar-io-canal-2.10.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.1 \| pulsar-io-data-generator-2.10.2.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.1 \| pulsar-io-debezium-mongodb-2.10.2.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.1 \| pulsar-io-debezium-mssql-2.10.2.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.1 \| pulsar-io-debezium-mysql-2.10.2.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.1 \| pulsar-io-debezium-oracle-2.10.2.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.1 \| pulsar-io-debezium-postgres-2.10.2.1.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.1 \| pulsar-io-dynamodb-2.10.2.1.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.1 \| pulsar-io-file-2.10.2.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.1 \| pulsar-io-flume-2.10.2.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.1 \| pulsar-io-kafka-2.10.2.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.1 \| pulsar-io-kinesis-2.10.2.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.1 \| pulsar-io-mongo-2.10.2.1.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.1 \| pulsar-io-netty-2.10.2.1.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.1 \| pulsar-io-nsq-2.10.2.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.1 \| pulsar-io-rabbitmq-2.10.2.1.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.1 \| pulsar-io-twitter-2.10.2.1.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


## Luna Streaming Distribution 2.10 2.0

This is a maintenance release containing important security and stability
updates. NOTE: It is highly suggested to upgrade to Luna Streaming Distribution
2.10 2.1 due to stability issues.

### Most notable commits

- [35d3f6be84c](https://github.com/datastax/pulsar/commit/35d3f6be84c) Add CLI
  command to get available built-in functions (#16822)
- [4bd86dcfa98](https://github.com/datastax/pulsar/commit/4bd86dcfa98) Add CLI
  command to reload built-in functions (#17102)
- [00fe3ed3a57](https://github.com/datastax/pulsar/commit/00fe3ed3a57)
  \[fix\]\[functions\] Fix the download of builtin Functions (#17877)
- [9058375d16c](https://github.com/datastax/pulsar/commit/9058375d16c)
  \[fix\]\[broker\]Consumer can't consume messages because there has two sames
  topics in one broker (#17526)
- [a26e2c1da9b](https://github.com/datastax/pulsar/commit/a26e2c1da9b)
  \[fix\]\[tiered-storage\] Don't cleanup data when offload met Metastore
  exception (#17512)
- [6469b8d9ded](https://github.com/datastax/pulsar/commit/6469b8d9ded)
  \[fix\]\[storage\]fix OpAddEntry release error when exception in
  ManagedLedgerInterceptor (#17394)
- [1e8eef32abd](https://github.com/datastax/pulsar/commit/1e8eef32abd)
  \[fix\]\[build\] duplicate entry when merging services (#17659)
- [b6815cb0584](https://github.com/datastax/pulsar/commit/b6815cb0584)
  \[fix\]\[broker\] Fix namespace backlog quota check with retention. (#17706)
- [404953f3403](https://github.com/datastax/pulsar/commit/404953f3403)
  \[fix\]\[metadata\] Don't execute Bookkeeper metadata callbacks on Zookeeper
  event thread (#17620)
- [526de9f524e](https://github.com/datastax/pulsar/commit/526de9f524e)
  \[fix\]\[tableview\] fixed ack failure in ReaderImpl due to null messageId
  (#17728) (#17828)
- [ea183f355e2](https://github.com/datastax/pulsar/commit/ea183f355e2)
  \[improve\]\[broker\] Make MessageRedeliveryController work more efficiently
  (#17804)
- [d3f4c4ae7f3](https://github.com/datastax/pulsar/commit/d3f4c4ae7f3)
  \[improve\]\[loadbalance\] added loadBalancerReportUpdateMinIntervalMillis and
  ignores memory usage in getMaxResourceUsage() (#17598)
- [ba3c1d7837f](https://github.com/datastax/pulsar/commit/ba3c1d7837f) Make
  BookieId work with PulsarRegistrationDriver (#138)
- [84d4f08a6eb](https://github.com/datastax/pulsar/commit/84d4f08a6eb)
  \[improve\]\[pulsar-io-kafka\] Add option to copy Kafka headers to Pulsar
  properties (#17829)
- [7d07754ebb7](https://github.com/datastax/pulsar/commit/7d07754ebb7) fix kafla
  source config when consumerConfigProperties='' (#16731)
- [19769d4308e](https://github.com/datastax/pulsar/commit/19769d4308e)
  \[fix\]\[sec\] Bump snakeyaml to 1.32 for CVE-2022-38752 (#17779)
- [d0d96ec1907](https://github.com/datastax/pulsar/commit/d0d96ec1907)
  \[fix\]\[connector\] KCA: use reflection to get pulsar-client impl classes

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.0 \| pulsar-io-data-generator-2.10.2.0.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.0 \| pulsar-io-elastic-search-2.10.2.0.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.0 \| pulsar-io-jdbc-clickhouse-2.10.2.0.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.0 \| pulsar-io-jdbc-mariadb-2.10.2.0.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.0 \| pulsar-io-jdbc-postgres-2.10.2.0.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.0 \| pulsar-io-jdbc-sqlite-2.10.2.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.0 \| pulsar-io-kafka-2.10.2.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.0 \| pulsar-io-kinesis-2.10.2.0.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.0 \| pulsar-io-data-generator-2.10.2.0.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.0 \| pulsar-io-debezium-mongodb-2.10.2.0.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.0 \| pulsar-io-debezium-mssql-2.10.2.0.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.0 \| pulsar-io-debezium-mysql-2.10.2.0.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.0 \| pulsar-io-debezium-oracle-2.10.2.0.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.0 \| pulsar-io-debezium-postgres-2.10.2.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.0 \| pulsar-io-kafka-2.10.2.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.0 \| pulsar-io-kinesis-2.10.2.0.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.6 \|
cassandra-enhanced-pulsar-sink-1.6.6-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.2.0 \| pulsar-io-aerospike-2.10.2.0.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.0 \|
pulsar-io-batch-data-generator-2.10.2.0.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.0 \| pulsar-io-data-generator-2.10.2.0.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.2.0 \| pulsar-io-elastic-search-2.10.2.0.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.0 \| pulsar-io-flume-2.10.2.0.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.2.0 \| pulsar-io-hbase-2.10.2.0.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.2.0 \| pulsar-io-hdfs2-2.10.2.0.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.2.0 \| pulsar-io-hdfs3-2.10.2.0.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.2.0 \| pulsar-io-influxdb-2.10.2.0.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.2.0 \| pulsar-io-jdbc-clickhouse-2.10.2.0.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.2.0 \| pulsar-io-jdbc-mariadb-2.10.2.0.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.2.0 \| pulsar-io-jdbc-postgres-2.10.2.0.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.2.0 \| pulsar-io-jdbc-sqlite-2.10.2.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.0 \| pulsar-io-kafka-2.10.2.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.0 \| pulsar-io-kinesis-2.10.2.0.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.0 \| pulsar-io-mongo-2.10.2.0.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.0 \| pulsar-io-rabbitmq-2.10.2.0.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.2.0 \| pulsar-io-redis-2.10.2.0.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.2.0 \| pulsar-io-solr-2.10.2.0.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.2.0 \|
pulsar-io-batch-data-generator-2.10.2.0.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.2.0 \| pulsar-io-canal-2.10.2.0.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.2.0 \| pulsar-io-data-generator-2.10.2.0.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.2.0 \| pulsar-io-debezium-mongodb-2.10.2.0.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.2.0 \| pulsar-io-debezium-mssql-2.10.2.0.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.2.0 \| pulsar-io-debezium-mysql-2.10.2.0.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.2.0 \| pulsar-io-debezium-oracle-2.10.2.0.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.2.0 \| pulsar-io-debezium-postgres-2.10.2.0.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.2.0 \| pulsar-io-dynamodb-2.10.2.0.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.2.0 \| pulsar-io-file-2.10.2.0.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.2.0 \| pulsar-io-flume-2.10.2.0.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.2.0 \| pulsar-io-kafka-2.10.2.0.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.2.0 \| pulsar-io-kinesis-2.10.2.0.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.2.0 \| pulsar-io-mongo-2.10.2.0.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.2.0 \| pulsar-io-netty-2.10.2.0.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.2.0 \| pulsar-io-nsq-2.10.2.0.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.2.0 \| pulsar-io-rabbitmq-2.10.2.0.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.2.0 \| pulsar-io-twitter-2.10.2.0.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 3.0.0 \| pulsar-jms-3.0.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


## Luna Streaming Distribution 2.10 1.7

This is a maintenance release containing important stability and security
updates.

### Most notable commits

- [b8350485432](https://github.com/datastax/pulsar/commit/b8350485432) Fix NPE
  on subscriptions-visual-stats command
- [1aa6c7c285a](https://github.com/datastax/pulsar/commit/1aa6c7c285a)
  \[feat\]\[build\] Print out more info for bin/pulsar version (#17752)
- [84927f724f4](https://github.com/datastax/pulsar/commit/84927f724f4)
  ManagedLedger: move to FENCED state in case of BadVersionException
- [69b47127428](https://github.com/datastax/pulsar/commit/69b47127428)
  \[fix\]\[security\] Upgrade reload4j in file-system offloader (#17716)
- [d4a829ae970](https://github.com/datastax/pulsar/commit/d4a829ae970)
  \[fix\]\[broker\] Fix stats-internal with option -m cause active ledger
  recover then close (#16662)
- [7c50e4114e0](https://github.com/datastax/pulsar/commit/7c50e4114e0) Add tests
  for PendingReadsManager
- [7dde1e45302](https://github.com/datastax/pulsar/commit/7dde1e45302)
  \[improve\]\[sec\] suppress CVE-2021-3563 of openstack-keystone-2.5.0 (#17458)
- [7544def154c](https://github.com/datastax/pulsar/commit/7544def154c) Update
  proxy lookup throw exception type (#17600)
- [359c0c3991e](https://github.com/datastax/pulsar/commit/359c0c3991e)
  \[fix\]\[cpp\] Fix libcurl build failure when building deb package (#17614)
- [f17a59ceefd](https://github.com/datastax/pulsar/commit/f17a59ceefd)
  \[improve\]\[cpp\] Upgrade OpenSSL to version 1.1.1n (#17538)
- [b3041302669](https://github.com/datastax/pulsar/commit/b3041302669)
  \[improve\]\[broker\] Cancel the loadShedding task when closing pulsar service
  (#17632)
- [85ec13d7f17](https://github.com/datastax/pulsar/commit/85ec13d7f17)
  \[fix\]\[functions\] Ensure InternalConfigurationData data model is compatible
  across different versions (#17690)
- [2cfa182bb4a](https://github.com/datastax/pulsar/commit/2cfa182bb4a)
  \[fix\]\[metadata\] Cleanup state when lock revalidation gets
  `LockBusyException` (#17700)
- [58b501114b5](https://github.com/datastax/pulsar/commit/58b501114b5)
  \[fix\]\[schema\]ledger handle leak when update schema (#17283)
- [f15b2f2d0c6](https://github.com/datastax/pulsar/commit/f15b2f2d0c6) Update
  BookKeeper to 4.14.5.1.0.3
- [0c72bb2f95e](https://github.com/datastax/pulsar/commit/0c72bb2f95e)
  \[improve\]\[broker\] Make log flushing configurable in Pulsar broker (#17591)
- [f1d72bfcf1f](https://github.com/datastax/pulsar/commit/f1d72bfcf1f)
  \[fix\]\[metadata\] Set revalidateAfterReconnection true for certain failures
  (#17664)
- [f394cc85578](https://github.com/datastax/pulsar/commit/f394cc85578)
  \[improve\]\[cli\] Pulsar shell: add command to set/get property of a config
  (#17651)
- [7bba51fab21](https://github.com/datastax/pulsar/commit/7bba51fab21) \[cli\]
  Topic subscriptions visualizer (#133)
- [1f9283971ff](https://github.com/datastax/pulsar/commit/1f9283971ff)
  \[fix\]\[broker\] Fix the broker close hanged issue. (#15755) (#17689)
- [957a16b3411](https://github.com/datastax/pulsar/commit/957a16b3411)
  \[PIP-152\] Support subscription level dispatch rate limiter setting. (#15295)
- [0e409f06283](https://github.com/datastax/pulsar/commit/0e409f06283) Move
  normalize in DispatchRateImpl (#14737)
- [770684e85d8](https://github.com/datastax/pulsar/commit/770684e85d8)
  \[Broker\] Tidy up code about dispatchRate (#14594)
- [ba47adb71e1](https://github.com/datastax/pulsar/commit/ba47adb71e1)
  \[fix\]\[broker\] Avoid storing `MessageMetadata` instances returned by
  `peekMessageMetadata` (#15983)
- [2e628248a9a](https://github.com/datastax/pulsar/commit/2e628248a9a)
  \[refactor\]\[broker\] Remove EntryWrapper usages and use MessageMetadata
  instead (#15967)
- [522dfd8c509](https://github.com/datastax/pulsar/commit/522dfd8c509)
  \[feat\]\[broker\] Add config to count filtered entries towards rate limits
  (#132)
- [dff29cfa757](https://github.com/datastax/pulsar/commit/dff29cfa757)
  \[improve\]\[cli\] Pulsar shell: allow to create a new config (--file) with a
  relative path (#17675)
- [c2684ab4776](https://github.com/datastax/pulsar/commit/c2684ab4776) \[C++\]
  Reset `havePendingPingRequest` flag for any data received from broker (#17658)
- [562f2d464d3](https://github.com/datastax/pulsar/commit/562f2d464d3)
  \[fix\]\[admin\] Add SNI header when tlsHostnameVerification is not enabled
  (#17543)
- [382e9aa2d49](https://github.com/datastax/pulsar/commit/382e9aa2d49)
  \[fix\]\[cpp\] Fix potential segfault when resending messages (#17395)
- [6bc7cf8d7d5](https://github.com/datastax/pulsar/commit/6bc7cf8d7d5)
  \[fix\]\[client\]Fix scheduledExecutorProvider not shutdown (#17527)
- [91471e7f391](https://github.com/datastax/pulsar/commit/91471e7f391)
  \[refactor\]\[client c++\] Delete PartitionedConsumerImpl, use
  MultiTopicsConsumerImpl instead (#16969)
- [829034fea69](https://github.com/datastax/pulsar/commit/829034fea69) Move into
  future stage to catch the exception (#17556)
- [052da7056d5](https://github.com/datastax/pulsar/commit/052da7056d5)
  \[fix\]\[broker\] Topic policy reader can't recover when get any exception
  (#17562)
- [366354230e1](https://github.com/datastax/pulsar/commit/366354230e1)
  \[fix\]\[broker\] Multiple consumer dispatcher stuck when `unackedMessages`
  greater than `maxUnackedMessages` (#17483)
- [25f5c1e791a](https://github.com/datastax/pulsar/commit/25f5c1e791a) \[ci\]
  Remove post-commit trigger for old release branches (#17570)
- [d9365868930](https://github.com/datastax/pulsar/commit/d9365868930)
  \[improve\]\[broker\] Improve cursor.getNumberOfEntries if
  isUnackedRangesOpenCacheSetEnabled=true (#17465)
- [6ad65051726](https://github.com/datastax/pulsar/commit/6ad65051726)
  \[fix\]\[broker\] Fix the replicator unnecessary get schema request for bytes
  schema (#17523)
- [7982b468809](https://github.com/datastax/pulsar/commit/7982b468809)
  \[fix\]\[broker\]fail to update partition meta of topic due to
  ConflictException: subscription already exists for topic (#17488)
- [b9c3bde213e](https://github.com/datastax/pulsar/commit/b9c3bde213e)
  \[Branch-2.10\] \[fix\]\[ML\] Fix offload read handle NPE. (#17478)
- [0f8c9aab496](https://github.com/datastax/pulsar/commit/0f8c9aab496)
  \[fix\]\[admin\] Fix unWarp Exception when getPoliciesAsync (#17249)
- [1b517297e97](https://github.com/datastax/pulsar/commit/1b517297e97)
  \[fix\]\[tool\] Using int instead of long in python scriptsc (#17215)
- [41100a10d9c](https://github.com/datastax/pulsar/commit/41100a10d9c)
  \[fix\]\[flaky-test\] Fix flaky test testBacklogNoDelayedForPartitionedTopic
  (#17180)
- [f99ee6885a4](https://github.com/datastax/pulsar/commit/f99ee6885a4)
  \[fix\]\[flay-test\]BrokerInterceptorTest.testProducerCreation (#17159)
- [5a12199d8f9](https://github.com/datastax/pulsar/commit/5a12199d8f9)
  \[fix\]\[flaky-test\]AdminApi2Test.testDeleteNamespace (#17157)
- [b92f0029116](https://github.com/datastax/pulsar/commit/b92f0029116)
  \[fix\]\[flaky-test\]ConsumedLedgersTrimTest (#17116)
- [74ed03c84ba](https://github.com/datastax/pulsar/commit/74ed03c84ba)
  \[fix\]\[flaky-test\] Fix DefaultMessageFormatter.formatMessage (#17104)
- [e528c55e014](https://github.com/datastax/pulsar/commit/e528c55e014)
  \[fix\]\[sql\]Fix presto sql avro decode error when publish non-batched msgs
  (#17093)
- [241ada67fd7](https://github.com/datastax/pulsar/commit/241ada67fd7)
  \[fix\]\[broker\] Fix calculate avg message per entry (#17046)
- [f8cf23dbf9b](https://github.com/datastax/pulsar/commit/f8cf23dbf9b)
  \[fix\]\[flaky-test\]ManagedCursorMetricsTest.testCursorReadWriteMetrics
  (#17045)
- [0fc39b37aa5](https://github.com/datastax/pulsar/commit/0fc39b37aa5)
  \[fix\]\[broker\]remove exception log when access status.html (#17025)
- [684a5049762](https://github.com/datastax/pulsar/commit/684a5049762)
  \[fix\]\[tiered-storage\] move the state check forward (#17020)
- [1f9ca51a5ae](https://github.com/datastax/pulsar/commit/1f9ca51a5ae)
  \[fix\]\[client\] Release semaphore before discarding messages in
  batchMessageContainer (#17019)
- [b11181f9b5d](https://github.com/datastax/pulsar/commit/b11181f9b5d)
  \[fix\]\[txn\] fix ack with txn compute ackedCount error (#17016)
- [6f9ab4fc3a5](https://github.com/datastax/pulsar/commit/6f9ab4fc3a5)
  \[fix\]\[broker\] fix broker unackmessages number reduce error (#17003)
- [cbbecdbbbcc](https://github.com/datastax/pulsar/commit/cbbecdbbbcc)
  \[improve\]\[broker\]Remove unnecessary lock on the stats thread (#16983)
- [b9aa38e6f57](https://github.com/datastax/pulsar/commit/b9aa38e6f57)
  \[fix\]\[load-balancer\] skip mis-configured resource usage(\>100%) in load
  computation (#16937)
- [663fa5c69d4](https://github.com/datastax/pulsar/commit/663fa5c69d4)
  \[fix\]\[cli\] Pulsar shell: support relative paths (cliextensions) (#17648)
- [ca00eb5dd19](https://github.com/datastax/pulsar/commit/ca00eb5dd19)
  \[fix\]\[cli\] Pulsar shell: ensure admin client is recycled or disposed
  (#17619)
- [70532b311af](https://github.com/datastax/pulsar/commit/70532b311af)
  \[bugfix\] Prevent Automatic Topic Creation during namespace deletion (#17609)
- [9517704345b](https://github.com/datastax/pulsar/commit/9517704345b)
  \[improve\]\[admin-cli\] Add TLS provider support (#16700)
- [90c9d895499](https://github.com/datastax/pulsar/commit/90c9d895499)
  \[fix\]\[metadata\] Don't execute Bookkeeper metadata callbacks on Zookeeper
  event thread (#17620)
- [cfb28d66bbb](https://github.com/datastax/pulsar/commit/cfb28d66bbb)
  \[broker\] Do not log stacktrace for 'Failed to flush mark-delete position'
  case (#17432)

### `lunastreaming-all` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.5 \|
cassandra-enhanced-pulsar-sink-1.6.5-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.7 \| pulsar-io-data-generator-2.10.1.7.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.7 \| pulsar-io-elastic-search-2.10.1.7.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.7 \| pulsar-io-jdbc-clickhouse-2.10.1.7.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.7 \| pulsar-io-jdbc-mariadb-2.10.1.7.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.7 \| pulsar-io-jdbc-postgres-2.10.1.7.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.7 \| pulsar-io-jdbc-sqlite-2.10.1.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.7 \| pulsar-io-kafka-2.10.1.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.7 \| pulsar-io-kinesis-2.10.1.7.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.7 \| pulsar-io-data-generator-2.10.1.7.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.7 \| pulsar-io-debezium-mongodb-2.10.1.7.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.7 \| pulsar-io-debezium-mssql-2.10.1.7.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.7 \| pulsar-io-debezium-mysql-2.10.1.7.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.7 \| pulsar-io-debezium-oracle-2.10.1.7.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.7 \| pulsar-io-debezium-postgres-2.10.1.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.7 \| pulsar-io-kafka-2.10.1.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.7 \| pulsar-io-kinesis-2.10.1.7.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.9 \| pulsar-jms-2.4.9-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.5 \|
cassandra-enhanced-pulsar-sink-1.6.5-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.1.7 \| pulsar-io-aerospike-2.10.1.7.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.7 \|
pulsar-io-batch-data-generator-2.10.1.7.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.7 \| pulsar-io-data-generator-2.10.1.7.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.7 \| pulsar-io-elastic-search-2.10.1.7.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.7 \| pulsar-io-flume-2.10.1.7.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.1.7 \| pulsar-io-hbase-2.10.1.7.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.1.7 \| pulsar-io-hdfs2-2.10.1.7.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.1.7 \| pulsar-io-hdfs3-2.10.1.7.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.1.7 \| pulsar-io-influxdb-2.10.1.7.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.7 \| pulsar-io-jdbc-clickhouse-2.10.1.7.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.7 \| pulsar-io-jdbc-mariadb-2.10.1.7.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.7 \| pulsar-io-jdbc-postgres-2.10.1.7.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.7 \| pulsar-io-jdbc-sqlite-2.10.1.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.7 \| pulsar-io-kafka-2.10.1.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.7 \| pulsar-io-kinesis-2.10.1.7.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.7 \| pulsar-io-mongo-2.10.1.7.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.7 \| pulsar-io-rabbitmq-2.10.1.7.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.1.7 \| pulsar-io-redis-2.10.1.7.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.1.7 \| pulsar-io-solr-2.10.1.7.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.7 \|
pulsar-io-batch-data-generator-2.10.1.7.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.1.7 \| pulsar-io-canal-2.10.1.7.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.7 \| pulsar-io-data-generator-2.10.1.7.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.7 \| pulsar-io-debezium-mongodb-2.10.1.7.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.7 \| pulsar-io-debezium-mssql-2.10.1.7.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.7 \| pulsar-io-debezium-mysql-2.10.1.7.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.7 \| pulsar-io-debezium-oracle-2.10.1.7.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.7 \| pulsar-io-debezium-postgres-2.10.1.7.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.1.7 \| pulsar-io-dynamodb-2.10.1.7.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.1.7 \| pulsar-io-file-2.10.1.7.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.7 \| pulsar-io-flume-2.10.1.7.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.7 \| pulsar-io-kafka-2.10.1.7.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.7 \| pulsar-io-kinesis-2.10.1.7.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.7 \| pulsar-io-mongo-2.10.1.7.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.1.7 \| pulsar-io-netty-2.10.1.7.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.1.7 \| pulsar-io-nsq-2.10.1.7.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.7 \| pulsar-io-rabbitmq-2.10.1.7.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.1.7 \| pulsar-io-twitter-2.10.1.7.nar \|

</details>

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.4 \| pulsar-kafka-proxy-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.4 \| pulsar-protocol-handler-kafka-2.10.0.4.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.9 \| pulsar-jms-2.4.9-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>


## Luna Streaming Distribution 2.10 1.6

This release contains new features, improvements and stability updates.

### Most notable commits

- [4eea638d6ff](https://github.com/datastax/pulsar/commit/4eea638d6ff) fix
  duplicate calculation for msgRateIn and msgThroughputIn in replication stats
  (#15062)
- [a6d8016acdf](https://github.com/datastax/pulsar/commit/a6d8016acdf) Issue
  17588: Allow deletion of a namespace that was left in deleted status
- [8659d3f4d23](https://github.com/datastax/pulsar/commit/8659d3f4d23)
  \[fix\]\[functions\] Fix K8S download function method with auth enabled
- [224e49e9142](https://github.com/datastax/pulsar/commit/224e49e9142)
  \[PIP-193\] Support Transform Function with LocalRunner (#17445)
- [1bca43290a1](https://github.com/datastax/pulsar/commit/1bca43290a1) Factorize
  code in LocalRunner (#17400)
- [c4c6eb708e1](https://github.com/datastax/pulsar/commit/c4c6eb708e1)
  \[fix\]\[broker\] Fix issue where leader broker information isn't available
  after 10 minutes (#17401)
- [ff0875233e9](https://github.com/datastax/pulsar/commit/ff0875233e9) Use
  `safeRun` to log thread exception. (#17484)
- [6c7fdf204e0](https://github.com/datastax/pulsar/commit/6c7fdf204e0)
  \[feature\]\[broker\] Allow to configure the entry filters per namespace and
  per topic (#17153)
- [ea426df578f](https://github.com/datastax/pulsar/commit/ea426df578f)
  \[fix\]\[broker\] Fix calculate avg message per entry (#17046)
- [08761296664](https://github.com/datastax/pulsar/commit/08761296664) Bump
  dependency check and spring version to avoid potential FP (#15408)
- [f08b7dca6fd](https://github.com/datastax/pulsar/commit/f08b7dca6fd)
  \[fix\]\[sec\] bump snakeyaml to 1.31 fix CVE-2022-25857 (#17457)
- [fa06cac1eb2](https://github.com/datastax/pulsar/commit/fa06cac1eb2)
  \[improve\]\[cli\] Pulsar shell: fix custom commands autocompletion
- [725f3284d83](https://github.com/datastax/pulsar/commit/725f3284d83)
  \[improve\]\[cli\] CLI extensions: rename default location to 'cliextensions'
  (#17435)
- [bb0b94bf9bc](https://github.com/datastax/pulsar/commit/bb0b94bf9bc)
  \[fix\]\[broker\] Increment topic stats outbound message counters after
  messages have been written to the TCP/IP connection (#17043)
- [894fde1bb27](https://github.com/datastax/pulsar/commit/894fde1bb27) Revert
  "\[Fix\]\[Flaky-test\] Fix testConsumeTxnMessage (#16981)"
- [a9653884483](https://github.com/datastax/pulsar/commit/a9653884483) Upgrade
  debezium to 1.9.5 (#17340)
- [8b131d7f533](https://github.com/datastax/pulsar/commit/8b131d7f533) Fix
  OutputRecordSinkRecord getValue and getSchema (#17434)
- [dbf3b5923f4](https://github.com/datastax/pulsar/commit/dbf3b5923f4)
  \[Fix\]\[Flaky-test\] Fix testConsumeTxnMessage (#16981)
- [3275c82b9ee](https://github.com/datastax/pulsar/commit/3275c82b9ee)
  \[fix\]\[broker\] Support loadBalancerSheddingIntervalMinutes dynamic
  configuration (#16408)
- [013cb0111fe](https://github.com/datastax/pulsar/commit/013cb0111fe)
  \[fix\]\[connector\] IOConfigUtils support required and defaultValue
  annotations (#16785)
- [b7e91927573](https://github.com/datastax/pulsar/commit/b7e91927573)
  \[fix\]\[flaky-test\] testSplitBundleForMultiTimes (#16562)
- [6de8ecae848](https://github.com/datastax/pulsar/commit/6de8ecae848)
  \[improve\]\[CI\] Cancel duplicate build jobs for maintenance branches
- [98712542799](https://github.com/datastax/pulsar/commit/98712542799)
  \[fix\]\[broker\]ManagedLedger metrics fail cause of zero period (#17257)
- [ff22fb84e54](https://github.com/datastax/pulsar/commit/ff22fb84e54)
  \[fix\]\[broker\] Remove timestamp from broker metrics (#129)
- [b980f73909c](https://github.com/datastax/pulsar/commit/b980f73909c)
  \[PIP-193\] \[feature\]\[connectors\] Add support for a transform Function in
  Sinks (#16740)
- [7b9c433963e](https://github.com/datastax/pulsar/commit/7b9c433963e)
  \[fix\]\[functions\] Fix netty.DnsResolverUtil compat issue on JDK9+ for the
  function Runtimes (#16423)
- [45f373a2232](https://github.com/datastax/pulsar/commit/45f373a2232)
  \[cleanup\]\[functions\] Remove unused code (#16472)
- [8ec343ff4b2](https://github.com/datastax/pulsar/commit/8ec343ff4b2)
  \[fix\]\[cli\] Exclude windows script from the docker image

### `lunastreaming-all` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.5 \|
cassandra-enhanced-pulsar-sink-1.6.5-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.6 \| pulsar-io-data-generator-2.10.1.6.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.6 \| pulsar-io-elastic-search-2.10.1.6.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.6 \| pulsar-io-jdbc-clickhouse-2.10.1.6.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.6 \| pulsar-io-jdbc-mariadb-2.10.1.6.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.6 \| pulsar-io-jdbc-postgres-2.10.1.6.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.6 \| pulsar-io-jdbc-sqlite-2.10.1.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.6 \| pulsar-io-kafka-2.10.1.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.6 \| pulsar-io-kinesis-2.10.1.6.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.6 \| pulsar-io-data-generator-2.10.1.6.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.6 \| pulsar-io-debezium-mongodb-2.10.1.6.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.6 \| pulsar-io-debezium-mssql-2.10.1.6.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.6 \| pulsar-io-debezium-mysql-2.10.1.6.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.6 \| pulsar-io-debezium-oracle-2.10.1.6.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.6 \| pulsar-io-debezium-postgres-2.10.1.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.6 \| pulsar-io-kafka-2.10.1.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.6 \| pulsar-io-kinesis-2.10.1.6.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.9 \| pulsar-jms-2.4.9-nar.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.5 \|
cassandra-enhanced-pulsar-sink-1.6.5-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.1.6 \| pulsar-io-aerospike-2.10.1.6.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.6 \|
pulsar-io-batch-data-generator-2.10.1.6.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.6 \| pulsar-io-data-generator-2.10.1.6.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.6 \| pulsar-io-elastic-search-2.10.1.6.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.6 \| pulsar-io-flume-2.10.1.6.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.1.6 \| pulsar-io-hbase-2.10.1.6.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.1.6 \| pulsar-io-hdfs2-2.10.1.6.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.1.6 \| pulsar-io-hdfs3-2.10.1.6.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.1.6 \| pulsar-io-influxdb-2.10.1.6.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.6 \| pulsar-io-jdbc-clickhouse-2.10.1.6.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.6 \| pulsar-io-jdbc-mariadb-2.10.1.6.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.6 \| pulsar-io-jdbc-postgres-2.10.1.6.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.6 \| pulsar-io-jdbc-sqlite-2.10.1.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.6 \| pulsar-io-kafka-2.10.1.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.6 \| pulsar-io-kinesis-2.10.1.6.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.6 \| pulsar-io-mongo-2.10.1.6.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.6 \| pulsar-io-rabbitmq-2.10.1.6.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.1.6 \| pulsar-io-redis-2.10.1.6.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.1.6 \| pulsar-io-solr-2.10.1.6.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.6 \|
pulsar-io-batch-data-generator-2.10.1.6.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.1.6 \| pulsar-io-canal-2.10.1.6.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.6 \| pulsar-io-data-generator-2.10.1.6.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.6 \| pulsar-io-debezium-mongodb-2.10.1.6.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.6 \| pulsar-io-debezium-mssql-2.10.1.6.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.6 \| pulsar-io-debezium-mysql-2.10.1.6.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.6 \| pulsar-io-debezium-oracle-2.10.1.6.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.6 \| pulsar-io-debezium-postgres-2.10.1.6.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.1.6 \| pulsar-io-dynamodb-2.10.1.6.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.1.6 \| pulsar-io-file-2.10.1.6.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.6 \| pulsar-io-flume-2.10.1.6.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.6 \| pulsar-io-kafka-2.10.1.6.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.6 \| pulsar-io-kinesis-2.10.1.6.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.6 \| pulsar-io-mongo-2.10.1.6.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.1.6 \| pulsar-io-netty-2.10.1.6.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.1.6 \| pulsar-io-nsq-2.10.1.6.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.6 \| pulsar-io-rabbitmq-2.10.1.6.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.1.6 \| pulsar-io-twitter-2.10.1.6.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 2.0.0 \| pulsar-transformations-2.0.0.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.9 \| pulsar-jms-2.4.9-nar.nar \|

</details>


## Luna Streaming Distribution 2.10 1.5

This is a release containing important stability, security updates and
enhancements.

### Most notable commits

- [83cef793765](https://github.com/datastax/pulsar/commit/83cef793765) Clean up
  the ledgers cache in PendingReadsManager (#126)
- [39eeb760851](https://github.com/datastax/pulsar/commit/39eeb760851)
  \[improve\]\[dependency\] Upgrade JNA to 5.12.1 (#17262)
- [4271c184a69](https://github.com/datastax/pulsar/commit/4271c184a69)
  \[improve\]\[cli\] Pulsar shell, Pulsar admin, Pulsar client and Pulsar perf:
  support for Windows (#17243)
- [c361cf315cd](https://github.com/datastax/pulsar/commit/c361cf315cd)
  \[fix\]\[tiered-storage\] Fix the wrong secret key name get from env (#15814)
- [8bcb0464b77](https://github.com/datastax/pulsar/commit/8bcb0464b77)
  \[fix\]\[client\] Fix the message present in incoming queue after go to DLQ
  (#17326)
- [255d489bdb6](https://github.com/datastax/pulsar/commit/255d489bdb6)
  \[improve\]\[functions\]\[admin\] Improve the package download process
  (#16365)
- [2c45fb008f4](https://github.com/datastax/pulsar/commit/2c45fb008f4)
  \[Branch-2.10\] \[fix\] \[broker\] Fix bookeeper packages npe (#17291)
- [d33b6b1ddf1](https://github.com/datastax/pulsar/commit/d33b6b1ddf1)
  \[fix\]\[client\] Fix reach redeliverCount client can't send batch messages to
  DLQ (#17317)
- [b6d43cb34d2](https://github.com/datastax/pulsar/commit/b6d43cb34d2)
  \[fix\]\[client\] Fix reach redeliverCount client can't send messages to DLQ
  (#17287)
- [f84a5cef499](https://github.com/datastax/pulsar/commit/f84a5cef499)
  \[fix\]\[cpp\] Fix multi-topics consumer close segmentation fault (#17239)
- [c4d93b23f41](https://github.com/datastax/pulsar/commit/c4d93b23f41)
  \[improve\]\[client-c++\] Use an atomic `state_` instead of the lock to
  improve performance (#16940)
- [513d308c27a](https://github.com/datastax/pulsar/commit/513d308c27a)
  \[fix\]\[broker\] Fix pulsarLedgerIdGenerator can't delete index path when zk
  metadata store config rootPath. (#17192)
- [c27363b4d8f](https://github.com/datastax/pulsar/commit/c27363b4d8f)
  \[fix\]\[broker\] Fix broker cache eviction of entries read by active cursors
  (#17273)
- [201cf0bb316](https://github.com/datastax/pulsar/commit/201cf0bb316) Pending
  cache reads: reuse pending reads that partially overlaps
- [3d1d175a2a3](https://github.com/datastax/pulsar/commit/3d1d175a2a3)
  \[enh\]\[broker\] Allow to leverage pending reads with partial coverage
  (#120) - fix metrics
- [0427838f134](https://github.com/datastax/pulsar/commit/0427838f134)
  \[enh\]\[broker\] Allow to leverage pending reads with partial coverage (#120)
- [3f9f557a256](https://github.com/datastax/pulsar/commit/3f9f557a256) Pulsar
  shell: allow custom commands (#119)
- [4b61d7d6bd0](https://github.com/datastax/pulsar/commit/4b61d7d6bd0) Remove
  import in RangeEntryCacheImpl to fix checkstyle
- [cc490b8eeb9](https://github.com/datastax/pulsar/commit/cc490b8eeb9)
  \[fix\]\[broker\] Revert 5895: fix redeliveryCount (#17060)
- [f3ce1be9bb1](https://github.com/datastax/pulsar/commit/f3ce1be9bb1)
  \[fix\]\[function\] Use the schema set by the Function when it returns a
  Record (#17142)
- [d27ba9dc79f](https://github.com/datastax/pulsar/commit/d27ba9dc79f)
  \[fix\]\[functions\] Make mandatory to provide a schema in
  Context::newOutputRecordBuilder (#17118)
- [925072f6414](https://github.com/datastax/pulsar/commit/925072f6414)
  \[managed-ledger\] prevent sending duplicate reads to BK/offloaders
- [d0c3087d391](https://github.com/datastax/pulsar/commit/d0c3087d391)
  \[enh\]\[broker\] Add metrics for entry cache insertion, eviction
- [d0d4ee26637](https://github.com/datastax/pulsar/commit/d0d4ee26637)
  \[fix\]\[broker\] Make timestamp fields thread safe by using volatile
- [34934aabb03](https://github.com/datastax/pulsar/commit/34934aabb03) PIP-201
  Extensions mechanism for Pulsar Admin CLI tools (#111)
- [3e4dd4bfb5e](https://github.com/datastax/pulsar/commit/3e4dd4bfb5e)
  \[fix\]\[cli\] Pulsar shell: fix using directory '?' in the docker image
  (#17185)
- [68c1907f9da](https://github.com/datastax/pulsar/commit/68c1907f9da)
  \[fix\]\[broker\] Avoid messages being repeatedly replayed with SHARED
  subscriptions (streaming dispatcher) (#17163)
- [82bf2ede48d](https://github.com/datastax/pulsar/commit/82bf2ede48d)
  \[fix\]\[broker\] Streaming dispatcher stuck after reading the first entry
- [478bf0869b7](https://github.com/datastax/pulsar/commit/478bf0869b7)
  \[fix\]\[broker\] Fix out of order data replication (#17154)
- [6bbc9c8d288](https://github.com/datastax/pulsar/commit/6bbc9c8d288)
  \[fix\]\[broker\] Fix schema does not replicate successfully (#17049)
- [b2b4ba2a209](https://github.com/datastax/pulsar/commit/b2b4ba2a209)
  \[Fix\]\[Client\] Fixed cnx channel Inactive causing the request fail to time
  out and fail to return (#17051)
- [4d0e3b27c61](https://github.com/datastax/pulsar/commit/4d0e3b27c61)
  Pulsar-perf produce add possibility to set eventTime on messages
- [cd9f48336a9](https://github.com/datastax/pulsar/commit/cd9f48336a9)
  \[broker\]\[monitoring\] add per-subscription EntryFilter metrics (#16932)

### `lunastreaming-all` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.4 \|
cassandra-enhanced-pulsar-sink-1.6.4-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.5 \| pulsar-io-data-generator-2.10.1.5.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.5 \| pulsar-io-elastic-search-2.10.1.5.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.5 \| pulsar-io-jdbc-clickhouse-2.10.1.5.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.5 \| pulsar-io-jdbc-mariadb-2.10.1.5.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.5 \| pulsar-io-jdbc-postgres-2.10.1.5.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.5 \| pulsar-io-jdbc-sqlite-2.10.1.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.5 \| pulsar-io-kafka-2.10.1.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.5 \| pulsar-io-kinesis-2.10.1.5.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.5 \| pulsar-io-data-generator-2.10.1.5.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.5 \| pulsar-io-debezium-mongodb-2.10.1.5.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.5 \| pulsar-io-debezium-mssql-2.10.1.5.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.5 \| pulsar-io-debezium-mysql-2.10.1.5.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.5 \| pulsar-io-debezium-oracle-2.10.1.5.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.5 \| pulsar-io-debezium-postgres-2.10.1.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.5 \| pulsar-io-kafka-2.10.1.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.5 \| pulsar-io-kinesis-2.10.1.5.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 1.0.2 \| pulsar-transformations-1.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.6 \| pulsar-jms-2.4.6-nar.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.4 \|
cassandra-enhanced-pulsar-sink-1.6.4-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.1.5 \| pulsar-io-aerospike-2.10.1.5.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.5 \|
pulsar-io-batch-data-generator-2.10.1.5.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.5 \| pulsar-io-data-generator-2.10.1.5.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.5 \| pulsar-io-elastic-search-2.10.1.5.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.5 \| pulsar-io-flume-2.10.1.5.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.1.5 \| pulsar-io-hbase-2.10.1.5.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.1.5 \| pulsar-io-hdfs2-2.10.1.5.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.1.5 \| pulsar-io-hdfs3-2.10.1.5.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.1.5 \| pulsar-io-influxdb-2.10.1.5.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.5 \| pulsar-io-jdbc-clickhouse-2.10.1.5.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.5 \| pulsar-io-jdbc-mariadb-2.10.1.5.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.5 \| pulsar-io-jdbc-postgres-2.10.1.5.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.5 \| pulsar-io-jdbc-sqlite-2.10.1.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.5 \| pulsar-io-kafka-2.10.1.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.5 \| pulsar-io-kinesis-2.10.1.5.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.5 \| pulsar-io-mongo-2.10.1.5.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.5 \| pulsar-io-rabbitmq-2.10.1.5.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.1.5 \| pulsar-io-redis-2.10.1.5.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.1.5 \| pulsar-io-solr-2.10.1.5.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.2.1 \| pulsar-cassandra-source-2.2.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.5 \|
pulsar-io-batch-data-generator-2.10.1.5.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.1.5 \| pulsar-io-canal-2.10.1.5.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.5 \| pulsar-io-data-generator-2.10.1.5.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.5 \| pulsar-io-debezium-mongodb-2.10.1.5.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.5 \| pulsar-io-debezium-mssql-2.10.1.5.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.5 \| pulsar-io-debezium-mysql-2.10.1.5.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.5 \| pulsar-io-debezium-oracle-2.10.1.5.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.5 \| pulsar-io-debezium-postgres-2.10.1.5.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.1.5 \| pulsar-io-dynamodb-2.10.1.5.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.1.5 \| pulsar-io-file-2.10.1.5.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.5 \| pulsar-io-flume-2.10.1.5.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.5 \| pulsar-io-kafka-2.10.1.5.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.5 \| pulsar-io-kinesis-2.10.1.5.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.5 \| pulsar-io-mongo-2.10.1.5.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.1.5 \| pulsar-io-netty-2.10.1.5.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.1.5 \| pulsar-io-nsq-2.10.1.5.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.5 \| pulsar-io-rabbitmq-2.10.1.5.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.1.5 \| pulsar-io-twitter-2.10.1.5.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 1.0.2 \| pulsar-transformations-1.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.6 \| pulsar-jms-2.4.6-nar.nar \|

</details>


## Luna Streaming Distribution 2.10 1.4

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [f1caacc0794](https://github.com/datastax/pulsar/commit/f1caacc0794)
  \[feat\]\[connector\] ElasticSearch Sink: add ignoreUnsupportedFields option
- [fd321a75e30](https://github.com/datastax/pulsar/commit/fd321a75e30)
  \[improve\]\[proxy\] Consolidate Netty channel flushes to mitigate syscall
  overhead (#16372)
- [c2b346da480](https://github.com/datastax/pulsar/commit/c2b346da480)
  \[cleanup\]\[broker\] Follow up on \#16968 to restore some behavior in
  PersistentDispatcherMultipleConsumers class (#17018)
- [bb8ef6e6665](https://github.com/datastax/pulsar/commit/bb8ef6e6665) Fix ut
  MessageDispatchThrottlingTest#testDispatchRateCompatibility2 (#15999)
- [36eed47eeb9](https://github.com/datastax/pulsar/commit/36eed47eeb9)
  \[clean\]\[broker\]Cleanup DispatchRateLimiter#onPoliciesUpdate \#15986
- [9d21e1a8a41](https://github.com/datastax/pulsar/commit/9d21e1a8a41) Upgrade
  DS Bookkeeper to 4.14.5.1.0.2
- [414578b8582](https://github.com/datastax/pulsar/commit/414578b8582)
  \[fix\]\[broker\]Prevent `StackOverFlowException` in SHARED
  subscription(#16968)
- [f120e61d73c](https://github.com/datastax/pulsar/commit/f120e61d73c)
  \[fix\]\[security\] Bump PostgreSQL version to 42.4.1(#17066)
- [16c93e5a1a4](https://github.com/datastax/pulsar/commit/16c93e5a1a4)
  \[improve\]\[authentication\] Support for get token from HTTP params (#16986)
- [4d3fc2e3153](https://github.com/datastax/pulsar/commit/4d3fc2e3153)
  \[branch-2.10\]\[cherry-pick\] Fix topic dispatch rate limiter not init on
  broker-level \#16084 (#17000)
- [f87e765221d](https://github.com/datastax/pulsar/commit/f87e765221d) Fix
  failed test introduced by cherry-pick, according to
  <https://github.com/apache/pulsar/pull/16971/files>\#diff-6e09b03081dd6077066c65b656ed10be6125d2b7fc9a12c9a78d391afbb6b081R72-R99
- [07f90d135cf](https://github.com/datastax/pulsar/commit/07f90d135cf)
  \[fix\]\[client\] Remove redundant check for chunked message TotalChunkMsgSize
  in ConsumerImpl (#16797)
- [30ce121fd1c](https://github.com/datastax/pulsar/commit/30ce121fd1c)
  \[improve\]\[test\] Verify the authentication data in the authorization
  provider (#16900)
- [23038927125](https://github.com/datastax/pulsar/commit/23038927125)
  \[improve\]\[authentication\] Adapt basic authentication configuration with
  prefix (#16935)
- [713a9f45c57](https://github.com/datastax/pulsar/commit/713a9f45c57)
  \[improve\]\[authentication\] Improve get the basic authentication config
  (#16526)
- [f848de61bce](https://github.com/datastax/pulsar/commit/f848de61bce)
  \[fix\]\[function\] Fix python instance not process zip file correctly
  (#16697)
- [d68dd3b9d04](https://github.com/datastax/pulsar/commit/d68dd3b9d04)
  \[fix\]\[broker\] PulsarLedgerManager to pass correct error code to BK client
  (#16857)
- [eeb2ed27c95](https://github.com/datastax/pulsar/commit/eeb2ed27c95)
  \[fix\]\[client\]Fix MaxQueueSize semaphore release leak in createOpSendMsg
  (#16915)
- [12a18d57612](https://github.com/datastax/pulsar/commit/12a18d57612) fix
  Flaky-test:
  PulsarFunctionLocalRunTest.testE2EPulsarFunctionLocalRunMultipleInstance
  (#16872)
- [6048307a072](https://github.com/datastax/pulsar/commit/6048307a072)
  \[fix\]\[broker\] Upgrade log4j2 version to 2.18.0 (#16884)
- [bbcbe080e53](https://github.com/datastax/pulsar/commit/bbcbe080e53)
  \[fix\]\[client\]Fix client memory limit currentUsage leak and semaphore
  release duplicated in ProducerImpl (#16837)
- [94968bd35c9](https://github.com/datastax/pulsar/commit/94968bd35c9) \[Java
  Client\] Send CloseConsumer on timeout (#16616)
- [38a1e475cbd](https://github.com/datastax/pulsar/commit/38a1e475cbd) fix
  PatternTopicsChangedListener blocked when topic removed (#16842)
- [1d4b4a3560f](https://github.com/datastax/pulsar/commit/1d4b4a3560f)
  \[fix\]\[client\] Fix load trust certificate (#16789)
- [e04377608b9](https://github.com/datastax/pulsar/commit/e04377608b9)
  \[fix\]\[broker\] ManagedCursor: mark delete no callback when create
  meta-ledger fail (#16841)
- [d09899fdbfa](https://github.com/datastax/pulsar/commit/d09899fdbfa) Forget to
  update memory usage when invalid message (#16835)
- [27c49838091](https://github.com/datastax/pulsar/commit/27c49838091)
  \[fix\]\[broker\] Avoid IllegalStateException while client_version is not set
  (#16788)
- [e3f4e1f90d4](https://github.com/datastax/pulsar/commit/e3f4e1f90d4)
  \[fix\]\[flaky-test\] Fix ClassCastException: BrokerService cannot be cast to
  class PulsarResources (#16821)
- [e034160de74](https://github.com/datastax/pulsar/commit/e034160de74)
  \[Branch-2.10\]\[Cherry-pick\] tidy update subscriptions dispatcher
  rate-limiter (#16778)
- [d36c40038ab](https://github.com/datastax/pulsar/commit/d36c40038ab)
  \[improve\]\[broker\]\[PIP-149\]Make resetCursor async (#16355) (#16774)
- [cb28c46c336](https://github.com/datastax/pulsar/commit/cb28c46c336)
  \[improve\]\[connector\] add reader config to `pulsar-io-debezium` and
  `pulsar-io-kafka-connect-adaptor` (#16675)
- [7fbd450ce16](https://github.com/datastax/pulsar/commit/7fbd450ce16) Fix
  newLookup TooManyRequestsException message (#16594)
- [c4ad0ed3dfc](https://github.com/datastax/pulsar/commit/c4ad0ed3dfc)
  \[fix\]\[broker\] Fix consumer does not abide by the max unacks limitation for
  Key_Shared subscription (#16718)
- [e9af98ab362](https://github.com/datastax/pulsar/commit/e9af98ab362)
  \[fix\]\[proxy\] Do not preserve host when forwarding admin requests. (#16342)
- [622d65da6e4](https://github.com/datastax/pulsar/commit/622d65da6e4)
  \[improve\]\[security\] Upgrade aws-java-sdk-s3 to 1.12.261 (#16684)
- [e068ec4eba3](https://github.com/datastax/pulsar/commit/e068ec4eba3)
  \[fix\]\[broker\] Retry to delete the namespace if new topics created during
  the namespace deletion (#16676)
- [8f5dc77b9e3](https://github.com/datastax/pulsar/commit/8f5dc77b9e3)
  \[fix\]\[broker\] Fix consumer does not abide by the max unacks limitation for
  Shared subscription (#16670)
- [2365a03b848](https://github.com/datastax/pulsar/commit/2365a03b848)
  \[fix\]\[broker\] The configuration loadBalancerNamespaceMaximumBundles is
  invalid (#16552)
- [6a0f3381b9b](https://github.com/datastax/pulsar/commit/6a0f3381b9b)
  \[fix\]\[broker\] BadVersionException when splitting bundles, delay 100ms and
  try again (#16612)
- [48810e148fe](https://github.com/datastax/pulsar/commit/48810e148fe)
  \[improve\]\[client\] Add message key if exists to deadLetter messages
  (#16615)
- [8688b6ab3ff](https://github.com/datastax/pulsar/commit/8688b6ab3ff)
  Update/fix Swagger Annotation for param: authoritative (#16222)
- [bda6b605ede](https://github.com/datastax/pulsar/commit/bda6b605ede)
  \[fix\]\[function\] Ensure bytes is a well-formed UTF-8 byte sequence when
  decode the `FunctionState` bytes to string (#16199)
- [09d04c8aa01](https://github.com/datastax/pulsar/commit/09d04c8aa01)
  \[improve\]\[security\] Add load multiple certificates support in
  TrustManagerProxy (#14798)
- [fea2d3cc209](https://github.com/datastax/pulsar/commit/fea2d3cc209)
  \[fix\]\[flaky-test\] ElasticSearchClientTests.testBulkBlocking (#16920)
- [21e2143dfc1](https://github.com/datastax/pulsar/commit/21e2143dfc1) Add a
  copyPkFields option to the ES sink (#20)
- [0d8a4b23150](https://github.com/datastax/pulsar/commit/0d8a4b23150)
  \[fix\]\[broker\] Duplicate ByteBuffer when Caching Backlogged Consumers
  (#17105)
- [71763f4867c](https://github.com/datastax/pulsar/commit/71763f4867c)
  \[fix\]\[broker\] Fix memory leak if entry exists in cache (#16996)
- [9817b8faed3](https://github.com/datastax/pulsar/commit/9817b8faed3)
  \[pulsar-broker\] Support caching to drain backlog consumers (#12258)
- [ff98753da7d](https://github.com/datastax/pulsar/commit/ff98753da7d) \[Pulsar
  Admin CLI Tool\] Use NoSplitter for subscription properties
- [e2e31876427](https://github.com/datastax/pulsar/commit/e2e31876427) PIP-187:
  Add API to analyze a subscription backlog and provide a accurate value
- [6a4f773fcc1](https://github.com/datastax/pulsar/commit/6a4f773fcc1)
  \[fix\]\[proxy\] Fix client service url (#16834)
- [cc2b8995fa9](https://github.com/datastax/pulsar/commit/cc2b8995fa9) Fix rack
  awareness cache expiration race condition (#16825)
- [c86cc77c6be](https://github.com/datastax/pulsar/commit/c86cc77c6be)
  \[Broker\] Expose topic level storage write and read rate metrics (#16855)

### `lunastreaming-all` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.3 \|
cassandra-enhanced-pulsar-sink-1.6.3-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.4 \| pulsar-io-data-generator-2.10.1.4.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.4 \| pulsar-io-elastic-search-2.10.1.4.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.4 \| pulsar-io-jdbc-clickhouse-2.10.1.4.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.4 \| pulsar-io-jdbc-mariadb-2.10.1.4.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.4 \| pulsar-io-jdbc-postgres-2.10.1.4.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.4 \| pulsar-io-jdbc-sqlite-2.10.1.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.4 \| pulsar-io-kafka-2.10.1.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.4 \| pulsar-io-kinesis-2.10.1.4.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.1.0 \| pulsar-cassandra-source-2.1.0.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.4 \| pulsar-io-data-generator-2.10.1.4.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.4 \| pulsar-io-debezium-mongodb-2.10.1.4.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.4 \| pulsar-io-debezium-mssql-2.10.1.4.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.4 \| pulsar-io-debezium-mysql-2.10.1.4.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.4 \| pulsar-io-debezium-oracle-2.10.1.4.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.4 \| pulsar-io-debezium-postgres-2.10.1.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.4 \| pulsar-io-kafka-2.10.1.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.4 \| pulsar-io-kinesis-2.10.1.4.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 1.0.2 \| pulsar-transformations-1.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.0 \| pulsar-jms-2.4.0-nar.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.3 \|
cassandra-enhanced-pulsar-sink-1.6.3-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.1.4 \| pulsar-io-aerospike-2.10.1.4.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.4 \|
pulsar-io-batch-data-generator-2.10.1.4.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.4 \| pulsar-io-data-generator-2.10.1.4.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.4 \| pulsar-io-elastic-search-2.10.1.4.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.4 \| pulsar-io-flume-2.10.1.4.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.1.4 \| pulsar-io-hbase-2.10.1.4.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.1.4 \| pulsar-io-hdfs2-2.10.1.4.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.1.4 \| pulsar-io-hdfs3-2.10.1.4.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.1.4 \| pulsar-io-influxdb-2.10.1.4.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.4 \| pulsar-io-jdbc-clickhouse-2.10.1.4.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.4 \| pulsar-io-jdbc-mariadb-2.10.1.4.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.4 \| pulsar-io-jdbc-postgres-2.10.1.4.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.4 \| pulsar-io-jdbc-sqlite-2.10.1.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.4 \| pulsar-io-kafka-2.10.1.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.4 \| pulsar-io-kinesis-2.10.1.4.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.4 \| pulsar-io-mongo-2.10.1.4.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.4 \| pulsar-io-rabbitmq-2.10.1.4.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.1.4 \| pulsar-io-redis-2.10.1.4.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.1.4 \| pulsar-io-solr-2.10.1.4.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.1.0 \| pulsar-cassandra-source-2.1.0.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.4 \|
pulsar-io-batch-data-generator-2.10.1.4.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.1.4 \| pulsar-io-canal-2.10.1.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.4 \| pulsar-io-data-generator-2.10.1.4.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.4 \| pulsar-io-debezium-mongodb-2.10.1.4.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.4 \| pulsar-io-debezium-mssql-2.10.1.4.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.4 \| pulsar-io-debezium-mysql-2.10.1.4.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.4 \| pulsar-io-debezium-oracle-2.10.1.4.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.4 \| pulsar-io-debezium-postgres-2.10.1.4.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.1.4 \| pulsar-io-dynamodb-2.10.1.4.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.1.4 \| pulsar-io-file-2.10.1.4.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.4 \| pulsar-io-flume-2.10.1.4.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.4 \| pulsar-io-kafka-2.10.1.4.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.4 \| pulsar-io-kinesis-2.10.1.4.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.4 \| pulsar-io-mongo-2.10.1.4.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.1.4 \| pulsar-io-netty-2.10.1.4.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.1.4 \| pulsar-io-nsq-2.10.1.4.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.4 \| pulsar-io-rabbitmq-2.10.1.4.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.1.4 \| pulsar-io-twitter-2.10.1.4.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 1.0.2 \| pulsar-transformations-1.0.2.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.0 \| pulsar-jms-2.4.0-nar.nar \|

</details>


## Luna Streaming Distribution 2.10 1.3

This is a maintenance release containing important stability updates.

### Most notable commits

- [39fc69a944d](https://github.com/datastax/pulsar/commit/39fc69a944d) Reduce
  Flakyness in PersistentStickyKeyDispatcherMultipleConsumersTest
- [af5441cfef3](https://github.com/datastax/pulsar/commit/af5441cfef3) Broker:
  Fix KEY_SHARED dispatcher and tests

### `lunastreaming-all` distribution

<details><summary>Filters</summary>


| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0   | pulsar-jms-2.4.0-nar.nar |

</details>

<details><summary>Sinks</summary>


| Name                                                            | Description                                                                                                  | Version  | File                                         |
|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|----------|----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)   | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3    | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors)   | Writes data into cloud storage                                                                               | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar         |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)  | Test data generator source                                                                                   | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar        |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)  | Writes data into Elastic Search                                                                              | 2.10.1.3 | pulsar-io-elastic-search-2.10.1.3.nar        |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse                                                                                     | 2.10.1.3 | pulsar-io-jdbc-clickhouse-2.10.1.3.nar       |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)    | JDBC sink for MariaDB                                                                                        | 2.10.1.3 | pulsar-io-jdbc-mariadb-2.10.1.3.nar          |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)   | JDBC sink for PostgreSQL                                                                                     | 2.10.1.3 | pulsar-io-jdbc-postgres-2.10.1.3.nar         |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)     | JDBC sink for SQLite                                                                                         | 2.10.1.3 | pulsar-io-jdbc-sqlite-2.10.1.3.nar           |
| [kafka](https://pulsar.apache.org/docs/io-connectors)           | Kafka source and sink connector                                                                              | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar                 |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)         | Kinesis connectors                                                                                           | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar               |
| [snowflake](https://github.com/datastax/snowflake-connector)    | Snowflake Connector                                                                                          | 0.1.10   | pulsar-snowflake-connector-0.1.10.nar        |

</details>

<details><summary>Sources</summary>


| Name                                                                     | Description                          | Version  | File                                     |
|--------------------------------------------------------------------------|--------------------------------------|----------|------------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.1.0    | pulsar-cassandra-source-2.1.0.nar        |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 2.10.1.3 | pulsar-io-debezium-mongodb-2.10.1.3.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 2.10.1.3 | pulsar-io-debezium-mssql-2.10.1.3.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 2.10.1.3 | pulsar-io-debezium-mysql-2.10.1.3.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 2.10.1.3 | pulsar-io-debezium-oracle-2.10.1.3.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 2.10.1.3 | pulsar-io-debezium-postgres-2.10.1.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar           |

</details>

<details><summary>Proxy extensions</summary>


| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>

<details><summary>Protocol handlers</summary>


| Name                                                           | Description                            | Version  | File                                       |
|----------------------------------------------------------------|----------------------------------------|----------|--------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |

</details>

<details><summary>Functions</summary>


| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2   | pulsar-transformations-1.0.2.nar |

</details>


### `lunastreaming-experimental` distribution

<details><summary>Filters</summary>


| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0   | pulsar-jms-2.4.0-nar.nar |

</details>

<details><summary>Sinks</summary>


| Name                                                                 | Description                                                                                                  | Version  | File                                                            |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)        | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3    | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar                    |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector                                                                                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector                                                                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar      |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector)    | Big Query Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar         |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector)        | CoAP Connector                                                                                               | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar             |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector)   | Couchbase Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar        |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector)     | DataDog Connector                                                                                            | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar          |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector)   | Diffusion Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar        |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector)       | Apache Geode Connector                                                                                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar            |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector)   | Hazelcast Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar        |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector)       | Humio Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar            |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector)         | JMS Connector                                                                                                | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar              |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector)    | Kinetica Connector                                                                                           | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar         |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector)        | Apache Kudu Connector                                                                                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar             |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector)   | MarkLogic Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar        |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector)        | MQTT Connector                                                                                               | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar             |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector)       | Neo4J Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar            |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector)    | New Relic Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar         |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector)    | OrientDB Connector                                                                                           | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar         |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector)     | Apache Phoenix Connector                                                                                     | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar          |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector)       | PLC4X Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar            |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector)       | Redis Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar            |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector)    | SAP HANA Connector                                                                                           | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar         |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector                                                                                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar      |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector)      | Splunk Connector                                                                                             | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar           |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector)        | XTDB Connector                                                                                               | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar             |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector)       | Zeebe Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar            |
| [aerospike](https://pulsar.apache.org/docs/io-connectors)            | Aerospike database sink                                                                                      | 2.10.1.3 | pulsar-io-aerospike-2.10.1.3.nar                                |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source                                                                             | 2.10.1.3 | pulsar-io-batch-data-generator-2.10.1.3.nar                     |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors)        | Writes data into cloud storage                                                                               | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar                            |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)       | Test data generator source                                                                                   | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar                           |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)       | Writes data into Elastic Search                                                                              | 2.10.1.3 | pulsar-io-elastic-search-2.10.1.3.nar                           |
| [flume](https://pulsar.apache.org/docs/io-connectors)                | flume source and sink connector                                                                              | 2.10.1.3 | pulsar-io-flume-2.10.1.3.nar                                    |
| [hbase](https://pulsar.apache.org/docs/io-connectors)                | Writes data into hbase table                                                                                 | 2.10.1.3 | pulsar-io-hbase-2.10.1.3.nar                                    |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors)                | Writes data into HDFS 2.x                                                                                    | 2.10.1.3 | pulsar-io-hdfs2-2.10.1.3.nar                                    |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors)                | Writes data into HDFS 3.x                                                                                    | 2.10.1.3 | pulsar-io-hdfs3-2.10.1.3.nar                                    |
| [influxdb](https://pulsar.apache.org/docs/io-connectors)             | Writes data into InfluxDB database                                                                           | 2.10.1.3 | pulsar-io-influxdb-2.10.1.3.nar                                 |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)      | JDBC sink for ClickHouse                                                                                     | 2.10.1.3 | pulsar-io-jdbc-clickhouse-2.10.1.3.nar                          |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)         | JDBC sink for MariaDB                                                                                        | 2.10.1.3 | pulsar-io-jdbc-mariadb-2.10.1.3.nar                             |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)        | JDBC sink for PostgreSQL                                                                                     | 2.10.1.3 | pulsar-io-jdbc-postgres-2.10.1.3.nar                            |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for SQLite                                                                                         | 2.10.1.3 | pulsar-io-jdbc-sqlite-2.10.1.3.nar                              |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                | Kafka source and sink connector                                                                              | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar                                    |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)              | Kinesis connectors                                                                                           | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar                                  |
| [mongo](https://pulsar.apache.org/docs/io-connectors)                | MongoDB source and sink connector                                                                            | 2.10.1.3 | pulsar-io-mongo-2.10.1.3.nar                                    |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors)             | RabbitMQ source and sink connector                                                                           | 2.10.1.3 | pulsar-io-rabbitmq-2.10.1.3.nar                                 |
| [redis](https://pulsar.apache.org/docs/io-connectors)                | Writes data into Redis                                                                                       | 2.10.1.3 | pulsar-io-redis-2.10.1.3.nar                                    |
| [solr](https://pulsar.apache.org/docs/io-connectors)                 | Writes data into solr collection                                                                             | 2.10.1.3 | pulsar-io-solr-2.10.1.3.nar                                     |
| [snowflake](https://github.com/datastax/snowflake-connector)         | Snowflake Connector                                                                                          | 0.1.10   | pulsar-snowflake-connector-0.1.10.nar                           |

</details>

<details><summary>Sources</summary>


| Name                                                                     | Description                           | Version  | File                                                            |
|--------------------------------------------------------------------------|---------------------------------------|----------|-----------------------------------------------------------------|
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector)     | Azure DocumentDB Connector            | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector)        | Big Query Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar         |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector)            | CoAP Connector                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar             |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector)       | Couchbase Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar        |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector)         | DataDog Connector                     | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar          |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector)       | Diffusion Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar        |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector)           | Apache Geode Connector                | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar            |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector)       | Hazelcast Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar        |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector)           | Humio Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar            |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector)             | JMS Connector                         | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar              |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector)        | Kinetica Connector                    | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar         |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector)            | Apache Kudu Connector                 | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar             |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector)       | MarkLogic Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar        |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector)            | MQTT Connector                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar             |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector)           | Neo4J Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar            |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector)        | New Relic Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar         |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector)        | OrientDB Connector                    | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar         |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector)         | Apache Phoenix Connector              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar          |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector)           | PLC4X Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar            |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector)           | Redis Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar            |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector)        | SAP HANA Connector                    | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar         |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector)     | SingleStore Connector                 | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar      |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector)          | Splunk Connector                      | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar           |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector)            | XTDB Connector                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar             |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector)           | Zeebe Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar            |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra              | 2.1.0    | pulsar-cassandra-source-2.1.0.nar                               |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors)     | Test batch data generator source      | 2.10.1.3 | pulsar-io-batch-data-generator-2.10.1.3.nar                     |
| [canal](https://pulsar.apache.org/docs/io-connectors)                    | canal source and read data from mysql | 2.10.1.3 | pulsar-io-canal-2.10.1.3.nar                                    |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source            | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar                           |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source               | 2.10.1.3 | pulsar-io-debezium-mongodb-2.10.1.3.nar                         |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source  | 2.10.1.3 | pulsar-io-debezium-mssql-2.10.1.3.nar                           |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                 | 2.10.1.3 | pulsar-io-debezium-mysql-2.10.1.3.nar                           |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source                | 2.10.1.3 | pulsar-io-debezium-oracle-2.10.1.3.nar                          |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source              | 2.10.1.3 | pulsar-io-debezium-postgres-2.10.1.3.nar                        |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors)                 | DynamoDB connectors                   | 2.10.1.3 | pulsar-io-dynamodb-2.10.1.3.nar                                 |
| [file](https://pulsar.apache.org/docs/io-connectors)                     | Reads data from local filesystem      | 2.10.1.3 | pulsar-io-file-2.10.1.3.nar                                     |
| [flume](https://pulsar.apache.org/docs/io-connectors)                    | flume source and sink connector       | 2.10.1.3 | pulsar-io-flume-2.10.1.3.nar                                    |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector       | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar                                    |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                    | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar                                  |
| [mongo](https://pulsar.apache.org/docs/io-connectors)                    | MongoDB source and sink connector     | 2.10.1.3 | pulsar-io-mongo-2.10.1.3.nar                                    |
| [netty](https://pulsar.apache.org/docs/io-connectors)                    | Netty Tcp or Udp Source Connector     | 2.10.1.3 | pulsar-io-netty-2.10.1.3.nar                                    |
| [nsq](https://pulsar.apache.org/docs/io-connectors)                      | Ingest data from an NSQ topic         | 2.10.1.3 | pulsar-io-nsq-2.10.1.3.nar                                      |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors)                 | RabbitMQ source and sink connector    | 2.10.1.3 | pulsar-io-rabbitmq-2.10.1.3.nar                                 |
| [twitter](https://pulsar.apache.org/docs/io-connectors)                  | Ingest data from Twitter firehose     | 2.10.1.3 | pulsar-io-twitter-2.10.1.3.nar                                  |

</details>

<details><summary>Proxy extensions</summary>


| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>

<details><summary>Protocol handlers</summary>


| Name                                                           | Description                            | Version  | File                                       |
|----------------------------------------------------------------|----------------------------------------|----------|--------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |

</details>

<details><summary>Functions</summary>


| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2   | pulsar-transformations-1.0.2.nar |

</details>


## Luna Streaming Distribution 2.10 1.2

**NOTE: IF YOU'RE USING THIS VERSION PLEASE UPGRADE TO A NEWER ONE. VERSION 2.10
1.2 CONTAINS STABILITY ISSUES ABOUT KEY_SHARED SUBSCRIPTIONS.**

This is a maintenance release containing important stability updates.

### Most notable commits

- [6c80ce26acb](https://github.com/datastax/pulsar/commit/6c80ce26acb) Issue
  16802: fix Repeated messages of shared dispatcher Changes:
  sendMessagesToConsumer must block reads of new entries otherwise we will end
  up in reading duplicates
- [73c14dbc968](https://github.com/datastax/pulsar/commit/73c14dbc968) Fix
  pulsar-experimental-docker-image version
- [e8283824ff7](https://github.com/datastax/pulsar/commit/e8283824ff7) Create
  -experimental docker image with all the builtin connectors
- [e47236100d1](https://github.com/datastax/pulsar/commit/e47236100d1) KCA:
  handle kafka's logical schemas
- [a79fbd931bd](https://github.com/datastax/pulsar/commit/a79fbd931bd)
  \[Fix\]\[pulsar-io\] KCA: handle kafka preCommit() returning earlier offsets
  than requested (#16100)
- [3d754337c80](https://github.com/datastax/pulsar/commit/3d754337c80) KCA to
  use index (if available) instead of sequence and to handle batched messages
  non-unique sequenceIds (#16098)
- [d14af5c2f94](https://github.com/datastax/pulsar/commit/d14af5c2f94) Fix flaky
  DelayedDeliveryTest
- [1d552518103](https://github.com/datastax/pulsar/commit/1d552518103) Fix
  owasp-dependency-check supression file
- [91bf7b5b215](https://github.com/datastax/pulsar/commit/91bf7b5b215) Fixed
  deadlock in key-shared dispatcher (#16660)
- [83fe4270a78](https://github.com/datastax/pulsar/commit/83fe4270a78) Avoid
  tracking the delays of all the message when we detect that they are fixed
  (#16609)
- [650ce37a71c](https://github.com/datastax/pulsar/commit/650ce37a71c) \[Branch
  2.10\] Fix some OWASP dependency problems. (#16260)
- [b9166972de1](https://github.com/datastax/pulsar/commit/b9166972de1)
  \[fix\]\[pulsar-broker\] Fix RawReader hasMessageAvailable returns true when
  no messages (#16443)
- [d64593c907f](https://github.com/datastax/pulsar/commit/d64593c907f) Fix: Make
  DeadLetterPolicy deserializable (#16513)
- [4847928a3bc](https://github.com/datastax/pulsar/commit/4847928a3bc)
  \[improve\]\[metadataStore\] Update namespace policies would cause
  metadata-store thread waiting too long (#16438)
- [f435dc74981](https://github.com/datastax/pulsar/commit/f435dc74981)
  \[fix\]\[flaky-test\] Fix flaky test
  testConsumerBacklogEvictionTimeQuotaWithEmptyLedger (#16419)
- [165f1ac303b](https://github.com/datastax/pulsar/commit/165f1ac303b)
  \[fix\]\[broker\] Retry when DistributedIdGenerator has BadVersion error
  (#16491)
- [c2122357ee0](https://github.com/datastax/pulsar/commit/c2122357ee0)
  \[improve\]\[test\] Fix flaky C++ ClientTest.testWrongListener (#16510)
- [05fff208477](https://github.com/datastax/pulsar/commit/05fff208477) Fix
  flaky-test: NonPersistentTopicE2ETest.testGC (#16505)
- [9d5108891f1](https://github.com/datastax/pulsar/commit/9d5108891f1)
  \[improve\]\[test\] Reduce the time consumption of BacklogQuotaManagerTest
  (#16550)
- [5fc0731f1c2](https://github.com/datastax/pulsar/commit/5fc0731f1c2)
  \[fix\]\[flaky-test\]
  PersistentFailoverE2ETest.testSimpleConsumerEventsWithPartition (#16493)
- [493f451112d](https://github.com/datastax/pulsar/commit/493f451112d)
  \[fix\]\[test\] Catch exception when update data in mockZookeeper (#16473)
- [bc0e10eb487](https://github.com/datastax/pulsar/commit/bc0e10eb487)
  \[fix\]\[test\] Fix jvm oom on Unit Test broker group 1 (#16542)
- [f9dd46bbde1](https://github.com/datastax/pulsar/commit/f9dd46bbde1)
  \[fix\]\[broker\] Expose timestamp field for SchemaData&SchemaInfo (#16380)
- [77957d8879e](https://github.com/datastax/pulsar/commit/77957d8879e)
  \[fix\]\[flaky-test\] MessageTTLTest.testMessageExpiryAfterTopicUnload
  (#16462)
- [f79fd657a89](https://github.com/datastax/pulsar/commit/f79fd657a89)
  \[fix\]\[broker\]Fix getInternalStats occasional lack of LeaderInfo again
  (#16238)
- [747d5bd70a5](https://github.com/datastax/pulsar/commit/747d5bd70a5) \[fix\]
  PulsarLedgerManager: add missed return statement (#16607)

### `lunastreaming-all` distribution

<details><summary>Filters</summary>


| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0   | pulsar-jms-2.4.0-nar.nar |

</details>

<details><summary>Sinks</summary>


| Name                                                            | Description                                                                                                  | Version  | File                                         |
|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|----------|----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)   | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3    | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors)   | Writes data into cloud storage                                                                               | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar         |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)  | Test data generator source                                                                                   | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar        |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)  | Writes data into Elastic Search                                                                              | 2.10.1.2 | pulsar-io-elastic-search-2.10.1.2.nar        |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse                                                                                     | 2.10.1.2 | pulsar-io-jdbc-clickhouse-2.10.1.2.nar       |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)    | JDBC sink for MariaDB                                                                                        | 2.10.1.2 | pulsar-io-jdbc-mariadb-2.10.1.2.nar          |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)   | JDBC sink for PostgreSQL                                                                                     | 2.10.1.2 | pulsar-io-jdbc-postgres-2.10.1.2.nar         |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)     | JDBC sink for SQLite                                                                                         | 2.10.1.2 | pulsar-io-jdbc-sqlite-2.10.1.2.nar           |
| [kafka](https://pulsar.apache.org/docs/io-connectors)           | Kafka source and sink connector                                                                              | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar                 |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)         | Kinesis connectors                                                                                           | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar               |
| [snowflake](https://github.com/datastax/snowflake-connector)    | Snowflake Connector                                                                                          | 0.1.10   | pulsar-snowflake-connector-0.1.10.nar        |

</details>

<details><summary>Sources</summary>


| Name                                                                     | Description                          | Version  | File                                     |
|--------------------------------------------------------------------------|--------------------------------------|----------|------------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.1.0    | pulsar-cassandra-source-2.1.0.nar        |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 2.10.1.2 | pulsar-io-debezium-mongodb-2.10.1.2.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 2.10.1.2 | pulsar-io-debezium-mssql-2.10.1.2.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 2.10.1.2 | pulsar-io-debezium-mysql-2.10.1.2.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 2.10.1.2 | pulsar-io-debezium-oracle-2.10.1.2.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 2.10.1.2 | pulsar-io-debezium-postgres-2.10.1.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar           |

</details>

<details><summary>Proxy extensions</summary>


| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>

<details><summary>Protocol handlers</summary>


| Name                                                           | Description                            | Version  | File                                       |
|----------------------------------------------------------------|----------------------------------------|----------|--------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |

</details>

<details><summary>Functions</summary>


| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2   | pulsar-transformations-1.0.2.nar |

</details>


### `lunastreaming-experimental` distribution

<details><summary>Filters</summary>


| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0   | pulsar-jms-2.4.0-nar.nar |

</details>

<details><summary>Sinks</summary>


| Name                                                                 | Description                                                                                                  | Version  | File                                                            |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)        | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3    | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar                    |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector                                                                                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector                                                                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar      |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector)    | Big Query Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar         |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector)        | CoAP Connector                                                                                               | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar             |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector)   | Couchbase Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar        |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector)     | DataDog Connector                                                                                            | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar          |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector)   | Diffusion Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar        |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector)       | Apache Geode Connector                                                                                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar            |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector)   | Hazelcast Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar        |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector)       | Humio Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar            |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector)         | JMS Connector                                                                                                | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar              |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector)    | Kinetica Connector                                                                                           | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar         |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector)        | Apache Kudu Connector                                                                                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar             |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector)   | MarkLogic Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar        |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector)        | MQTT Connector                                                                                               | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar             |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector)       | Neo4J Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar            |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector)    | New Relic Connector                                                                                          | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar         |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector)    | OrientDB Connector                                                                                           | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar         |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector)     | Apache Phoenix Connector                                                                                     | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar          |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector)       | PLC4X Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar            |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector)       | Redis Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar            |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector)    | SAP HANA Connector                                                                                           | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar         |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector                                                                                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar      |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector)      | Splunk Connector                                                                                             | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar           |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector)        | XTDB Connector                                                                                               | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar             |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector)       | Zeebe Connector                                                                                              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar            |
| [aerospike](https://pulsar.apache.org/docs/io-connectors)            | Aerospike database sink                                                                                      | 2.10.1.2 | pulsar-io-aerospike-2.10.1.2.nar                                |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source                                                                             | 2.10.1.2 | pulsar-io-batch-data-generator-2.10.1.2.nar                     |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors)        | Writes data into cloud storage                                                                               | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar                            |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)       | Test data generator source                                                                                   | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar                           |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)       | Writes data into Elastic Search                                                                              | 2.10.1.2 | pulsar-io-elastic-search-2.10.1.2.nar                           |
| [flume](https://pulsar.apache.org/docs/io-connectors)                | flume source and sink connector                                                                              | 2.10.1.2 | pulsar-io-flume-2.10.1.2.nar                                    |
| [hbase](https://pulsar.apache.org/docs/io-connectors)                | Writes data into hbase table                                                                                 | 2.10.1.2 | pulsar-io-hbase-2.10.1.2.nar                                    |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors)                | Writes data into HDFS 2.x                                                                                    | 2.10.1.2 | pulsar-io-hdfs2-2.10.1.2.nar                                    |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors)                | Writes data into HDFS 3.x                                                                                    | 2.10.1.2 | pulsar-io-hdfs3-2.10.1.2.nar                                    |
| [influxdb](https://pulsar.apache.org/docs/io-connectors)             | Writes data into InfluxDB database                                                                           | 2.10.1.2 | pulsar-io-influxdb-2.10.1.2.nar                                 |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)      | JDBC sink for ClickHouse                                                                                     | 2.10.1.2 | pulsar-io-jdbc-clickhouse-2.10.1.2.nar                          |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)         | JDBC sink for MariaDB                                                                                        | 2.10.1.2 | pulsar-io-jdbc-mariadb-2.10.1.2.nar                             |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)        | JDBC sink for PostgreSQL                                                                                     | 2.10.1.2 | pulsar-io-jdbc-postgres-2.10.1.2.nar                            |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for SQLite                                                                                         | 2.10.1.2 | pulsar-io-jdbc-sqlite-2.10.1.2.nar                              |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                | Kafka source and sink connector                                                                              | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar                                    |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)              | Kinesis connectors                                                                                           | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar                                  |
| [mongo](https://pulsar.apache.org/docs/io-connectors)                | MongoDB source and sink connector                                                                            | 2.10.1.2 | pulsar-io-mongo-2.10.1.2.nar                                    |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors)             | RabbitMQ source and sink connector                                                                           | 2.10.1.2 | pulsar-io-rabbitmq-2.10.1.2.nar                                 |
| [redis](https://pulsar.apache.org/docs/io-connectors)                | Writes data into Redis                                                                                       | 2.10.1.2 | pulsar-io-redis-2.10.1.2.nar                                    |
| [solr](https://pulsar.apache.org/docs/io-connectors)                 | Writes data into solr collection                                                                             | 2.10.1.2 | pulsar-io-solr-2.10.1.2.nar                                     |
| [snowflake](https://github.com/datastax/snowflake-connector)         | Snowflake Connector                                                                                          | 0.1.10   | pulsar-snowflake-connector-0.1.10.nar                           |

</details>

<details><summary>Sources</summary>


| Name                                                                     | Description                           | Version  | File                                                            |
|--------------------------------------------------------------------------|---------------------------------------|----------|-----------------------------------------------------------------|
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector)     | Azure DocumentDB Connector            | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector)        | Big Query Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar         |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector)            | CoAP Connector                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar             |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector)       | Couchbase Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar        |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector)         | DataDog Connector                     | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar          |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector)       | Diffusion Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar        |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector)           | Apache Geode Connector                | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar            |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector)       | Hazelcast Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar        |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector)           | Humio Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar            |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector)             | JMS Connector                         | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar              |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector)        | Kinetica Connector                    | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar         |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector)            | Apache Kudu Connector                 | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar             |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector)       | MarkLogic Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar        |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector)            | MQTT Connector                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar             |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector)           | Neo4J Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar            |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector)        | New Relic Connector                   | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar         |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector)        | OrientDB Connector                    | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar         |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector)         | Apache Phoenix Connector              | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar          |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector)           | PLC4X Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar            |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector)           | Redis Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar            |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector)        | SAP HANA Connector                    | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar         |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector)     | SingleStore Connector                 | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar      |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector)          | Splunk Connector                      | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar           |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector)            | XTDB Connector                        | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar             |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector)           | Zeebe Connector                       | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar            |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra              | 2.1.0    | pulsar-cassandra-source-2.1.0.nar                               |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors)     | Test batch data generator source      | 2.10.1.2 | pulsar-io-batch-data-generator-2.10.1.2.nar                     |
| [canal](https://pulsar.apache.org/docs/io-connectors)                    | canal source and read data from mysql | 2.10.1.2 | pulsar-io-canal-2.10.1.2.nar                                    |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source            | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar                           |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source               | 2.10.1.2 | pulsar-io-debezium-mongodb-2.10.1.2.nar                         |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source  | 2.10.1.2 | pulsar-io-debezium-mssql-2.10.1.2.nar                           |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                 | 2.10.1.2 | pulsar-io-debezium-mysql-2.10.1.2.nar                           |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source                | 2.10.1.2 | pulsar-io-debezium-oracle-2.10.1.2.nar                          |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source              | 2.10.1.2 | pulsar-io-debezium-postgres-2.10.1.2.nar                        |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors)                 | DynamoDB connectors                   | 2.10.1.2 | pulsar-io-dynamodb-2.10.1.2.nar                                 |
| [file](https://pulsar.apache.org/docs/io-connectors)                     | Reads data from local filesystem      | 2.10.1.2 | pulsar-io-file-2.10.1.2.nar                                     |
| [flume](https://pulsar.apache.org/docs/io-connectors)                    | flume source and sink connector       | 2.10.1.2 | pulsar-io-flume-2.10.1.2.nar                                    |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector       | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar                                    |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                    | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar                                  |
| [mongo](https://pulsar.apache.org/docs/io-connectors)                    | MongoDB source and sink connector     | 2.10.1.2 | pulsar-io-mongo-2.10.1.2.nar                                    |
| [netty](https://pulsar.apache.org/docs/io-connectors)                    | Netty Tcp or Udp Source Connector     | 2.10.1.2 | pulsar-io-netty-2.10.1.2.nar                                    |
| [nsq](https://pulsar.apache.org/docs/io-connectors)                      | Ingest data from an NSQ topic         | 2.10.1.2 | pulsar-io-nsq-2.10.1.2.nar                                      |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors)                 | RabbitMQ source and sink connector    | 2.10.1.2 | pulsar-io-rabbitmq-2.10.1.2.nar                                 |
| [twitter](https://pulsar.apache.org/docs/io-connectors)                  | Ingest data from Twitter firehose     | 2.10.1.2 | pulsar-io-twitter-2.10.1.2.nar                                  |

</details>

<details><summary>Proxy extensions</summary>


| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>

<details><summary>Protocol handlers</summary>


| Name                                                           | Description                            | Version  | File                                       |
|----------------------------------------------------------------|----------------------------------------|----------|--------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar            |

</details>

<details><summary>Functions</summary>


| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2   | pulsar-transformations-1.0.2.nar |

</details>


## Luna Streaming Distribution 2.10 1.1

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [037b9fc981d](https://github.com/datastax/pulsar/commit/037b9fc981d) Broker:
  fix Key_Shared dispatcher when using
  dispatcherDispatchMessagesInSubscriptionThread
- [0f748e6e908](https://github.com/datastax/pulsar/commit/0f748e6e908) \[enh\]
  Broker/EntryFilter: make the delay for RESCHEDULED messages configurable
  (dispatcherFilterRescheduledMessageDelay) (#16602)
- [9fafe31df54](https://github.com/datastax/pulsar/commit/9fafe31df54) Fix
  PersistentStickyKeyDispatcherMultipleConsumersTest
- [cb28169717c](https://github.com/datastax/pulsar/commit/cb28169717c)
  \[feature\]\[connector\] JDBC sinks: support upsert and row deletion (#16448)
- [66d205ad7d4](https://github.com/datastax/pulsar/commit/66d205ad7d4)
  \[fix\]\[test\]\[branch-2.10\] Fix test
  TransactionEndToEndTest#testSendTxnMessageTimeout (only release branches)
  (#16570)
- [6ae4175d3a0](https://github.com/datastax/pulsar/commit/6ae4175d3a0) Shared
  subscription: run filters in a separate (per-subscription) thread
  (dispatcherDispatchMessagesInSubscriptionThread)
- [ab5687f2348](https://github.com/datastax/pulsar/commit/ab5687f2348) Pulsar
  shell: configs to manage multiple clusters/tenants
- [d62fb98094a](https://github.com/datastax/pulsar/commit/d62fb98094a)
  \[fix\]\[broker\] Skip reading more entries for a pending read with no more
  entries (#16400)
- [7c002e6c4fb](https://github.com/datastax/pulsar/commit/7c002e6c4fb)
  \[fix\]\[security\] Upgrade to Jetty to 9.4.48.v20220622 to get rid of
  CVE-2022-2047 (#16520)
- [6a112d3bff9](https://github.com/datastax/pulsar/commit/6a112d3bff9)
  cherry-pick \[fix\]\[txn\] fix pattern sub filter transaction system topic
  (#16533)
- [2ae0ee032c3](https://github.com/datastax/pulsar/commit/2ae0ee032c3)
  \[fix\]\[broker\] Fixed error when delayed messages trackers state grows to
  \>1.5GB (#16490)
- [6ab833340ba](https://github.com/datastax/pulsar/commit/6ab833340ba) Support
  shrink for TripleLongPriorityQueue (#15936)
- [63980fbf058](https://github.com/datastax/pulsar/commit/63980fbf058) Pulsar
  Shell: fix sh command and better error message for non-interactive mode
  failures
- [04610605c47](https://github.com/datastax/pulsar/commit/04610605c47)
  \[fix\]\[txn\] Allow producer enable send timeout in transaction (#16519)
- [c03f3cb1590](https://github.com/datastax/pulsar/commit/c03f3cb1590) Fix get
  non-persistent topics issue in Namespaces. (#16170) (#16514)
- [ef16e303db7](https://github.com/datastax/pulsar/commit/ef16e303db7)
  \[fix\]\[broker\] fix No such ledger exception (#16420)
- [2ab1991a0de](https://github.com/datastax/pulsar/commit/2ab1991a0de)
  \[fix\]\[broker\] Fix setManagedLedgerOffloadedReadPriority not work. (#16436)
- [43e239ac5eb](https://github.com/datastax/pulsar/commit/43e239ac5eb)
  \[improve\]\[broker\] Recycle OpReadEntry in some corner cases (#16399)
- [1c28da327bf](https://github.com/datastax/pulsar/commit/1c28da327bf)
  \[fix\]\[C++ client\] Fix the close of Client might stuck or return a wrong
  result (#16285)
- [e163dc5a752](https://github.com/datastax/pulsar/commit/e163dc5a752)
  \[fix\]\[broker\] Release the entry in getEarliestMessagePublishTimeOfPos
  (#16386)
- [88c907a8743](https://github.com/datastax/pulsar/commit/88c907a8743) Exclude
  the Netty Reactive Stream from asynchttpclient (#16312)
- [e8534707f76](https://github.com/datastax/pulsar/commit/e8534707f76)
  \[improve\]\[java-client\] Improve performance of multi-topic consumer with
  more than one IO thread (#16336)
- [3f0641573a9](https://github.com/datastax/pulsar/commit/3f0641573a9)
  \[improve\]\[java-client\] Support passing existing scheduled executor
  providers to the client (#16334)
- [a6d97f07848](https://github.com/datastax/pulsar/commit/a6d97f07848)
  \[fix\]\[flaky-test\] Fix failed test
  NonPersistentTopicE2ETest.testGCWillDeleteSchema (#16381)
- [25424651d65](https://github.com/datastax/pulsar/commit/25424651d65)
  \[fix\]\[flaky-test\] Try to fix flaky test related to
  PersistentTopicTest.setup (#16383)
- [643625b9b81](https://github.com/datastax/pulsar/commit/643625b9b81)
  \[fix\]\[flaky-test\] Fix failed test
  PatternTopicsConsumerImplTest.testAutoSubscribePatternConsumer (#16375)
- [23e5ccd480d](https://github.com/datastax/pulsar/commit/23e5ccd480d)
  \[improve\]\[broker\] Use shared broker client scheduled executor provider
  (#16338)
- [8611de81c4f](https://github.com/datastax/pulsar/commit/8611de81c4f) fix
  select broker is none (#16316)
- [47a7368bf6c](https://github.com/datastax/pulsar/commit/47a7368bf6c)
  \[fix\]\[txn\] Fix TopicTransactionBuffer ledger apend marker throw
  ManagedLedgerAlreadyClosedException (#16265)
- [dcf80fac0f5](https://github.com/datastax/pulsar/commit/dcf80fac0f5)
  \[improve\]\[broker\] Optimise msgOutCounter and bytesOutCounter (#16214)
  (#16286)
- [a9d62b59aec](https://github.com/datastax/pulsar/commit/a9d62b59aec)
  \[fix\]\[broker\]fix bug: fail to expose managed ledger client stats to
  prometheus if bookkeeperClientExposeStatsToPrometheus is true (#16219)
- [5f8b65b70ae](https://github.com/datastax/pulsar/commit/5f8b65b70ae) \[fix\]
  \[transaction\] Cmd-Subscribe and Cmd-Producer will not succeed even after 100
  retries (#16248)
- [eb481fc9803](https://github.com/datastax/pulsar/commit/eb481fc9803)
  \[improve\]\[broker\] Use LinkedHashSet for config items of type Set to
  preserve elements order (#16138)
- [2b09f7d170f](https://github.com/datastax/pulsar/commit/2b09f7d170f)
  \[fix\]\[txn\] Fix append txn message is lower than lowWaterMark decrease
  pendingWriteOps (#16266)
- [d7068c1cddb](https://github.com/datastax/pulsar/commit/d7068c1cddb) fix npe
  when doCacheEviction (#15184)
- [96666e1158d](https://github.com/datastax/pulsar/commit/96666e1158d) Add a
  cache eviction policy&#65306;Evicting cache data by the slowest
  markDeletedPosition (#14985)
- [5ef2183f320](https://github.com/datastax/pulsar/commit/5ef2183f320) Extracted
  interface for EntryCacheManager (#15933)
- [8a6f0fb832d](https://github.com/datastax/pulsar/commit/8a6f0fb832d) Support
  dynamic update cache config (#13679)
- [9480b49fcc3](https://github.com/datastax/pulsar/commit/9480b49fcc3)
  \[fix\]\[broker\] Do not use IO thread for consumerFlow in Shared subscription
- [7e9dee3f928](https://github.com/datastax/pulsar/commit/7e9dee3f928) Shared
  subscription: improvement with offloaded ledgers
- [d95fb1e09ed](https://github.com/datastax/pulsar/commit/d95fb1e09ed)
  \[fix\]\[broker\] Fix RawReader out of order (#16390)
- [c143bd97791](https://github.com/datastax/pulsar/commit/c143bd97791) Pulsar
  shell: symlink support
- [52cf9e8124c](https://github.com/datastax/pulsar/commit/52cf9e8124c) Pulsar
  Shell: use service hostname as prompt
- [bea45683d4e](https://github.com/datastax/pulsar/commit/bea45683d4e) Pulsar
  shell: use -c to specify client configuration file
- [fc6c37b636b](https://github.com/datastax/pulsar/commit/fc6c37b636b)
  \[cleanup\] CLI: fix pulsar-websocket dependency importing only needed jars
- [cc4c7be3916](https://github.com/datastax/pulsar/commit/cc4c7be3916)
  Offloaders: fix metrics - pass the Scheduler for periodic calculations - add
  raw brk_ledgeroffloader_read_bytes counter - fix read latency from JClouds
  calculation
- [90399643a68](https://github.com/datastax/pulsar/commit/90399643a68) Fixed
  deadlock when checking topic ownership (#16310)
- [52e0711d373](https://github.com/datastax/pulsar/commit/52e0711d373) Ensure
  ack-timeout task gets re-scheduled when there are exception in the final stage
  (#16337)
- [ee1a89ccc8d](https://github.com/datastax/pulsar/commit/ee1a89ccc8d)
  \[improve\]\[workflow\] Sync the new docbot to branch-2.10 \#16288
- [7468f8b9ea8](https://github.com/datastax/pulsar/commit/7468f8b9ea8)
  \[fix\]\[broker\] Fix passing incorrect authentication data (#16201)
- [b72c5089738](https://github.com/datastax/pulsar/commit/b72c5089738) Avoid
  AuthenticationDataSource mutation for subscription name (#16065)
- [91ca4b4c906](https://github.com/datastax/pulsar/commit/91ca4b4c906)
  \[fix\]\[broker\]fix npe when invoke replaceBookie. (#16239)
- [bd7c63aec4c](https://github.com/datastax/pulsar/commit/bd7c63aec4c)
  \[fix\]\[broker\] Fix NPE when drop backlog for time limit. (#16235)
- [8b1d7a0c894](https://github.com/datastax/pulsar/commit/8b1d7a0c894)
  \[improve\]\[broker\] Reduce the re-schedule message read operation for
  PersistentDispatcherMultipleConsumers (#16241)
- [da72a32112c](https://github.com/datastax/pulsar/commit/da72a32112c)
  \[improve\]\[java-client\] Replace ScheduledExecutor to improve performance of
  message consumption (#16236)
- [a8695ff3aff](https://github.com/datastax/pulsar/commit/a8695ff3aff)
  \[improve\]\[broker\] Avoid go through all the consumers to get the message
  ack owner (#16245)
- [8347ed2218d](https://github.com/datastax/pulsar/commit/8347ed2218d)
  \[fix\]\[broker\]Fix subscribe dispathcer limiter not be initialized (#16175)
- [17be098c6af](https://github.com/datastax/pulsar/commit/17be098c6af)
  \[fix\]\[broker\] Fix compaction subscription acknowledge Marker msg issue.
  (#16205)
- [03a9ea7bc73](https://github.com/datastax/pulsar/commit/03a9ea7bc73)
  \[fix\]\[tests\] TieredStorageConfigurationTests - clear system properties
  (#15957)
- [f26597a4002](https://github.com/datastax/pulsar/commit/f26597a4002)
  \[fix\]\[client\] Add classLoader field for `SchemaDefinition` (#15915)
- [e676ae08319](https://github.com/datastax/pulsar/commit/e676ae08319)
  \[fix\]\[broker\] Fix NPE when get
  /admin/v2/namespaces/public/default/maxTopicsPerNamespace (#16076)
- [25638e068be](https://github.com/datastax/pulsar/commit/25638e068be)
  \[improve\]\[java-client\] Only trigger the batch receive timeout when having
  pending batch receives requests (#16160)
- [dc27dee3ef8](https://github.com/datastax/pulsar/commit/dc27dee3ef8)
  \[fix\]\[Java Client\] Fix thread safety issue of `LastCumulativeAck` (#16072)
- [fbfaa516315](https://github.com/datastax/pulsar/commit/fbfaa516315)
  \[fix\]\[client\] Fix the startMessageId can't be respected as the
  ChunkMessageID (#16154)
- [208b0a8abc3](https://github.com/datastax/pulsar/commit/208b0a8abc3) Fix
  `messageQueue` release message issue. (#16155)
- [21f06632351](https://github.com/datastax/pulsar/commit/21f06632351)
  \[fix\]\[broker\]\[monitoring\] fix message ack rate (#16108)
- [f22a8779e31](https://github.com/datastax/pulsar/commit/f22a8779e31)
  \[fix\]\[txn\] Fix NPE when ack message with transaction at cnx = null
  (#16142)
- [04b3a81b87b](https://github.com/datastax/pulsar/commit/04b3a81b87b)
  \[Flakey-test\] fix flaky-test RackAwareTest.testRackUpdate (#16071)
- [5d92ad89ad7](https://github.com/datastax/pulsar/commit/5d92ad89ad7)
  \[fix\]\[broker\] Fix create client with TLS config (#16014)
- [6d37fb9b357](https://github.com/datastax/pulsar/commit/6d37fb9b357)
  \[fix\]\[broker\]Fix topic policies update not check message expiry (#15941)
- [3d8618711ea](https://github.com/datastax/pulsar/commit/3d8618711ea)
  \[Transaction\] Set TC state is Ready after open MLTransactionMetadataStore
  completely. (#13957)
- [6d4487a5346](https://github.com/datastax/pulsar/commit/6d4487a5346)
  \[improve\]\[tests\] improved flaky test runs (#16011)
- [92a8237c0a9](https://github.com/datastax/pulsar/commit/92a8237c0a9) \[ML\]
  Fix thread safety issues in ManagedCursorContainer related to "heap" field
  access (#16049)
- [ccda354b3ef](https://github.com/datastax/pulsar/commit/ccda354b3ef)
  \[improve\]\[broker\] Avoid reconnection when a partitioned topic was created
  concurrently (#16043)
- [c99b6ce0c16](https://github.com/datastax/pulsar/commit/c99b6ce0c16) rename
  pulsar_producer_configuration_set_crypto_failure_action to
  pulsar_producer_configuration_get_crypto_failure_action (#16031)
- [85cac9f87cb](https://github.com/datastax/pulsar/commit/85cac9f87cb)
  \[fix\]\[client\] Remove producer when close producer command is received
  (#16028)
- [c3f6c48063e](https://github.com/datastax/pulsar/commit/c3f6c48063e)
  \[fix\]\[admin\] Fix typo in validation message (#16021)
- [65109b23256](https://github.com/datastax/pulsar/commit/65109b23256)
  \[fix\]\[client\] Remove consumer when close consumer command is received
  (#15761)
- [251d1eded27](https://github.com/datastax/pulsar/commit/251d1eded27)
  \[Fix\]\[broker\] Fix NPE when ledger id not found in `OpReadEntry` (#15837)
- [09cb1026fea](https://github.com/datastax/pulsar/commit/09cb1026fea)
  \[improve\]\[broker\] Make PulsarWebResource#getOwnerFromPeerClusterList
  async. (#15940)
- [4e05c32c65b](https://github.com/datastax/pulsar/commit/4e05c32c65b)
  \[improve\]\[cli\] Pulsar shell: include pulsar-shell in released tarballs
- [a34536e27eb](https://github.com/datastax/pulsar/commit/a34536e27eb) Pulsar
  shell: support comments in file
- [83fbe08cf1c](https://github.com/datastax/pulsar/commit/83fbe08cf1c) Pulsar
  shell: disable jansi to avoid JVM crashes on Ubuntu

### `lunastreaming-all` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.0 \| pulsar-jms-2.4.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 1.0.2 \| pulsar-transformations-1.0.2.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.3 \|
cassandra-enhanced-pulsar-sink-1.6.3-nar.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.1 \| pulsar-io-data-generator-2.10.1.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.1 \| pulsar-io-elastic-search-2.10.1.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.1 \| pulsar-io-jdbc-clickhouse-2.10.1.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.1 \| pulsar-io-jdbc-mariadb-2.10.1.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.1 \| pulsar-io-jdbc-postgres-2.10.1.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.1 \| pulsar-io-jdbc-sqlite-2.10.1.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.1 \| pulsar-io-kafka-2.10.1.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.1 \| pulsar-io-kinesis-2.10.1.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \| Read
data from Cassandra \| 2.1.0 \| pulsar-cassandra-source-2.1.0.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.1 \| pulsar-io-data-generator-2.10.1.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.1 \| pulsar-io-debezium-mongodb-2.10.1.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.1 \| pulsar-io-debezium-mssql-2.10.1.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.1 \| pulsar-io-debezium-mysql-2.10.1.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.1 \| pulsar-io-debezium-oracle-2.10.1.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.1 \| pulsar-io-debezium-postgres-2.10.1.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.1 \| pulsar-io-kafka-2.10.1.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.1 \| pulsar-io-kinesis-2.10.1.1.nar \|

</details>


### `lunastreaming-experimental` distribution

<details><summary>Proxy extensions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka
Proxy Extension \| 2.10.0.3 \| pulsar-kafka-proxy-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Protocol handlers</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \|
Starlight for RabbitMQ Proxy Extension \| 2.10.0.1 \|
starlight-rabbitmq-2.10.0.1.nar \| \|
[kafka](https://github.com/datastax/starlight-for-kafka) \| Kafka Protocol
Handler \| 2.10.0.3 \| pulsar-protocol-handler-kafka-2.10.0.3.nar \| \|
[rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) \| Starlight for
RabbitMQ Proxy Extension \| 2.10.0.1 \| starlight-rabbitmq-2.10.0.1.nar \|

</details>

<details><summary>Filters</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [jms](https://pulsar.apache.org/docs/io-connectors) \| Starlight
for JMS

- support for server side filters \| 2.4.0 \| pulsar-jms-2.4.0-nar.nar \|

</details>

<details><summary>Functions</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [transforms](https://pulsar.apache.org/docs/io-connectors) \|
Transformation function \| 1.0.2 \| pulsar-transformations-1.0.2.nar \|

</details>

<details><summary>Sinks</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) \| A
DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R)
or DataStax Enterprise(DSE) \| 1.6.3 \|
cassandra-enhanced-pulsar-sink-1.6.3-nar.nar \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
Data Explorer (Kusto) Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [aerospike](https://pulsar.apache.org/docs/io-connectors) \| Aerospike
database sink \| 2.10.1.1 \| pulsar-io-aerospike-2.10.1.1.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.1 \|
pulsar-io-batch-data-generator-2.10.1.1.nar \| \|
[cloud-storage](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into cloud storage \| 2.10.0.4 \| pulsar-io-cloud-storage-2.10.0.4.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.1 \| pulsar-io-data-generator-2.10.1.1.nar \| \|
[elastic_search](https://pulsar.apache.org/docs/io-connectors) \| Writes data
into Elastic Search \| 2.10.1.1 \| pulsar-io-elastic-search-2.10.1.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.1 \| pulsar-io-flume-2.10.1.1.nar \| \|
[hbase](https://pulsar.apache.org/docs/io-connectors) \| Writes data into hbase
table \| 2.10.1.1 \| pulsar-io-hbase-2.10.1.1.nar \| \|
[hdfs2](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
2.x \| 2.10.1.1 \| pulsar-io-hdfs2-2.10.1.1.nar \| \|
[hdfs3](https://pulsar.apache.org/docs/io-connectors) \| Writes data into HDFS
3.x \| 2.10.1.1 \| pulsar-io-hdfs3-2.10.1.1.nar \| \|
[influxdb](https://pulsar.apache.org/docs/io-connectors) \| Writes data into
InfluxDB database \| 2.10.1.1 \| pulsar-io-influxdb-2.10.1.1.nar \| \|
[jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
ClickHouse \| 2.10.1.1 \| pulsar-io-jdbc-clickhouse-2.10.1.1.nar \| \|
[jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
MariaDB \| 2.10.1.1 \| pulsar-io-jdbc-mariadb-2.10.1.1.nar \| \|
[jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
PostgreSQL \| 2.10.1.1 \| pulsar-io-jdbc-postgres-2.10.1.1.nar \| \|
[jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) \| JDBC sink for
SQLite \| 2.10.1.1 \| pulsar-io-jdbc-sqlite-2.10.1.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.1 \| pulsar-io-kafka-2.10.1.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.1 \| pulsar-io-kinesis-2.10.1.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.1 \| pulsar-io-mongo-2.10.1.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.1 \| pulsar-io-rabbitmq-2.10.1.1.nar \| \|
[redis](https://pulsar.apache.org/docs/io-connectors) \| Writes data into Redis
\| 2.10.1.1 \| pulsar-io-redis-2.10.1.1.nar \| \|
[solr](https://pulsar.apache.org/docs/io-connectors) \| Writes data into solr
collection \| 2.10.1.1 \| pulsar-io-solr-2.10.1.1.nar \| \|
[snowflake](https://github.com/datastax/snowflake-connector) \| Snowflake
Connector \| 0.1.10 \| pulsar-snowflake-connector-0.1.10.nar \|

</details>

<details><summary>Sources</summary>


\| Name \| Description \| Version \| File \| \| ---- \| ----------- \| -------
\| ---- \| \|
[azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) \| Azure
DocumentDB Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar \| \|
[bigquery](https://github.com/datastax/pulsar-3rdparty-connector) \| Big Query
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar
\| \| [coap](https://github.com/datastax/pulsar-3rdparty-connector) \| CoAP
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar \|
\| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) \|
Couchbase Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar \| \|
[datadog](https://github.com/datastax/pulsar-3rdparty-connector) \| DataDog
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar
\| \| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) \|
Diffusion Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar \| \|
[geode](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache Geode
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar \|
\| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) \|
Hazelcast Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar \| \|
[humio](https://github.com/datastax/pulsar-3rdparty-connector) \| Humio
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar \|
\| [jms](https://github.com/datastax/pulsar-3rdparty-connector) \| JMS Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar \| \|
[Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) \| Kinetica
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar
\| \| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Kudu Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar \| \|
[marklogic](https://github.com/datastax/pulsar-3rdparty-connector) \| MarkLogic
Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar \| \|
[mqtt](https://github.com/datastax/pulsar-3rdparty-connector) \| MQTT Connector
\| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar \| \|
[neo4j](https://github.com/datastax/pulsar-3rdparty-connector) \| Neo4J
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar \|
\| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) \| New
Relic Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar \| \|
[orientdb](https://github.com/datastax/pulsar-3rdparty-connector) \| OrientDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar
\| \| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) \| Apache
Phoenix Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar \| \|
[plc4x](https://github.com/datastax/pulsar-3rdparty-connector) \| PLC4X
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar \|
\| [redis](https://github.com/datastax/pulsar-3rdparty-connector) \| Redis
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar \|
\| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) \| SAP HANA
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar
\| \| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) \|
SingleStore Connector \| 2.10.1.1 \|
pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar \| \|
[splunk](https://github.com/datastax/pulsar-3rdparty-connector) \| Splunk
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar
\| \| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) \| XTDB
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar \|
\| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) \| Zeebe
Connector \| 2.10.1.1 \| pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar \|
\| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) \|
Read data from Cassandra \| 2.1.0 \| pulsar-cassandra-source-2.1.0.nar \| \|
[batch-data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test
batch data generator source \| 2.10.1.1 \|
pulsar-io-batch-data-generator-2.10.1.1.nar \| \|
[canal](https://pulsar.apache.org/docs/io-connectors) \| canal source and read
data from mysql \| 2.10.1.1 \| pulsar-io-canal-2.10.1.1.nar \| \|
[data-generator](https://pulsar.apache.org/docs/io-connectors) \| Test data
generator source \| 2.10.1.1 \| pulsar-io-data-generator-2.10.1.1.nar \| \|
[debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MongoDb Source \| 2.10.1.1 \| pulsar-io-debezium-mongodb-2.10.1.1.nar \| \|
[debezium-mssql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Microsoft SQL Server Source \| 2.10.1.1 \| pulsar-io-debezium-mssql-2.10.1.1.nar
\| \| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) \| Debezium
MySql Source \| 2.10.1.1 \| pulsar-io-debezium-mysql-2.10.1.1.nar \| \|
[debezium-oracle](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Oracle Source \| 2.10.1.1 \| pulsar-io-debezium-oracle-2.10.1.1.nar \| \|
[debezium-postgres](https://pulsar.apache.org/docs/io-connectors) \| Debezium
Postgres Source \| 2.10.1.1 \| pulsar-io-debezium-postgres-2.10.1.1.nar \| \|
[dynamodb](https://pulsar.apache.org/docs/io-connectors) \| DynamoDB connectors
\| 2.10.1.1 \| pulsar-io-dynamodb-2.10.1.1.nar \| \|
[file](https://pulsar.apache.org/docs/io-connectors) \| Reads data from local
filesystem \| 2.10.1.1 \| pulsar-io-file-2.10.1.1.nar \| \|
[flume](https://pulsar.apache.org/docs/io-connectors) \| flume source and sink
connector \| 2.10.1.1 \| pulsar-io-flume-2.10.1.1.nar \| \|
[kafka](https://pulsar.apache.org/docs/io-connectors) \| Kafka source and sink
connector \| 2.10.1.1 \| pulsar-io-kafka-2.10.1.1.nar \| \|
[kafka-connect-adaptor](https://pulsar.apache.org/docs/io-connectors) \| Kafka
source connect adaptor \| 2.10.1.1 \|
pulsar-io-kafka-connect-adaptor-2.10.1.1.nar \| \|
[kinesis](https://pulsar.apache.org/docs/io-connectors) \| Kinesis connectors \|
2.10.1.1 \| pulsar-io-kinesis-2.10.1.1.nar \| \|
[mongo](https://pulsar.apache.org/docs/io-connectors) \| MongoDB source and sink
connector \| 2.10.1.1 \| pulsar-io-mongo-2.10.1.1.nar \| \|
[netty](https://pulsar.apache.org/docs/io-connectors) \| Netty Tcp or Udp Source
Connector \| 2.10.1.1 \| pulsar-io-netty-2.10.1.1.nar \| \|
[nsq](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from an NSQ
topic \| 2.10.1.1 \| pulsar-io-nsq-2.10.1.1.nar \| \|
[rabbitmq](https://pulsar.apache.org/docs/io-connectors) \| RabbitMQ source and
sink connector \| 2.10.1.1 \| pulsar-io-rabbitmq-2.10.1.1.nar \| \|
[twitter](https://pulsar.apache.org/docs/io-connectors) \| Ingest data from
Twitter firehose \| 2.10.1.1 \| pulsar-io-twitter-2.10.1.1.nar \|

</details>


## Luna Streaming Distribution 2.10 1.0

This is release contains new features such as Pulsar Transforms and Pulsar
Shell. It also contains several stability issues about transactions.

### Most notable commits

- [010629e5a39](https://github.com/datastax/pulsar/commit/010629e5a39) Add
  commons-text to LICENSE
- [6f636a1c24e](https://github.com/datastax/pulsar/commit/6f636a1c24e) Fix JDK
  11 compatibility
- [0c81490391c](https://github.com/datastax/pulsar/commit/0c81490391c)
  \[feature\]\[cli\] Pulsar shell - Env variables interpolation
- [3501b0ce7d4](https://github.com/datastax/pulsar/commit/3501b0ce7d4)
  \[feature\]\[cli\] Pulsar shell - add support for input files and pipe for
  running multiple commands - part 2
- [698f225d6d2](https://github.com/datastax/pulsar/commit/698f225d6d2)
  \[feature\]\[cli\] Pulsar Shell
- [57b80e25f49](https://github.com/datastax/pulsar/commit/57b80e25f49)
  \[fix\]\[client\] Fix JDK17 compatibility issue (#15964)
- [fa3dfdd5068](https://github.com/datastax/pulsar/commit/fa3dfdd5068)
  \[fix\]\[functions\] Handle uploading of builtin Functions to BK if
  uploadBuiltinSinksSources is true (#16111)
- [8d9c008f938](https://github.com/datastax/pulsar/commit/8d9c008f938)
  \[improve\]\[functions\] Use the classloader of the builtin Function in
  ThreadRuntime (#16092)
- [80af58eaff0](https://github.com/datastax/pulsar/commit/80af58eaff0)
  \[improve\]\[function\] Support Record\<?\> as WindowFunction output type
  (#16129)
- [9e24d8f6b7f](https://github.com/datastax/pulsar/commit/9e24d8f6b7f)
  \[improve\]\[function\] Allow not providing the class name when loading a
  Function nar file (#16079)
- [19b36c6b830](https://github.com/datastax/pulsar/commit/19b36c6b830)
  \[improve\]\[broker\] Reduce the consumers list sort by priority level
  (#16243)
- [b4f1126b943](https://github.com/datastax/pulsar/commit/b4f1126b943)
  \[fix\]\[branch-2.10\] Fix wrong unit of NIC speed on linux (#16166)
- [ba6fe1213b4](https://github.com/datastax/pulsar/commit/ba6fe1213b4)
  \[fix\]\[txn\] Ack the same batch message different batchIndex with
  transaction (#16032)
- [1d34c98e87f](https://github.com/datastax/pulsar/commit/1d34c98e87f)
  \[improvement\]\[broker\]: remove spammy log 'The count of topics on the
  bundle {} is less than 2, skip split!' (#16212)
- [8926fd2df65](https://github.com/datastax/pulsar/commit/8926fd2df65)
  Transactions: fix race in TransactionMetaStoreHandler (#16147)
- [4d7fe72c16c](https://github.com/datastax/pulsar/commit/4d7fe72c16c) PIP-105:
  new API to get subscription properties (#16095)
- [7e7a95b67b8](https://github.com/datastax/pulsar/commit/7e7a95b67b8)
  \[improve\]\[function\] Support Record\<?\> as Function output type (#16041)
- [15722152dc3](https://github.com/datastax/pulsar/commit/15722152dc3)
  \[improve\]\[admin\] Add option function-type to admin CLI for Functions
  (#16075)
- [eb525cfabcf](https://github.com/datastax/pulsar/commit/eb525cfabcf) Use
  OrderedExecutor instead of OrderedScheduler for consumer dispatch (#16115)
- [a71a2b5d57e](https://github.com/datastax/pulsar/commit/a71a2b5d57e)
  \[improve\]\[function\] Get function class name from the NAR when using
  built-in functions (#15693)
- [044c0a0a145](https://github.com/datastax/pulsar/commit/044c0a0a145)
  \[fix\]\[admin\] Fix check on create function class name (#15700)
- [c92e672d6d7](https://github.com/datastax/pulsar/commit/c92e672d6d7) Allow
  creating builtin functions in pulsar-admin CLI (#15671)
- [450a83db0d1](https://github.com/datastax/pulsar/commit/450a83db0d1) Parse
  function userConfig to Map\<String, Object\> (#15669)
- [03a80b0ce1b](https://github.com/datastax/pulsar/commit/03a80b0ce1b)
  \[improve\]\[pulsar-perf\] Transactions: improve client options (#16090)
- [870af8a495f](https://github.com/datastax/pulsar/commit/870af8a495f) \[Cli
  tools\] Disable Pulsar client memory limit by default (#15748)
- [acd6424a03c](https://github.com/datastax/pulsar/commit/acd6424a03c)
  \[pulsar-perf\] Change the default for max-connections from 100 to 1 (#15387)

### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.2-nar.nar
- pulsar-cassandra-source-2.1.0.nar
- pulsar-io-cloud-storage-2.10.0.4.nar
- pulsar-io-data-generator-2.10.1.0.nar
- pulsar-io-debezium-mongodb-2.10.1.0.nar
- pulsar-io-debezium-mssql-2.10.1.0.nar
- pulsar-io-debezium-mysql-2.10.1.0.nar
- pulsar-io-debezium-oracle-2.10.1.0.nar
- pulsar-io-debezium-postgres-2.10.1.0.nar
- pulsar-io-elastic-search-2.10.1.0.nar
- pulsar-io-jdbc-clickhouse-2.10.1.0.nar
- pulsar-io-jdbc-mariadb-2.10.1.0.nar
- pulsar-io-jdbc-postgres-2.10.1.0.nar
- pulsar-io-jdbc-sqlite-2.10.1.0.nar
- pulsar-io-kafka-2.10.1.0.nar
- pulsar-io-kinesis-2.10.1.0.nar
- pulsar-snowflake-connector-0.1.10.nar
- pulsar-transformations-1.0.2.nar
- pulsar-protocol-handler-kafka-2.10.0.3.nar
- starlight-rabbitmq-2.10.0.1.nar
- pulsar-kafka-proxy-2.10.0.3.nar
- pulsar-jms-2.4.0-nar.nar

## Luna Streaming Distribution 2.10 0.6

This is a maintenance release containing important stability and security
updates.

### Most notable commits

- [4930f6c45c2](https://github.com/datastax/pulsar/commit/4930f6c45c2)
  \[fix\]\[broker\]Fix topic-level replicator rate limiter not init (#15825)
- [421bf6dc957](https://github.com/datastax/pulsar/commit/421bf6dc957) Optimize
  topic policy with HierarchyTopicPolicies about replicatorDispatchRate (#14161)
- [3312986d869](https://github.com/datastax/pulsar/commit/3312986d869)
  \[broker\] Add config to allow deliverAt time to be strictly honored (#16068)
- [8d0c054d5fc](https://github.com/datastax/pulsar/commit/8d0c054d5fc) \[Issue
  15896\] Fix LockTimeout when storePut on the same key concurrently in
  RocksdbMetadataStore (#16005)
- [0e46a881bdc](https://github.com/datastax/pulsar/commit/0e46a881bdc) Clean up
  C++ client curl configuration (#16064)
- [ad3a814c37a](https://github.com/datastax/pulsar/commit/ad3a814c37a) Fix wrong
  response type for swagger definitions (#16022)
- [4923e15dcaf](https://github.com/datastax/pulsar/commit/4923e15dcaf)
  \[broker\] Make invalid namespace and topic name logs more descriptive
  (#16047)
- [7b556f44d70](https://github.com/datastax/pulsar/commit/7b556f44d70) \[ML\]
  When skipping updating mark delete position, execute callback with executor to
  prevent deadlock (#15971)
- [790ee2f72e2](https://github.com/datastax/pulsar/commit/790ee2f72e2)
  \[fix\]\[admin\] Fix producer/consume permission can&rsquo;t get schema
  (#15956) (#16026)
- [91ea44756f5](https://github.com/datastax/pulsar/commit/91ea44756f5)
  \[broker\]\[monitoring\] add message ack rate metric for consumer (#15674)
- [54e36a46603](https://github.com/datastax/pulsar/commit/54e36a46603)
  \[Function\] provide default error handler for function log appender (#15728)
- [6a7d024e5fb](https://github.com/datastax/pulsar/commit/6a7d024e5fb)
  \[fix\]\[security\] Add timeout of sync methods and avoid call sync method for
  AuthoriationService (#15694)
- [64f5de79a58](https://github.com/datastax/pulsar/commit/64f5de79a58)
  \[Broker\]make revokePermissionsOnTopic method async (#14149)
- [99f54cb8e31](https://github.com/datastax/pulsar/commit/99f54cb8e31)
  \[cleanup\]\[function\] refine file io connector (#15250)
- [666435c951e](https://github.com/datastax/pulsar/commit/666435c951e) \[fix\]
  \[admin\] fix reach max tenants error if the tenant already exists (#15961)
- [7f08804b4cc](https://github.com/datastax/pulsar/commit/7f08804b4cc)
  \[fix\]\[txn\] fix NPE of TransactionMetaStoreHandler (#15840)
- [353ffcbe9f9](https://github.com/datastax/pulsar/commit/353ffcbe9f9)
  \[feature\]\[admin\] Support to get topic properties. (#15944)
- [f12f06750b1](https://github.com/datastax/pulsar/commit/f12f06750b1)
  \[fix\]\[auth\] Generate correct well-known OpenID configuration URL (#15928)
- [1146c9c7368](https://github.com/datastax/pulsar/commit/1146c9c7368) Allow
  PULSAR_MEM & PULSAR_GC to be Overridden in pulsar_tool_env.sh (#15868)
- [ae7cd9c965b](https://github.com/datastax/pulsar/commit/ae7cd9c965b)
  \[fix\]\[pulsar\] Bump pyyaml from 5.3.1 to 5.4.1 to solve CVE-2020-14343
  (#15989)
- [2889092f6d7](https://github.com/datastax/pulsar/commit/2889092f6d7) Upgrade
  Netty Reactive Streams to 2.0.6 (#15990)
- [f95c371b3ff](https://github.com/datastax/pulsar/commit/f95c371b3ff) Removing
  log4j-1.2-api from dependencies (#15991)
- [64d8e0c3e20](https://github.com/datastax/pulsar/commit/64d8e0c3e20) Fix:
  org.apache.kafka.connect.errors.DataException: Not a struct schema:
  Schema{ARRAY} + tests (#15988)

### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.2-nar.nar
- pulsar-cassandra-source-2.1.0.nar
- pulsar-io-cloud-storage-2.10.0.4.nar
- pulsar-io-data-generator-2.10.0.6.nar
- pulsar-io-debezium-mongodb-2.10.0.6.nar
- pulsar-io-debezium-mssql-2.10.0.6.nar
- pulsar-io-debezium-mysql-2.10.0.6.nar
- pulsar-io-debezium-oracle-2.10.0.6.nar
- pulsar-io-debezium-postgres-2.10.0.6.nar
- pulsar-io-elastic-search-2.10.0.6.nar
- pulsar-io-jdbc-clickhouse-2.10.0.6.nar
- pulsar-io-jdbc-mariadb-2.10.0.6.nar
- pulsar-io-jdbc-postgres-2.10.0.6.nar
- pulsar-io-jdbc-sqlite-2.10.0.6.nar
- pulsar-io-kafka-2.10.0.6.nar
- pulsar-io-kinesis-2.10.0.6.nar
- pulsar-snowflake-connector-0.1.11-beta.nar
- pulsar-transformations-1.0.0.nar
- pulsar-protocol-handler-kafka-2.10.0.3.nar
- starlight-rabbitmq-2.10.0.1.nar
- pulsar-kafka-proxy-2.10.0.3.nar
- pulsar-jms-2.4.0-nar.nar

## Luna Streaming Distribution 2.10 0.5

This is a maintenance release containing important stability and security
updates.

### Most notable commits

- [bb6db424376](https://github.com/datastax/pulsar/commit/bb6db424376)
  \[Python\] Use MacOS 10.15 as the target OS version for Python wheel files
  (#15788)
- [5a5030587aa](https://github.com/datastax/pulsar/commit/5a5030587aa)
  \[Python\] Adjusted script to build wheel for Python 3.7 on Mac (#15407)
- [86cdc542c98](https://github.com/datastax/pulsar/commit/86cdc542c98)
  \[Fix\]\[Docker\] Add write permissions to /pulsar subdirectories to enable
  running as non-root user (#15769)
- [26236cd29f2](https://github.com/datastax/pulsar/commit/26236cd29f2)
  \[fix\]\[broker\] Fix creating producer failure when set backlog quota.
  (#15663)
- [a716a300415](https://github.com/datastax/pulsar/commit/a716a300415)
  \[fix\]\[sql\] Fix the decimal type error convert in json schema (#15687)
- [142689a902f](https://github.com/datastax/pulsar/commit/142689a902f)
  \[fix\]\[txn\]Fix transasction ack batch message (#15875)
- [cdb8c372909](https://github.com/datastax/pulsar/commit/cdb8c372909)
  \[improve\]\[tiered storage\] Reduce cpu usage when offloading the ledger
  (#15063)
- [ce9349ceffb](https://github.com/datastax/pulsar/commit/ce9349ceffb)
  \[fix\]\[broker\]Fast return if ack cumulative illegal (#15695)
- [168228c14e6](https://github.com/datastax/pulsar/commit/168228c14e6)
  \[Revert\] \[#15483\] Remove sensitive msg from consumer/producer stats log
  (#15817)
- [7a04b7ddee7](https://github.com/datastax/pulsar/commit/7a04b7ddee7) Avoid
  contended synchronized block on topic load (#15883)
- [06aa6c031e4](https://github.com/datastax/pulsar/commit/06aa6c031e4) Fix avro
  conversion order of registration (#15863)
- [8130645b4c0](https://github.com/datastax/pulsar/commit/8130645b4c0) Fix NPE
  in MessageDeduplication. (#15820)
- [57acd651ac5](https://github.com/datastax/pulsar/commit/57acd651ac5) fix bug
  in getNumberOfEntriesInStorage (#15627)
- [df5685f8c1d](https://github.com/datastax/pulsar/commit/df5685f8c1d) Sync
  topicPublishRateLimiter update (#15599)
- [f554598cc62](https://github.com/datastax/pulsar/commit/f554598cc62) \[feat\]
  \[tiered-storage\] Add pure S3 provider for the offloader (#15710)
- [29dc9a7b497](https://github.com/datastax/pulsar/commit/29dc9a7b497)
  \[fix\]\[ML\]Fix NPE when put value to `RangeCache`. (#15707)
- [4fd06d369ae](https://github.com/datastax/pulsar/commit/4fd06d369ae)
  \[fix\]\[broker-common\] expose configurationMetadataStore and
  localMetadataStore (#15661)
- [797aa0e696b](https://github.com/datastax/pulsar/commit/797aa0e696b)
  \[optimize\]\[txn\] Optimize transaction lowWaterMark to clean useless data
  faster (#15592)
- [a86141b7a0d](https://github.com/datastax/pulsar/commit/a86141b7a0d) Use
  dispatchRateLimiterLock to update dispatchRateLimiter. (#15601)
- [eef7d61efc5](https://github.com/datastax/pulsar/commit/eef7d61efc5)
  \[cleanup\] \[broker\] Remove useless code to avoid confusion in
  OpReadEntry#checkReadCompletion. (#15104)
- [378e19b63c7](https://github.com/datastax/pulsar/commit/378e19b63c7)
  \[Transaction\] Fix cursor readPosition is bigger than maxPosition in
  OpReadEntry (#14667)
- [cf7a72cba47](https://github.com/datastax/pulsar/commit/cf7a72cba47) Fix NPE
  when TableView handles null value message (#15951)
- [a3370e52e29](https://github.com/datastax/pulsar/commit/a3370e52e29) Upgrade
  BookKeeper to 4.14.5.1.0.1
- [f9da03ee823](https://github.com/datastax/pulsar/commit/f9da03ee823)
  \[fix\]\[connector\] KCA sinks: fix offset mapping when sanitizeTopicName=true
  (#15950)
- [a1251385cde](https://github.com/datastax/pulsar/commit/a1251385cde) Enable
  TCP/IP keepalive for all ZK client connections in all components (#15908)
- [f7fa04ca2e3](https://github.com/datastax/pulsar/commit/f7fa04ca2e3) \[ML\]
  Fix race condition in getManagedLedgerInternalStats when
  includeLedgerMetadata=true (#15918)
- [a52d1f99736](https://github.com/datastax/pulsar/commit/a52d1f99736)
  \[Broker\] Add timeout to closing CoordinationServiceImpl (#15777)
- [e2dea872548](https://github.com/datastax/pulsar/commit/e2dea872548) \[Broker,
  Functions, Websocket\] Disable memory limit controller in internal Pulsar
  clients (#15752)
- [d40383d6ec9](https://github.com/datastax/pulsar/commit/d40383d6ec9)
  \[PIP-146\] ManagedCursorInfo compression (#14542)
- [9bc493ddf90](https://github.com/datastax/pulsar/commit/9bc493ddf90) PIP-105
  add support for updating the Subscription properties (#15751)
- [9f5e0732cb3](https://github.com/datastax/pulsar/commit/9f5e0732cb3)
  \[improve\]\[connector\] JDBC sinks: support Avro specific datatypes (#15845)
- [177a9dd36ca](https://github.com/datastax/pulsar/commit/177a9dd36ca) Configure
  DLog Bookie, Pulsar, and Admin clients via pass through config (#15818)
- [b41bf129565](https://github.com/datastax/pulsar/commit/b41bf129565) Switch to
  rely on Netty for Hostname Verification (#15824)
- [8988740a1cb](https://github.com/datastax/pulsar/commit/8988740a1cb)
  \[fix\]\[python\]Fix generated Python protobuf code not compatible with latest
  protobuf package (#15846)
- [0e84d66ac33](https://github.com/datastax/pulsar/commit/0e84d66ac33)
  \[improve\]\[connector\] JDBC Sinks: support KeyValue schema (#15807)
- [9b6d2eafcd4](https://github.com/datastax/pulsar/commit/9b6d2eafcd4) Replaced
  unicode 'comma and space' as single glyph with regular comma and space
  characters (#15461)

### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.2-nar.nar
- pulsar-cassandra-source-2.1.0.nar
- pulsar-io-cloud-storage-2.10.0.4.nar
- pulsar-io-data-generator-2.10.0.5.nar
- pulsar-io-debezium-mongodb-2.10.0.5.nar
- pulsar-io-debezium-mssql-2.10.0.5.nar
- pulsar-io-debezium-mysql-2.10.0.5.nar
- pulsar-io-debezium-oracle-2.10.0.5.nar
- pulsar-io-debezium-postgres-2.10.0.5.nar
- pulsar-io-elastic-search-2.10.0.5.nar
- pulsar-io-jdbc-clickhouse-2.10.0.5.nar
- pulsar-io-jdbc-mariadb-2.10.0.5.nar
- pulsar-io-jdbc-postgres-2.10.0.5.nar
- pulsar-io-jdbc-sqlite-2.10.0.5.nar
- pulsar-io-kafka-2.10.0.5.nar
- pulsar-io-kinesis-2.10.0.5.nar
- pulsar-snowflake-connector-0.1.11-beta.nar
- pulsar-protocol-handler-kafka-2.10.0.1.nar
- starlight-rabbitmq-2.10.0.0.nar
- pulsar-kafka-proxy-2.10.0.1.nar
- pulsar-jms-2.4.0-nar.nar

## Luna Streaming Distribution 2.10 0.4

This is a maintenance release containing important security and stability
updates.

### Most notable commits

- [1b2a97888e3](https://github.com/datastax/pulsar/commit/1b2a97888e3)
  \[fix\]\[common\] Add back FutureUtil#waitForAll and FutureUtil#waitForAny
  methods with List parameter
- [1ba180cbc74](https://github.com/datastax/pulsar/commit/1ba180cbc74) PIP-105:
  Store Subscription properties
- [4a2f75e71eb](https://github.com/datastax/pulsar/commit/4a2f75e71eb)
  \[Broker\] Disable memory limit controller for broker client and replication
  clients (#15723)
- [abec5d8c3c2](https://github.com/datastax/pulsar/commit/abec5d8c3c2) \[enh\]
  Broker: make max size of Consumer metadata configurable (#15713)
- [ee43c96373f](https://github.com/datastax/pulsar/commit/ee43c96373f)
  \[fix\]\[owasp\] Fix false positive google-http-client-gson-1.41.0.jar
  (#15651)
- [4f85fbcc2d2](https://github.com/datastax/pulsar/commit/4f85fbcc2d2) \[enh\]
  Issue 15455: Pulsar Admin: create subscripion with Properties (PIP-105)
  (#15503) (#15681)
- [73c313664f9](https://github.com/datastax/pulsar/commit/73c313664f9)
  \[fix\]\[security\] Tiered storage: Upgrade Hadoop to 3.3.3 to get rid of
  CVE-2022-26612 (#15660)
- [95fddf691cd](https://github.com/datastax/pulsar/commit/95fddf691cd)
  \[fix\]\[broker\] Fix NPE when set `AutoTopicCreationOverride` (#15653)
- [7b37a8f63cf](https://github.com/datastax/pulsar/commit/7b37a8f63cf)
  \[fix\]\[broker\] fix MetadataStoreException\$NotFoundException while doing
  topic lookup (#15633)
- [b31898f9aae](https://github.com/datastax/pulsar/commit/b31898f9aae) Fix
  potential to add duplicated consumer (#15051)
- [602e8ad73b1](https://github.com/datastax/pulsar/commit/602e8ad73b1)
  \[cleanup\]\[broker\] Override close method to avoid caching exception
  (#15529)
- [c244892e7ee](https://github.com/datastax/pulsar/commit/c244892e7ee) \[Java
  Client\] Fix messages sent by producers without schema cannot be decoded
  (#15622)
- [c04bebcf0f3](https://github.com/datastax/pulsar/commit/c04bebcf0f3)
  \[improve\]\[common\] Use `Collection` to instead of `List` parameter type
  (#15329)
- [206b7a58668](https://github.com/datastax/pulsar/commit/206b7a58668)
  \[PIP-153\]\[optimize\]\[txn\] Optimize metadataPositions in MLPendingAckStore
  (#15137)
- [50fc82778e2](https://github.com/datastax/pulsar/commit/50fc82778e2)
  \[fix\]\[broker\] Fix to avoid TopicStatsImpl NPE even if producerName is null
  (#15502)
- [2579fae36ca](https://github.com/datastax/pulsar/commit/2579fae36ca) Fix http
  produce msg redirect issue. (#15551)
- [b7b447bab6e](https://github.com/datastax/pulsar/commit/b7b447bab6e)
  \[PIP-163\]\[Txn\]Add lowWaterMark check before appending entry to TB (#15424)
- [1055ae396a5](https://github.com/datastax/pulsar/commit/1055ae396a5)
  \[fix\]\[broker\]Close publishLimiter when disable it (#15520)
- [aa7f2081786](https://github.com/datastax/pulsar/commit/aa7f2081786)
  \[fix\]\[txn\] Topic transaction buffer recover don't close reader when throw
  RuntimeException (#15361)
- [37397912703](https://github.com/datastax/pulsar/commit/37397912703) Fix grant
  all permissions but can't list topic. (#15501)
- [4bcbf93b5d6](https://github.com/datastax/pulsar/commit/4bcbf93b5d6)
  \[Authorization\] Role with namespace produce authz can also get topics
  (#13773)
- [13f3c7922e2](https://github.com/datastax/pulsar/commit/13f3c7922e2)
  \[fix\]\[broker\] Fix MultiRolesTokenAuthorizationProvider `authorize` issue.
  (#15454)
- [4d3ea536808](https://github.com/datastax/pulsar/commit/4d3ea536808)
  \[security\] Remove sensitive msg from consumer/producer stats log (#15483)
- [bb900fcb287](https://github.com/datastax/pulsar/commit/bb900fcb287) Support
  handling single role and non-jwt-token in MultiRolesTokenAuthorizationProvider
  (#14857)
- [e3a0ad6c7d3](https://github.com/datastax/pulsar/commit/e3a0ad6c7d3)
  \[improve\]\[client\] improve logic when ACK grouping tracker checks
  duplicated message id (#15465)
- [550e14de451](https://github.com/datastax/pulsar/commit/550e14de451)
  \[Improve\]\[doc\] Add config of IO and acceptor threads in proxy (#15340)
- [c4ac6d50229](https://github.com/datastax/pulsar/commit/c4ac6d50229)
  \[fix\]\[package-management\] Fix the new path `/data` introduced regression
  (#15367)
- [f0700865253](https://github.com/datastax/pulsar/commit/f0700865253)
  \[improve\]\[java-client\] Add pending messages information while print the
  producer stats (#15440)
- [717b3459a9a](https://github.com/datastax/pulsar/commit/717b3459a9a) fix bug
  in contructor of RocksdbMetadataStore (#15405)
- [37e09eaf14c](https://github.com/datastax/pulsar/commit/37e09eaf14c)
  \[improve\]\[broker-web&websocket&proxy&function-worker\] Full-support set ssl
  provider, ciphers and protocols (#13740)
- [f7ce317244a](https://github.com/datastax/pulsar/commit/f7ce317244a)
  \[Improve\]\[admin\|client\] AsyncHttpConnector doesn't use the system
  properties configured (#15307)
- [4f7c7191c51](https://github.com/datastax/pulsar/commit/4f7c7191c51)
  \[Broker\] Fix typo in enum name and handle closing of the channel properly
  since writeAndFlush is asynchronous (#15384)
- [7d245e6d1e7](https://github.com/datastax/pulsar/commit/7d245e6d1e7) Add
  KeyStore support in WebSocket, Function Worker HTTPS Servers (#15084)
- [626c0de3948](https://github.com/datastax/pulsar/commit/626c0de3948)
  \[enh\]\[monitor\]: add metrics for pulsar web service thread pool (#14742)
- [3816b039331](https://github.com/datastax/pulsar/commit/3816b039331) \[CI\]
  Upgrade zlib version to 1.2.12 (#14964)
- [1fdbeee1e1a](https://github.com/datastax/pulsar/commit/1fdbeee1e1a)
  \[improve\]\[offloaders\] Upgrade JClouds to 2.5.0 (#15649)
- [eb03e976f3a](https://github.com/datastax/pulsar/commit/eb03e976f3a)
  \[Fix\]\[Txn\] Fix transaction PendingAck lowWaterMark (#15530)
- [e23a44f3289](https://github.com/datastax/pulsar/commit/e23a44f3289)
  \[Fix\]\[Txn\]Fix transaction component recover fillQueue (#15418)
- [f4fc76f2aec](https://github.com/datastax/pulsar/commit/f4fc76f2aec)
  \[Fix\]\[txn\] Make transaction stats consistent at end txn (#15472)
- [6b85f8a68e2](https://github.com/datastax/pulsar/commit/6b85f8a68e2) Upgrade
  Netty to 4.1.77.Final and netty-tcnative to 2.0.52.Final (#15646)

### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
- pulsar-cassandra-source-2.0.0.nar
- pulsar-io-data-generator-2.10.0.4.nar
- pulsar-io-debezium-mongodb-2.10.0.4.nar
- pulsar-io-debezium-mssql-2.10.0.4.nar
- pulsar-io-debezium-mysql-2.10.0.4.nar
- pulsar-io-debezium-oracle-2.10.0.4.nar
- pulsar-io-debezium-postgres-2.10.0.4.nar
- pulsar-io-elastic-search-2.10.0.4.nar
- pulsar-io-jdbc-clickhouse-2.10.0.4.nar
- pulsar-io-jdbc-mariadb-2.10.0.4.nar
- pulsar-io-jdbc-postgres-2.10.0.4.nar
- pulsar-io-jdbc-sqlite-2.10.0.4.nar
- pulsar-io-kafka-2.10.0.4.nar
- pulsar-io-kinesis-2.10.0.4.nar
- pulsar-snowflake-connector-0.1.9.nar
- pulsar-protocol-handler-kafka-2.10.0.1.nar
- starlight-rabbitmq-2.10.0.0.nar
- pulsar-kafka-proxy-2.10.0.1.nar
- pulsar-jms-2.3.0-nar.nar

## Luna Streaming Distribution 2.10 0.3

This is a maintenance release containing important stability updates.

### Most notable commits

- [b0a2a5e4fd0](https://github.com/datastax/pulsar/commit/b0a2a5e4fd0) fix:
  org.apache.kafka.connect.errors.DataException: Invalid Java object for schema
  with type... (#15598)
- [8ef565e8171](https://github.com/datastax/pulsar/commit/8ef565e8171)
  \[fix\]\[broker\] Fix deadlock in broker after race condition in topic
  creation failure (#15570)
- [2dba8e8084f](https://github.com/datastax/pulsar/commit/2dba8e8084f) Offloader
  metrics (#13833)
- [51e35187b50](https://github.com/datastax/pulsar/commit/51e35187b50) Pulsar
  Functions: allow a Function\<GenericObject,?\> to access the original Schema
  of the Message and use it (#14847)
- [b58211de4d4](https://github.com/datastax/pulsar/commit/b58211de4d4) Fix
  pulsar-client-all shade - include BookKeeper libraries
- [babea4bfb28](https://github.com/datastax/pulsar/commit/babea4bfb28) Upgrade
  to DataStax BookKeeper 4.14.5.1.0.0
- [19daad5a5bb](https://github.com/datastax/pulsar/commit/19daad5a5bb)
  \[fix\]\[test\] Add receive timeout to avoid block thread. (#15088)
- [41417f9d8dd](https://github.com/datastax/pulsar/commit/41417f9d8dd)
  \[WebSocket\] Fix MultiTopicReader#getConsumer ClassCastException (#15534)

### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
- pulsar-cassandra-source-2.0.0.nar
- pulsar-io-data-generator-2.10.0.3.nar
- pulsar-io-debezium-mongodb-2.10.0.3.nar
- pulsar-io-debezium-mssql-2.10.0.3.nar
- pulsar-io-debezium-mysql-2.10.0.3.nar
- pulsar-io-debezium-oracle-2.10.0.3.nar
- pulsar-io-debezium-postgres-2.10.0.3.nar
- pulsar-io-elastic-search-2.10.0.3.nar
- pulsar-io-jdbc-clickhouse-2.10.0.3.nar
- pulsar-io-jdbc-mariadb-2.10.0.3.nar
- pulsar-io-jdbc-postgres-2.10.0.3.nar
- pulsar-io-jdbc-sqlite-2.10.0.3.nar
- pulsar-io-kafka-2.10.0.3.nar
- pulsar-io-kinesis-2.10.0.3.nar
- pulsar-snowflake-connector-0.1.9.nar
- pulsar-protocol-handler-kafka-2.10.0.1.nar
- starlight-rabbitmq-2.10.0.0.nar
- pulsar-kafka-proxy-2.10.0.1.nar
- pulsar-jms-2.1.0-nar.nar

## Luna Streaming Distribution 2.10 0.2

This is a maintenance release containing important stability updates.

### Most notable commits

- [d0105dfe006](https://github.com/datastax/pulsar/commit/d0105dfe006) \[Proxy\]
  Remove unnecessary blocking DNS lookup in LookupProxyHandler (#15415)
- [de3fef3f49f](https://github.com/datastax/pulsar/commit/de3fef3f49f)
  \[Proxy/Client\] Fix DNS server denial-of-service issue when DNS entry expires
  (#15403)
- [91ab03c029f](https://github.com/datastax/pulsar/commit/91ab03c029f)
  \[fix\]\[kinesis-sink\] Handle Avro collections native types
  (GenericData.Array and Utf8 map keys) (#15432)
- [d30126b01d1](https://github.com/datastax/pulsar/commit/d30126b01d1)
  \[feat\]\[elasticsearch-sink\] Option to strip out non printable characters
  (#15431)
- [d65d6bd8e0e](https://github.com/datastax/pulsar/commit/d65d6bd8e0e)
  \[fix\]\[elasticsearch-sink\] Handle Avro collections native types
  (GenericData.Array and Utf8 map keys) (#15430)
- [bfa5a02ee7a](https://github.com/datastax/pulsar/commit/bfa5a02ee7a)
  \[feat\]\[elasticsearch\] Add hashed id support (#15428)
- [cfd467fd3f5](https://github.com/datastax/pulsar/commit/cfd467fd3f5)
  \[feat\]\[elasticsearch-sink\] Option to output canonical JSON (#15426)
- [bda6fdd32bc](https://github.com/datastax/pulsar/commit/bda6fdd32bc) Sinks:
  allow to reset --timeout-ms to zero
- [f2f6e607d6a](https://github.com/datastax/pulsar/commit/f2f6e607d6a) Include
  circe-checksum in pulsar-client dependency (#60)
- [97a7b3b049e](https://github.com/datastax/pulsar/commit/97a7b3b049e) Include
  correct bookkeeper jars in pulsar-client jar (#16)

### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
- pulsar-cassandra-source-2.0.0.nar
- pulsar-io-data-generator-2.10.0.2.nar
- pulsar-io-debezium-mongodb-2.10.0.2.nar
- pulsar-io-debezium-mssql-2.10.0.2.nar
- pulsar-io-debezium-mysql-2.10.0.2.nar
- pulsar-io-debezium-oracle-2.10.0.2.nar
- pulsar-io-debezium-postgres-2.10.0.2.nar
- pulsar-io-elastic-search-2.10.0.2.nar
- pulsar-io-jdbc-clickhouse-2.10.0.2.nar
- pulsar-io-jdbc-mariadb-2.10.0.2.nar
- pulsar-io-jdbc-postgres-2.10.0.2.nar
- pulsar-io-jdbc-sqlite-2.10.0.2.nar
- pulsar-io-kafka-2.10.0.2.nar
- pulsar-io-kinesis-2.10.0.2.nar
- pulsar-snowflake-connector-0.1.9.nar
- pulsar-protocol-handler-kafka-2.10.0.1.nar
- starlight-rabbitmq-2.10.0.0.nar
- pulsar-kafka-proxy-2.10.0.1.nar
