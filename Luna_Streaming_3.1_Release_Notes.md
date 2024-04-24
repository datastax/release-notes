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
| [ai-tools](https://pulsar.apache.org/docs/io-connectors) | Generative AI tools | 3.1.7 | pulsar-ai-tools-3.1.7.nar |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 3.1.1 | pulsar-transformations-3.1.1.nar |
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