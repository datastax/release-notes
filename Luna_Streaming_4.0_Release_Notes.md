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
## Luna Streaming Distribution 4.0 7.1
This maintenance release of the DataStax Luna Streaming Distribution for 4.0 which includes important stability and security updates for Luna Streaming, as well as for the various connectors packaged alongside it, such as sinks, sources, functions, protocol extensions, proxy extensions, filters, and client extensions.

### Most notable commits
* [d28392d](https://github.com/datastax/pulsar/commit/d28392d) [fix][broker][branch-4.0] Fix failed testFinishTakeSnapshotWhenTopicLoading due to topic future cache conflicts (#24947)
* [1510ecf](https://github.com/datastax/pulsar/commit/1510ecf) [fix][txn] fix concurrent error cause txn stuck in TransactionBufferHandlerImpl#endTxn (#23551)
* [eb17c66](https://github.com/datastax/pulsar/commit/eb17c66) [fix][broker] Avoid recursive update in ConcurrentHashMap during policy cache cleanup (#24939)
* [354c517](https://github.com/datastax/pulsar/commit/354c517) [fix][monitor] Fix the incorrect metrics name (#21981)
* [a97a9dd](https://github.com/datastax/pulsar/commit/a97a9dd) [improve][broker] Add tests for using absolute FQDN for advertisedAddress and remove extra dot from brokerId (#24787)
* [e6dd5ef](https://github.com/datastax/pulsar/commit/e6dd5ef) [fix][admin] Set local policies overwrites "number of bundles" passed during namespace creation (#24762)
* [14a6749](https://github.com/datastax/pulsar/commit/14a6749) [fix][sec] Override nimbus-jose-jwt to remediate CVE-2023-52428 and CVE-2025-53864 (#24937)
* [d03cf00](https://github.com/datastax/pulsar/commit/d03cf00) [fix][broker] Fix bug in PersistentMessageExpiryMonitor which blocked further expirations (#24941)
* [4fb254d](https://github.com/datastax/pulsar/commit/4fb254d) [fix][test] Stabilize testMsgDropStat by reliably triggering non-persistent publisher drop (#24929)
* [5ca3b8c](https://github.com/datastax/pulsar/commit/5ca3b8c) [fix][sec] Override commons-beanutils and commons-configuration2 to remediate CVEs (#24936)
* [563e58c](https://github.com/datastax/pulsar/commit/563e58c) [fix][sec] Override kafka-clients in kinesis-kpl-shaded to remediate CVE-2024-31141 and CVE-2025-27817 (#24935)
* [9e47425](https://github.com/datastax/pulsar/commit/9e47425) [fix][broker] Fix stack overflow caused by race condition when closing a connection (#24934)
* [176e07d](https://github.com/datastax/pulsar/commit/176e07d) [fix][broker] ExtensibleLoadManager: handle SessionReestablished and Reconnected events to re-register broker metadata (#24932)
* [fb87033](https://github.com/datastax/pulsar/commit/fb87033) [fix][broker] Use poll instead remove to avoid NoSuchElementException (#24933)
* [891aa50](https://github.com/datastax/pulsar/commit/891aa50) [fix][broker] fix getMaxReadPosition in TransactionBufferDisable should return latest (#24898)
* [5998856](https://github.com/datastax/pulsar/commit/5998856) [improve][broker] Don't log an error when updatePartitionedTopic is called on a non-partitioned topic (#24943)
* [b2ff7e6](https://github.com/datastax/pulsar/commit/b2ff7e6) [improve][broker] Optimize lookup result warn log (#24942)
* [91ba207](https://github.com/datastax/pulsar/commit/91ba207) [fix][client] Fix thread leak in reloadLookUp method which is used by ServiceUrlProvider (#24794)
* [2cf6dc0](https://github.com/datastax/pulsar/commit/2cf6dc0) [fix][broker] Run ResourceGroup tasks only when tenants/namespaces registered (#24859)
* [3eff549](https://github.com/datastax/pulsar/commit/3eff549) [fix][sec] Upgrade BouncyCastle FIPS to 2.0.10 to remediate CVE-2025-8916 (#24923)
* [73808c4](https://github.com/datastax/pulsar/commit/73808c4) [fix][broker] BacklogMessageAge is not reset when cursor mdPosition is on an open ledger (#24915)
* [0c68377](https://github.com/datastax/pulsar/commit/0c68377) [fix][broker] Fix wrong behaviour when using namespace.allowed_clusters, such as namespace deletion and namespace policies updating (#24860)
* [4cfc53b](https://github.com/datastax/pulsar/commit/4cfc53b) [improve][ci] Move replication tests to new group Broker Group 5 in Pulsar CI (#24917)
* [7ac7438](https://github.com/datastax/pulsar/commit/7ac7438) [fix][sec] Upgrade Spring to 6.2.12 to remediate CVE-2025-22233 and CVE-2025-41249 (#24903)
* [10d9820](https://github.com/datastax/pulsar/commit/10d9820) [improve][misc] Upgrade Netty to 4.1.128.Final (#24911)
* [29bec39](https://github.com/datastax/pulsar/commit/29bec39) [fix][test] Fix flaky ReplicatorTest.testResumptionAfterBacklogRelaxed (#24904)
* [c8375e7](https://github.com/datastax/pulsar/commit/c8375e7) [improve][broker] Reduce the broker close time to avoid useless wait for event loop shutdown (#24895)
* [f7c4f95](https://github.com/datastax/pulsar/commit/f7c4f95) [fix][broker] Fix totalAvailablePermits not reduced when removing consumer from non-persistent dispatcher (#24885)
* [5ecdcaa](https://github.com/datastax/pulsar/commit/5ecdcaa) [fix][test]fix flaky SimpleProducerConsumerTest.testReceiveAsyncCompletedWhenClosing (#24858)
* [16e8ae4](https://github.com/datastax/pulsar/commit/16e8ae4) [fix][test] Made ProtobufSchemaTest.testParsingInfoProperty order-independent (#24807)
* [61c2480](https://github.com/datastax/pulsar/commit/61c2480) [improve][client]Add null check for Pulsar client clock configuration (#24848)
* [377133e](https://github.com/datastax/pulsar/commit/377133e) [fix][test] BacklogQuotaManagerTest.backlogsAgeMetricsNoPreciseWithoutBacklogQuota handle empty /metrics scrape (#24887)
* [ea1e3e4](https://github.com/datastax/pulsar/commit/ea1e3e4) [improve][broker]Skip to mark delete if the target position of expira… (#24881)
* [74892dc](https://github.com/datastax/pulsar/commit/74892dc) [fix][broker] Stop to retry to read entries if the replicator has terminated (#24880)
* [cd4cea8](https://github.com/datastax/pulsar/commit/cd4cea8) [fix][broker] Flaky-test: TopicTransactionBufferTest.testMessagePublishInOrder (#24826)
* [e5b61fc](https://github.com/datastax/pulsar/commit/e5b61fc) [fix][test] Stabilize PublishRateLimiterOverconsumingTest by aligning measurement and using adjacent 2-sec averages (#24864)
* [a02310b](https://github.com/datastax/pulsar/commit/a02310b) [fix][test] Fix flaky LookupPropertiesTest.testConcurrentLookupProperties (#24854)
* [ce14580](https://github.com/datastax/pulsar/commit/ce14580) [fix][sec] Upgrade Jetty to 9.4.58.v20250814 to address CVE-2025-5115 (#24897)
* [22defed](https://github.com/datastax/pulsar/commit/22defed) [fix][sec] Bump io.vertx:vertx-web from 4.5.10 to 4.5.22 (#24889)
* [824019a](https://github.com/datastax/pulsar/commit/824019a) [fix][test] Stabilize SequenceIdWithErrorTest by fencing after first publish to avoid empty-ledger deletion and send timeout (#24861)
* [8be9698](https://github.com/datastax/pulsar/commit/8be9698) [fix][test] Fix flaky SubscriptionSeekTest.testSeekWillNotEncounteredFencedError by counting subscription is fenced only after seek (#24865)
* [26f5a2c](https://github.com/datastax/pulsar/commit/26f5a2c) [fix][ml] Fix ledger trimming race causing cursor to point to deleted ledgers (#24855)
* [97368ed](https://github.com/datastax/pulsar/commit/97368ed) Fix compile issue by cherry-picked #24852
* [997aea2](https://github.com/datastax/pulsar/commit/997aea2) [fix]Fixed getChildren('/') on Oxia based provider (#24863)
* [9c83d13](https://github.com/datastax/pulsar/commit/9c83d13) [fix][ml] Fix getNumberOfEntries may point to deleted ledger (#24852)
* [6c5c797](https://github.com/datastax/pulsar/commit/6c5c797) [fix][broker] Ensure LoadSheddingTask is scheduled after metadata service is available again (#24838)
* [ed13768](https://github.com/datastax/pulsar/commit/ed13768) [improve][ci] Upgrade GitHub Actions workflows to use ubuntu-24.04 (#24841)
* [dcccbb9](https://github.com/datastax/pulsar/commit/dcccbb9) [fix][client] Fix getPendingQueueSize for PartitionedTopicProducerStatsRecorderImpl: avoid NPE and implement aggregation (#24830)
* [283b123](https://github.com/datastax/pulsar/commit/283b123) [fix] Fix mixed lookup/partition metadata requests causing reliability issues and incorrect responses (#24832)
* [62350ef](https://github.com/datastax/pulsar/commit/62350ef) [fix][broker] Allow intermittent error from topic policies service when loading topics (#24829)
* [2dd7a5c](https://github.com/datastax/pulsar/commit/2dd7a5c) [fix][broker] Fix incorrect topic loading latency metric and timeout might not be respected (#24785)
* [e734235](https://github.com/datastax/pulsar/commit/e734235) [fix][client] Make auto partitions update work for old brokers without PIP-344 (#24822)
* [8531eef](https://github.com/datastax/pulsar/commit/8531eef) [improve][broker]Improve NamespaceService log that is printed when cluster was removed (#24801)
* [ac9bb27](https://github.com/datastax/pulsar/commit/ac9bb27) [fix][broker] Flaky-test: ExtensibleLoadManagerImplTest.testDisableBroker (#24770)
* [e4c4a35](https://github.com/datastax/pulsar/commit/e4c4a35) [improve][broker] Replace isServiceUnitActiveAsync with checkTopicNsOwnership (#24780)
* [cd6d4a5](https://github.com/datastax/pulsar/commit/cd6d4a5) [improve][ml] Upgrade Oxia client to 0.7.0 (#24824)
* [88d4253](https://github.com/datastax/pulsar/commit/88d4253) [fix][build] Remove invalid profile in settings.xml that caused gpg signing to fail (#24812)
* [c3d669e](https://github.com/datastax/pulsar/commit/c3d669e) [fix][build] Fix maven deploy with maven-source-plugin 3.3.1 (#24811)
* [0b53b79](https://github.com/datastax/pulsar/commit/0b53b79) [fix] Update gRPC to 1.75.0 (#24813)



### `lunastreaming-all` distribution

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.3.2 | pulsar-cassandra-admin-2.3.2-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 6.0.6 | pulsar-jms-admin-6.0.6-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 6.0.6 | pulsar-jms-6.0.6-nar.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 4.0.3.3 | pulsar-protocol-handler-kafka-4.0.3.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 4.0.3.3 | pulsar-kafka-proxy-4.0.3.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.14 | cassandra-enhanced-pulsar-sink-1.6.14-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 3.2.4 | pulsar-io-cloud-storage-3.2.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.7.1 | pulsar-io-data-generator-4.0.7.1.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 4.0.7.1 | pulsar-io-elastic-search-4.0.7.1.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 4.0.7.1 | pulsar-io-http-4.0.7.1.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 4.0.7.1 | pulsar-io-jdbc-clickhouse-4.0.7.1.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 4.0.7.1 | pulsar-io-jdbc-mariadb-4.0.7.1.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 4.0.7.1 | pulsar-io-jdbc-openmldb-4.0.7.1.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 4.0.7.1 | pulsar-io-jdbc-postgres-4.0.7.1.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 4.0.7.1 | pulsar-io-jdbc-sqlite-4.0.7.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.7.1 | pulsar-io-kafka-4.0.7.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.7.1 | pulsar-io-kinesis-4.0.7.1.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.2.1 | pulsar-snowflake-connector-0.2.1.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.3.2 | pulsar-cassandra-source-2.3.2.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.7.1 | pulsar-io-data-generator-4.0.7.1.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 4.0.7.1 | pulsar-io-debezium-mongodb-4.0.7.1.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 4.0.7.1 | pulsar-io-debezium-mssql-4.0.7.1.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 4.0.7.1 | pulsar-io-debezium-mysql-4.0.7.1.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 4.0.7.1 | pulsar-io-debezium-oracle-4.0.7.1.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 4.0.7.1 | pulsar-io-debezium-postgres-4.0.7.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.7.1 | pulsar-io-kafka-4.0.7.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.7.1 | pulsar-io-kinesis-4.0.7.1.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.2.1 | pulsar-ai-tools-3.2.1.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.1 | pulsar-transformations-3.2.1.nar |
</details>

See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls_4.0.7_1/build.json) used for the build

## Luna Streaming Distribution 4.0 7.0
This maintenance release of the DataStax Luna Streaming Distribution for 4.0 which includes important stability and security updates for Luna Streaming, as well as for the various connectors packaged alongside it, such as sinks, sources, functions, protocol extensions, proxy extensions, filters, and client extensions.

### Most notable commits
* [0bb2c25](https://github.com/datastax/pulsar/commit/0bb2c25) [improve][misc] Cherrypick Add API endpoint for function-worker for liveness check with configurable flag into 4.x (#530)
* [7b653a8](https://github.com/datastax/pulsar/commit/7b653a8) Update project.version to 4.0.7.0
* [239c42b](https://github.com/datastax/pulsar/commit/239c42b) Bump org.apache.zookeeper:zookeeper from 3.9.3 to 3.9.4 (#24779)
* [3c9b0b0](https://github.com/datastax/pulsar/commit/3c9b0b0) [improve][broker] Call scheduleAtFixedRateNonConcurrently for scheduled tasks, instead of scheduleAtFixedRate (#24596)
* [e740e41](https://github.com/datastax/pulsar/commit/e740e41) [fix][test] Flaky-test: BrokerServiceTest.testShutDownWithMaxConcurrentUnload (#24769)
* [35042f3](https://github.com/datastax/pulsar/commit/35042f3) [improve][build] Upgrade Mockito, AssertJ and ByteBuddy to fully support JDK25 (#24764)
* [fa8a318](https://github.com/datastax/pulsar/commit/fa8a318) [fix][client] Exclude io.prometheus:simpleclient_caffeine from client-side dependencies (#24761)
* [1ba2e08](https://github.com/datastax/pulsar/commit/1ba2e08) [improve][build] Upgrade Lombok to 1.18.42 to fully support JDK25 (#24763)
* [e3190a8](https://github.com/datastax/pulsar/commit/e3190a8) [improve][broker] If there is a deadlock in the service, the probe should return a failure because the service may be unavailable (#23634)
* [ffd8a0c](https://github.com/datastax/pulsar/commit/ffd8a0c) [fix][broker] First entry will be skipped if opening NonDurableCursor while trimmed ledger is adding first entry. (#24738)
* [cf11b88](https://github.com/datastax/pulsar/commit/cf11b88) [fix][ml] Fix EOFException after enabled topics offloading (#24753)
* [aca4c1c](https://github.com/datastax/pulsar/commit/aca4c1c) [fix][misc] Fix compareTo contract violation for NamespaceBundleStats, TimeAverageMessageData and ResourceUnitRanking (#24772)
* [514b6d0](https://github.com/datastax/pulsar/commit/514b6d0) [improve][build] Upgrade SpotBugs to a version that supports JDK25 (#24768)
* [123ac4d](https://github.com/datastax/pulsar/commit/123ac4d) [fix][ci] Fix CI for Java 25 including upgrade of Gradle Develocity Maven extension (#24767)
* [b985640](https://github.com/datastax/pulsar/commit/b985640) [improve][broker] Separate offload read and write thread pool (#24025)
* [11769a9](https://github.com/datastax/pulsar/commit/11769a9) Remove unbundled jars from license
* [4514ab1](https://github.com/datastax/pulsar/commit/4514ab1) Upgrade bookkeeper to 4.17.1.0.0.4
* [c3cf5e0](https://github.com/datastax/pulsar/commit/c3cf5e0) [improve][misc] LS-1356: Upgrade debezium to 3.2.0.Final (#496)


### `lunastreaming-all` distribution

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.3.2 | pulsar-cassandra-admin-2.3.2-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 6.0.6 | pulsar-jms-admin-6.0.6-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 6.0.6 | pulsar-jms-6.0.6-nar.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 4.0.3.2 | pulsar-protocol-handler-kafka-4.0.3.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 4.0.3.2 | pulsar-kafka-proxy-4.0.3.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.14 | cassandra-enhanced-pulsar-sink-1.6.14-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 3.2.4 | pulsar-io-cloud-storage-3.2.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.7.0 | pulsar-io-data-generator-4.0.7.0.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 4.0.7.0 | pulsar-io-elastic-search-4.0.7.0.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 4.0.7.0 | pulsar-io-http-4.0.7.0.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 4.0.7.0 | pulsar-io-jdbc-clickhouse-4.0.7.0.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 4.0.7.0 | pulsar-io-jdbc-mariadb-4.0.7.0.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 4.0.7.0 | pulsar-io-jdbc-openmldb-4.0.7.0.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 4.0.7.0 | pulsar-io-jdbc-postgres-4.0.7.0.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 4.0.7.0 | pulsar-io-jdbc-sqlite-4.0.7.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.7.0 | pulsar-io-kafka-4.0.7.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.7.0 | pulsar-io-kinesis-4.0.7.0.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.2.1 | pulsar-snowflake-connector-0.2.1.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.3.2 | pulsar-cassandra-source-2.3.2.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.7.0 | pulsar-io-data-generator-4.0.7.0.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 4.0.7.0 | pulsar-io-debezium-mongodb-4.0.7.0.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 4.0.7.0 | pulsar-io-debezium-mssql-4.0.7.0.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 4.0.7.0 | pulsar-io-debezium-mysql-4.0.7.0.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 4.0.7.0 | pulsar-io-debezium-oracle-4.0.7.0.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 4.0.7.0 | pulsar-io-debezium-postgres-4.0.7.0.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.7.0 | pulsar-io-kafka-4.0.7.0.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.7.0 | pulsar-io-kinesis-4.0.7.0.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.2.1 | pulsar-ai-tools-3.2.1.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.1 | pulsar-transformations-3.2.1.nar |
</details>

See the [environment variables](https://https://github.com/riptano/pulsar-distro/blob/ls_4.0.7_0/build.json) used for the build


## Luna Streaming Distribution 4.0 3.6
This maintenance release of the DataStax Luna Streaming Distribution for 4.0 which includes important stability and security updates for Luna Streaming, as well as for the various connectors packaged alongside it, such as sinks, sources, functions, protocol extensions, proxy extensions, filters, and client extensions.

### Most notable commits
* [f8f5fb055f2](https://github.com/datastax/pulsar/commit/f8f5fb055f2) Release 4.0.3.6

### `lunastreaming-all` distribution

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.3.2 | pulsar-cassandra-admin-2.3.2-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 6.0.6 | pulsar-jms-admin-6.0.6-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 6.0.6 | pulsar-jms-6.0.6-nar.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 4.0.3.2 | pulsar-protocol-handler-kafka-4.0.3.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 4.0.3.2 | pulsar-kafka-proxy-4.0.3.2.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.14 | cassandra-enhanced-pulsar-sink-1.6.14-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 3.2.4 | pulsar-io-cloud-storage-3.2.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.3.6 | pulsar-io-data-generator-4.0.3.6.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 4.0.3.6 | pulsar-io-elastic-search-4.0.3.6.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 4.0.3.6 | pulsar-io-http-4.0.3.6.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 4.0.3.6 | pulsar-io-jdbc-clickhouse-4.0.3.6.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 4.0.3.6 | pulsar-io-jdbc-mariadb-4.0.3.6.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 4.0.3.6 | pulsar-io-jdbc-openmldb-4.0.3.6.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 4.0.3.6 | pulsar-io-jdbc-postgres-4.0.3.6.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 4.0.3.6 | pulsar-io-jdbc-sqlite-4.0.3.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.3.6 | pulsar-io-kafka-4.0.3.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.3.6 | pulsar-io-kinesis-4.0.3.6.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.2.1 | pulsar-snowflake-connector-0.2.1.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.3.2 | pulsar-cassandra-source-2.3.2.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.3.6 | pulsar-io-data-generator-4.0.3.6.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 4.0.3.6 | pulsar-io-debezium-mongodb-4.0.3.6.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 4.0.3.6 | pulsar-io-debezium-mssql-4.0.3.6.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 4.0.3.6 | pulsar-io-debezium-mysql-4.0.3.6.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 4.0.3.6 | pulsar-io-debezium-oracle-4.0.3.6.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 4.0.3.6 | pulsar-io-debezium-postgres-4.0.3.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.3.6 | pulsar-io-kafka-4.0.3.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.3.6 | pulsar-io-kinesis-4.0.3.6.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.2.1 | pulsar-ai-tools-3.2.1.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.1 | pulsar-transformations-3.2.1.nar |
</details>

See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls40_3.6/build.json) used for the build


## Luna Streaming Distribution 4.0 3.4
This maintenance release of the DataStax Luna Streaming Distribution for 4.0 which includes important stability and security updates for Luna Streaming, as well as for the various connectors packaged alongside it, such as sinks, sources, functions, protocol extensions, proxy extensions, filters, and client extensions.

### Most notable commits
* [c179c99bd66](https://github.com/datastax/pulsar/commit/c179c99bd66) [fix][client] Prevent NPE when seeking with null topic in TopicMessageId (#24404)
* [46a5bf7a6ee](https://github.com/datastax/pulsar/commit/46a5bf7a6ee) [fix][ml] Enhance OpFindNewest to support skip non-recoverable data (#24441)
* [cdb952c7aad](https://github.com/datastax/pulsar/commit/cdb952c7aad) [improve][broker][branch-4.0] Update to Oxia 0.6.0 and use new group-id (#24454)
* [11d7afdb575](https://github.com/datastax/pulsar/commit/11d7afdb575) [refactor][broker] Expose the managedLedger field for the sub class (#24448)
* [3387d98bcd3](https://github.com/datastax/pulsar/commit/3387d98bcd3) [fix][ml]Still got BK ledger, even though it has been deleted after offloaded (#24432)
* [623841b50ca](https://github.com/datastax/pulsar/commit/623841b50ca) [improve][broker] Deny removing local cluster from topic level replicated cluster policy (#24351)
* [9164a2351ff](https://github.com/datastax/pulsar/commit/9164a2351ff) [fix][broker] Once the cluster is configured incorrectly, the broker maintains the incorrect cluster configuration even if you removed it (#24419)
* [452397d566e](https://github.com/datastax/pulsar/commit/452397d566e) [fix][ml]Received more than once callback when calling cursor.delete (#24405)
* [75f91c2a147](https://github.com/datastax/pulsar/commit/75f91c2a147) [fix][ml] Cursor ignores the position that has an empty ack-set if disabled deletionAtBatchIndexLevelEnabled (#24406)
* [9e88dda06b3](https://github.com/datastax/pulsar/commit/9e88dda06b3) [fix][broker] Fix the wrong cache name (#24407)
* [014ad5d2a96](https://github.com/datastax/pulsar/commit/014ad5d2a96) [fix][client] Fix some potential resource leak (#24402)
* [cb388d2355f](https://github.com/datastax/pulsar/commit/cb388d2355f) [fix][broker][branch-4.0] Revert "[improve][broker] Reduce memory occupation of the delayed message queue (#23611)" (#24429)
* [c3d99c65a71](https://github.com/datastax/pulsar/commit/c3d99c65a71) [fix][txn] Fix deadlock when loading transaction buffer snapshot (#24401)
* [a2859bd7760](https://github.com/datastax/pulsar/commit/a2859bd7760) [fix] [broker] No longer allow creating subscription that contains slash (#23594)
* [cf0b0ee9250](https://github.com/datastax/pulsar/commit/cf0b0ee9250) [fix][ml]Revert a behavior change of releasing idle offloaded ledger handle: only release idle BlobStoreBackedReadHandle (#24384)
* [6034e76667a](https://github.com/datastax/pulsar/commit/6034e76667a) [improve][misc] Upgrade Netty to 4.1.122.Final and tcnative to 2.0.72.Final (#24397)
* [deee63e3a62](https://github.com/datastax/pulsar/commit/deee63e3a62) [improve][broker] Add managedCursor/LedgerInfoCompressionType settings to broker.conf (#24391)
* [ccd54371a2d](https://github.com/datastax/pulsar/commit/ccd54371a2d) [improve][broker] Make maxBatchDeletedIndexToPersist configurable and document other related configs (#24392)
* [7721c2c4895](https://github.com/datastax/pulsar/commit/7721c2c4895) [fix][client] Fix consumer not returning encrypted messages on decryption failure with compression enabled (#24356)
* [b682de9cbf4](https://github.com/datastax/pulsar/commit/b682de9cbf4) [improve][broker] Added synchronized for sendMessages in Non-Persistent message dispatchers (#24386)
* [93ee1375f25](https://github.com/datastax/pulsar/commit/93ee1375f25) [improve][ml]Release idle offloaded read handle only the ref count is 0 (#24381)
* [209aa342719](https://github.com/datastax/pulsar/commit/209aa342719) [fix][broker]Fix deadlock when compaction and topic deletion execute concurrently (#24366)
* [e1cfe3f564e](https://github.com/datastax/pulsar/commit/e1cfe3f564e) [fix][broker] expose consumer name for partitioned topic stats (#24360)
* [113f8bc8aa1](https://github.com/datastax/pulsar/commit/113f8bc8aa1) [fix][broker] Fix issue that topic policies was deleted after a sub topic deleted, even if the partitioned topic still exists (#24350)
* [89bdc3141c2](https://github.com/datastax/pulsar/commit/89bdc3141c2) [fix][io] Acknowledge RabbitMQ message after processing the message successfully (#24354)
* [7f638dfd6d3](https://github.com/datastax/pulsar/commit/7f638dfd6d3) [fix][broker] Ignore metadata changes when broker is not in the Started state (#24352)
* [ca1983c5963](https://github.com/datastax/pulsar/commit/ca1983c5963) [improve][broker] Enable concurrent processing of pending read Entries to avoid duplicate Reads (#24346)
* [f31ecb2f3c7](https://github.com/datastax/pulsar/commit/f31ecb2f3c7) [fix][broker] Resolve the issue of frequent updates in message expiration deletion rate (#24190)
* [9d895268cec](https://github.com/datastax/pulsar/commit/9d895268cec) [fix][ml] Fix ManagedCursorImpl.individualDeletedMessages concurrent issue (#24338)
* [f5a3b061d50](https://github.com/datastax/pulsar/commit/f5a3b061d50) [fix][offload] Complete the future outside of the reading loop in BlobStoreBackedReadHandleImplV2.readAsync (#24331)
* [199397c6133](https://github.com/datastax/pulsar/commit/199397c6133) [fix][cli] Fix pulsar-shell cannot produce message with quotes and space (#24320)
* [a986ffa9f73](https://github.com/datastax/pulsar/commit/a986ffa9f73) [fix][test] Fix flaky AutoScaledReceiverQueueSizeTest.testNegativeClientMemory (#24324)
* [3228d7a04ae](https://github.com/datastax/pulsar/commit/3228d7a04ae) [fix][io] Fix kinesis avro bytes handling (#24316)
* [27011a2025d](https://github.com/datastax/pulsar/commit/27011a2025d) [improve] Enable metrics for all broker caches (#24365)
* [22e01e20a1f](https://github.com/datastax/pulsar/commit/22e01e20a1f) [improve][broker]Improve the log when encountered in-flight read limitation (#24359)
* [bf2147f986e](https://github.com/datastax/pulsar/commit/bf2147f986e) [improve][ml] Offload ledgers without check ledger length (#24344)
* [270d3f79d32](https://github.com/datastax/pulsar/commit/270d3f79d32) [fix][broker]Non-global topic policies and global topic policies overwrite each other (#24286)
* [a5505806369](https://github.com/datastax/pulsar/commit/a5505806369) [fix][broker]Global topic policies do not affect after unloading topic and persistence global topic policies never affect (#24279)
* [b93e161cbfa](https://github.com/datastax/pulsar/commit/b93e161cbfa) [fix][test] Fix more resource leaks in tests (#24314)
* [aaaf6331ab8](https://github.com/datastax/pulsar/commit/aaaf6331ab8) [cleanup] Remove unused config `autoShrinkForConsumerPendingAcksMap` (#24315)
* [28767222d82](https://github.com/datastax/pulsar/commit/28767222d82) [fix][broker] Fix potential deadlock when creating partitioned topic (#24313)
* [d11278ab309](https://github.com/datastax/pulsar/commit/d11278ab309) [fix][broker] fix wrong method name checkTopicExists. (#24293)
* [a0078da9bb0](https://github.com/datastax/pulsar/commit/a0078da9bb0) [improve][cli] Make pulsar-perf termination more responsive by using Thread interrupt status (#24309)
* [415d847b190](https://github.com/datastax/pulsar/commit/415d847b190) [fix][build] Ensure that buildtools is Java 8 compatible and fix remaining compatibility issue (#24307)
* [2d44251df92](https://github.com/datastax/pulsar/commit/2d44251df92) [fix][test] Simplify BetweenTestClassesListenerAdapter and fix issue with BeforeTest/AfterTest annotations (#24304)
* [f38ba5b52cc](https://github.com/datastax/pulsar/commit/f38ba5b52cc) [improve][io] Add configuration parameter for disabling aggregation for Kinesis Producers (#24289)
* [21d727d42d0](https://github.com/datastax/pulsar/commit/21d727d42d0) [fix][broker]fix memory leak, messages lost, incorrect replication state if using multiple schema versions(auto_produce) (#24178)
* [ab628f8e246](https://github.com/datastax/pulsar/commit/ab628f8e246) Fix group id
* [cac0ce52edb](https://github.com/datastax/pulsar/commit/cac0ce52edb) [improve][ci] Add Netty leak detection reporting to Pulsar CI (#24272)
* [e5dbd040599](https://github.com/datastax/pulsar/commit/e5dbd040599) [improve] Upgrade pulsar-client-python to 3.7.0 in Docker image (#24302)
* [d4dea701cf9](https://github.com/datastax/pulsar/commit/d4dea701cf9) [fix][test] Fix more Netty ByteBuf leaks in tests (#24299)
* [b072ee8b3df](https://github.com/datastax/pulsar/commit/b072ee8b3df) [fix][io] Fix SyntaxWarning in Pulsar Python functions (#24297)
* [e891aef43d0](https://github.com/datastax/pulsar/commit/e891aef43d0) [fix][client] Fix producer publishing getting stuck after message with incompatible schema is discarded (#24282)
* [cbf4ea4da4f](https://github.com/datastax/pulsar/commit/cbf4ea4da4f) [cleanup][test] Remove unused parameter from deleteNamespaceWithRetry method in MockedPulsarServiceBaseTest (#24283)
* [5e27492079d](https://github.com/datastax/pulsar/commit/5e27492079d) [improve][build] Improve thread leak detector by ignoring "Attach Listener" thread (#24277)
* [9e6291291ce](https://github.com/datastax/pulsar/commit/9e6291291ce) [improve][build] Upgrade zstd version from 1.5.2-3 to 1.5.7-3 (#24263)
* [a387d17e02f](https://github.com/datastax/pulsar/commit/a387d17e02f) [fix][test] Fix multiple ByteBuf leaks in tests (#24281)
* [3918efa2a80](https://github.com/datastax/pulsar/commit/3918efa2a80) [improve][build] Suppress JVM class sharing warning when running tests (#24278)
* [40e637227e5](https://github.com/datastax/pulsar/commit/40e637227e5) [fix][broker] Fix HashedWheelTimer leak in PulsarService by stopping it in shutdown (#24275)
* [d1afaeac83f](https://github.com/datastax/pulsar/commit/d1afaeac83f) [fix][misc] Fix ByteBuf leak in SchemaUtils (#24274)
* [90f6c63b609](https://github.com/datastax/pulsar/commit/90f6c63b609) [fix][misc] Fix ByteBuf leaks in tests by making ByteBufPair.coalesce release the input ByteBufPair (#24273)
* [f6e9710d53c](https://github.com/datastax/pulsar/commit/f6e9710d53c) [improve][build] Upgrade commons-compress version from 1.27.0 to 1.27.1 (#24270)
* [1b7932c5e21](https://github.com/datastax/pulsar/commit/1b7932c5e21) [improve][build] Allow building and running tests on JDK 24 and upcoming JDK 25 LTS (#24268)
* [0f8c0061bd0](https://github.com/datastax/pulsar/commit/0f8c0061bd0) [fix][broker]Fix incorrect priority between topic policies and global topic policies (#24254)
* [c3747d69870](https://github.com/datastax/pulsar/commit/c3747d69870) [improve][ci] Disable detailed console logging for integration tests in CI (#24266)
* [3ab114985c9](https://github.com/datastax/pulsar/commit/3ab114985c9) [improve][build] Upgrade Mockito to 5.17.0 and byte-buddy to 1.15.11 (#24241)
* [a4c8e21da37](https://github.com/datastax/pulsar/commit/a4c8e21da37) [fix][test] Fix flaky ManagedCursorTest.testLastActiveAfterResetCursor and disable failing SchemaTest (#24261)
* [f55a2f4cdb9](https://github.com/datastax/pulsar/commit/f55a2f4cdb9) [fix][test] Fix flaky ManagedCursorTest.testSkipEntriesWithIndividualDeletedMessages (#24244)
* [85abaf7f451](https://github.com/datastax/pulsar/commit/85abaf7f451) [improve][io][kca] support fully-qualified topic names in source records (#24248)
* [610297e8422](https://github.com/datastax/pulsar/commit/610297e8422) [improve][build] Upgrade Gradle Develocity Maven Extension dependencies (#24260)
* [645d5f92d93](https://github.com/datastax/pulsar/commit/645d5f92d93) [fix][test] Fix TestNG BetweenTestClassesListenerAdapter listener (#24258)
* [0f510acfe73](https://github.com/datastax/pulsar/commit/0f510acfe73) [fix][broker] Unregister non-static metrics collectors registered in Prometheus default registry (#24257)
* [bd8b19f4225](https://github.com/datastax/pulsar/commit/bd8b19f4225) [cleanup] Remove unused static fields in BrokerService (#24251)
* [71ddb2cb79d](https://github.com/datastax/pulsar/commit/71ddb2cb79d) [cleanup] remove unused config messagePublishBufferCheckIntervalInMillis (#24252)
* [a10c4e0b466](https://github.com/datastax/pulsar/commit/a10c4e0b466) [fix] chore: remove unused preciseTopicPublishRateLimiterEnable (#24249)
* [3661572026c](https://github.com/datastax/pulsar/commit/3661572026c) [fix][build] Fix errorprone maven profile configuration (#24246)
* [e83da306e92](https://github.com/datastax/pulsar/commit/e83da306e92) [improve][build] Upgrade SpotBugs to 4.9.x (#24243)
* [9b8b9c90b41](https://github.com/datastax/pulsar/commit/9b8b9c90b41) [improve][misc] Migrate from multiple nullness annotation libraries to JSpecify annotations (#24239)
* [0b3cb4b37af](https://github.com/datastax/pulsar/commit/0b3cb4b37af) [improve][build] Upgrade to jacoco 0.8.13 (#24240)
* [a6052e7d573](https://github.com/datastax/pulsar/commit/a6052e7d573) [improve] Adapt startup scripts for Java 24 changes (#24236)
* [089dbe52471](https://github.com/datastax/pulsar/commit/089dbe52471) [improve][build] Upgrade errorprone to 2.38.0 (#24242)
* [b739072e601](https://github.com/datastax/pulsar/commit/b739072e601) [improve][build] Upgrade Lombok to 1.18.38 to support JDK 24 (#24237)
* [3dbbbaddc73](https://github.com/datastax/pulsar/commit/3dbbbaddc73) [fix][test] Fix resource leaks in PulsarBrokerStarterTest (#24235)

### `lunastreaming-all` distribution

<details><summary>CLI extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-cdc](https://pulsar.apache.org/docs/io-connectors) | Cassandra CDC - Pulsar Admin Custom Commands | 2.3.1 | pulsar-cassandra-admin-2.3.1-nar.nar |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - Pulsar Admin Custom Commands | 6.0.6 | pulsar-jms-admin-6.0.6-nar.nar |
</details>

<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 6.0.6 | pulsar-jms-6.0.6-nar.nar |
</details>

<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 4.0.3.1 | pulsar-protocol-handler-kafka-4.0.3.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
</details>

<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 4.0.0.2 | starlight-rabbitmq-4.0.0.2.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 4.0.3.1 | pulsar-kafka-proxy-4.0.3.1.nar |

</details>

<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.14 | cassandra-enhanced-pulsar-sink-1.6.14-nar.nar |
| [cloud-storage](https://github.com/streamnative/pulsar-io-cloud-storage) | Writes data into cloud storage | 3.2.4 | pulsar-io-cloud-storage-3.2.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.3.4 | pulsar-io-data-generator-4.0.3.4.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 4.0.3.4 | pulsar-io-elastic-search-4.0.3.4.nar |
| [http](https://pulsar.apache.org/docs/io-connectors) | Writes data to an HTTP server (Webhook) | 4.0.3.4 | pulsar-io-http-4.0.3.4.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 4.0.3.4 | pulsar-io-jdbc-clickhouse-4.0.3.4.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 4.0.3.4 | pulsar-io-jdbc-mariadb-4.0.3.4.nar |
| [jdbc-openmldb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for OpenMLDB | 4.0.3.4 | pulsar-io-jdbc-openmldb-4.0.3.4.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 4.0.3.4 | pulsar-io-jdbc-postgres-4.0.3.4.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 4.0.3.4 | pulsar-io-jdbc-sqlite-4.0.3.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.3.4 | pulsar-io-kafka-4.0.3.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.3.4 | pulsar-io-kinesis-4.0.3.4.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.2.1 | pulsar-snowflake-connector-0.2.1.nar |
</details>

<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.3.1 | pulsar-cassandra-source-2.3.1.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 4.0.3.4 | pulsar-io-data-generator-4.0.3.4.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 4.0.3.4 | pulsar-io-debezium-mongodb-4.0.3.4.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 4.0.3.4 | pulsar-io-debezium-mssql-4.0.3.4.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 4.0.3.4 | pulsar-io-debezium-mysql-4.0.3.4.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 4.0.3.4 | pulsar-io-debezium-oracle-4.0.3.4.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 4.0.3.4 | pulsar-io-debezium-postgres-4.0.3.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 4.0.3.4 | pulsar-io-kafka-4.0.3.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 4.0.3.4 | pulsar-io-kinesis-4.0.3.4.nar |
| [lakehouse](https://pulsar.apache.org/docs/io-connectors) | Lakehouse connectors | 3.3.5.2 | pulsar-io-lakehouse-3.3.5.2-cloud.nar |
</details>

<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.2.1 | pulsar-ai-tools-3.2.1.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.2.1 | pulsar-transformations-3.2.1.nar |
</details>

## Environment (Connectors, Protocol Handlers, Proxy Extensions, extra libraries)
See the [environment variables](https://github.com/riptano/pulsar-distro/blob/ls40_3.4/build.json) used for the build

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