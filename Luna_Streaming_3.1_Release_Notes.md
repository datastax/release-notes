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

## Luna Streaming Distribution 3.1 4.8
This maintenance release of the DataStax Luna Streaming Distribution for 3.1 which includes important stability and security updates for Luna Streaming, as well as for the various connectors packaged alongside it, such as sinks, sources, functions, protocol extensions, proxy extensions, filters, and client extensions.

### Most notable commits

* [8ea3944](https://github.com/datastax/pulsar/commit/8ea3944) [fix][sec] Upgrade Avro to 1.11.4 to address CVE-2024-47561 (#23394)
* [2d95226](https://github.com/datastax/pulsar/commit/2d95226) [fix] Bump commons-io:commons-io from 2.8.0 to 2.14.0 (#23393)
* [58febad](https://github.com/datastax/pulsar/commit/58febad) [fix][sec][branch-3.0] Upgrade protobuf-java to 3.25.5 (#23356) (#23357)
* [4fa2584](https://github.com/datastax/pulsar/commit/4fa2584) Revert "[improve][broker] Reschedule reads with increasing backoff when no messages are dispatched (#23226)"
* [1d2de0b](https://github.com/datastax/pulsar/commit/1d2de0b) Revert "[fix][broker] Fix retry backoff for PersistentDispatcherMultipleConsumers (#23284)"
* [35d086e](https://github.com/datastax/pulsar/commit/35d086e) [fix][sec] Upgrade vertx to 4.5.10 to address CVE-2024-8391 (#23338)
* [818887d](https://github.com/datastax/pulsar/commit/818887d) [fix][build] Fix problem where git.commit.id.abbrev is missing in image tagging (#23337)
* [fc3d028](https://github.com/datastax/pulsar/commit/fc3d028) [fix][test] Fix flaky test LeaderElectionTest.revalidateLeaderWithinSameSession (#22383)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.13  | cassandra-enhanced-pulsar-sink-1.6.13-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.2   | pulsar-io-cloud-storage-3.2.2.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.8 | pulsar-io-data-generator-3.1.4.8.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.8 | pulsar-io-elastic-search-3.1.4.8.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.8 | pulsar-io-http-3.1.4.8.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.8 | pulsar-io-jdbc-clickhouse-3.1.4.8.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.8 | pulsar-io-jdbc-mariadb-3.1.4.8.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.8 | pulsar-io-jdbc-openmldb-3.1.4.8.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.8 | pulsar-io-jdbc-postgres-3.1.4.8.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.8 | pulsar-io-jdbc-sqlite-3.1.4.8.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.8 | pulsar-io-kafka-3.1.4.8.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.8 | pulsar-io-kinesis-3.1.4.8.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.15  | pulsar-snowflake-connector-0.1.15.nar         |
| [lakehouse](https://github.com/streamnative/pulsar-io-lakehouse)         | Lakehouse Connector                                                                                          | 3.3.1.6 | pulsar-io-lakehouse-3.3.1.6.nar               |
| [lakehouse-cloud](https://github.com/streamnative/pulsar-io-lakehouse)   | Lakehouse Cloud Connector                                                                                    | 3.3.1.6 | pulsar-io-lakehouse-3.3.1.6-cloud.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.3.0   | pulsar-cassandra-source-2.3.0.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.8 | pulsar-io-data-generator-3.1.4.8.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.8 | pulsar-io-debezium-mongodb-3.1.4.8.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.8 | pulsar-io-debezium-mssql-3.1.4.8.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.8 | pulsar-io-debezium-mysql-3.1.4.8.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.8 | pulsar-io-debezium-oracle-3.1.4.8.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.8 | pulsar-io-debezium-postgres-3.1.4.8.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.8 | pulsar-io-kafka-3.1.4.8.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.8 | pulsar-io-kinesis-3.1.4.8.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.0.3  | pulsar-kafka-proxy-3.1.0.3.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version  | File                                      |
|----------------------------------------------------------------|----------------------------------------|----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.0.3  | pulsar-protocol-handler-kafka-3.1.0.3.nar |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.3.0   | pulsar-cassandra-admin-2.3.0-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 5.0.4   | pulsar-jms-admin-5.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 5.0.4   | pulsar-jms-5.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.2.0   | pulsar-ai-tools-3.2.0.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.0   | pulsar-transformations-3.2.0.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


## Luna Streaming Distribution 3.1 4.7
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 20th September 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [38f90bd](https://github.com/datastax/pulsar/commit/38f90bd) upgrade opensearch sink to client 2.16 and tests to use server 2.16.0
* [c8b4b5d](https://github.com/datastax/pulsar/commit/c8b4b5d) [fix][broker] Fix incomplete NAR file extraction which prevents broker from starting (#23274)
* [c9adb43](https://github.com/datastax/pulsar/commit/c9adb43) [fix][io] Upgrade mssql server docker tag in DebeziumMsSqlContainer (#23318)
* [ceab81b](https://github.com/datastax/pulsar/commit/ceab81b) [fix][broker][branch-3.0] Fail fast if the extensible load manager failed to start (#23297) (#23302)
* [2498da0](https://github.com/datastax/pulsar/commit/2498da0) [fix][sql][branch-3.0] Fix UUID convert failed for JSON schema (#23292) | * 4d6310c](https://github.com/apache/pulsar/commit/4d6310c)
* [fe27172](https://github.com/datastax/pulsar/commit/fe27172) Added updated-datastax-license-version.sh to update datastax jar licenses while releasing 3.1 automatically
* [1b37382](https://github.com/datastax/pulsar/commit/1b37382) Revert "Update actions/upload-artifact to v4"
* [8997b77](https://github.com/datastax/pulsar/commit/8997b77) Update actions/upload-artifact to v4

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.12  | cassandra-enhanced-pulsar-sink-1.6.12-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.0   | pulsar-io-cloud-storage-3.2.0.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.7 | pulsar-io-data-generator-3.1.4.7.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.7 | pulsar-io-elastic-search-3.1.4.7.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.7 | pulsar-io-http-3.1.4.7.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.7 | pulsar-io-jdbc-clickhouse-3.1.4.7.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.7 | pulsar-io-jdbc-mariadb-3.1.4.7.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.7 | pulsar-io-jdbc-openmldb-3.1.4.7.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.7 | pulsar-io-jdbc-postgres-3.1.4.7.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.7 | pulsar-io-jdbc-sqlite-3.1.4.7.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.7 | pulsar-io-kafka-3.1.4.7.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.7 | pulsar-io-kinesis-3.1.4.7.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.14  | pulsar-snowflake-connector-0.1.14.nar         |
| [lakehouse](https://github.com/streamnative/pulsar-io-lakehouse) | Lakehouse Connector | 3.3.1.6   | pulsar-io-lakehouse-3.3.1.6.nar         |
| [lakehouse-cloud](https://github.com/streamnative/pulsar-io-lakehouse) | Lakehouse Cloud Connector | 3.3.1.6   | pulsar-io-lakehouse-3.3.1.6-cloud.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.7 | pulsar-io-data-generator-3.1.4.7.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.7 | pulsar-io-debezium-mongodb-3.1.4.7.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.7 | pulsar-io-debezium-mssql-3.1.4.7.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.7 | pulsar-io-debezium-mysql-3.1.4.7.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.7 | pulsar-io-debezium-oracle-3.1.4.7.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.7 | pulsar-io-debezium-postgres-3.1.4.7.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.7 | pulsar-io-kafka-3.1.4.7.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.7 | pulsar-io-kinesis-3.1.4.7.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.0.1  | pulsar-kafka-proxy-3.1.0.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version   | File                                      |
|----------------------------------------------------------------|----------------------------------------|-----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.0.1   | pulsar-protocol-handler-kafka-3.1.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 5.0.4   | pulsar-jms-admin-5.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 5.0.4   | pulsar-jms-5.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.9   | pulsar-ai-tools-3.1.9.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.9   | pulsar-transformations-3.1.9.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.7.nar
- pulsar-io-jdbc-sqlite-3.1.4.7.nar
- pulsar-io-kinesis-3.1.4.7.nar
- pulsar-io-data-generator-3.1.4.7.nar
- pulsar-io-elastic-search-3.1.4.7.nar
- pulsar-io-jdbc-clickhouse-3.1.4.7.nar
- pulsar-io-debezium-oracle-3.1.4.7.nar
- pulsar-io-jdbc-openmldb-3.1.4.7.nar
- pulsar-io-jdbc-postgres-3.1.4.7.nar
- pulsar-io-debezium-mssql-3.1.4.7.nar
- pulsar-io-debezium-mysql-3.1.4.7.nar
- pulsar-io-jdbc-mariadb-3.1.4.7.nar
- pulsar-io-debezium-postgres-3.1.4.7.nar
- pulsar-io-http-3.1.4.7.nar
- pulsar-io-kafka-3.1.4.7.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.6
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 12th September 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [43249a0](https://github.com/datastax/pulsar/commit/43249a0) Add vi/vim to luna 31 images (#310)
* [b0c3ffb](https://github.com/datastax/pulsar/commit/b0c3ffb) [improve][broker] Part 2 of PIP-370: add metrics "pulsar_replication_disconnected_count" (#23213)
* [ada390b](https://github.com/datastax/pulsar/commit/ada390b) [improve][broker] Phase 1 of PIP-370 support disable create topics on remote cluster through replication  (#23169)
* [751aea3](https://github.com/datastax/pulsar/commit/751aea3) AS-4027: add string write function (#308)
* [7b7d335](https://github.com/datastax/pulsar/commit/7b7d335) [fix][log] Do not print warn log when concurrently publishing and switching ledgers (#23209)
* [8ad5249](https://github.com/datastax/pulsar/commit/8ad5249) [fix][client] the nullValue in msgMetadata should be true by default (#22372)
* [959f80b](https://github.com/datastax/pulsar/commit/959f80b) [improve][client] Don't print info logs for each schema loaded by client (#23206)
* [336d5d6](https://github.com/datastax/pulsar/commit/336d5d6) [improve][broker] Improve pulsar_topic_load_failed metric to record correct failed time (#23199)
* [c29f36a](https://github.com/datastax/pulsar/commit/c29f36a) [improve][broker] Optimize high CPU usage when consuming from topics with ongoing txn (#23189)
* [7047c2c](https://github.com/datastax/pulsar/commit/7047c2c) [fix] [broker] Topic can never be loaded up due to broker maintains a failed topic creation future (#23184)
* [8d7f750](https://github.com/datastax/pulsar/commit/8d7f750) [fix][broker] Skip reading entries from closed cursor. (#22751)
* [ae7a71c](https://github.com/datastax/pulsar/commit/ae7a71c) [improve] [broker] Optimize performance for checking max topics when the topic is a system topic (#23185)
*  [6c6f6bf](https://github.com/datastax/pulsar/commit/6c6f6bf) [improve][broker] Should notify bundle ownership listener onLoad event when ServiceUnitState start (ExtensibleLoadManagerImpl only)
* [69064c3](https://github.com/datastax/pulsar/commit/69064c3) [improve][broker] Support customized shadow managed ledger implementation (#23179)
* [b463ba4](https://github.com/datastax/pulsar/commit/b463ba4) [fix][test] Fix flaky SubscriptionSeekTest.testSeekIsByReceive (#23170)
* [e3b9cdc](https://github.com/datastax/pulsar/commit/e3b9cdc) [feat] Add scripts for updating BK RocksDB ini files (#23178)
* [42e9157](https://github.com/datastax/pulsar/commit/42e9157) [fix][client] Copy orderingKey to retry letter topic and DLQ messages and fix bug in copying (#23182)
* [ef00bb2](https://github.com/datastax/pulsar/commit/ef00bb2) [fix] DLQ to handle bytes key properly (#23172)
* [bb6c14f](https://github.com/datastax/pulsar/commit/bb6c14f) [fix][broker] Fix shadow topics cannot be consumed when the entry is not cached (#23147)
* [c228b5d](https://github.com/datastax/pulsar/commit/c228b5d) [improve] [broker] Avoid subscription fenced error with consumer.seek whenever possible (#23163)
* [b8aa905](https://github.com/datastax/pulsar/commit/b8aa905) [fix][client] Create the retry producer async (#23157)
* [bdfc591](https://github.com/datastax/pulsar/commit/bdfc591) [fix][client] Fix for early hit `beforeConsume` for MultiTopicConsumer (#23141)
* [b04b905](https://github.com/datastax/pulsar/commit/b04b905) [improve][proxy] Reuse authentication instance in pulsar-proxy (#23113)
* [b46125e](https://github.com/datastax/pulsar/commit/b46125e) [improve] [client]Add new ServiceUrlProvider implementation: SameAuthParamsAutoClusterFailover (#23129)
* [68db449](https://github.com/datastax/pulsar/commit/68db449) [fix] [broker] Let Pending ack handler can retry to init when encounters a metadata store error (#23153)
* [b3d47d2](https://github.com/datastax/pulsar/commit/b3d47d2) [fix][broker] Fix 'Disabled replicated subscriptions controller' logic and logging (#23142)
* [e16a0e2](https://github.com/datastax/pulsar/commit/e16a0e2) [improve][broker] Explicitly close LB internal topics when playing a follower (ExtensibleLoadManagerImpl only) (#23144)
* [6cfacf2](https://github.com/datastax/pulsar/commit/6cfacf2) [fix] [broker] Fix compatibility issues for PIP-344 (#23136)
* [62fbcc9](https://github.com/datastax/pulsar/commit/62fbcc9) [improve][client] Add maxConnectionsPerHost and connectionMaxIdleSeconds to PulsarAdminBuilder (#22541)
* [5149aef](https://github.com/datastax/pulsar/commit/5149aef) [improve][misc] Upgrade jersey to 2.41 (#22290)
* [2455b1e](https://github.com/datastax/pulsar/commit/2455b1e) [fix][broker] Fix the bug that elected leader thinks it's a follower (#23138)
* [fcb4809](https://github.com/datastax/pulsar/commit/fcb4809) [improve][fn] Add support for overriding additionalJavaRuntimeArguments with PF_additionalJavaRuntimeArguments env (#23130)
* [be739ab](https://github.com/datastax/pulsar/commit/be739ab) [fix][client] Fix timeout handling in Pulsar Admin client (#23128)
* [9eca32d](https://github.com/datastax/pulsar/commit/9eca32d) [fix][fn] Make python install dependencies from requirements.txt (#20174)
* [13b6669](https://github.com/datastax/pulsar/commit/13b6669) [improve][misc] Optimize TLS performance by omitting extra buffer copies (#23115)
* [fcd02df](https://github.com/datastax/pulsar/commit/fcd02df) [improve][broker] Reduce the CPU pressure from the transaction buffer in rolling restarts (#23062)
* [ef1eacc](https://github.com/datastax/pulsar/commit/ef1eacc) [improve][broker] Support to specify auth-plugin, auth-parameters and tls-enable arguments when init cluster metadata (#23087) (#23126)
* [f598675](https://github.com/datastax/pulsar/commit/f598675) [improve][misc] Improve AES-GCM cipher performance (#23122)
* [26e63e1](https://github.com/datastax/pulsar/commit/26e63e1) [fix][broker] Handle the case when `getOwnedServiceUnits` fails gracefully (#23119)
* [156ce19](https://github.com/datastax/pulsar/commit/156ce19) [fix][broker]A failed consumer/producer future in ServerCnx can never be removed (#23123)
* [d2a8e86](https://github.com/datastax/pulsar/commit/d2a8e86) [fix][broker] Fix authenticate order in AuthenticationProviderList (#23111)
* [415f283](https://github.com/datastax/pulsar/commit/415f283) [fix][broker] type cast on exceptions in exceptionally can lead to lost calls (#23117)
* [b0a40f4](https://github.com/datastax/pulsar/commit/b0a40f4) [fix][broker] fix exception may hidden and result in stuck when topic loading (#23102)
* [85150dc](https://github.com/datastax/pulsar/commit/85150dc) [fix] [broker] fix replicated namespaces filter in filterAndUnloadMatchedNamespaceAsync (#23100)
* [e322642](https://github.com/datastax/pulsar/commit/e322642) [improve][broker]Reuse method getAvailableBrokersAsync (#23099)
* [5631b66](https://github.com/datastax/pulsar/commit/5631b66) [fix][client] TransactionCoordinatorClient support retry (#23081)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.12  | cassandra-enhanced-pulsar-sink-1.6.12-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.0   | pulsar-io-cloud-storage-3.2.0.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.6 | pulsar-io-data-generator-3.1.4.6.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.6 | pulsar-io-elastic-search-3.1.4.6.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.6 | pulsar-io-http-3.1.4.6.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.6 | pulsar-io-jdbc-clickhouse-3.1.4.6.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.6 | pulsar-io-jdbc-mariadb-3.1.4.6.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.6 | pulsar-io-jdbc-openmldb-3.1.4.6.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.6 | pulsar-io-jdbc-postgres-3.1.4.6.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.6 | pulsar-io-jdbc-sqlite-3.1.4.6.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.6 | pulsar-io-kafka-3.1.4.6.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.6 | pulsar-io-kinesis-3.1.4.6.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.14  | pulsar-snowflake-connector-0.1.14.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.6 | pulsar-io-data-generator-3.1.4.6.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.6 | pulsar-io-debezium-mongodb-3.1.4.6.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.6 | pulsar-io-debezium-mssql-3.1.4.6.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.6 | pulsar-io-debezium-mysql-3.1.4.6.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.6 | pulsar-io-debezium-oracle-3.1.4.6.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.6 | pulsar-io-debezium-postgres-3.1.4.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.6 | pulsar-io-kafka-3.1.4.6.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.6 | pulsar-io-kinesis-3.1.4.6.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.0.1  | pulsar-kafka-proxy-3.1.0.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version   | File                                      |
|----------------------------------------------------------------|----------------------------------------|-----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.0.1   | pulsar-protocol-handler-kafka-3.1.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 5.0.4   | pulsar-jms-admin-5.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 5.0.4   | pulsar-jms-5.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.9   | pulsar-ai-tools-3.1.9.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.9   | pulsar-transformations-3.1.9.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.6.nar
- pulsar-io-jdbc-sqlite-3.1.4.6.nar
- pulsar-io-kinesis-3.1.4.6.nar
- pulsar-io-data-generator-3.1.4.6.nar
- pulsar-io-elastic-search-3.1.4.6.nar
- pulsar-io-jdbc-clickhouse-3.1.4.6.nar
- pulsar-io-debezium-oracle-3.1.4.6.nar
- pulsar-io-jdbc-openmldb-3.1.4.6.nar
- pulsar-io-jdbc-postgres-3.1.4.6.nar
- pulsar-io-debezium-mssql-3.1.4.6.nar
- pulsar-io-debezium-mysql-3.1.4.6.nar
- pulsar-io-jdbc-mariadb-3.1.4.6.nar
- pulsar-io-debezium-postgres-3.1.4.6.nar
- pulsar-io-http-3.1.4.6.nar
- pulsar-io-kafka-3.1.4.6.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.5
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 26th August 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [43249a0](https://github.com/datastax/pulsar/commit/43249a0) Add vi/vim to luna 31 images (#310)
* [b0c3ffb](https://github.com/datastax/pulsar/commit/b0c3ffb) [improve][broker] Part 2 of PIP-370: add metrics "pulsar_replication_disconnected_count" (#23213)
* [ada390b](https://github.com/datastax/pulsar/commit/ada390b) [improve][broker] Phase 1 of PIP-370 support disable create topics on remote cluster through replication  (#23169)
* [751aea3](https://github.com/datastax/pulsar/commit/751aea3) AS-4027: add string write function (#308)
* [7b7d335](https://github.com/datastax/pulsar/commit/7b7d335) [fix][log] Do not print warn log when concurrently publishing and switching ledgers (#23209)
* [8ad5249](https://github.com/datastax/pulsar/commit/8ad5249) [fix][client] the nullValue in msgMetadata should be true by default (#22372)
* [959f80b](https://github.com/datastax/pulsar/commit/959f80b) [improve][client] Don't print info logs for each schema loaded by client (#23206)
* [336d5d6](https://github.com/datastax/pulsar/commit/336d5d6) [improve][broker] Improve pulsar_topic_load_failed metric to record correct failed time (#23199)
* [c29f36a](https://github.com/datastax/pulsar/commit/c29f36a) [improve][broker] Optimize high CPU usage when consuming from topics with ongoing txn (#23189)
* [7047c2c](https://github.com/datastax/pulsar/commit/7047c2c) [fix] [broker] Topic can never be loaded up due to broker maintains a failed topic creation future (#23184)
* [8d7f750](https://github.com/datastax/pulsar/commit/8d7f750) [fix][broker] Skip reading entries from closed cursor. (#22751)
* [ae7a71c](https://github.com/datastax/pulsar/commit/ae7a71c) [improve] [broker] Optimize performance for checking max topics when the topic is a system topic (#23185)
*  [6c6f6bf](https://github.com/datastax/pulsar/commit/6c6f6bf) [improve][broker] Should notify bundle ownership listener onLoad event when ServiceUnitState start (ExtensibleLoadManagerImpl only)
* [69064c3](https://github.com/datastax/pulsar/commit/69064c3) [improve][broker] Support customized shadow managed ledger implementation (#23179)
* [b463ba4](https://github.com/datastax/pulsar/commit/b463ba4) [fix][test] Fix flaky SubscriptionSeekTest.testSeekIsByReceive (#23170)
* [e3b9cdc](https://github.com/datastax/pulsar/commit/e3b9cdc) [feat] Add scripts for updating BK RocksDB ini files (#23178)
* [42e9157](https://github.com/datastax/pulsar/commit/42e9157) [fix][client] Copy orderingKey to retry letter topic and DLQ messages and fix bug in copying (#23182)
* [ef00bb2](https://github.com/datastax/pulsar/commit/ef00bb2) [fix] DLQ to handle bytes key properly (#23172)
* [bb6c14f](https://github.com/datastax/pulsar/commit/bb6c14f) [fix][broker] Fix shadow topics cannot be consumed when the entry is not cached (#23147)
* [c228b5d](https://github.com/datastax/pulsar/commit/c228b5d) [improve] [broker] Avoid subscription fenced error with consumer.seek whenever possible (#23163)
* [b8aa905](https://github.com/datastax/pulsar/commit/b8aa905) [fix][client] Create the retry producer async (#23157)
* [bdfc591](https://github.com/datastax/pulsar/commit/bdfc591) [fix][client] Fix for early hit `beforeConsume` for MultiTopicConsumer (#23141)
* [b04b905](https://github.com/datastax/pulsar/commit/b04b905) [improve][proxy] Reuse authentication instance in pulsar-proxy (#23113)
* [b46125e](https://github.com/datastax/pulsar/commit/b46125e) [improve] [client]Add new ServiceUrlProvider implementation: SameAuthParamsAutoClusterFailover (#23129)
* [68db449](https://github.com/datastax/pulsar/commit/68db449) [fix] [broker] Let Pending ack handler can retry to init when encounters a metadata store error (#23153)
* [b3d47d2](https://github.com/datastax/pulsar/commit/b3d47d2) [fix][broker] Fix 'Disabled replicated subscriptions controller' logic and logging (#23142)
* [e16a0e2](https://github.com/datastax/pulsar/commit/e16a0e2) [improve][broker] Explicitly close LB internal topics when playing a follower (ExtensibleLoadManagerImpl only) (#23144)
* [6cfacf2](https://github.com/datastax/pulsar/commit/6cfacf2) [fix] [broker] Fix compatibility issues for PIP-344 (#23136)
* [62fbcc9](https://github.com/datastax/pulsar/commit/62fbcc9) [improve][client] Add maxConnectionsPerHost and connectionMaxIdleSeconds to PulsarAdminBuilder (#22541)
* [5149aef](https://github.com/datastax/pulsar/commit/5149aef) [improve][misc] Upgrade jersey to 2.41 (#22290)
* [2455b1e](https://github.com/datastax/pulsar/commit/2455b1e) [fix][broker] Fix the bug that elected leader thinks it's a follower (#23138)
* [fcb4809](https://github.com/datastax/pulsar/commit/fcb4809) [improve][fn] Add support for overriding additionalJavaRuntimeArguments with PF_additionalJavaRuntimeArguments env (#23130)
* [be739ab](https://github.com/datastax/pulsar/commit/be739ab) [fix][client] Fix timeout handling in Pulsar Admin client (#23128)
* [9eca32d](https://github.com/datastax/pulsar/commit/9eca32d) [fix][fn] Make python install dependencies from requirements.txt (#20174)
* [13b6669](https://github.com/datastax/pulsar/commit/13b6669) [improve][misc] Optimize TLS performance by omitting extra buffer copies (#23115)
* [fcd02df](https://github.com/datastax/pulsar/commit/fcd02df) [improve][broker] Reduce the CPU pressure from the transaction buffer in rolling restarts (#23062)
* [ef1eacc](https://github.com/datastax/pulsar/commit/ef1eacc) [improve][broker] Support to specify auth-plugin, auth-parameters and tls-enable arguments when init cluster metadata (#23087) (#23126)
* [f598675](https://github.com/datastax/pulsar/commit/f598675) [improve][misc] Improve AES-GCM cipher performance (#23122)
* [26e63e1](https://github.com/datastax/pulsar/commit/26e63e1) [fix][broker] Handle the case when `getOwnedServiceUnits` fails gracefully (#23119)
* [156ce19](https://github.com/datastax/pulsar/commit/156ce19) [fix][broker]A failed consumer/producer future in ServerCnx can never be removed (#23123)
* [d2a8e86](https://github.com/datastax/pulsar/commit/d2a8e86) [fix][broker] Fix authenticate order in AuthenticationProviderList (#23111)
* [415f283](https://github.com/datastax/pulsar/commit/415f283) [fix][broker] type cast on exceptions in exceptionally can lead to lost calls (#23117)
* [b0a40f4](https://github.com/datastax/pulsar/commit/b0a40f4) [fix][broker] fix exception may hidden and result in stuck when topic loading (#23102)
* [85150dc](https://github.com/datastax/pulsar/commit/85150dc) [fix] [broker] fix replicated namespaces filter in filterAndUnloadMatchedNamespaceAsync (#23100)
* [e322642](https://github.com/datastax/pulsar/commit/e322642) [improve][broker]Reuse method getAvailableBrokersAsync (#23099)
* [5631b66](https://github.com/datastax/pulsar/commit/5631b66) [fix][client] TransactionCoordinatorClient support retry (#23081)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11  | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.0   | pulsar-io-cloud-storage-3.2.0.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.5 | pulsar-io-data-generator-3.1.4.5.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.5 | pulsar-io-elastic-search-3.1.4.5.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.5 | pulsar-io-http-3.1.4.5.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.5 | pulsar-io-jdbc-clickhouse-3.1.4.5.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.5 | pulsar-io-jdbc-mariadb-3.1.4.5.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.5 | pulsar-io-jdbc-openmldb-3.1.4.5.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.5 | pulsar-io-jdbc-postgres-3.1.4.5.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.5 | pulsar-io-jdbc-sqlite-3.1.4.5.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.5 | pulsar-io-kafka-3.1.4.5.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.5 | pulsar-io-kinesis-3.1.4.5.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.14  | pulsar-snowflake-connector-0.1.14.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.5 | pulsar-io-data-generator-3.1.4.5.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.5 | pulsar-io-debezium-mongodb-3.1.4.5.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.5 | pulsar-io-debezium-mssql-3.1.4.5.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.5 | pulsar-io-debezium-mysql-3.1.4.5.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.5 | pulsar-io-debezium-oracle-3.1.4.5.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.5 | pulsar-io-debezium-postgres-3.1.4.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.5 | pulsar-io-kafka-3.1.4.5.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.5 | pulsar-io-kinesis-3.1.4.5.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.0.1  | pulsar-kafka-proxy-3.1.0.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version   | File                                      |
|----------------------------------------------------------------|----------------------------------------|-----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.0.1   | pulsar-protocol-handler-kafka-3.1.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 5.0.4   | pulsar-jms-admin-5.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 5.0.4   | pulsar-jms-5.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.9   | pulsar-ai-tools-3.1.9.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.9   | pulsar-transformations-3.1.9.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.5.nar
- pulsar-io-jdbc-sqlite-3.1.4.5.nar
- pulsar-io-kinesis-3.1.4.5.nar
- pulsar-io-data-generator-3.1.4.5.nar
- pulsar-io-elastic-search-3.1.4.5.nar
- pulsar-io-jdbc-clickhouse-3.1.4.5.nar
- pulsar-io-debezium-oracle-3.1.4.5.nar
- pulsar-io-jdbc-openmldb-3.1.4.5.nar
- pulsar-io-jdbc-postgres-3.1.4.5.nar
- pulsar-io-debezium-mssql-3.1.4.5.nar
- pulsar-io-debezium-mysql-3.1.4.5.nar
- pulsar-io-jdbc-mariadb-3.1.4.5.nar
- pulsar-io-debezium-postgres-3.1.4.5.nar
- pulsar-io-http-3.1.4.5.nar
- pulsar-io-kafka-3.1.4.5.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.4
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 30th June 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [f5eebae](https://github.com/datastax/pulsar/commit/f5eebae) [improve][broker] Optimize the performance of individual acknowledgments (#23072)
* [148077c](https://github.com/datastax/pulsar/commit/148077c) [fix] [broker] Internal reader of __change_events can not started after metadata store session rebuilt (#23018)
* [de5ccbd](https://github.com/datastax/pulsar/commit/de5ccbd) [improve][ci] Switch to use DEVELOCITY_ACCESS_KEY from GRADLE_ENTERPRISE_ACCESS_KEY (#23090)
* [453d964](https://github.com/datastax/pulsar/commit/453d964) [improve] [broker] Check max producers/consumers limitation first before other ops to save resources (#23074)
* [f5da2bf](https://github.com/datastax/pulsar/commit/f5da2bf) [fix] [broker] Remove blocking calls from Subscription.getStats (#23088)
* [c2fda68](https://github.com/datastax/pulsar/commit/c2fda68) [fix][client] Fix negative acknowledgement by messageId (#23060)
* [4b715b6](https://github.com/datastax/pulsar/commit/4b715b6) [fix][broker] Handle BucketDelayedDeliveryTracker recover failed (#22735)
* [8124284](https://github.com/datastax/pulsar/commit/8124284) [improve][broker] GetPartitionMetadata fail also can produce messages (#23050)
* [86d4ea0](https://github.com/datastax/pulsar/commit/86d4ea0) [fix][broker][branch-3.0] Do not try to clean owned bundles from inactive source brokers (ExtensibleLoadManagerImpl only) (#23064)
* [40a797c](https://github.com/datastax/pulsar/commit/40a797c) [improve] [broker] high CPU usage caused by list topics under namespace (#23049)
* [1897068](https://github.com/apache/pulsar/commit/1897068) fix code style 
* [082dfb5](https://github.com/datastax/pulsar/commit/082dfb5) [improve] [broker] Improve CPU resources usege of TopicName Cache (#23052)
* [235f7c5](https://github.com/datastax/pulsar/commit/235f7c5) [improve][broker][branch-3.0] PIP-364: Introduce a new load balance algorithm AvgShedder (#23053)
* [fdd9747](https://github.com/apache/pulsar/commit/fdd9747) fix code style introduce by #22983
* [326271a](https://github.com/datastax/pulsar/commit/326271a) [fix][broker] Replication stuck when partitions count between two clusters is not the same (#22983)
* [4c58701](https://github.com/datastax/pulsar/commit/4c58701) Reverted changes for oracle
* [4788375](https://github.com/datastax/pulsar/commit/4788375) Debezium upgrade to 2.6.1.Final
* [f6f2db2](https://github.com/datastax/pulsar/commit/f6f2db2) [fix][broker] Fix stuck when enable topic level replication and build remote admin fails (#23028)
* [182b704](https://github.com/datastax/pulsar/commit/182b704) [fix][admin] Fix half deletion when attempt to topic with a incorrect API (#23002)
* [f74d3df](https://github.com/datastax/pulsar/commit/f74d3df) [fix][broker] Fix geo-replication admin client url (#22584)
* [3d9d7e6](https://github.com/datastax/pulsar/commit/3d9d7e6) [fix][broker]Fix lookupService.getTopicsUnderNamespace can not work with a quote pattern (#23014)
* [044840a](https://github.com/datastax/pulsar/commit/044840a) [fix][client] Fix pattern consumer create crash if a part of partitions of a topic have been deleted (#22854)
* [c917de3](https://github.com/datastax/pulsar/commit/c917de3) [fix][misc] Remove RoaringBitmap dependency from pulsar-common (#23008)
* [b488f1f](https://github.com/datastax/pulsar/commit/b488f1f) [improve][broker] Use RoaringBitmap in tracking individual acks to reduce memory usage (#23006)
* [1560edb](https://github.com/datastax/pulsar/commit/1560edb) [fix][broker] Fix MessageDeduplication replay timeout cause topic loading stuck (#23004)
* [1db5939](https://github.com/datastax/pulsar/commit/1db5939) [fix] Make operations on `individualDeletedMessages` in lock scope (#22966)
* [65c8b23](https://github.com/datastax/pulsar/commit/65c8b23) [fix][broker] Can't connecte to non-persist topic when enable broker client tls (#22991)
* [2a0af99](https://github.com/datastax/pulsar/commit/2a0af99) [fix][broker] Fix broker OOM when upload a large package. (#22989)
* [538f68e](https://github.com/datastax/pulsar/commit/538f68e) [improve][broker] Improve exception for topic does not have schema to check (#22974)
* [b36266c](https://github.com/datastax/pulsar/commit/b36266c) [improve][build] Upgrade dependency-check-maven-plugin to 10.0.2 (#23012)
* [c34d444](https://github.com/datastax/pulsar/commit/c34d444) [fix][broker] PulsarStandalone started with error if --stream-storage-port is not 4181 (#22993)
* [8708d5f](https://github.com/datastax/pulsar/commit/8708d5f) [fix][ci] Fix OWASP Dependency Check download by using NVD API key (#22999)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11  | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.0   | pulsar-io-cloud-storage-3.2.0.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.4 | pulsar-io-data-generator-3.1.4.4.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.4 | pulsar-io-elastic-search-3.1.4.4.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.4 | pulsar-io-http-3.1.4.4.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.4 | pulsar-io-jdbc-clickhouse-3.1.4.4.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.4 | pulsar-io-jdbc-mariadb-3.1.4.4.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.4 | pulsar-io-jdbc-openmldb-3.1.4.4.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.4 | pulsar-io-jdbc-postgres-3.1.4.4.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.4 | pulsar-io-jdbc-sqlite-3.1.4.4.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.4 | pulsar-io-kafka-3.1.4.4.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.4 | pulsar-io-kinesis-3.1.4.4.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.14  | pulsar-snowflake-connector-0.1.14.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.4 | pulsar-io-data-generator-3.1.4.4.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.4 | pulsar-io-debezium-mongodb-3.1.4.4.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.4 | pulsar-io-debezium-mssql-3.1.4.4.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.4 | pulsar-io-debezium-mysql-3.1.4.4.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.4 | pulsar-io-debezium-oracle-3.1.4.4.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.4 | pulsar-io-debezium-postgres-3.1.4.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.4 | pulsar-io-kafka-3.1.4.4.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.4 | pulsar-io-kinesis-3.1.4.4.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.0.1  | pulsar-kafka-proxy-3.1.0.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version   | File                                      |
|----------------------------------------------------------------|----------------------------------------|-----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.0.1   | pulsar-protocol-handler-kafka-3.1.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 5.0.4   | pulsar-jms-admin-5.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 5.0.4   | pulsar-jms-5.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.9   | pulsar-ai-tools-3.1.9.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.9   | pulsar-transformations-3.1.9.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.4.nar
- pulsar-io-jdbc-sqlite-3.1.4.4.nar
- pulsar-io-kinesis-3.1.4.4.nar
- pulsar-io-data-generator-3.1.4.4.nar
- pulsar-io-elastic-search-3.1.4.4.nar
- pulsar-io-jdbc-clickhouse-3.1.4.4.nar
- pulsar-io-debezium-oracle-3.1.4.4.nar
- pulsar-io-jdbc-openmldb-3.1.4.4.nar
- pulsar-io-jdbc-postgres-3.1.4.4.nar
- pulsar-io-debezium-mssql-3.1.4.4.nar
- pulsar-io-debezium-mysql-3.1.4.4.nar
- pulsar-io-jdbc-mariadb-3.1.4.4.nar
- pulsar-io-debezium-postgres-3.1.4.4.nar
- pulsar-io-http-3.1.4.4.nar
- pulsar-io-kafka-3.1.4.4.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.3
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 30th June 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [b453330](https://github.com/datastax/pulsar/commit/b453330) [fix][ci] Fix jacoco code coverage report aggregation (#22964)
* [fe09af2](https://github.com/datastax/pulsar/commit/fe09af2) [cleanup][misc] Remove classifier from netty-transport-native-unix-common dependency (#22951)
* [8ced787](https://github.com/datastax/pulsar/commit/8ced787) [improve][misc] Upgrade to Netty 4.1.111.Final and switch to use grpc-netty-shaded (#22892)
* [3d16cf7](https://github.com/datastax/pulsar/commit/3d16cf7) [feat][broker][branch-3.0] PIP-321 Introduce allowed-cluster at the namespace level (#22378) (#22960)
* [1a44c3d](https://github.com/datastax/pulsar/commit/1a44c3d) [improve] [broker] PIP-356 Support Geo-Replication starts at earliest position (#22856)
* [6e7943f](https://github.com/datastax/pulsar/commit/6e7943f) |[fix][broker] Fix updatePartitionedTopic when replication at ns level and topic policy is set (#22971)
* [64682a7](https://github.com/datastax/pulsar/commit/64682a7) [fix][broker] Support lookup options for extensible load manager (#22487)
* [fb72821](https://github.com/datastax/pulsar/commit/fb72821) [fix][broker] Check the broker is available for the SLA monitor bundle when the ExtensibleLoadManager is enabled (#22485)
* [b691da9](https://github.com/datastax/pulsar/commit/b691da9) [fix][broker] Ensure that PulsarService is ready for serving incoming requests (#22977)
* [eeb084f](https://github.com/datastax/pulsar/commit/eeb084f) [fix][broker] Update init and shutdown time and other minor logic (ExtensibleLoadManagerImpl only) (#22930)
* [cd5b194](https://github.com/datastax/pulsar/commit/cd5b194) [fix][broker] Asynchronously return brokerRegistry.lookupAsync when checking if broker is active(ExtensibleLoadManagerImpl only) (#22899)
* [d26f20d](https://github.com/datastax/pulsar/commit/d26f20d) [fix][broker] Fix NPE after publishing a tombstone to the service unit channel (#22859)
* [93b5fcf](https://github.com/datastax/pulsar/commit/93b5fcf) [fix][broker] Immediately tombstone Deleted and Free state bundles (#22743)
* [2049c72](https://github.com/datastax/pulsar/commit/2049c72) [fix][broker] Fix Replicated Topic unload bug when ExtensibleLoadManager is enabled (#22496)
* [3f48e5f](https://github.com/datastax/pulsar/commit/3f48e5f) [fix][client] Fix orphan consumer when reconnection and closing are concurrency executing (#22958)
* [2331017](https://github.com/datastax/pulsar/commit/2331017) [improve][misc] Replace rename-netty-native-libs.sh script with renaming with maven-shade-plugin (#22957)
* [245b197](https://github.com/datastax/pulsar/commit/245b197) Revert "[improve][broker] Optimize `ConcurrentOpenLongPairRangeSet` by RoaringBitmap (#22908)"
* [c404e19](https://github.com/datastax/pulsar/commit/c404e19) [improve] [broker] make system topic distribute evenly. (#22953)
* [659896e](https://github.com/datastax/pulsar/commit/659896e) [fix][misc] Rename netty native libraries in pulsar-client-admin-shaded (#22954)
* [717db84](https://github.com/datastax/pulsar/commit/717db84) [improve][fn] Make producer cache bounded and expiring in Functions/Connectors (#22945)
* [0f4c208](https://github.com/datastax/pulsar/commit/0f4c208) [improve][misc] Replace rename-netty-native-libs.sh script with renaming with maven-shade-plugin (#22957)
* [c4ab0b8](https://github.com/datastax/pulsar/commit/c4ab0b8) [fix][misc] Rename netty native libraries in pulsar-client-admin-shaded (#22954)
* [d8ddba4](https://github.com/datastax/pulsar/commit/d8ddba4) [fix][ci] Replace removed macos-11 with macos-latest in GitHub Actions (#22965)
* [59028a6](https://github.com/datastax/pulsar/commit/59028a6) [improve][misc][branch-3.2] Upgrade to Bookkeeper 4.16.6 (#22963)
* [f11db32](https://github.com/datastax/pulsar/commit/f11db32) [improve][broker] Optimize `ConcurrentOpenLongPairRangeSet` by RoaringBitmap (#22908)
* [8edc5ab](https://github.com/datastax/pulsar/commit/8edc5ab) [fix][broker] Check the markDeletePosition and calculate the backlog (#22947)
* [7d13506](https://github.com/datastax/pulsar/commit/7d13506) [fix][fn] Support compression type and crypto config for all producers in Functions and Connectors (#22950)
* [1610af1](https://github.com/datastax/pulsar/commit/1610af1) [fix] [broker] broker log a full thread dump when a deadlock is detected in healthcheck every time (#22916)
* [1dc870c](https://github.com/datastax/pulsar/commit/1dc870c) [fix] [client] Fix resource leak in Pulsar Client since HttpLookupService doesn't get closed (#22858)
* [4fc7561](https://github.com/datastax/pulsar/commit/4fc7561) [fix][test] Fix TableViewBuilderImplTest NPE and infinite loop (#22924)
* [01a2e20](https://github.com/datastax/pulsar/commit/01a2e20) [fix][fn] Enable optimized Netty direct byte buffer support for Pulsar Function runtimes (#22910)
* [94f9ec3](https://github.com/datastax/pulsar/commit/94f9ec3) [fix] [broker] Messages lost on the remote cluster when using topic level replication (#22890)
* [2c987c8](https://github.com/datastax/pulsar/commit/2c987c8) [fix][test] Fix thread leaks in Managed Ledger tests and remove duplicate shutdown code (#21426)
* [1ba6b3a](https://github.com/datastax/pulsar/commit/1ba6b3a) [fix][proxy] Add missing parameter in newPartitionMetadataRequest call
* [db274ec](https://github.com/datastax/pulsar/commit/db274ec) [fix][client] fix producer/consumer perform lookup for migrated topic (#21356)
* [b9c9930](https://github.com/datastax/pulsar/commit/b9c9930) [fix] [broker] response not-found error if topic does not exist when calling getPartitionedTopicMetadata (#22838)
* [87013b4](https://github.com/datastax/pulsar/commit/87013b4) [improve] [client] PIP-344 support feature flag supportsGetPartitionedMetadataWithoutAutoCreation (#22773)
* [a4094fa](https://github.com/datastax/pulsar/commit/a4094fa) [fix] [client] PIP-344 Do not create partitioned metadata when calling pulsarClient.getPartitionsForTopic(topicName) (#22206)
* [1d80bd3](https://github.com/datastax/pulsar/commit/1d80bd3) fix: cannot find symbol from cherry-pick 73b50e
* [7e7e2af](https://github.com/datastax/pulsar/commit/7e7e2af) [fix][broker] Fix topic status for oldestBacklogMessageAgeSeconds continuously increases even when there is no backlog. (#22907)
* [ee21988](https://github.com/datastax/pulsar/commit/ee21988) [fix][cli] Fix the pulsar-daemon parameter passthrough syntax (#22905)
* [f7ee78d](https://github.com/datastax/pulsar/commit/f7ee78d) [fix][broker][branch-3.0] The topic might reference a closed ledger (#22860) (#22900)
* [8ba2f71](https://github.com/datastax/pulsar/commit/8ba2f71) [improve][broker] Include runtime dependencies in server distribution (#22001)
* [0aa3d43](https://github.com/datastax/pulsar/commit/0aa3d43) [improve][broker] Optimize PersistentTopic.getLastDispatchablePosition (#22707)
* [48c2b7d](https://github.com/datastax/pulsar/commit/48c2b7d) [fix][misc] Topic name from persistence name should decode local name (#22879)
* [78a8e30](https://github.com/datastax/pulsar/commit/78a8e30) [improve] Upgrade IPAddress to 5.5.0 (#22886)
* [cf96763](https://github.com/datastax/pulsar/commit/cf96763) [fix][cli] Fix Pulsar standalone "--wipe-data" (#22885)
* [338f52d](https://github.com/datastax/pulsar/commit/338f52d) [fix][cli] Fix Pulsar standalone shutdown - bkCluster wasn't closed (#22868)
* [ed9e77a](https://github.com/datastax/pulsar/commit/ed9e77a) [fix] Remove blocking calls from BookieRackAffinityMapping (#22846)
* [aa39152](https://github.com/datastax/pulsar/commit/aa39152) [improve][misc] Include native epoll library for Netty for arm64 (#22319)
* [35876cc](https://github.com/datastax/pulsar/commit/35876cc) [improve][broker] Include runtime dependencies in server distribution (#22001)
* [0704fae](https://github.com/datastax/pulsar/commit/0704fae) [improve][ci] Migrate from Gradle Enterprise to Develocity (#22880)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11  | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.0   | pulsar-io-cloud-storage-3.2.0.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.3 | pulsar-io-data-generator-3.1.4.3.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.3 | pulsar-io-elastic-search-3.1.4.3.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.3 | pulsar-io-http-3.1.4.3.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.3 | pulsar-io-jdbc-clickhouse-3.1.4.3.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.3 | pulsar-io-jdbc-mariadb-3.1.4.3.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.3 | pulsar-io-jdbc-openmldb-3.1.4.3.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.3 | pulsar-io-jdbc-postgres-3.1.4.3.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.3 | pulsar-io-jdbc-sqlite-3.1.4.3.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.3 | pulsar-io-kafka-3.1.4.3.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.3 | pulsar-io-kinesis-3.1.4.3.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.14  | pulsar-snowflake-connector-0.1.14.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.3 | pulsar-io-data-generator-3.1.4.3.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.3 | pulsar-io-debezium-mongodb-3.1.4.3.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.3 | pulsar-io-debezium-mssql-3.1.4.3.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.3 | pulsar-io-debezium-mysql-3.1.4.3.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.3 | pulsar-io-debezium-oracle-3.1.4.3.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.3 | pulsar-io-debezium-postgres-3.1.4.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.3 | pulsar-io-kafka-3.1.4.3.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.3 | pulsar-io-kinesis-3.1.4.3.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.0.1  | pulsar-kafka-proxy-3.1.0.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version   | File                                      |
|----------------------------------------------------------------|----------------------------------------|-----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.0.1   | pulsar-protocol-handler-kafka-3.1.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0  | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 5.0.4   | pulsar-jms-admin-5.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 5.0.4   | pulsar-jms-5.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.9   | pulsar-ai-tools-3.1.9.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.9   | pulsar-transformations-3.1.9.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.3.nar
- pulsar-io-jdbc-sqlite-3.1.4.3.nar
- pulsar-io-kinesis-3.1.4.3.nar
- pulsar-io-data-generator-3.1.4.3.nar
- pulsar-io-elastic-search-3.1.4.3.nar
- pulsar-io-jdbc-clickhouse-3.1.4.3.nar
- pulsar-io-debezium-oracle-3.1.4.3.nar
- pulsar-io-jdbc-openmldb-3.1.4.3.nar
- pulsar-io-jdbc-postgres-3.1.4.3.nar
- pulsar-io-debezium-mssql-3.1.4.3.nar
- pulsar-io-debezium-mysql-3.1.4.3.nar
- pulsar-io-jdbc-mariadb-3.1.4.3.nar
- pulsar-io-debezium-postgres-3.1.4.3.nar
- pulsar-io-http-3.1.4.3.nar
- pulsar-io-kafka-3.1.4.3.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.2
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 7th June 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [22a0603](https://github.com/datastax/pulsar/commit/22a0603) [improve] Upgrade Jetcd to 0.7.7 and VertX to 4.5.8 (#22835) 
* [2c34c2c](https://github.com/datastax/pulsar/commit/2c34c2c) [improve] [client] improve the class GetTopicsResult (#22766) 
* [90bd00d](https://github.com/datastax/pulsar/commit/90bd00d) [fix][broker] Fix cursor should use latest ledger config (#22644)  
* [ec6af44](https://github.com/datastax/pulsar/commit/ec6af44) [cleanup][ml] ManagedCursor clean up. (#22246) 
* [4b6e6b5](https://github.com/datastax/pulsar/commit/4b6e6b5) [fix] Bump io.airlift:aircompressor from 0.20 to 0.27 (#22819) 
* [7b426c6](https://github.com/datastax/pulsar/commit/7b426c6) [fix][sec] Upgrade Bouncycastle libraries to address CVEs (#22826) 
* [12971bc](https://github.com/datastax/pulsar/commit/12971bc) [improve][ml] RangeCache refactoring follow-up: use StampedLock instead of synchronized (#22818) 
* [040465d](https://github.com/datastax/pulsar/commit/040465d) [improve][ml] RangeCache refactoring: test race conditions and prevent endless loops (#22814) 
* [6812af7](https://github.com/datastax/pulsar/commit/6812af7) [fix][ml] Fix race conditions in RangeCache (#22789) 
* [0ee3687](https://github.com/datastax/pulsar/commit/0ee3687) [fix][meta] Check if metadata store is closed in RocksdbMetadataStore (#22852) 
* [8f59cfb](https://github.com/datastax/pulsar/commit/8f59cfb) [improve][build] Support git worktree working directory while building docker images (#22851) 
* [232cde3](https://github.com/datastax/pulsar/commit/232cde3) [improve][broker] Remove ClassLoaderSwitcher to avoid objects allocations and consistent the codestyle (#22796) 
* [49902fe](https://github.com/datastax/pulsar/commit/49902fe) [improve][broker] Clear thread local BrokerEntryMetadata instance before reuse (#22752) 
* [bf9cdeb](https://github.com/datastax/pulsar/commit/bf9cdeb) [fix][broker] EntryFilters fix NoClassDefFoundError due to closed classloader (#22767) 
* [0f86864](https://github.com/datastax/pulsar/commit/0f86864) [improve][broker] avoid creating new objects when intercepting (#22790) 
* [b2ccc5f](https://github.com/datastax/pulsar/commit/b2ccc5f) [improve][cli][branch-3.0] PIP-353: Improve transaction message visibility for peek-message (#22788) 
* [f0c5776](https://github.com/datastax/pulsar/commit/f0c5776) [fix] [broker] fix topic partitions was expanded even if disabled topic level replication (#22769) 
* [0ddcd49](https://github.com/datastax/pulsar/commit/0ddcd49) [fix][admin] Clearly define REST API on Open API (#22783) 
* [80fd482](https://github.com/datastax/pulsar/commit/80fd482) [fix][admin] Clearly define REST API on Open API for Topics (#22782) 
* [37f16db](https://github.com/datastax/pulsar/commit/37f16db) [fix][admin] Clearly define REST API on Open API for Namesaces@v2 (#22775) 
* [3d57b6e](https://github.com/datastax/pulsar/commit/3d57b6e) [fix][admin][part-1]Clearly define REST API on Open API (#22774) 
* [1baa094](https://github.com/datastax/pulsar/commit/1baa094) [fix] [ml] Add entry fail due to race condition about add entry failed/timeout and switch ledger (#22221) 
* [8027d5c](https://github.com/datastax/pulsar/commit/8027d5c) [fix][ml]: subscription props could be lost in case of missing ledger during recovery (#22637) 
* [323013a](https://github.com/datastax/pulsar/commit/323013a) [fix] [broker] fix deadlock when disable topic level Geo-Replication (#22738) 
* [6b7e727](https://github.com/datastax/pulsar/commit/6b7e727) [improve] [test] Add a test to guarantee the TNX topics will not be replicated (#22721) 
* [f54d72d](https://github.com/datastax/pulsar/commit/f54d72d) [improve][broker] checkTopicExists supports checking partitioned topic without index (#21701) 
* [d611a3d](https://github.com/datastax/pulsar/commit/d611a3d) [feat][broker] Implementation of PIP-323: Complete Backlog Quota Telemetry (#21816) (#22740) | 
* [97a6c45](https://github.com/datastax/pulsar/commit/97a6c45) [fix][offload] Break the fillbuffer loop when met EOF (#22722) 
* [f52b0f5](https://github.com/datastax/pulsar/commit/f52b0f5) [fix][schema] Error checking schema compatibility on a schema-less topic via REST API (#22720) 
* [7e6d2c8](https://github.com/datastax/pulsar/commit/7e6d2c8) [improve] [broker] [break change] Do not create partitioned DLQ/Retry topic automatically (#22705) 
* [421188e](https://github.com/datastax/pulsar/commit/421188e) [fix][broker] Make ExtensibleLoadManagerImpl.getOwnedServiceUnits async (#22727) 

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11  | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 2.10.0  | pulsar-io-cloud-storage-2.10.0.nar            |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.2| pulsar-io-data-generator-3.1.4.2.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.2 | pulsar-io-elastic-search-3.1.4.2.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.2 | pulsar-io-http-3.1.4.2.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.2 | pulsar-io-jdbc-clickhouse-3.1.4.2.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.2 | pulsar-io-jdbc-mariadb-3.1.4.2.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.2 | pulsar-io-jdbc-openmldb-3.1.4.2.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.2 | pulsar-io-jdbc-postgres-3.1.4.2.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.2 | pulsar-io-jdbc-sqlite-3.1.4.2.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.2 | pulsar-io-kafka-3.1.4.2.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.2 | pulsar-io-kinesis-3.1.4.2.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.13  | pulsar-snowflake-connector-0.1.13.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.2 | pulsar-io-data-generator-3.1.4.2.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.2 | pulsar-io-debezium-mongodb-3.1.4.2.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.2 | pulsar-io-debezium-mssql-3.1.4.2.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.2 | pulsar-io-debezium-mysql-3.1.4.2.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.2 | pulsar-io-debezium-oracle-3.1.4.2.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.2 | pulsar-io-debezium-postgres-3.1.4.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.2 | pulsar-io-kafka-3.1.4.2.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.2 | pulsar-io-kinesis-3.1.4.2.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.4.2  | pulsar-kafka-proxy-3.1.4.2.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version  | File                                      |
|----------------------------------------------------------------|----------------------------------------|----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.4.2  | pulsar-protocol-handler-kafka-3.1.4.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0   | pulsar-jms-admin-3.1.0-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0   | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.7   | pulsar-ai-tools-3.1.7.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.1   | pulsar-transformations-3.1.1.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.2.nar
- pulsar-io-jdbc-sqlite-3.1.4.2.nar
- pulsar-io-kinesis-3.1.4.2.nar
- pulsar-io-data-generator-3.1.4.2.nar
- pulsar-io-elastic-search-3.1.4.2.nar
- pulsar-io-jdbc-clickhouse-3.1.4.2.nar
- pulsar-io-debezium-oracle-3.1.4.2.nar
- pulsar-io-jdbc-openmldb-3.1.4.2.nar
- pulsar-io-jdbc-postgres-3.1.4.2.nar
- pulsar-io-debezium-mssql-3.1.4.2.nar
- pulsar-io-debezium-mysql-3.1.4.2.nar
- pulsar-io-jdbc-mariadb-3.1.4.2.nar
- pulsar-io-debezium-postgres-3.1.4.2.nar
- pulsar-io-http-3.1.4.2.nar
- pulsar-io-kafka-3.1.4.2.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.4.2.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.4.2.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.1
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 15th May 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [4fa1c21](https://github.com/datastax/pulsar/commit/4fa1c21) [improve][ci][branch-3.0] Upgrade actions in pulsar-ci and pulsar-ci-flaky, port owasp cache change
* [53f0b91](https://github.com/datastax/pulsar/commit/53f0b91) [fix][test] Fix NPE in BookKeeperClusterTestCase tearDown (#22493)
* [99c2a9d](https://github.com/datastax/pulsar/commit/99c2a9d) [fix][broker] fix replicated subscriptions for transactional messages (#22452)
* [7042b52](https://github.com/datastax/pulsar/commit/7042b52) [fix] [broker] rename to changeMaxReadPositionCount (#22656)
* [1a02229](https://github.com/datastax/pulsar/commit/1a02229) [fix][sec] Upgrade postgresql version to avoid CVE-2024-1597 (#22635)
* [0a02cd9](https://github.com/datastax/pulsar/commit/0a02cd9) [fix][client] Fix ReaderBuilder doest not give illegalArgument on connection failure retry (#22639)
* [79f8e29](https://github.com/datastax/pulsar/commit/79f8e29) [fix][broker] Fix ProducerBusy issue due to incorrect userCreatedProducerCount on non-persistent topic (#22685)
* [c07b665](https://github.com/datastax/pulsar/commit/c07b665) [fix][broker] avoid offload system topic (#22497)
* [df29a6c](https://github.com/datastax/pulsar/commit/df29a6c) [improve][ws] Add memory limit configuration for Pulsar client used in Websocket proxy (#22666)
* [b69857d](https://github.com/datastax/pulsar/commit/b69857d) [fix][broker] Disable system topic message deduplication (#22582)
* [45b86eb](https://github.com/datastax/pulsar/commit/45b86eb) [fix] Fix Reader can be stuck from transaction aborted messages. (#22610)
* [fc7e6d7](https://github.com/datastax/pulsar/commit/fc7e6d7) [fix][test] Clear MockedPulsarServiceBaseTest fields to prevent test runtime memory leak (#22659)
* [a62730f](https://github.com/datastax/pulsar/commit/a62730f) [fix][storage] ReadonlyManagedLedger initialization does not fill in the properties (#22630)
* [703bdc5](https://github.com/datastax/pulsar/commit/703bdc5) [fix][sec] Upgrade elasticsearch-java version to avoid CVE-2023-4043 (#22640)
* [c37f354](https://github.com/datastax/pulsar/commit/c37f354) [fix] [client] Fix Consumer should return configured batch receive max messages (#22619)
* [dd9db88](https://github.com/datastax/pulsar/commit/dd9db88) [fix][sec] Upgrade aws-sdk.version to avoid CVE-2024-21634 (#22633)
* [87c4df3](https://github.com/datastax/pulsar/commit/87c4df3) [fix][fn]make sure the classloader for ContextImpl is `functionClassLoader` in different runtimes (#22501)
* [d9dc63c](https://github.com/datastax/pulsar/commit/d9dc63c) [fix][broker] Avoid being stuck when closing the broker with extensible load manager (#22573)
* [d6500ee](https://github.com/datastax/pulsar/commit/d6500ee) [fix][io] Fix es index creation (#22654) (#22701)
* [eede7fc](https://github.com/datastax/pulsar/commit/eede7fc) [improve] [log] Print source client addr when enabled haProxyProtocolEnabled (#22686)
* [cf92979](https://github.com/datastax/pulsar/commit/cf92979) [fix][broker] usedLocallySinceLastReport should always be reset (#22672)
* [790ac4e](https://github.com/datastax/pulsar/commit/790ac4e) [improve] Retry re-validating ResourceLock with backoff after errors (#22617)
* [0ac03da](https://github.com/datastax/pulsar/commit/0ac03da) [fix] [broker] Fix configurationMetadataSyncEventTopic is marked supporting dynamic setting, but not implemented  (#22684)
* [9669b4c](https://github.com/datastax/pulsar/commit/9669b4c) [fix][broker] Fix typos lister -> listener (#21068)
* [2a96f95](https://github.com/datastax/pulsar/commit/2a96f95) [improve][offload] Replace usage of shaded class in OffsetsCache (#22683)
* [3ed7f4c](https://github.com/datastax/pulsar/commit/3ed7f4c) [fix][offload] Fix OOM in tiered storage, caused by unbounded offsets cache (#22679)
* [fcf0183](https://github.com/datastax/pulsar/commit/fcf0183) [fix] [broker] Fix nothing changed after removing dynamic configs (#22673)
* [e3ac347](https://github.com/datastax/pulsar/commit/e3ac347) [fix] [test] Fix flaky test ReplicatorTest (#22594)
* [45de62a](https://github.com/datastax/pulsar/commit/45de62a) [fix][broker] One topic can be closed multiple times concurrently (#17524)
* [90036e1](https://github.com/datastax/pulsar/commit/90036e1) [fix] [broker] Part-2: Replicator can not created successfully due to an orphan replicator in the previous topic owner (#21948)
* [81fbc82](https://github.com/datastax/pulsar/commit/81fbc82) [improve] [broker] Create partitioned topics automatically when enable topic level replication (#22537)
* [ad55f97](https://github.com/datastax/pulsar/commit/ad55f97) [fix] [broker] Part-1: Replicator can not created successfully due to an orphan replicator in the previous topic owner (#21946)
* [43f4b41](https://github.com/datastax/pulsar/commit/43f4b41) [fix] [ml] Mark delete stuck due to switching cursor ledger fails (#22662)
* [da6212a](https://github.com/datastax/pulsar/commit/da6212a) [fix] [broker] Fix metrics pulsar_topic_load_failed_count is 0 when load non-persistent topic fails and fix the flaky test testBrokerStatsTopicLoadFailed (#22580)
* [32aff55](https://github.com/datastax/pulsar/commit/32aff55) [fix][test] Fix the flaky tests of ManagedLedgerImplUtilsTest (#22611)
* [275090a](https://github.com/datastax/pulsar/commit/275090a) [fix][broker] Reader stuck after call hasMessageAvailable when enable replicateSubscriptionState (#22572)
* [07b40ee](https://github.com/datastax/pulsar/commit/07b40ee) [fix][test] Clear fields in test cleanup to reduce memory consumption (#22583)
* [010a3f9](https://github.com/datastax/pulsar/commit/010a3f9) [fix][test] Fix resource leak in TransactionCoordinatorClientTest (#21380)
* [484f611](https://github.com/datastax/pulsar/commit/484f611) [fix][admin] Fix namespace admin api exception response (#22587)
* [09679d3](https://github.com/datastax/pulsar/commit/09679d3) [improve][sec] Align some namespace level policy authorisation check (#21640)
* [f2081cf](https://github.com/datastax/pulsar/commit/f2081cf) [fix][io] CompressionEnabled didn't work on elasticsearch sink (#22565)
* [72d2891](https://github.com/datastax/pulsar/commit/72d2891) [fix][test] Flaky-test: ManagedLedgerTest.testTimestampOnWorkingLedger (#22600)
* [c9586ae](https://github.com/datastax/pulsar/commit/c9586ae) [improve][broker] Propagate cause exception in TopicBusyException when applicable (#22596)
* [d1e3cce](https://github.com/datastax/pulsar/commit/d1e3cce) [improve][meta] Log a warning when ZK batch fails with connectionloss (#22566)
* [567aa99](https://github.com/datastax/pulsar/commit/567aa99) [fix][broker] Fix BufferOverflowException and EOFException bugs in /metrics gzip compression (#22576)
* [5bf373d](https://github.com/datastax/pulsar/commit/5bf373d) [improve][broker]Ensure namespace deletion doesn't fail (#259)
* [75b2db9](https://github.com/datastax/pulsar/commit/75b2db9) [improve][storage] Periodically rollover Cursor ledgers (#257)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11  | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 2.10.0  | pulsar-io-cloud-storage-2.10.0.nar            |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 3.1.4.1 | pulsar-io-data-generator-3.1.4.1.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 3.1.4.1 | pulsar-io-elastic-search-3.1.4.1.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 3.1.4.1 | pulsar-io-http-3.1.4.1.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 3.1.4.1 | pulsar-io-jdbc-clickhouse-3.1.4.1.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 3.1.4.1 | pulsar-io-jdbc-mariadb-3.1.4.1.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 3.1.4.1 | pulsar-io-jdbc-openmldb-3.1.4.1.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 3.1.4.1 | pulsar-io-jdbc-postgres-3.1.4.1.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 3.1.4.1 | pulsar-io-jdbc-sqlite-3.1.4.1.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 3.1.4.1 | pulsar-io-kafka-3.1.4.1.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 3.1.4.1 | pulsar-io-kinesis-3.1.4.1.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.13  | pulsar-snowflake-connector-0.1.13.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.2.9   | pulsar-cassandra-source-2.2.9.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 3.1.4.1 | pulsar-io-data-generator-3.1.4.1.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 3.1.4.1 | pulsar-io-debezium-mongodb-3.1.4.1.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 3.1.4.1 | pulsar-io-debezium-mssql-3.1.4.1.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 3.1.4.1 | pulsar-io-debezium-mysql-3.1.4.1.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 3.1.4.1 | pulsar-io-debezium-oracle-3.1.4.1.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 3.1.4.1 | pulsar-io-debezium-postgres-3.1.4.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 3.1.4.1 | pulsar-io-kafka-3.1.4.1.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 3.1.4.1 | pulsar-io-kinesis-3.1.4.1.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 3.1.4.1  | pulsar-kafka-proxy-3.1.4.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version  | File                                      |
|----------------------------------------------------------------|----------------------------------------|----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 3.1.4.1  | pulsar-protocol-handler-kafka-3.1.4.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.2.5   | pulsar-cassandra-admin-2.2.5-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 3.1.0   | pulsar-jms-admin-3.1.0-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 3.1.0   | pulsar-jms-3.1.0-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.1.7   | pulsar-ai-tools-3.1.7.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.1   | pulsar-transformations-3.1.1.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.1.nar
- pulsar-io-jdbc-sqlite-3.1.4.1.nar
- pulsar-io-kinesis-3.1.4.1.nar
- pulsar-io-data-generator-3.1.4.1.nar
- pulsar-io-elastic-search-3.1.4.1.nar
- pulsar-io-jdbc-clickhouse-3.1.4.1.nar
- pulsar-io-debezium-oracle-3.1.4.1.nar
- pulsar-io-jdbc-openmldb-3.1.4.1.nar
- pulsar-io-jdbc-postgres-3.1.4.1.nar
- pulsar-io-debezium-mssql-3.1.4.1.nar
- pulsar-io-debezium-mysql-3.1.4.1.nar
- pulsar-io-jdbc-mariadb-3.1.4.1.nar
- pulsar-io-debezium-postgres-3.1.4.1.nar
- pulsar-io-http-3.1.4.1.nar
- pulsar-io-kafka-3.1.4.1.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.4.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.4.1.nar
- pulsar-jms-3.1.0-nar.nar

## Luna Streaming Distribution 3.1 4.0
This is a maintenance release of the DataStax Luna Streaming Distribution for 3.1. This release contains all the commits included in the Apache Pulsar branch-3.0 till 23 April 2024 plus the changes specific to Luna Streaming & important security updates.

### Most notable commits

* [6b7aa50bdda](https://github.com/datastax/pulsar/commit/6b7aa50bdda) [fix][test][branch-3.0] Fix test PersistentTopicsTest.testUpdatePartitionedTopic
* [2f451301e26](https://github.com/datastax/pulsar/commit/2f451301e26) Revert "[fix][test][branch-3.0] Fix broken ManagedLedgerTest.testGetNumberOfEntriesInStorage"
* [b7c5eaf94fc](https://github.com/datastax/pulsar/commit/b7c5eaf94fc) [fix][offload] Increase file upload limit from 2048MiB to 4096MiB for GCP/GCS offloading (#22554)
* [fd8329d93f1](https://github.com/datastax/pulsar/commit/fd8329d93f1) [fix][ml] Fix NPE of getValidPositionAfterSkippedEntries when recovering a terminated managed ledger (#22552)
* [287e456b0c1](https://github.com/datastax/pulsar/commit/287e456b0c1) [improve][broker] Support X-Forwarded-For and HA Proxy Protocol for resolving original client IP of http/https requests (#22524)
* [0904a475d47](https://github.com/datastax/pulsar/commit/0904a475d47) [fix][broker] Fix broken topic policy implementation compatibility with old pulsar version (#22535)
* [973fdceb34b](https://github.com/datastax/pulsar/commit/973fdceb34b) [fix][broker] Fix typos in Consumer class (#22532)
* [a207029aedb](https://github.com/datastax/pulsar/commit/a207029aedb) [improve][test] Move ShadowManagedLedgerImplTest to flaky tests (#22526)
* [58029496b2b](https://github.com/datastax/pulsar/commit/58029496b2b) [improve][broker] Repeat the handleMetadataChanges callback when configurationMetadataStore equals localMetadataStore (#22519)
* [00c2fbb4597](https://github.com/datastax/pulsar/commit/00c2fbb4597) [improve][broker] Add topic name to emitted error messages. (#22506)
* [d2b3eb7351f](https://github.com/datastax/pulsar/commit/d2b3eb7351f) [improve] Make the config `metricsBufferResponse` description more effective (#22490)
* [19c7f8e86e0](https://github.com/datastax/pulsar/commit/19c7f8e86e0) [fix][test] SchemaMap in AutoConsumeSchema has been reused (#22500)
* [ef4deb13abf](https://github.com/datastax/pulsar/commit/ef4deb13abf) [fix][broker] Fix message drop record in producer stat (#22458)
* [fcf433d7d01](https://github.com/datastax/pulsar/commit/fcf433d7d01) [fix][broker] Update topic partition failed when config maxNumPartitionsPerPartitionedTopic<0 (#22397)
* [b195ef00a7b](https://github.com/datastax/pulsar/commit/b195ef00a7b) [improve][build] Upgrade Lombok to 1.18.32 for Java 22 support (#22425)
* [b336996a926](https://github.com/datastax/pulsar/commit/b336996a926) Fix [improve] [proxy] Not close the socket if lookup failed caused by too many requests (apache#21216)
* [b7e0a19a6bc](https://github.com/datastax/pulsar/commit/b7e0a19a6bc) [improve][broker] backlog quota exceed limit log replaced with `debug` (#22475)
* [b356f1be1f3](https://github.com/datastax/pulsar/commit/b356f1be1f3) [improve][offload] Apply autoSkipNonRecoverableData configuration to tiered storage (#22531)
* [f87ef7487dd](https://github.com/datastax/pulsar/commit/f87ef7487dd) [fix][broker] Fix NPE causing dispatching to stop when using Key_Shared mode and allowOutOfOrderDelivery=true (#22533)
* [3008d35a079](https://github.com/datastax/pulsar/commit/3008d35a079) [improve][build] Upgrade OWASP Dependency check version to 9.1.0 (#22530)
* [984d3c06748](https://github.com/datastax/pulsar/commit/984d3c06748) [fix][broker] Fix a deadlock in SystemTopicBasedTopicPoliciesService during NamespaceEventsSystemTopicFactory init (#22528)
* [f8d509852cd](https://github.com/datastax/pulsar/commit/f8d509852cd) [improve][broker] Optimize gzip compression for /metrics endpoint by sharing/caching compressed result (#22521)
* [c87fa4ea1c4](https://github.com/datastax/pulsar/commit/c87fa4ea1c4) [fix][io] Kafka Source connector maybe stuck (#22511)
* [f3740572aaa](https://github.com/datastax/pulsar/commit/f3740572aaa) [fix][sec] Upgrade Bouncycastle to 1.78 (#22509)
* [ce3b816b691](https://github.com/datastax/pulsar/commit/ce3b816b691) [fix][test] Flaky-test: testMessageExpiryWithTimestampNonRecoverableException and testIncorrectClientClock (#22489)
* [7d1d0bb61a5](https://github.com/datastax/pulsar/commit/7d1d0bb61a5) [fix][broker] Create new ledger after the current ledger is closed (#22034)
* [0b001837598](https://github.com/datastax/pulsar/commit/0b001837598) [fix][broker] Optimize /metrics, fix unbounded request queue issue and fix race conditions in metricsBufferResponse mode (#22494)
* [961ecce291d](https://github.com/datastax/pulsar/commit/961ecce291d) [improve][broker] Improve Gzip compression, allow excluding specific paths or disabling it (#22370)
* [7f05b6e1f3e](https://github.com/datastax/pulsar/commit/7f05b6e1f3e) [improve][test] Replace usage of curl in Java test and fix stream leaks (#22463)
* [ba98afe1225](https://github.com/datastax/pulsar/commit/ba98afe1225) [improve] [broker] Servlet support response compression (#21667)
* [ca62ee3aba1](https://github.com/datastax/pulsar/commit/ca62ee3aba1) [fix] [broker] Prevent long deduplication cursor backlog so that topic loading wouldn't timeout (#22479)
* [d1b4588de82](https://github.com/datastax/pulsar/commit/d1b4588de82) [fix][txn]Handle exceptions in the transaction pending ack init (#21274)
* [aae0f48cb7e](https://github.com/datastax/pulsar/commit/aae0f48cb7e) [improve][misc] Upgrade to Bookkeeper 4.16.5 (#22484)
* [6d1bd3a82a0](https://github.com/datastax/pulsar/commit/6d1bd3a82a0) Remove unused fields `msgSize`
* [457257c9846](https://github.com/datastax/pulsar/commit/457257c9846) [fix][client] Fix client side memory leak when call MessageImpl.create and fix imprecise client-side metrics: pendingMessagesUpDownCounter, pendingBytesUpDownCounter, latencyHistogram (#22393)
* [cedc250faa7](https://github.com/datastax/pulsar/commit/cedc250faa7) [fix][ml] No rollover inactive ledgers when metadata service invalid (#22284)
* [fd4c9c6c8ec](https://github.com/datastax/pulsar/commit/fd4c9c6c8ec) [improve][io]: Add validation for JDBC sink not supporting primitive schema (#22376)
* [a5b9be343c8](https://github.com/datastax/pulsar/commit/a5b9be343c8) [admin][broker] Fix force delete subscription not working (#22423)
* [8f3e1fd6759](https://github.com/datastax/pulsar/commit/8f3e1fd6759) [fix][broker] Fix consumer stops receiving messages when with large backlogs processing (#22454)
* [8e2bd551915](https://github.com/datastax/pulsar/commit/8e2bd551915) [fix][misc] Rename all shaded Netty native libraries (#22415)
* [2e1c0c78fe2](https://github.com/datastax/pulsar/commit/2e1c0c78fe2) [fix][broker] Support OIDC providers with JWK without alg field set in keys (#22421)
* [3eb5c2d8f49](https://github.com/datastax/pulsar/commit/3eb5c2d8f49) [improve] [broker] Avoid repeated Read-and-discard when using Key_Shared mode (#22245)
* [ddf77be02eb](https://github.com/datastax/pulsar/commit/ddf77be02eb) [improve][test][branch-3.0] Improve ManagedLedgerTest.testGetNumberOfEntriesInStorage
* [6b37ac6ab94](https://github.com/datastax/pulsar/commit/6b37ac6ab94) [improve][misc] Pin Netty version in pulsar-io/alluxio (#21728)
* [9c1a8f28345](https://github.com/datastax/pulsar/commit/9c1a8f28345) [fix][build] Upgrade alluxio version to 2.9.3 to fix CVE-2023-38889 (#21715)
* [ec47aa7972c](https://github.com/datastax/pulsar/commit/ec47aa7972c) [fix][test] Fix flaky test BrokerServiceAutoSubscriptionCreationTest (#22190)
* [8035e668cbb](https://github.com/datastax/pulsar/commit/8035e668cbb) [fix][test][branch-3.0] Fix broken ManagedLedgerTest.testGetNumberOfEntriesInStorage
* [fcb759c6ae5](https://github.com/datastax/pulsar/commit/fcb759c6ae5) [improve][misc] Remove the call to sun InetAddressCachePolicy (#22329)
* [95c06755fa6](https://github.com/datastax/pulsar/commit/95c06755fa6) [fix][broker] Check cursor state before adding it to the `waitingCursors` (#22191)
* [6916dfade17](https://github.com/datastax/pulsar/commit/6916dfade17) [fix][client] Fix wrong results of hasMessageAvailable and readNext after seeking by timestamp (#22363)
* [60d8ecc481f](https://github.com/datastax/pulsar/commit/60d8ecc481f) [fix][broker] Avoid execute prepareInitPoliciesCacheAsync if namespace is deleted (#22268)
* [e9e57ded38c](https://github.com/datastax/pulsar/commit/e9e57ded38c) [fix][broker] Fix wrong double-checked locking for readOnActiveConsumerTask in dispatcher (#22279)
* [51f7cf5bcd1](https://github.com/datastax/pulsar/commit/51f7cf5bcd1) [fix][client] fix Reader.hasMessageAvailable might return true after seeking to latest (#22201)
* [4fcaec3cd63](https://github.com/datastax/pulsar/commit/4fcaec3cd63) [improve][client] Add backoff for `seek` (#20963)
* [781423d7d2c](https://github.com/datastax/pulsar/commit/781423d7d2c) [fix][misc] Make ConcurrentBitSet thread safe (#22361)
* [db1005dbbb6](https://github.com/datastax/pulsar/commit/db1005dbbb6) [fix][broker] Avoid expired unclosed ledgers when checking expired messages by ledger closure time (#22335)
* [b54b249a6bb](https://github.com/datastax/pulsar/commit/b54b249a6bb) [fix][test] Fix flaky RGUsageMTAggrWaitForAllMsgsTest (#22252)
* [3233fd29733](https://github.com/datastax/pulsar/commit/3233fd29733) [fix][client] Consumer lost message ack due to race condition in acknowledge with batch message (#22353)
* [00477abf668](https://github.com/datastax/pulsar/commit/00477abf668) [fix][test] Fix flaky ManagedLedgerErrorsTest.recoverAfterZnodeVersionError (#22368)
* [afd46d22838](https://github.com/datastax/pulsar/commit/afd46d22838) [fix] [test] Fix flaky test ManagedLedgerTest.testGetNumberOfEntriesInStorage (#22344)
* [b46b0c365dd](https://github.com/datastax/pulsar/commit/b46b0c365dd) [fix][ml]Expose ledger timestamp  (#22338)
* [d67d44df59f](https://github.com/datastax/pulsar/commit/d67d44df59f) [fix][client]Fixed getting an incorrect `maxMessageSize` value when accessing multiple clusters in the same process (#22306)
* [eb8fb8226d0](https://github.com/datastax/pulsar/commit/eb8fb8226d0) [improve][admin] Fix the `createMissingPartitions` doesn't response correctly (#22311)
* [f1213831ce3](https://github.com/datastax/pulsar/commit/f1213831ce3) [fix][sec] Go Functions security updates (#21844)
* [b1eae3b2f38](https://github.com/datastax/pulsar/commit/b1eae3b2f38) [fix][sec] Bump google.golang.org/grpc from 1.38.0 to 1.56.3 in /pulsar-function-go (#21444)
* [29b83591a7f](https://github.com/datastax/pulsar/commit/29b83591a7f) [fix] [broker] fix mismatch between dispatcher.consumerList and dispatcher.consumerSet (#22283)
* [4764b4439a7](https://github.com/datastax/pulsar/commit/4764b4439a7) [fix] [broker] Close dispatchers stuck due to mismatch between dispatcher.consumerList and dispatcher.consumerSet (#22270)
* [66959be7541](https://github.com/datastax/pulsar/commit/66959be7541) [fix] [client] Unclear error message when creating a consumer with two same topics (#22255)
* [53c09015291](https://github.com/datastax/pulsar/commit/53c09015291) [improve][broker] Add missing configuration keys for caching catch-up reads (#22295)
* [874847b35b8](https://github.com/datastax/pulsar/commit/874847b35b8) [improve][broker] Add createTopicIfDoesNotExist option to RawReader constructor (#22264)
* [ba9ac4c97d4](https://github.com/datastax/pulsar/commit/ba9ac4c97d4) Fix the tests with same namespace name (#22240)
* [153413750b0](https://github.com/datastax/pulsar/commit/153413750b0) Check the validity of config before start websocket service (#22231)
* [ac10a3c2a0a](https://github.com/datastax/pulsar/commit/ac10a3c2a0a) [fix][client] GenericProtobufNativeSchema not implement getNativeSchema method. (#22204)
* [9edef69d353](https://github.com/datastax/pulsar/commit/9edef69d353) [improve][broker] Change log level to reduce duplicated logs (#22147)
* [1c6206b6347](https://github.com/datastax/pulsar/commit/1c6206b6347) [improve][fn][branch-3.0] Add missing "exception" argument to some `log.error` (#22140) (#22213)
* [fcb76f781ac](https://github.com/datastax/pulsar/commit/fcb76f781ac) [improve][admin][branch-3.0] Expose the offload threshold in seconds to the admin (#22169)
* [98aa8078cf0](https://github.com/datastax/pulsar/commit/98aa8078cf0) [fix][broker] Fix String wrong format (#21829)
* [0381bc4ad7f](https://github.com/datastax/pulsar/commit/0381bc4ad7f) [fix] [broker] [branch-3.0] Fast fix infinite HTTP call createSubscriptions caused by wrong topicName (#21997)
* [9231e727c78](https://github.com/datastax/pulsar/commit/9231e727c78) [fix] [build] Remove test testNoOrphanTopicIfInitFailed (#21569)
* [7857ffb3290](https://github.com/datastax/pulsar/commit/7857ffb3290) [fix] [broker] Make the new exclusive consumer instead the inactive one faster (#21183)
* [e55318c1e30](https://github.com/datastax/pulsar/commit/e55318c1e30) [fix] [ml] fix wrong msg backlog of non-durable cursor after trim ledgers (#21250)
* [ed12a345c98](https://github.com/datastax/pulsar/commit/ed12a345c98) [fix] [ml] Reader can set read-pos to a deleted ledger (#21248)
* [5ceb05663eb](https://github.com/datastax/pulsar/commit/5ceb05663eb) [fix] [client] fix reader.hasMessageAvailable return false when incoming queue is not empty (#21259)
* [0c95498009f](https://github.com/datastax/pulsar/commit/0c95498009f) [improve] [broker] Print warn log if ssl handshake error & print ledger id when switch ledger (#21201)
* [c691c75f859](https://github.com/datastax/pulsar/commit/c691c75f859) [improve] [proxy] Not close the socket if lookup failed caused by too many requests (#21216)
* [7dfa2000bee](https://github.com/datastax/pulsar/commit/7dfa2000bee) [improve] [broker] improve read entry error log for troubleshooting (#21169)
* [8ddc0763571](https://github.com/datastax/pulsar/commit/8ddc0763571) [improve] [broker] Improve cache handling for partitioned topic metadata when doing lookup (#21063)
* [63f9385da41](https://github.com/datastax/pulsar/commit/63f9385da41) [fix] [broker] Producer is blocked on creation because backlog exceeded on topic, when dedup is enabled and no producer is there (#20951)
* [1ccb17ac8e6](https://github.com/datastax/pulsar/commit/1ccb17ac8e6) Revert "[fix][broker] Fix get topic policies as null during clean cache (#20763)"
* [23f6213b525](https://github.com/datastax/pulsar/commit/23f6213b525) [fix] [bk] Correctct the bookie info after ZK client is reconnected (#21035)
* [5b9dff35f6c](https://github.com/datastax/pulsar/commit/5b9dff35f6c) [fix] [ml] fix discontinuous ledger deletion (#20898)
* [7352c8f92ed](https://github.com/datastax/pulsar/commit/7352c8f92ed) [fix][io][branch-3.0] Not restart instance when kafka source poll exception. (#20818)
* [a64286773c3](https://github.com/datastax/pulsar/commit/a64286773c3) Revert Add listener interface for namespace service #20406
* [cbfb1301b39](https://github.com/datastax/pulsar/commit/cbfb1301b39) Revert "[fix][broker] Fix NPE when reset Replicator's cursor by position. (#20597)"
* [f64edd39532](https://github.com/datastax/pulsar/commit/f64edd39532) [fix][broker] Fix OpReadEntry.skipCondition NPE issue (#22367)
* [5ae9877d9f4](https://github.com/datastax/pulsar/commit/5ae9877d9f4) [feat]PIP 167: Make it Configurable to Require Subscription Permission for Consumer (#246)


### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 3.1.4.0 | pulsar-io-data-generator-3.1.4.0.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 3.1.4.0 | pulsar-io-elastic-search-3.1.4.0.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 3.1.4.0 | pulsar-io-http-3.1.4.0.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 3.1.4.0 | pulsar-io-jdbc-clickhouse-3.1.4.0.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 3.1.4.0 | pulsar-io-jdbc-mariadb-3.1.4.0.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 3.1.4.0 | pulsar-io-jdbc-openmldb-3.1.4.0.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 3.1.4.0 | pulsar-io-jdbc-postgres-3.1.4.0.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 3.1.4.0 | pulsar-io-jdbc-sqlite-3.1.4.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 3.1.4.0 | pulsar-io-kafka-3.1.4.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 3.1.4.0 | pulsar-io-kinesis-3.1.4.0.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 3.1.4.0 | pulsar-io-data-generator-3.1.4.0.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 3.1.4.0 | pulsar-io-debezium-mongodb-3.1.4.0.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 3.1.4.0 | pulsar-io-debezium-mssql-3.1.4.0.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 3.1.4.0 | pulsar-io-debezium-mysql-3.1.4.0.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 3.1.4.0 | pulsar-io-debezium-oracle-3.1.4.0.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 3.1.4.0 | pulsar-io-debezium-postgres-3.1.4.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 3.1.4.0 | pulsar-io-kafka-3.1.4.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 3.1.4.0 | pulsar-io-kinesis-3.1.4.0.nar |
</details>
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 3.1.4.0 | pulsar-kafka-proxy-3.1.4.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 3.1.4.0 | pulsar-protocol-handler-kafka-3.1.4.0.nar |
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
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.1.7   | pulsar-ai-tools-3.1.7.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.1   | pulsar-transformations-3.1.1.nar |
</details>


### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.4.0.nar
- pulsar-io-jdbc-sqlite-3.1.4.0.nar
- pulsar-io-kinesis-3.1.4.0.nar
- pulsar-io-data-generator-3.1.4.0.nar
- pulsar-io-elastic-search-3.1.4.0.nar
- pulsar-io-jdbc-clickhouse-3.1.4.0.nar
- pulsar-io-debezium-oracle-3.1.4.0.nar
- pulsar-io-jdbc-openmldb-3.1.4.0.nar
- pulsar-io-jdbc-postgres-3.1.4.0.nar
- pulsar-io-debezium-mssql-3.1.4.0.nar
- pulsar-io-debezium-mysql-3.1.4.0.nar
- pulsar-io-jdbc-mariadb-3.1.4.0.nar
- pulsar-io-debezium-postgres-3.1.4.0.nar
- pulsar-io-http-3.1.4.0.nar
- pulsar-io-kafka-3.1.4.0.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.4.0.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.4.0.nar
- pulsar-jms-3.1.0-nar.nar


## Luna Streaming Distribution 3.1 3.1
This is a maintenance release containing important stability and security updates.

### Most notable commits

* [5b82329](https://github.com/datastax/pulsar/commit/5b82329) [improve][misc] Specify valid home dir for the default user in the Ubuntu based docker image (#22446)
* [a20af42](https://github.com/datastax/pulsar/commit/a20af42) [fix][build] Fix building docker images without setting UBUNTU_MIRROR
* [4e10b22](https://github.com/datastax/pulsar/commit/4e10b22) [fix][broker][admin] Fix cannot update properties on NonDurable subscription. (#22411)
* [d18f429](https://github.com/datastax/pulsar/commit/d18f429) [improve][test] Move most flaky tests to flaky group (#22433)
* [7ab68ca](https://github.com/datastax/pulsar/commit/7ab68ca) [improve][misc] Upgrade to Netty 4.1.108 and tcnative 2.0.65 (#22369)
* [d0373e2](https://github.com/datastax/pulsar/commit/d0373e2) [fix][broker] Update TransferShedder underloaded broker check to consider max loaded broker's msgThroughputEMA and update IsExtensibleLoadBalancerImpl check (#22321) (#22417)
* [08fcc87](https://github.com/datastax/pulsar/commit/08fcc87) [fix][broker] upgrade jclouds 2.5.0 -> 2.6.0 (#22220)
* [cca9630](https://github.com/datastax/pulsar/commit/cca9630) [fix][broker] Fix invalid condition in logging exceptions (#22412)
* [95a75a8](https://github.com/datastax/pulsar/commit/95a75a8) [fix][broker] Skip topic.close during unloading if the topic future fails with ownership check, and fix isBundleOwnedByAnyBroker to use ns.checkOwnershipPresentAsync for ExtensibleLoadBalancer (#22379) (#22406)
* [b080c7f](https://github.com/datastax/pulsar/commit/b080c7f) [fix][build] Fix networkaddress.cache.negative.ttl config (#22400)
* [2ac546c](https://github.com/datastax/pulsar/commit/2ac546c) [improve][broker] Don't log brokerClientAuthenticationParameters and bookkeeperClientAuthenticationParameters by default (#22395)
* [5f68f51](https://github.com/datastax/pulsar/commit/5f68f51)  [fix][broker] Fix issue of field 'topic' is not set when handle GetSchema request (#22377)
* [6cd168b](https://github.com/datastax/pulsar/commit/6cd168b) [fix][broker] Fix ResourceGroups loading (#21781)
* [0a5100f](https://github.com/datastax/pulsar/commit/0a5100f) [fix][broker] Fix ResourceGroup report local usage (#22340)
* [b1c4de9](https://github.com/datastax/pulsar/commit/b1c4de9) [fix][ci][branch-3.1] Increase Maven's heap size from 1024m to 1500m as it is in master
* [248efe9](https://github.com/datastax/pulsar/commit/248efe9) [improve][misc] Upgrade checkstyle to 10.14.2 (#22291)
* [c78f70f](https://github.com/datastax/pulsar/commit/c78f70f) [fix] Upgrade jose4j to 0.9.4 (#22273)
* [28404f3](https://github.com/datastax/pulsar/commit/28404f3) [fix][sec] Upgrade Zookeeper to 3.9.2 to address CVE-2024-23944 (#22275)
* [c401aa2](https://github.com/datastax/pulsar/commit/c401aa2) [fix][ci] Tolerate mount option change failing in CI (#22241)
* [53b02df](https://github.com/datastax/pulsar/commit/53b02df) [fix][sec]  Revert "[fix][sec] Add a check for the input time value (apache#22023)"  (#22243)
* [039b8aa](https://github.com/datastax/pulsar/commit/039b8aa) [improve][broker] Consistently add fine-grain authorization to REST API (#22202)
* [a7742d2](https://github.com/datastax/pulsar/commit/a7742d2) [fix][broker][branch-3.1] Fix broker not starting when both transactions and the Extensible Load Manager are enabled (#22194)
* [07609e6](https://github.com/datastax/pulsar/commit/07609e6) [improve][broker] Add fine-grain authorization to ns/topic management endpoints (#22305)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.11 | cassandra-enhanced-pulsar-sink-1.6.11-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 2.10.0 | pulsar-io-cloud-storage-2.10.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 3.1.3.1 | pulsar-io-data-generator-3.1.3.1.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 3.1.3.1 | pulsar-io-elastic-search-3.1.3.1.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 3.1.3.1 | pulsar-io-http-3.1.3.1.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 3.1.3.1 | pulsar-io-jdbc-clickhouse-3.1.3.1.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 3.1.3.1 | pulsar-io-jdbc-mariadb-3.1.3.1.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 3.1.3.1 | pulsar-io-jdbc-openmldb-3.1.3.1.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 3.1.3.1 | pulsar-io-jdbc-postgres-3.1.3.1.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 3.1.3.1 | pulsar-io-jdbc-sqlite-3.1.3.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 3.1.3.1 | pulsar-io-kafka-3.1.3.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 3.1.3.1 | pulsar-io-kinesis-3.1.3.1.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.13 | pulsar-snowflake-connector-0.1.13.nar |
</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.9 | pulsar-cassandra-source-2.2.9.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 3.1.3.1 | pulsar-io-data-generator-3.1.3.1.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 3.1.3.1 | pulsar-io-debezium-mongodb-3.1.3.1.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 3.1.3.1 | pulsar-io-debezium-mssql-3.1.3.1.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 3.1.3.1 | pulsar-io-debezium-mysql-3.1.3.1.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 3.1.3.1 | pulsar-io-debezium-oracle-3.1.3.1.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 3.1.3.1 | pulsar-io-debezium-postgres-3.1.3.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 3.1.3.1 | pulsar-io-kafka-3.1.3.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 3.1.3.1 | pulsar-io-kinesis-3.1.3.1.nar |
</details>
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 3.1.0.1 | pulsar-kafka-proxy-3.1.0.1.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Protocol Handler | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 3.1.0.1 | pulsar-protocol-handler-kafka-3.1.0.1.nar |
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

### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls31_3.1/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.11-nar.nar
- pulsar-cassandra-source-2.2.9.nar
- pulsar-io-cloud-storage-2.10.0.nar
- pulsar-io-debezium-mongodb-3.1.3.1.nar
- pulsar-io-jdbc-sqlite-3.1.3.1.nar
- pulsar-io-kinesis-3.1.3.1.nar
- pulsar-io-data-generator-3.1.3.1.nar
- pulsar-io-elastic-search-3.1.3.1.nar
- pulsar-io-jdbc-clickhouse-3.1.3.1.nar
- pulsar-io-debezium-oracle-3.1.3.1.nar
- pulsar-io-jdbc-openmldb-3.1.3.1.nar
- pulsar-io-jdbc-postgres-3.1.3.1.nar
- pulsar-io-debezium-mssql-3.1.3.1.nar
- pulsar-io-debezium-mysql-3.1.3.1.nar
- pulsar-io-jdbc-mariadb-3.1.3.1.nar
- pulsar-io-debezium-postgres-3.1.3.1.nar
- pulsar-io-http-3.1.3.1.nar
- pulsar-io-kafka-3.1.3.1.nar
- pulsar-snowflake-connector-0.1.13.nar
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
- pulsar-jms-3.1.0-nar.nar


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

| Name | Description | Version | File                            | 
| ---- | ----------- | ------- |---------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 3.1.3.0 | pulsar-kafka-proxy-3.1.0.1.nar  |
</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File                                      | 
| ---- | ----------- | ------- |-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Protocol Handler | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 3.1.3.0 | pulsar-protocol-handler-kafka-3.1.0.1.nar |
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

### Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
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
- pulsar-protocol-handler-kafka-3.1.0.1.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-3.1.0.1.nar
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