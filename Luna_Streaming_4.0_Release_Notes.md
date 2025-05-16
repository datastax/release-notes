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

## Luna Streaming Distribution 4.0 3.3
This maintenance release of the DataStax Luna Streaming Distribution for 4.0 which includes important stability and security updates for Luna Streaming, as well as for the various connectors packaged alongside it, such as sinks, sources, functions, protocol extensions, proxy extensions, filters, and client extensions.

### Most notable commits

* [fff5e69](https://github.com/datastax/pulsar/commit/fff5e69) Fix code style in DefaultLookupProxyHandler
* [aec9ec1](https://github.com/datastax/pulsar/commit/aec9ec1) Fix ProxyTest.testGetPartitionedMetadataErrorCode
* [f85b7ee](https://github.com/datastax/pulsar/commit/f85b7ee) [fix][sec] Upgrade Jetty to 9.4.57.v20241219 to mitigate CVE-2024-6763 (#24232)
* [a5ad67c](https://github.com/datastax/pulsar/commit/a5ad67c) [improve][io] support kafka connect transforms and predicates (#24221)
* [6c0b79d](https://github.com/datastax/pulsar/commit/6c0b79d) [improve][client]Improve transaction log when a TXN command timeout (#24230)
* [3a296fd](https://github.com/datastax/pulsar/commit/3a296fd) [fix][broker] Orphan schema after disabled a cluster for a namespace (#24223)
* [c40b89e](https://github.com/datastax/pulsar/commit/c40b89e) [fix][broker] Fix ByteBuf memory leak in REST API for publishing messages (#24228)
* [f30c4e2](https://github.com/datastax/pulsar/commit/f30c4e2) [fix][client] Fix incorrect producer.getPendingQueueSize due to incomplete queue implementation (#24184)
* [adb43b9](https://github.com/datastax/pulsar/commit/adb43b9) [improve][broker]Improve the feature "Optimize subscription seek (cursor reset) by timestamp": search less entries (#24219)
* [c7922db](https://github.com/datastax/pulsar/commit/c7922db) [improve] Upgrade Netty to 4.1.121.Final (#24214)
* [dca2e53](https://github.com/datastax/pulsar/commit/dca2e53) [fix][test] Fix flaky BatchMessageWithBatchIndexLevelTest.testBatchMessageAck (#24212)
* [7bd7f61](https://github.com/datastax/pulsar/commit/7bd7f61) [fix][test] Fix multiple resource leaks in tests (#24218)
* [8c462ff](https://github.com/datastax/pulsar/commit/8c462ff) [improve][client] validate ClientConfigurationData earlier to avoid resource leaks (#24187)
* [f5bc20b](https://github.com/datastax/pulsar/commit/f5bc20b) [fix][broker] Fix HealthChecker deadlock in shutdown (#24216)
* [950d043](https://github.com/datastax/pulsar/commit/950d043) [fix][broker] Fix tenant creation and update with null value (#24209)
* [1a6b37c](https://github.com/datastax/pulsar/commit/1a6b37c) [fix][admin] Backlog quota's policy is null which causes a NPE (#24192)
* [3caf8f2](https://github.com/datastax/pulsar/commit/3caf8f2) [improve] Upgrade Apache Commons library versions to compatible versions (#24205)
* [ae47f1f](https://github.com/datastax/pulsar/commit/ae47f1f) [fix][broker] Fix broker shutdown delay by resolving hanging health checks (#24210)
* [ef10693](https://github.com/datastax/pulsar/commit/ef10693) [fix][broker] Fix compaction service log's wrong condition (#24207)
* [ed464f8](https://github.com/datastax/pulsar/commit/ed464f8) [fix][test] Fix resource leaks in ProxyTest and fix invalid tests (#24204)
* [d499c63](https://github.com/datastax/pulsar/commit/d499c63) [improve][io] Upgrade Kafka client and compatible Confluent platform version (#24201)
* [33e8d3f](https://github.com/datastax/pulsar/commit/33e8d3f) Revert "[fix][broker] Add topic consistency check (#24118)"
* [a169bc4](https://github.com/datastax/pulsar/commit/a169bc4) Revert "[fix][broker] Directly query single topic existence when the topic is partitioned (#24154)"
* [7cfe3d4](https://github.com/datastax/pulsar/commit/7cfe3d4) [fix][test] Fix flaky NamespacesTest.testNamespacesApiRedirects (#24194)
* [062e2cb](https://github.com/datastax/pulsar/commit/062e2cb) [fix][broker] Fix NPE from the wrong iterator in the ownership cleanup job(ExtensibleLoadManagerImpl only) (#24196)
* [1594e91](https://github.com/datastax/pulsar/commit/1594e91) [fix][broker] Fix cluster level OffloadedReadPriority to bookkeeper-first does not work (#24151)
* [6921a49](https://github.com/datastax/pulsar/commit/6921a49) [fix][broker] Fixes Inconsistent ServiceUnitStateData View (ExtensibleLoadManagerImpl only) (#24186)
* [67c4c46](https://github.com/datastax/pulsar/commit/67c4c46) [fix][schema] Reject unsupported Avro schema types during schema registration (#24103)
* [eb3fc87](https://github.com/datastax/pulsar/commit/eb3fc87) [fix][proxy] Fix incorrect client error when calling get topic metadata (#24181)
* [32392a2](https://github.com/datastax/pulsar/commit/32392a2) [fix][broker] Fix some problems in calculate totalAvailableBookies in method getExcludedBookiesWithIsolationGroups when some bookies belongs to multiple isolation groups. (#24091)
* [8fefcdc](https://github.com/datastax/pulsar/commit/8fefcdc) [fix][test] Fix remaining UnfinishedStubbingException issue with AuthZTests (#24174)
* [ac38706](https://github.com/datastax/pulsar/commit/ac38706) [improve][test] Use configured session timeout for MockZooKeeper and TestZKServer in PulsarTestContext (#24171)
* [2a269d4](https://github.com/datastax/pulsar/commit/2a269d4) [fix][test] Improve reliability of IncrementPartitionsTest (#24172)
* [53d43ee](https://github.com/datastax/pulsar/commit/53d43ee) [fix][build] Fix skipTag and use explicit tag for image name (#24168)
* [c8cfcd9](https://github.com/datastax/pulsar/commit/c8cfcd9) [fix][test]flaky-test:ManagedLedgerInterceptorImplTest.testManagedLedgerPayloadInputProcessorFailure (#24170)
* [c37342b](https://github.com/datastax/pulsar/commit/c37342b) [fix][broker] Consumer stuck when delete subscription __compaction failed (#23980)
* [0e7de02](https://github.com/datastax/pulsar/commit/0e7de02) [fix][ml] Fix ML thread blocking issue in internalGetPartitionedStats API (#24167)
* [1f3b7c4](https://github.com/datastax/pulsar/commit/1f3b7c4) [fix][test] Fix invalid test CompactionTest.testDeleteCompactedLedgerWithSlowAck (#24166)
* [7b89129](https://github.com/datastax/pulsar/commit/7b89129) [fix][test] Fix UnfinishedStubbing issue in AuthZTests (#24165)
* [8fbab91](https://github.com/datastax/pulsar/commit/8fbab91) [fix][ml] Skip deleting cursor if it was already deleted before calling unsubscribe (#24098)
* [758e135](https://github.com/datastax/pulsar/commit/758e135) [fix][broker] Directly query single topic existence when the topic is partitioned (#24154)
* [38145e8](https://github.com/datastax/pulsar/commit/38145e8) [fix][broker] Add topic consistency check (#24118)
* [164268e](https://github.com/datastax/pulsar/commit/164268e) [fix][test] Update partitioned topic subscription assertions in IncrementPartitionsTest (#24056)
* [688c0e5](https://github.com/datastax/pulsar/commit/688c0e5) [cleanup][misc] Add override annotation (#24033)
* [23b428f](https://github.com/datastax/pulsar/commit/23b428f) [improve][build] Build apachepulsar/pulsar-io-kinesis-sink-kinesis_producer with Alpine 3.21 (#24180)
* [5247dfa](https://github.com/datastax/pulsar/commit/5247dfa) [fix][broker] fix ExtensibleLoadManager to override the ownerships concurrently without blocking load manager thread (#24156)
* [bd61088](https://github.com/datastax/pulsar/commit/bd61088) [fix][test] Fix flaky BrokerServiceChaosTest.testFetchPartitionedTopicMetadataWithCacheRefresh (#24161)
* [75e5cb3](https://github.com/datastax/pulsar/commit/75e5cb3) [fix][test] Fix flaky BrokerServiceChaosTest (#24162)
* [d049244](https://github.com/datastax/pulsar/commit/d049244) [fix][broker] The feature brokerDeleteInactivePartitionedTopicMetadataEnabled leaves orphan topic policies and topic schemas (#24150)
* [07dc37a](https://github.com/datastax/pulsar/commit/07dc37a) modified test to use newConnect method & Getter for FeatureFlags obj in ServerCnx
* [bc01ae8](https://github.com/datastax/pulsar/commit/bc01ae8) [fix][proxy] Propagate client connection feature flags through Pulsar Proxy to Broker (#24158)
* [5fde2a6](https://github.com/datastax/pulsar/commit/5fde2a6) [fix][build] Fix docker image building by replacing deprecated and removed compress argument (#24155)
* [1e55dc0](https://github.com/datastax/pulsar/commit/1e55dc0) [fix][misc]: ignore deleted ledger when tear down cluster (#23831)
* [05de7ce](https://github.com/datastax/pulsar/commit/05de7ce) [fix] [broker] topics infinitely failed to delete after remove cluster from replicated clusters modifying when using partitioned system topic (#24097)
* [10c3dbd](https://github.com/datastax/pulsar/commit/10c3dbd) [improve][broker] extract getMaxEntriesInThisBatch into a method and add unit test for it (#24117)
* [38eb99f](https://github.com/datastax/pulsar/commit/38eb99f) [fix][sec] Upgrade jwt/v5 to 5.2.2 to address CVE-2025-30204 (#24140)
* [3164e2d](https://github.com/datastax/pulsar/commit/3164e2d) [fix][sec] Upgrade pulsar-function-go dependencies to address CVE-2025-22870 (#24135)
* [f9bde70](https://github.com/datastax/pulsar/commit/f9bde70) [improve][fn] Introduce NewOutputMessageWithError to enable error handling (#24122)
* [2ef9063](https://github.com/datastax/pulsar/commit/2ef9063) [fix][test] Fix flaky NonPersistentTopicTest.testMsgDropStat (#24134)
* [4b18610](https://github.com/datastax/pulsar/commit/4b18610) [fix][io] Fix KinesisSink json flattening for AVRO's SchemaType.BYTES (#24132)

### `lunastreaming-all` distribution
<details><summary>Sinks</summary>

| Name                                                                     | Description                                                                                                  | Version | File                                          |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------|
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink)            | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.14  | cassandra-enhanced-pulsar-sink-1.6.14-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage                                                                               | 3.2.4   | pulsar-io-cloud-storage-3.2.4.nar             |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source                                                                                   | 4.0.3.3 | pulsar-io-data-generator-4.0.3.3.nar          |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors)           | Writes data into Elastic Search                                                                              | 4.0.3.3 | pulsar-io-elastic-search-4.0.3.3.nar          |
| [http](https://pulsar.apache.org/docs/io-connectors)                     | Writes data to an HTTP server (Webhook)                                                                      | 4.0.3.3 | pulsar-io-http-4.0.3.3.nar                    |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors)          | JDBC sink for ClickHouse                                                                                     | 4.0.3.3 | pulsar-io-jdbc-clickhouse-4.0.3.3.nar         |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors)             | JDBC sink for MariaDB                                                                                        | 4.0.3.3 | pulsar-io-jdbc-mariadb-4.0.3.3.nar            |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for OpenMLDB                                                                                       | 4.0.3.3 | pulsar-io-jdbc-openmldb-4.0.3.3.nar           |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors)            | JDBC sink for PostgreSQL                                                                                     | 4.0.3.3 | pulsar-io-jdbc-postgres-4.0.3.3.nar           |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors)              | JDBC sink for SQLite                                                                                         | 4.0.3.3 | pulsar-io-jdbc-sqlite-4.0.3.3.nar             |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector                                                                              | 4.0.3.3 | pulsar-io-kafka-4.0.3.3.nar                   |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                                                                                           | 4.0.3.3 | pulsar-io-kinesis-4.0.3.3.nar                 |
| [snowflake](https://github.com/datastax/snowflake-connector)             | Snowflake Connector                                                                                          | 0.2.1  | pulsar-snowflake-connector-0.2.1.nar         |
| [lakehouse](https://github.com/streamnative/pulsar-io-lakehouse)         | Lakehouse Connector                                                                                          | 3.3.3.1 | pulsar-io-lakehouse-3.3.3.1.nar               |
| [lakehouse-cloud](https://github.com/streamnative/pulsar-io-lakehouse)   | Lakehouse Cloud Connector                                                                                    | 3.3.3.1 | pulsar-io-lakehouse-3.3.3.1-cloud.nar         |
</details>
<details><summary>Sources</summary>

| Name                                                                     | Description                          | Version | File                                    |
|--------------------------------------------------------------------------|--------------------------------------|---------|-----------------------------------------|
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra             | 2.3.1   | pulsar-cassandra-source-2.3.1.nar       |
| [data-generator](https://pulsar.apache.org/docs/io-connectors)           | Test data generator source           | 4.0.3.3 | pulsar-io-data-generator-4.0.3.3.nar    |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors)         | Debezium MongoDb Source              | 4.0.3.3 | pulsar-io-debezium-mongodb-4.0.3.3.nar  |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors)           | Debezium Microsoft SQL Server Source | 4.0.3.3 | pulsar-io-debezium-mssql-4.0.3.3.nar    |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors)           | Debezium MySql Source                | 4.0.3.3 | pulsar-io-debezium-mysql-4.0.3.3.nar    |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors)          | Debezium Oracle Source               | 4.0.3.3 | pulsar-io-debezium-oracle-4.0.3.3.nar   |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors)        | Debezium Postgres Source             | 4.0.3.3 | pulsar-io-debezium-postgres-4.0.3.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors)                    | Kafka source and sink connector      | 4.0.3.3 | pulsar-io-kafka-4.0.3.3.nar             |
| [kinesis](https://pulsar.apache.org/docs/io-connectors)                  | Kinesis connectors                   | 4.0.3.3 | pulsar-io-kinesis-4.0.3.3.nar           |
</details>
<details><summary>Proxy extensions</summary>

| Name                                                           | Description                            | Version  | File                            |
|----------------------------------------------------------------|----------------------------------------|----------|---------------------------------|
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Proxy Extension                  | 4.0.3.1  | pulsar-kafka-proxy-4.0.3.1.nar  |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>
<details><summary>Protocol handlers</summary>

| Name                                                           | Description                            | Version  | File                                      |
|----------------------------------------------------------------|----------------------------------------|----------|-------------------------------------------|
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar           |
| [kafka](https://github.com/datastax/starlight-for-kafka)       | Kafka Protocol Handler                 | 4.0.3.1  | pulsar-protocol-handler-kafka-4.0.3.1.nar |
</details>
<details><summary>CLI extensions</summary>

| Name                                                          | Description                                      | Version | File                                 |
|---------------------------------------------------------------|--------------------------------------------------|---------|--------------------------------------|
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands     | 2.3.1   | pulsar-cassandra-admin-2.3.1-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors)           | Starlight for JMS - Pulsar Admin Custom Commands | 6.0.4   | pulsar-jms-admin-6.0.4-nar.nar       |
</details>
<details><summary>Filters</summary>

| Name                                                | Description                                         | Version | File                     |
|-----------------------------------------------------|-----------------------------------------------------|---------|--------------------------|
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 6.0.4   | pulsar-jms-6.0.4-nar.nar |
</details>
<details><summary>Functions</summary>

| Name                                                       | Description             | Version | File                             |
|------------------------------------------------------------|-------------------------|---------|----------------------------------|
| [ai-tools](https://pulsar.apache.org/docs/io-connectors)   | Generative AI tools     | 3.2.1   | pulsar-ai-tools-3.2.1.nar        |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.1   | pulsar-transformations-3.2.1.nar |
</details>


## Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls40_3.3/build.json) used for the build


### Builtin connectors

- cassandra-enhanced-pulsar-sink-1.6.14-nar.nar
- pulsar-cassandra-source-2.3.1.nar
- pulsar-io-cloud-storage-3.2.4.nar
- pulsar-io-debezium-mongodb-4.0.3.3.nar 
- pulsar-io-jdbc-sqlite-4.0.3.3.nar
- pulsar-io-kinesis-4.0.3.3.nar
- pulsar-io-data-generator-4.0.3.3.nar
- pulsar-io-elastic-search-4.0.3.3.nar
- pulsar-io-jdbc-clickhouse-4.0.3.3.nar
- pulsar-io-debezium-oracle-4.0.3.3.nar
- pulsar-io-jdbc-openmldb-4.0.3.3.nar
- pulsar-io-jdbc-postgres-4.0.3.3.nar
- pulsar-io-debezium-mssql-4.0.3.3.nar
- pulsar-io-debezium-mysql-4.0.3.3.nar
- pulsar-io-jdbc-mariadb-4.0.3.3.nar
- pulsar-io-debezium-postgres-4.0.3.3.nar
- pulsar-io-http-4.0.3.3.nar
- pulsar-io-kafka-4.0.3.3.nar 
- pulsar-snowflake-connector-0.2.1.nar
- pulsar-protocol-handler-kafka-4.0.3.1.nar
- starlight-rabbitmq-4.0.0.2.nar
- pulsar-kafka-proxy-4.0.3.1.nar
- pulsar-jms-6.0.4-nar.nar


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
- pulsar-protocol-handler-kafka-4.0.3.0.nar
- starlight-rabbitmq-2.10.1.0.nar
- pulsar-kafka-proxy-4.0.3.0.nar
- pulsar-jms-6.0.1-nar.nar