# Release notes for DataStax Luna Streaming Distribution

## About DataStax Luna Streaming Distribution

Luna Streaming Distribution 3.1 is compatible with Apache Pulsar&TRADE; 3.1
and subsequent releases.

### Components

- [DataStax Luna Streaming](https://github.com/datastax/pulsar) (Apache Pulsar
  3.1 fork)
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

This release adds these features to the original Apache Pulsar 3.1 release:

- Stability improvements
- Third party libraries updates for security fixes
- Dependency upgrades (for security, stability and performances)
- An enhanced ElasticSearch Pulsar IO Sink
- An enhanced version of Apache BookKeeper with security fixes

*Note:* The DataStax Luna Streaming Distribution is designed for Java 17.
However, because the product releases Docker images, you do not need to install
Java (8 or 17) in advance. Java 17 is bundled in the Docker image.

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

# Releases

## Luna Streaming Distribution 3.1 3.0
This is the initial release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar v3.1.3 release plus the following changes specific to Luna Streaming:

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 3.1.3.0 | pulsar-io-data-generator-3.1.3.0.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 3.1.3.0 | pulsar-io-elastic-search-3.1.3.0.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 3.1.3.0 | pulsar-io-http-3.1.3.0.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 3.1.3.0 | pulsar-io-jdbc-clickhouse-3.1.3.0.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 3.1.3.0 | pulsar-io-jdbc-mariadb-3.1.3.0.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 3.1.3.0 | pulsar-io-jdbc-openmldb-3.1.3.0.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 3.1.3.0 | pulsar-io-jdbc-postgres-3.1.3.0.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 3.1.3.0 | pulsar-io-jdbc-sqlite-3.1.3.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 3.1.3.0 | pulsar-io-kafka-3.1.3.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 3.1.3.0 | pulsar-io-kinesis-3.1.3.0.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 3.1.3.0 | pulsar-io-data-generator-3.1.3.0.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 3.1.3.0 | pulsar-io-debezium-mongodb-3.1.3.0.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 3.1.3.0 | pulsar-io-debezium-mssql-3.1.3.0.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 3.1.3.0 | pulsar-io-debezium-mysql-3.1.3.0.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 3.1.3.0 | pulsar-io-debezium-oracle-3.1.3.0.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 3.1.3.0 | pulsar-io-debezium-postgres-3.1.3.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 3.1.3.0 | pulsar-io-kafka-3.1.3.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 3.1.3.0 | pulsar-io-kinesis-3.1.3.0.nar |
</details>
<details><summary>Proxy extensions</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 3.1.3.0 | pulsar-kafka-proxy-3.1.3.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>
| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 3.1.3.0 | pulsar-protocol-handler-kafka-3.1.3.0.nar |
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

## Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.0/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.3.0.nar
- pulsar-io-jdbc-sqlite-3.1.3.0.nar
- pulsar-io-kinesis-3.1.3.0.nar
- pulsar-io-data-generator-3.1.3.0.nar
- pulsar-io-elastic-search-3.1.3.0.nar
- pulsar-io-jdbc-clickhouse-3.1.3.0.nar
- pulsar-io-debezium-oracle-3.1.3.0.nar
- pulsar-io-jdbc-openmldb-3.1.3.0.nar
- pulsar-io-jdbc-postgres-3.1.3.0.nar
- pulsar-io-debezium-mssql-3.1.3.0.nar
- pulsar-io-debezium-mysql-3.1.3.0.nar
- pulsar-io-jdbc-mariadb-3.1.3.0.nar
- pulsar-io-debezium-postgres-3.1.3.0.nar
- pulsar-io-http-3.1.3.0.nar
- pulsar-io-kafka-3.1.3.0.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.3.0.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.3.0.nar
- pulsar-jms-3.1.0-nar.nar

## Migrating from Luna Streaming 2.10
- Upgrade is fully supported for all the components (connectors included).
- Pulsar-SQL: If you're upgrading Pulsar SQL from 2.11 or earlier, you should copy config files from conf/presto to trino/conf. If you're downgrading Pulsar SQL to 2.11 or earlier from newer versions, do the vice-versa.
- Downgrade is not supported for Bookies, rest all components support downgrade. 
  - Description -
    - Pulsar 3.1 uses RocksDB 7.x which writes in a format that is not compatible with RocksDB 6.x which is used by LunaStreaming 2.10 via Bookkeeper 4.14.
  - References - 
    - Issue - [[Bug] Downgrade issue #22051 - apache/pulsar · GitHub](https://github.com/apache/pulsar/issues/22051)
    - PR - [Make RrocksDB checksum type configurable #3793](https://github.com/apache/bookkeeper/pull/3793)
- Prometheus client version has been changed from 0.5.0 to 0.16.0. Metric type UNTYPED is renamed to UNKNOWN.
  The metrics have been renamed because OpenMetrics's counter name needs a _total suffix.
  E.g `pulsar_expired_token_count` changed to `pulsar_expired_token_total`.
  - References -
  - PR - [Bump prometheus client version from 0.5.0 to 0.15.0](https://github.com/apache/pulsar/pull/13785)
  - PR - [Rename Pulsar txn metrics to specify OpenMetrics](https://github.com/apache/pulsar/pull/16581)
  - PR - [Rename Pulsar schema metrics to specify OpenMetrics](https://github.com/apache/pulsar/pull/16610)
  - PR - [Rename Pulsar lb metrics to specify OpenMetrics](https://github.com/apache/pulsar/pull/16611)
  - PR - [Bump prometheus client version from 0.15.0 to 0.16.0](https://github.com/apache/pulsar/pull/16591)