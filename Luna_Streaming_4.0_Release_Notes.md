# Release notes for DataStax Luna Streaming Distribution

## About DataStax Luna Streaming Distribution

Luna Streaming Distribution 4.0 is compatible with Apache Pulsar&TRADE; 4.0
and subsequent releases.

### Components

- [DataStax Luna Streaming](https://github.com/datastax/pulsar) (Apache Pulsar 4.0 fork)
- [DataStax BookKeeper](https://github.com/datastax/bookkeeper) (Apache BookKeeper fork)
- DataStax Burnell
- DataStax Pulsar Admin Console
- DataStax Pulsar Heartbeat
- DataStax Apache Pulsar Cassandra Sink
- DataStax Apache Pulsar Cassandra Source
- DataStax Starlight For Kafka
- DataStax Starlight For RabbitMQ
- DataStax Starlight For JMS Broker filter
- DataStax Snowflake connector

This release adds these features to the original Apache Pulsar 4.0 release:

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

## Luna Streaming Distribution 4.0 3.2
This is the initial release of the DataStax Luna Streaming Distribution for 4.0. This release contains all the commits included in the Apache Pulsar v4.0.3 release plus the following changes specific to Luna Streaming:

### Most notable commits

* [96f25cd](https://github.com/datastax/pulsar/commit/96f25cd) [improve][meta] Change log level from error to warn for unknown notification types in OxiaMetadataStore (#24126)
* [ba8037d](https://github.com/datastax/pulsar/commit/ba8037d) [fix][ml] Return 1 when bytes size is 0 or negative for entry count estimation (#24131)
* [167ffea](https://github.com/datastax/pulsar/commit/167ffea) [improve][io] Enhance Kafka connector logging with focused bootstrap server information (#24128)
* [5edc57c](https://github.com/datastax/pulsar/commit/5edc57c) [improve][client] Prevent NullPointException when closing ClientCredentialsFlow (#24123)
* [21f0750](https://github.com/datastax/pulsar/commit/21f0750) [fix][ml] Don't estimate number of entries when ledgers are empty, return 1 instead (#24125)
* [f8816e1](https://github.com/datastax/pulsar/commit/f8816e1) [improve][io] Remove sleep when sourceTask.poll of kafka return null (#24124)
* [71330c4](https://github.com/datastax/pulsar/commit/71330c4) [improve][broker] Change topic exists log to warn (#24116)
* [d699029](https://github.com/datastax/pulsar/commit/d699029) [improve][broker][branch-4.0] PIP-406: Introduce metrics related to dispatch throttled events (#24111)
* [e53623d](https://github.com/datastax/pulsar/commit/e53623d) [fix][client] Pattern subscription regression when broker-side evaluation is disabled (#24104)
* [3ffcbfc](https://github.com/datastax/pulsar/commit/3ffcbfc) [fix][client] Fix consumer leak when thread is interrupted before subscribe completes (#24100)
* [83ba1ab](https://github.com/datastax/pulsar/commit/83ba1ab) [fix][ci] Bump dependency-check to 12.1.0 to fix OWASP Dependency Check job (#24083)
* [2b933c7](https://github.com/datastax/pulsar/commit/2b933c7) [fix][broker] Restore the behavior to dispatch batch messages according to consumer permits (#24092)
* [fef163c](https://github.com/datastax/pulsar/commit/fef163c) [improve][broker] Optimize message expiration rate repeated update issues (#24073)
* [814781d](https://github.com/datastax/pulsar/commit/814781d) [fix][ml] Fix issues in estimateEntryCountBySize (#24089)
* [dc0176e](https://github.com/datastax/pulsar/commit/dc0176e) [fix][broker] Fix Metadata Event Synchronizer producer creation retry so that the producer gets created eventually (#24081)
* [4a5f398](https://github.com/datastax/pulsar/commit/4a5f398) [fix][broker] Fix Metadata event synchronizer should not fail with bad version (#24080)
* [e9aedd2](https://github.com/datastax/pulsar/commit/e9aedd2) [fix][broker] Fix NPE while publishing Metadata-Event with not init producer (#24079)
* [cdaec92](https://github.com/datastax/pulsar/commit/cdaec92) [clean][client] Clean code for the construction of retry/dead letter topic name (#24082)
* [3c6b12a](https://github.com/datastax/pulsar/commit/3c6b12a) [fix][client] Fix building broken batched message when publishing (#24061)
* [3efd9bb](https://github.com/datastax/pulsar/commit/3efd9bb) [fix][broker]Fix failed consumption after loaded up a terminated topic (#24063)
* [f3dfaeb](https://github.com/datastax/pulsar/commit/f3dfaeb) [fix][test] Fix flaky PrometheusMetricsTest.testBrokerMetrics (#24042)
* [aaa2ed1](https://github.com/datastax/pulsar/commit/aaa2ed1) [fix][broker] http metric endpoint get compaction latency stats always be 0 (#24067)
* [00fedf9](https://github.com/datastax/pulsar/commit/00fedf9) [fix][client] PIP-409 retry/dead letter topic producer config don't take effect. (#24071)
* [c4b8ca9](https://github.com/datastax/pulsar/commit/c4b8ca9) [fix][ml] Corrected pulsar_storage_size metric to not multiply offloaded storage by the write quorum (#24054)
* [9ab3221](https://github.com/datastax/pulsar/commit/9ab3221) [fix][broker] Fix UnsupportedOperationException while setting subscription level dispatch rate policy (#24048)
* [6dd61f1](https://github.com/datastax/pulsar/commit/6dd61f1) [improve][broker] Optimize ThresholdShedder with improved boundary checks and parameter reuse (#24064)
* [5546d45](https://github.com/datastax/pulsar/commit/5546d45) [improve][client] PIP-409: support producer configuration for retry/dead letter topic producer (#24020)
* [1b250e3](https://github.com/datastax/pulsar/commit/1b250e3) [fix][client] Copy eventTime to retry letter topic and DLQ messages (#24059)
* [379a203](https://github.com/datastax/pulsar/commit/379a203) [improve][monitor] Add version=0.0.4 to /metrics content type for Prometheus 3.x compatibility (#24060)
* [dd26654](https://github.com/datastax/pulsar/commit/dd26654) [fix][broker] Pattern subscription doesn't work when the pattern excludes the topic domain. (#24072)
* [807a2bc](https://github.com/datastax/pulsar/commit/807a2bc) [fix] Avoid negative estimated entry count (#24055)
* [6b0806a](https://github.com/datastax/pulsar/commit/6b0806a) [fix][doc] fix doc related to chunk message feature. (#24023)
* [9feba1f](https://github.com/datastax/pulsar/commit/9feba1f) [fix][broker] Add expire check for replicator (#23975)
* [a9ffcb7](https://github.com/datastax/pulsar/commit/a9ffcb7) [fix][broker] Fix missing validation when setting retention policy on topic level (#24032)
* [55dfc00](https://github.com/datastax/pulsar/commit/55dfc00) [fix][broker] fix delay queue sequence issue. (#24035)
* [2bb61b2](https://github.com/datastax/pulsar/commit/2bb61b2) [fix][doc] Workaround Go Yaml issue go-yaml/yaml#789 in docker-compose example (#24040)
* [d9ab831](https://github.com/datastax/pulsar/commit/d9ab831) [improve] Upgrade Netty to 4.1.119.Final (#24049)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.13  | cassandra-enhanced-pulsar-sink-1.6.13-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.2   | pulsar-io-cloud-storage-3.2.2.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 4.0.3.2 | pulsar-io-data-generator-4.0.3.2.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 4.0.3.2 | pulsar-io-elastic-search-4.0.3.2.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 4.0.3.2 | pulsar-io-http-4.0.3.2.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 4.0.3.2 | pulsar-io-jdbc-clickhouse-4.0.3.2.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 4.0.3.2 | pulsar-io-jdbc-mariadb-4.0.3.2.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 4.0.3.2 | pulsar-io-jdbc-openmldb-4.0.3.2.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 4.0.3.2 | pulsar-io-jdbc-postgres-4.0.3.2.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 4.0.3.2 | pulsar-io-jdbc-sqlite-4.0.3.2.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 4.0.3.2 | pulsar-io-kafka-4.0.3.2.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 4.0.3.2 | pulsar-io-kinesis-4.0.3.2.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.1.15  | pulsar-snowflake-connector-0.1.15.nar         |
| [lakehouse](https://github.com/streamnative/pulsar-io-lakehouse)         | Lakehouse Connector                                                                                          | 3.3.3.1 | pulsar-io-lakehouse-3.3.3.1.nar               |
| [lakehouse-cloud](https://github.com/streamnative/pulsar-io-lakehouse)   | Lakehouse Cloud Connector                                                                                    | 3.3.3.1 | pulsar-io-lakehouse-3.3.3.1-cloud.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.3.1   | pulsar-cassandra-source-2.3.1.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 4.0.3.2 | pulsar-io-data-generator-4.0.3.2.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 4.0.3.2 | pulsar-io-debezium-mongodb-4.0.3.2.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 4.0.3.2 | pulsar-io-debezium-mssql-4.0.3.2.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 4.0.3.2 | pulsar-io-debezium-mysql-4.0.3.2.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 4.0.3.2 | pulsar-io-debezium-oracle-4.0.3.2.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 4.0.3.2 | pulsar-io-debezium-postgres-4.0.3.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 4.0.3.2 | pulsar-io-kafka-4.0.3.2.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 4.0.3.2 | pulsar-io-kinesis-4.0.3.2.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 4.0.3.0  | pulsar-kafka-proxy-4.0.3.0.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version  | File                                      |
|----------------------------------------------------------------|----------------------------------------|----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.1.0 | starlight-rabbitmq-2.10.1.0.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 4.0.3.0  | pulsar-protocol-handler-kafka-4.0.3.0.nar |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.3.1   | pulsar-cassandra-admin-2.3.1-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 6.0.1   | pulsar-jms-admin-6.0.1-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 6.0.1   | pulsar-jms-6.0.1-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.2.0   | pulsar-ai-tools-3.2.0.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.0   | pulsar-transformations-3.2.0.nar |
</details>


## Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls40_3.2/build.json) used for the build.


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.13-nar.nar
- pulsar-cassandra-source-2.3.1.nar
- pulsar-io-cloud-storage-3.2.2.nar
- pulsar-io-debezium-mongodb-4.0.3.2.nar 
- pulsar-io-jdbc-sqlite-4.0.3.2.nar
- pulsar-io-kinesis-4.0.3.2.nar
- pulsar-io-data-generator-4.0.3.2.nar
- pulsar-io-elastic-search-4.0.3.2.nar
- pulsar-io-jdbc-clickhouse-4.0.3.2.nar
- pulsar-io-debezium-oracle-4.0.3.2.nar
- pulsar-io-jdbc-openmldb-4.0.3.2.nar
- pulsar-io-jdbc-postgres-4.0.3.2.nar
- pulsar-io-debezium-mssql-4.0.3.2.nar
- pulsar-io-debezium-mysql-4.0.3.2.nar
- pulsar-io-jdbc-mariadb-4.0.3.2.nar
- pulsar-io-debezium-postgres-4.0.3.2.nar
- pulsar-io-http-4.0.3.2.nar
- pulsar-io-kafka-4.0.3.2.nar 
- pulsar-snowflake-connector-0.1.15.nar
- pulsar-protocol-handler-kafka-4.0.3.2.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-4.0.3.2.nar
- pulsar-jms-6.0.1-nar.nar