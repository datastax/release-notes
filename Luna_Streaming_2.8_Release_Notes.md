# Release notes for DataStax Luna Streaming Distribution
 
## About DataStax Luna Streaming Distribution
Luna Streaming Distribution 2.8.0 is compatible with Apache Pulsar&trade; 2.8.0.

### Component versions for Luna Streaming Distribution 2.8.0

   * Apache Pulsar 2.8.0
   * DataStax Pulsar Admin Console 1.0.0
   * DataStax Pulsar Heartbeat 1.0.2
   * DataStax Apache Pulsar Cassandra Sink 1.5.0
   * DataStax Apache Pulsar Cassandra Source 1.0.2
   * DataStax Burnell 1.0.0
   * Datastax BookKeeper 4.14.3.1.0.0
 
This release adds these features to the original Apache Pulsar 2.8.0 release:
  
   * Stability improvements
   * Rootless Docker image
   * Third party library updates for security fixes
   * Docker images based on Ubuntu (instead of Debian based images in Pulsar 2.8.0, for security reasons)
   * Dependency upgrades (for security, stability, and performance)
   * An Enhanced ElasticSearch Pulsar IO Sink  
   * An Enhanced version of Apache BookKeeper 4.14.3 with security fixes
   * Pulsar IO source for Debezium Oracle
   * [Pulsar Proxy extensions](https://github.com/apache/pulsar/wiki/PIP-99%3A-Pulsar-Proxy-Extensions) feature 
 
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

### Source Code of Main Components

The source code for these versions of Apache Pulsar and Apache BookKeeper code is in
   
   * https://github.com/datastax/pulsar
   * https://github.com/datastax/bookkeeper

### Security
Luna Streaming is developed with great attention to security.

Since it is based on Apache Pulsar&trade;, Luna Streaming Pulsar distribution has all the security processes and requirements required by the Apache Software Foundation&trade;, such as:
* Peer to peer code reviews.
* Clear process for handling possible security vulnerabilities.

On top of that, Luna Streaming development processes are enhanced with additional security best practices for all the components involved:
* Robust Continuous Integration and reproducible Release pipeline in a secure monitored environment. Such monitoring improves the overall security of the application. 
* Reactivity to third-party vulnerabilities. Every component is scanned and monitored daily, ensuring quick fixes in case of vulnerability disclosure.
* Regular docker images vulnerability scans on latest Luna Streaming releases, with a well-defined release procedure.

At the time of the creation of the release, all the components included in the _[all](#packaging)_ packages are scanned by [Sonatype IQ Server service](https://help.sonatype.com/iqserver) and they don't have any critical (severity 8 or higher) security issues.

### Upgrade considerations for Luna Streaming Distribution 2.8.0

As with Luna Streaming 2.7, this release uses non-root containers for enhanced security. When upgrading from a previous version (for example, 2.6.2_1.0.1), files created while running that version will have root permissions and will not be readable by containers running the new version.

To fix this, manually log into the ZooKeeper, BookKeeper, and Function Worker containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs` directories are owned by UID 10000 (user pulsar). The group ID of the files should also be set to GID 10001 (group pulsar). Here is an example command:

```
chown -R 10000:10001 /pulsar/data
```

If you are using the Luna Streaming Helm chart, you can enable automatic repair of the permissions using the `fixRootlessPermissions` setting. For more details on this setting, go [here](https://github.com/datastax/pulsar-helm-chart).

### Upgrade considerations for custom Pulsar Functions and Pulsar IO Connectors

If you are upgrading from Apache Pulsar 2.7.0 or Luna Streaming 2.7.2 you may need to recompile your Pulsar Functions or Pulsar IO Connectors using Apache Pulsar 2.8.0 as a dependency in certain cases.
This is because there is a breaking API change in Apache Pulsar 2.8.0 (and therefore in Luna Streaming 2.8.0) related to the `SchemaInfo` java class.
More context [here](https://github.com/apache/pulsar/issues/11338).

### Packaging

Luna Streaming Distribution comes with different packages tooled for different purposes. 
The distributions are available as Docker images and tarballs, and both methods follow the same packaging patterns.

#### Patterns

* **lunastreaming**: the basic Luna Streaming Distribution **including Pulsar SQL** feature.
* **lunastreaming-core**: the basic Luna Streaming Distribution **without Pulsar SQL** feature. Pick this distribution if you don't need Pulsar SQL features.
* **lunastreaming-all**: contains the Core Luna Streaming Distribution, including **Pulsar Offloaders** and the **Datastax Pulsar IO Connectors** listed above. Pick this distribution if you want the Datastax connectors or the offloading feature.

# Releases

## Luna Streaming Distribution 2.8.0 1.1.37
This is a maintenance release containing important security and stability updates.
### Most notable commits
* [864f303400e](https://github.com/datastax/pulsar/commit/864f303400e) [cleanup][elasticsearch] improve the mapping between records and bulk requests (#67)
* [a949ef9ba0e](https://github.com/datastax/pulsar/commit/a949ef9ba0e) Ignore case when obfuscating passwords in python configuration scripts (#15077)
* [c4dc27e6b3d](https://github.com/datastax/pulsar/commit/c4dc27e6b3d) Sinks: allow to reset --timeout-ms to zero
* [bd36c6dd75b](https://github.com/datastax/pulsar/commit/bd36c6dd75b) [elasticsearch-sink] Fix memory leak while using OpenSearch High Level rest client
* [f208f9259c5](https://github.com/datastax/pulsar/commit/f208f9259c5) Improved logic for pausing replicated subscription snapshots when no traffic (#11922)
* [e59758b3465](https://github.com/datastax/pulsar/commit/e59758b3465) Fixes NPE - ``ReplicatedSubscriptionsController`` send marker message when enable deduplicated. (#14017)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.4.nar
* pulsar-io-data-generator-2.8.0.1.1.37.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.37.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.37.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.37.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.37.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.37.nar
* pulsar-io-elastic-search-2.8.0.1.1.37.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.37.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.37.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.37.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.37.nar
* pulsar-io-kafka-2.8.0.1.1.37.nar
* pulsar-io-kinesis-2.8.0.1.1.37.nar
* pulsar-snowflake-connector-0.1.9.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.18.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.18.nar
  
## Luna Streaming Distribution 2.8.0 1.1.35
This is a maintenance release containing important stability updates.
### Most notable commits
* [5e1e9e5cbfa](https://github.com/datastax/pulsar/commit/5e1e9e5cbfa) Add pulsar_subscription_consumers_count metric Fix #15032
* [121253a57e8](https://github.com/datastax/pulsar/commit/121253a57e8) [fix][elasticseach] ElasticSearch sink: client 'close' method is never called (#14995)
* [53a63afac1b](https://github.com/datastax/pulsar/commit/53a63afac1b) If mark-delete operation fails, mark the cursor as "dirty" (#14256)
* [397c9102221](https://github.com/datastax/pulsar/commit/397c9102221) [ML] Fix race condition in updating lastMarkDeleteEntry field (#15031)
* [cfe5790037b](https://github.com/datastax/pulsar/commit/cfe5790037b) KCA Sink to handle KeyValue<GenericRecord, GenericRecord>
* [652ea0f2afa](https://github.com/datastax/pulsar/commit/652ea0f2afa) Kinesis integration tests (#62)
* [a2e12a8eb93](https://github.com/datastax/pulsar/commit/a2e12a8eb93) Add FULL_MESSAGE_IN_JSON_EXPAND_VALUE message format to Kinesis sink (#52)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.4.nar
* pulsar-io-data-generator-2.8.0.1.1.35.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.35.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.35.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.35.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.35.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.35.nar
* pulsar-io-elastic-search-2.8.0.1.1.35.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.35.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.35.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.35.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.35.nar
* pulsar-io-kafka-2.8.0.1.1.35.nar
* pulsar-io-kinesis-2.8.0.1.1.35.nar
* pulsar-snowflake-connector-0.1.8.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.17.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.17.nar

## Luna Streaming Distribution 2.8.0 1.1.34
This is a maintenance release containing connector upgrades.
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.4.nar
* pulsar-io-data-generator-2.8.0.1.1.34.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.34.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.34.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.34.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.34.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.34.nar
* pulsar-io-elastic-search-2.8.0.1.1.34.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.34.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.34.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.34.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.34.nar
* pulsar-io-kafka-2.8.0.1.1.34.nar
* pulsar-io-kinesis-2.8.0.1.1.34.nar
* pulsar-snowflake-connector-0.1.8.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.17.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.17.nar
## Luna Streaming Distribution 2.8.0 1.1.33
This is a maintenance release containing important stability updates.
### Most notable commits
* [29a9bb5df44](https://github.com/datastax/pulsar/commit/29a9bb5df44) Include circe-checksum in pulsar-client dependency (#60)
* [0f2ea48d49b](https://github.com/datastax/pulsar/commit/0f2ea48d49b) handle whatever KeyValue getNativeObject() returns: org.apache.pulsar.io.core.KeyValue or org.apache.pulsar.common.schema.KeyValue (#61)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.4.nar
* pulsar-io-data-generator-2.8.0.1.1.33.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.33.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.33.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.33.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.33.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.33.nar
* pulsar-io-elastic-search-2.8.0.1.1.33.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.33.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.33.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.33.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.33.nar
* pulsar-io-kafka-2.8.0.1.1.33.nar
* pulsar-io-kinesis-2.8.0.1.1.33.nar
* pulsar-snowflake-connector-0.1.7.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.16.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.16.nar
* 
## Luna Streaming Distribution 2.8.0 1.1.32
This is a maintenance release containing important security updates.
### Most notable commits
* [eaadd8cd9ed](https://github.com/datastax/pulsar/commit/eaadd8cd9ed) [elasticsearch] Option to disable SSL certificate validation (#56)
* [d40f0b54f71](https://github.com/datastax/pulsar/commit/d40f0b54f71) handle null offsets from kafka connector (#53)
* [70f0fdddcbf](https://github.com/datastax/pulsar/commit/70f0fdddcbf) Clean up individually deleted messages before the mark-delete position (#14261)
* [2d1f85f1144](https://github.com/datastax/pulsar/commit/2d1f85f1144) Offloader: add API to scan objects on Tiered Storage: Move to JAX-RS StreamingOutput
* [5888bf5fbbb](https://github.com/datastax/pulsar/commit/5888bf5fbbb) [fix][kinesis] Remove internal dependency: pulsar-functions-instance (#14925)
* [154b4507cbc](https://github.com/datastax/pulsar/commit/154b4507cbc) Offloader: add API to scan objects on Tiered Storage
* [a8bdb63ff84](https://github.com/datastax/pulsar/commit/a8bdb63ff84) TieredStorage: add debug information (#14907)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.3.nar
* pulsar-io-data-generator-2.8.0.1.1.32.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.32.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.32.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.32.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.32.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.32.nar
* pulsar-io-elastic-search-2.8.0.1.1.32.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.32.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.32.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.32.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.32.nar
* pulsar-io-kafka-2.8.0.1.1.32.nar
* pulsar-io-kinesis-2.8.0.1.1.32.nar
* pulsar-snowflake-connector-0.1.7.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.16.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.16.nar

## Luna Streaming Distribution 2.8.0 1.1.31
This is a maintenance release containing important security updates.
### Most notable commits
* [a45886ccfc6](https://github.com/datastax/pulsar/commit/a45886ccfc6) ElasticSearch Sink: handle concurrent index creation requests (#51)
* [30048aa4b7c](https://github.com/datastax/pulsar/commit/30048aa4b7c) [fix][auth] Athenz: do not use uber-jar and bump to 1.10.50
* [b8133c23328](https://github.com/datastax/pulsar/commit/b8133c23328) [fix][security] Upgrade jackson and jackson-databind (2.13.2.1) to get rid of CVE-2020-36518
* [44d4e9cd445](https://github.com/datastax/pulsar/commit/44d4e9cd445) [security] Upgrade PostGre driver to 42.3.3 to get rid of CVE-2022-26520

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.3.nar
* pulsar-io-data-generator-2.8.0.1.1.31.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.31.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.31.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.31.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.31.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.31.nar
* pulsar-io-elastic-search-2.8.0.1.1.31.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.31.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.31.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.31.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.31.nar
* pulsar-io-kafka-2.8.0.1.1.31.nar
* pulsar-io-kinesis-2.8.0.1.1.31.nar
* pulsar-snowflake-connector-0.1.7.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.16.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.16.nar

## Luna Streaming Distribution 2.8.0 1.1.30
This is a maintenance release containing important stability updates.
### Most notable commits
* [cf13b39240b](https://github.com/datastax/pulsar/commit/cf13b39240b) [elasticsearch] support token based auth (#46)
* [1028aa78c09](https://github.com/datastax/pulsar/commit/1028aa78c09) Tiered Storage: add debug in case of missing blob (#47)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.0-nar.nar
* pulsar-cassandra-source-1.0.3.nar
* pulsar-io-data-generator-2.8.0.1.1.30.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.30.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.30.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.30.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.30.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.30.nar
* pulsar-io-elastic-search-2.8.0.1.1.30.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.30.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.30.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.30.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.30.nar
* pulsar-io-kafka-2.8.0.1.1.30.nar
* pulsar-io-kinesis-2.8.0.1.1.30.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.15.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.15.nar

## Luna Streaming Distribution 2.8.0 1.1.29
This is a maintenance release containing important stability updates.
### Most notable commits
* [a64222176e7](https://github.com/datastax/pulsar/commit/a64222176e7) [refactor][proxy] Refactor Proxy code and fix connection stalling by switching to auto read mode (#14713)
* [30783d0763d](https://github.com/datastax/pulsar/commit/30783d0763d) [Proxy] Log warning when opening connection to broker fails (#14710)
* [88023dbbd00](https://github.com/datastax/pulsar/commit/88023dbbd00) Handle kafka sinks that return immutable maps as configs (#14780)
* [6e964907c13](https://github.com/datastax/pulsar/commit/6e964907c13) Switch BlobStoreManagedLedgerOffloader to use removeBlob
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.0-nar.nar
* pulsar-cassandra-source-1.0.3.nar
* pulsar-io-data-generator-2.8.0.1.1.29.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.29.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.29.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.29.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.29.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.29.nar
* pulsar-io-elastic-search-2.8.0.1.1.29.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.29.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.29.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.29.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.29.nar
* pulsar-io-kafka-2.8.0.1.1.29.nar
* pulsar-io-kinesis-2.8.0.1.1.29.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.15.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.15.nar

## Luna Streaming Distribution 2.8.0 1.1.28
This is a maintenance release containing important stability updates about Pulsar IO Kinesis Sink connector.
### Most notable commits
* [5b3337d56b4](https://github.com/datastax/pulsar/commit/5b3337d56b4) Drop provided scope for the pulsar-functions-instance in kinesis sink (#41)
* [f5f4e41de96](https://github.com/datastax/pulsar/commit/f5f4e41de96) fix kinesis connector's dependency issue (#12246) (#40)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.0-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.28.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.28.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.28.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.28.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.28.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.28.nar
* pulsar-io-elastic-search-2.8.0.1.1.28.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.28.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.28.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.28.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.28.nar
* pulsar-io-kafka-2.8.0.1.1.28.nar
* pulsar-io-kinesis-2.8.0.1.1.28.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.15.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.15.nar

## Luna Streaming Distribution 2.8.0 1.1.27
This is a maintenance release containing important security and stability updates.
### Most notable commits
* [87a2908a02b](https://github.com/datastax/pulsar/commit/87a2908a02b) Fix Consumer listener does not respect receiver queue size (#11455)
* [d522f6dfac9](https://github.com/datastax/pulsar/commit/d522f6dfac9) Fail proxy startup if brokerServiceURL is missing scheme (#14682)
* [d781147616f](https://github.com/datastax/pulsar/commit/d781147616f) [pulsar-io] Elasticsearch sink support for Elastic 8 - switch to java-client (#35)
* [f57bf7e0c62](https://github.com/datastax/pulsar/commit/f57bf7e0c62) Add support of PrometheusRawMetricsProvider for the Pulsar-Proxy
* [a576a1b99aa](https://github.com/datastax/pulsar/commit/a576a1b99aa) Revert OkHttp3 upgrade to 5.0.0.alpha - partial porting of #13065
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.0-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.27.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.27.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.27.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.27.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.27.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.27.nar
* pulsar-io-elastic-search-2.8.0.1.1.27.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.27.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.27.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.27.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.27.nar
* pulsar-io-kafka-2.8.0.1.1.27.nar
* pulsar-io-kinesis-2.8.0.1.1.27.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.14.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.14.nar

## Luna Streaming Distribution 2.8.0 1.1.26
This is a maintenance release containing important stability updates.
### Most notable commits
* [d8573a4d0b1](https://github.com/datastax/pulsar/commit/d8573a4d0b1) Set the ignoreUnsupportedFields default to false
* [f8fb25ed9e2](https://github.com/datastax/pulsar/commit/f8fb25ed9e2) Remove support for CQL logical types
* [148a0c60781](https://github.com/datastax/pulsar/commit/148a0c60781) [Branch-2.8] Fix Broker HealthCheck Endpoint Exposes Race Conditions. (#14618)
* [0e98fbde3bd](https://github.com/datastax/pulsar/commit/0e98fbde3bd) Added Debezium Source for MS SQL Server (#12256)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.0-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.26.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.26.nar
* pulsar-io-debezium-mssql-2.8.0.1.1.26.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.26.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.26.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.26.nar
* pulsar-io-elastic-search-2.8.0.1.1.26.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.26.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.26.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.26.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.26.nar
* pulsar-io-kafka-2.8.0.1.1.26.nar
* pulsar-io-kinesis-2.8.0.1.1.26.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.14.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.14.nar
## Luna Streaming Distribution 2.8.0 1.1.25
This is a maintenance release containing important stability improvements.
### Most notable commits

* [89840426590](https://github.com/datastax/pulsar/commit/89840426590) Allow Pulsar Functions localrun to exit on error (#12278)
* [a89af949f43](https://github.com/datastax/pulsar/commit/a89af949f43) Allow Pulsar Functions / Sinks to pool messages (#11618)
* [9b23e26eba5](https://github.com/datastax/pulsar/commit/9b23e26eba5) Fix: Cast exception occurs if function/source/sink type is ByteBuffer (#11611)
* [24d7f357ba2](https://github.com/datastax/pulsar/commit/24d7f357ba2) KCA: Option to sanitize topic name for the conenctors that cannot handle pulsar topic names
* [190e6504ad6](https://github.com/datastax/pulsar/commit/190e6504ad6) [Transaction] Fix topicTransactionBuffer handle null snapshot (#12758)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.0-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.25.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.25.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.25.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.25.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.25.nar
* pulsar-io-elastic-search-2.8.0.1.1.25.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.25.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.25.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.25.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.25.nar
* pulsar-io-kafka-2.8.0.1.1.25.nar
* pulsar-io-kinesis-2.8.0.1.1.25.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.12.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.12.nar

## Luna Streaming Distribution 2.8.0 1.1.24
This is a maintenance release containing important security updates.
### Most notable commits
* [635f5691a4e](https://github.com/datastax/pulsar/commit/635f5691a4e) Upgrade BK to 4.14.4 and Grpc to 1.42.1 (#13714)
* [7953fed9ec1](https://github.com/datastax/pulsar/commit/7953fed9ec1) Remove --illegal-access errors resulting from Google Guice - Pulsar IO, Offloaders and Pulsar SQL - Bump Guice to 5.1.0 (#14300)
* [0b6667bd91c](https://github.com/datastax/pulsar/commit/0b6667bd91c) Fix NoClassDefFoundError: com/google/inject/AbstractModule in pulsar-io/batch-data-generator and Jcloud offloader (#14150)
* [cb37e2073be](https://github.com/datastax/pulsar/commit/cb37e2073be) Remove --illegal-access errors resulting from Google Guice (upgrade to 5.0.1) (#13810)
* [9a098e2f17b](https://github.com/datastax/pulsar/commit/9a098e2f17b) KCA: Option to sanitize topic name for the conenctors that cannot handle pulsar topic names (#14475)
* [dbc7dab8b01](https://github.com/datastax/pulsar/commit/dbc7dab8b01) [tools] Pulsar Client: add ability to produce KV messages (#11303)
* [c56000e3cd2](https://github.com/datastax/pulsar/commit/c56000e3cd2) [Issue 11067][pulsar-client] Fix bin/pulsar-client produce not supporting v2 topic name through websocket (#11069)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.5.0-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.24.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.24.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.24.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.24.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.24.nar
* pulsar-io-elastic-search-2.8.0.1.1.24.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.24.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.24.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.24.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.24.nar
* pulsar-io-kafka-2.8.0.1.1.24.nar
* pulsar-io-kinesis-2.8.0.1.1.24.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.11.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.11.nar

## Luna Streaming Distribution 2.8.0 1.1.23
This is a maintenance release containing important security updates and the upgrade of DataStax Apache Pulsar Cassandra Sink.
### Most notable commits
* [57aded2d6fc](https://github.com/datastax/pulsar/commit/57aded2d6fc) Bump netty version to 4.1.74.Final (#14257)
* [c8b1e6ff4a7](https://github.com/datastax/pulsar/commit/c8b1e6ff4a7) Include correct bookkeeper jars in pulsar-client jar (#16)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.5.0-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.23.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.23.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.23.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.23.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.23.nar
* pulsar-io-elastic-search-2.8.0.1.1.23.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.23.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.23.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.23.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.23.nar
* pulsar-io-kafka-2.8.0.1.1.23.nar
* pulsar-io-kinesis-2.8.0.1.1.23.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.9.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.9.nar
## Luna Streaming Distribution 2.8.0 1.1.22
This is a maintenance release containing important security updates.
### Most notable commits

* [ddb237e9464](https://github.com/datastax/pulsar/commit/ddb237e9464) [pulsar-broker] The log prints NamespaceService#isServiceUnitActive exception stack information (#13553)
* [b1a25f5dc8a](https://github.com/datastax/pulsar/commit/b1a25f5dc8a) Upgrade JDK version for docker images: 11.0.14_9-jdk
* [5741f79c2b9](https://github.com/datastax/pulsar/commit/5741f79c2b9) [Proxy] Fix port exhaustion and connection issues in Pulsar Proxy (#14078)
* [7f5a47bc650](https://github.com/datastax/pulsar/commit/7f5a47bc650) Allow config of IO and acceptor threads in proxy (#14054)
* [3a02e0a0bf2](https://github.com/datastax/pulsar/commit/3a02e0a0bf2) [Proxy] Remove unnecessary Pulsar Client usage from Pulsar Proxy (#13836)
* [820b06913e9](https://github.com/datastax/pulsar/commit/820b06913e9) fix npe when unloading persistent partitioned topic (#11310)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.22.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.22.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.22.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.22.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.22.nar
* pulsar-io-elastic-search-2.8.0.1.1.22.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.22.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.22.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.22.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.22.nar
* pulsar-io-kafka-2.8.0.1.1.22.nar
* pulsar-io-kinesis-2.8.0.1.1.22.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.9.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.9.nar

## Luna Streaming Distribution 2.8.0 1.1.21
This is a maintenance release containing bugfixes.
### Most notable commits

* [d5ce3a0](https://github.com/datastax/pulsar/commit/d5ce3a0) AbstractMetadataStore: invalidate childrenCache correctly when node created
* [60d462a](https://github.com/datastax/pulsar/commit/60d462a) Close the replicator and replication client when delete cluster. (#11342)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.21.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.21.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.21.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.21.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.21.nar
* pulsar-io-elastic-search-2.8.0.1.1.21.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.21.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.21.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.21.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.21.nar
* pulsar-io-kafka-2.8.0.1.1.21.nar
* pulsar-io-kinesis-2.8.0.1.1.21.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.8.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.8.nar
## Luna Streaming Distribution 2.8.0 1.1.20
This is a maintenance release containing important security updates.
### Most notable commits

* [ef4917c](https://github.com/datastax/pulsar/commit/ef4917c) [security] Upgrade Postgre driver to 42.2.25 to get rid of CVE-2022-21724 (#14119)
* [6281523](https://github.com/datastax/pulsar/commit/6281523) fix shedding heartbeat ns (#13208)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.20.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.20.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.20.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.20.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.20.nar
* pulsar-io-elastic-search-2.8.0.1.1.20.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.20.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.20.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.20.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.20.nar
* pulsar-io-kafka-2.8.0.1.1.20.nar
* pulsar-io-kinesis-2.8.0.1.1.20.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.8.nar
* starlight-rabbitmq-2.8.0.1.1.19-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.8.nar
## Luna Streaming Distribution 2.8.0 1.1.19
This is a maintenance release containing bufixes about KEY_SHARED subscriptions and enhancements for Pulsar IO ElasticSearch Sink connector.
### Most notable commits

* [65269e1](https://github.com/datastax/pulsar/commit/65269e1) add non-bulk index/delete with retry (#23)
* [ad512d6](https://github.com/datastax/pulsar/commit/ad512d6) Fix the default maxRetries=-1 (#22)
* [df59224](https://github.com/datastax/pulsar/commit/df59224) Prevent StackOverFlowException in KEY_SHARED subscription
* [a0354a7](https://github.com/datastax/pulsar/commit/a0354a7) Fix Issue #12885, Unordered consuming case in Key_Shared subscription (#12890)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.19.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.19.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.19.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.19.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.19.nar
* pulsar-io-elastic-search-2.8.0.1.1.19.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.19.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.19.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.19.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.19.nar
* pulsar-io-kafka-2.8.0.1.1.19.nar
* pulsar-io-kinesis-2.8.0.1.1.19.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.7.nar
* starlight-rabbitmq-1.1.3.nar
* pulsar-kafka-proxy-2.8.0.1.0.7.nar
## Luna Streaming Distribution 2.8.0 1.1.18
This is a maintenance release containing bugfixes and a new option in the ElasticSearch Sink connector.

### Most notable commits

* [04a21fc](https://github.com/datastax/pulsar/commit/04a21fc) Add a copyPkFields option to the ES sink (#20)
* [f888127](https://github.com/datastax/pulsar/commit/f888127) Fix returned wrong hash ranges for the consumer with same consumer name (#12212)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.18.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.18.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.18.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.18.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.18.nar
* pulsar-io-elastic-search-2.8.0.1.1.18.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.18.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.18.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.18.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.18.nar
* pulsar-io-kafka-2.8.0.1.1.18.nar
* pulsar-io-kinesis-2.8.0.1.1.18.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.7.nar
* starlight-rabbitmq-1.1.3.nar
* pulsar-kafka-proxy-2.8.0.1.0.7.nar
## Luna Streaming Distribution 2.8.0 1.1.17
This is a maintenance release containing important security updates.

### Most notable commits

* [f98b69b](https://github.com/datastax/pulsar/commit/f98b69b) Pulsar IO: implement --retain-key-ordering (KEY_SHARED subscription) for Sinks
* [532cd29](https://github.com/datastax/pulsar/commit/532cd29) kubernetesRuntime read metricsPort from kuberbetesRuntimeFactoryConfig

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.17.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.17.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.17.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.17.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.17.nar
* pulsar-io-elastic-search-2.8.0.1.1.17.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.17.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.17.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.17.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.17.nar
* pulsar-io-kafka-2.8.0.1.1.17.nar
* pulsar-io-kinesis-2.8.0.1.1.17.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.7.nar
* starlight-rabbitmq-1.1.3.nar
* pulsar-kafka-proxy-2.8.0.1.0.7.nar

## Luna Streaming Distribution 2.8.0 1.1.16
This is a maintenance release containing important security updates.

### Most notable commits

* [0930e73](https://github.com/datastax/pulsar/commit/0930e73) KeyShared stickyHashRange subscription: prevent message loss in case of consumer restart
* [879c7ed](https://github.com/datastax/pulsar/commit/879c7ed) Upgrade Netty to 4.1.73.Final (#13981)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.16.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.16.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.16.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.16.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.16.nar
* pulsar-io-elastic-search-2.8.0.1.1.16.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.16.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.16.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.16.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.16.nar
* pulsar-io-kafka-2.8.0.1.1.16.nar
* pulsar-io-kinesis-2.8.0.1.1.16.nar
* pulsar-snowflake-connector-0.1.6.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.7.nar
* starlight-rabbitmq-1.1.3.nar
* pulsar-kafka-proxy-2.8.0.1.0.7.nar
## Luna Streaming Distribution 2.8.0 1.1.15
This is a maintenance release containing important security updates.

### Most notable commits

* [5ea85a6](https://github.com/datastax/pulsar/commit/5ea85a6) [Issue #11351] Parallel Precise Publish Rate Limiting Fix (#11372)
* [0f08269](https://github.com/datastax/pulsar/commit/0f08269) [issue #13351] Solving precise rate limiting does not takes effect (#11446)
* [b197b98](https://github.com/datastax/pulsar/commit/b197b98) [configuration]exposeBunlesMetricsInPrometheus (#13460)
* [e6a8f04](https://github.com/datastax/pulsar/commit/e6a8f04) Fix MsgDropRate missing from NonPersistentTopics stats output. (#11119)
* [bba4cff](https://github.com/datastax/pulsar/commit/bba4cff) Non-persistent topic subscription metrics #13827
* [1bafbfa](https://github.com/datastax/pulsar/commit/1bafbfa) Fix bundle metrics would overwrite loadbalance metrics (#13641)
* [3bb075e](https://github.com/datastax/pulsar/commit/3bb075e) Expose broker bundles  metrics to prometheus (#12366)
* [2dd8093](https://github.com/datastax/pulsar/commit/2dd8093) [Metrics] Add support for splitting topic and partition label in Prometheus (#12225)
* [4cda985](https://github.com/datastax/pulsar/commit/4cda985) Expose compaction metrics to Prometheus (#11739)
* [54b6760](https://github.com/datastax/pulsar/commit/54b6760) Add compacted topic metrics for TopicStats in CLI (#11564)
* [4384fdc](https://github.com/datastax/pulsar/commit/4384fdc) Add offload ledger info for admin topics stats (#11465)
* [46707b2](https://github.com/datastax/pulsar/commit/46707b2) Add metrics [AddEntryWithReplicasBytesRate] for namespace (#11472)
* [53ff8d3](https://github.com/datastax/pulsar/commit/53ff8d3) Add metrics storageLogicalSize for the TopicStats and NamespaceStats (#11430)
* [a00650f](https://github.com/datastax/pulsar/commit/a00650f) Fix missing replicator metrics (#11264)
* [b034f5a](https://github.com/datastax/pulsar/commit/b034f5a) [security] pulsar-io-kafka: upgrade jakarta.el to 3.0.4 to get rid of CVE-2021-28170 #13943
* [249ef3f](https://github.com/datastax/pulsar/commit/249ef3f) [Broker] Fix set-publish-rate when using preciseTopicPublishRateLimiterEnable=true (#10384)
* [91e0710](https://github.com/datastax/pulsar/commit/91e0710) Upgrade JDK version for docker images: adoptopenjdk:11-jdk (11.0.9) to eclipse-temurin:11.0.13
* [df17d07](https://github.com/datastax/pulsar/commit/df17d07) [security] pulsar-io-kafka: upgrade jersey-bean-validation to get rid CVE-2017-7536 (brought in by Hibernate Validator 5.x) (#13868)
* [72e8ede](https://github.com/datastax/pulsar/commit/72e8ede) [security] remove Jackson ASL from kafka-connect-avro-converter-shaded (#13894)
* [f07f91a](https://github.com/datastax/pulsar/commit/f07f91a) Fixed internal topic effect by InactiveTopicPolicy. (#13816)
* [aa6b9ae](https://github.com/datastax/pulsar/commit/aa6b9ae) [Security] Use dependencyManagement to enforce snakeyaml version to 1.30 (#13722)
* [48311ed](https://github.com/datastax/pulsar/commit/48311ed) Updating dependencies (guava and what brought in older guava) to get rid of the guava-related CVE-2018-10237 and CVE-2020-8908 (#13716)
* [6deb24c](https://github.com/datastax/pulsar/commit/6deb24c) Upgraded ElasticSearch to get rid of CVEs (and switched client to OpenSearch one) (#13867)
* [7eadbe1](https://github.com/datastax/pulsar/commit/7eadbe1) Getting rid of CVEs in batch-data-generator (#13820)
* [4c25e83](https://github.com/datastax/pulsar/commit/4c25e83) Fix the deadlock while using zookeeper thread to create ledger (#13744)
* [01bc5d6](https://github.com/datastax/pulsar/commit/01bc5d6) Use numeric uid in Dockerfile's USER to overcome issue with runAsNonRoot
* [1b2b0e2](https://github.com/datastax/pulsar/commit/1b2b0e2) [security] Offloaders - get rid of several CVEs (Log4J included) (#13746)
* [af63541](https://github.com/datastax/pulsar/commit/af63541) Fixed NPE in ProxyConnection with no auth data (#12111)
* [01a3747](https://github.com/datastax/pulsar/commit/01a3747) Fixed ProxyConnection to check for existence of auth_data field (#12057)
* [c4782ff](https://github.com/datastax/pulsar/commit/c4782ff) Updating dependencies to get rid of CVEs brought in with kafka and log4j-1.2 libs (#13726)
* [936a4c8](https://github.com/datastax/pulsar/commit/936a4c8) Updated dependencies to get rid of pulsar-io/jdbc related CVE-2020-13692 (#13753)
* [672c06e](https://github.com/datastax/pulsar/commit/672c06e) Remove kafka-connect-adaptor from the lunastreaming-all distribution

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.1-nar.nar
* pulsar-cassandra-source-1.0.2.nar
* pulsar-io-data-generator-2.8.0.1.1.15.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.15.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.15.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.15.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.15.nar
* pulsar-io-elastic-search-2.8.0.1.1.15.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.15.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.15.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.15.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.15.nar
* pulsar-io-kafka-2.8.0.1.1.15.nar
* pulsar-io-kinesis-2.8.0.1.1.15.nar
* pulsar-snowflake-connector-0.1.6.nar
* starlight-rabbitmq-1.1.3.nar

## Luna Streaming Distribution 2.8.0 1.1.14
This is a maintenance release containing important security updates

### Most notable commits

* [b08c70e](https://github.com/datastax/pulsar/commit/b08c70e) Release 2.8.0.1.1.14
* [2e16dc2](https://github.com/datastax/pulsar/commit/2e16dc2) [Issue 13651][elastic-search] Fix Elasticsearch Sink Invalid type for uuid encoded as logical types #13652
* [d0aa3b4](https://github.com/datastax/pulsar/commit/d0aa3b4) [Security] Upgrade protobuf to 3.16.1 to address CVE-2021-22569 (#13695)
* [b3ec494](https://github.com/datastax/pulsar/commit/b3ec494) Start release 2.8.0.1.1.14-SNAPSHOT

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.4.0.nar
* pulsar-cassandra-source-1.0.1.nar
* pulsar-io-data-generator-2.8.0.1.1.14.nar
* pulsar-io-debezium-mongodb-2.8.0.1.1.14.nar
* pulsar-io-debezium-mysql-2.8.0.1.1.14.nar
* pulsar-io-debezium-oracle-2.8.0.1.1.14.nar
* pulsar-io-debezium-postgres-2.8.0.1.1.14.nar
* pulsar-io-elastic-search-2.8.0.1.1.14.nar
* pulsar-io-jdbc-clickhouse-2.8.0.1.1.14.nar
* pulsar-io-jdbc-mariadb-2.8.0.1.1.14.nar
* pulsar-io-jdbc-postgres-2.8.0.1.1.14.nar
* pulsar-io-jdbc-sqlite-2.8.0.1.1.14.nar
* pulsar-io-kafka-2.8.0.1.1.14.nar
* pulsar-io-kafka-connect-adaptor-nar-2.8.0.1.1.14.nar
* pulsar-io-kinesis-2.8.0.1.1.14.nar

## Luna Streaming Distribution 2.8.0 1.1.13

This is a maintenance release containing important security updates and bugfixes.

List of most notable commits:

* [56f27618161](https://github.com/datastax/pulsar/commit/56f27618161) [Security] Upgrade Jackson to 2.12.6 (#13694)
* [3db758c145c](https://github.com/datastax/pulsar/commit/3db758c145c) Upgrade Gson version 2.8.6 to 2.8.9 (#13610)
* [33313b3e341](https://github.com/datastax/pulsar/commit/33313b3e341) Fix issues 11964, deadlock bug when use key_shared mode (#11965)

## Luna Streaming Distribution 2.8.0 1.1.12

This is a maintenance release containing important security updates and bugfixes.

List of most notable commits:

* [e9243a1e2fc](https://github.com/datastax/pulsar/commit/e9243a1e2fc) [Security] Upgrade Log4j to 2.17.1 (#13552)
* [3a216c50723](https://github.com/datastax/pulsar/commit/3a216c50723) [testing] Make python3 the default python in java-test-image (#12130)
* [1969a267907](https://github.com/datastax/pulsar/commit/1969a267907) [Broker] Fix race conditions in closing producers and consumers (#13428)
* [a11da0ff73d](https://github.com/datastax/pulsar/commit/a11da0ff73d) [Broker] Fix race condition in stopping replicator while it is starting
* [85ddf126825](https://github.com/datastax/pulsar/commit/85ddf126825) [pulsar-broker] Add stop replicator producer logic when start replicator cluster failed. (#12724)


## Luna Streaming Distribution 2.8.0 1.1.11

This is a maintenance release containing important security updates.

List of most notable commits:

* [5f8dd840a22](https://github.com/datastax/pulsar/commit/5f8dd840a22) [Security] Upgrade to Log4J 2.17.0 to mitigate CVE-2021-45105
* [0c2eaa2694f](https://github.com/datastax/pulsar/commit/0c2eaa2694f) [Client]Allow to override PULSAR_MEM settings via PULSAR_EXTRA_OPS #13381
* [aed7cb10171](https://github.com/datastax/pulsar/commit/aed7cb10171) Function: add possibility to pass additional JVM arguments to the function JVM (additionalJavaRuntimeArguments) (#13282)
* [0a00ae08360](https://github.com/datastax/pulsar/commit/0a00ae08360) [security] Upgrade Netty to 4.1.72 - CVE-2021-43797 (#13328)

## Luna Streaming Distribution 2.8.0 1.1.10

This release contains several bugfixes and important security updates.

List of most notable commits:

* [3f0a7e255ed](https://github.com/datastax/pulsar/commit/3f0a7e255ed) Option to not upload builtin connectors to BK for k8s runtime (#12947)
* [e0dd6b3d81e](https://github.com/datastax/pulsar/commit/e0dd6b3d81e) Bump log4j to 2.16.0 (#13277)
* [acd92023248](https://github.com/datastax/pulsar/commit/acd92023248) [Broker] Synchronize updates to the inactiveProducers map in MessageDeduplication (#12820)
* [2f9e3d7a064](https://github.com/datastax/pulsar/commit/2f9e3d7a064) [Broker] Fix messageDedup delete inactive producer name (#12493)
* [7cc63d72acb](https://github.com/datastax/pulsar/commit/7cc63d72acb) [Java Client] Fix producer data race to get cnx (#13176)
* [1f43bcce078](https://github.com/datastax/pulsar/commit/1f43bcce078) Revert "Set default root log level to debug" and make PULSAR_LOG_ROOT_LEVEL to default to PULSAR_LOG_LEVEL (#12941)
* [fd502df4f20](https://github.com/datastax/pulsar/commit/fd502df4f20) [Perf] Evaluate the current protocol version once (#13045)
* [d6eb15eb436](https://github.com/datastax/pulsar/commit/d6eb15eb436) Catch exceptions in scheduled tasks to prevent unintended cancellation (#12853)

DataStax Apache Pulsar Cassandra Source has been upgraded to 1.0.1

## Luna Streaming Distribution 2.8.0 1.1.9

This release contains several bugfixes and important security updates.

List of most notable commits:

* [a4764ff84c1](https://github.com/datastax/pulsar/commit/a4764ff84c1) Bump log4j to 2.15.0 (#13226)
* [21a5c51e9ce](https://github.com/datastax/pulsar/commit/21a5c51e9ce) [Java Client] Send CloseProducer on timeout (#13161)
* [8f6691c31cd](https://github.com/datastax/pulsar/commit/8f6691c31cd) Fix namespace policy override ignored when creating subscription (#12699)
* [4f4072b5490](https://github.com/datastax/pulsar/commit/4f4072b5490) Cancel scheduled tasks when deleting ManagedLedgerImpl (#12565)

## Luna Streaming Distribution 2.8.0 1.1.8

This release contains several bugfixes and improvements, most notably:
* Several fixes to ensure correct message ordering processing
* Improvements on Topic ownership load balancing

List of most notable commits:

* [54e3539a53b](https://github.com/datastax/pulsar/commit/54e3539a53b) [Java Client] Use epoch to version producer's cnx to prevent early de… (#12779)
* [6b7ab4e7180](https://github.com/datastax/pulsar/commit/6b7ab4e7180) [Java Client] Improve state changes to Connecting
* [56078dfb3f1](https://github.com/datastax/pulsar/commit/56078dfb3f1) [Java Client] Remove invalid call to Thread.currentThread().interrupt(); (#12652)
* [4c96cb521b7](https://github.com/datastax/pulsar/commit/4c96cb521b7) Remove the uncorrect VisableTesting annotation in pulsar-client (#11784)
* [848ce2a31bb](https://github.com/datastax/pulsar/commit/848ce2a31bb) Cleanup already deleted namespace topics. (#12597)
* [7a3daaebee0](https://github.com/datastax/pulsar/commit/7a3daaebee0) Do not reuse the Failed OpAddEntry object. (#12993)
* [04f640d7734](https://github.com/datastax/pulsar/commit/04f640d7734) [Issue 12723] Fix race condition in PersistentTopic#addReplicationCluster (#12729)
* [6536bbc1713](https://github.com/datastax/pulsar/commit/6536bbc1713) revert the wrong modification in org.apache.pulsar.broker.namespace.OwnershipCache#checkOwnership (#12650)
* [8fe8c3f2794](https://github.com/datastax/pulsar/commit/8fe8c3f2794) The count of topics on the bundle is less than 2，skip split (#12527)
* [84d0b48a3d2](https://github.com/datastax/pulsar/commit/84d0b48a3d2) Upgrade debezium to 1.7.1 (#12644)
* [2276fc57519](https://github.com/datastax/pulsar/commit/2276fc57519) k8s runtime: force deletion to avoid hung function worker during connector restart (#12504)
* [3cd4d5f6546](https://github.com/datastax/pulsar/commit/3cd4d5f6546) [pulsar-broker] handle NPE when check active consumer in stats (#12214)
* [66f587f9bc9](https://github.com/datastax/pulsar/commit/66f587f9bc9) Functions: add -Dio.netty.tryReflectionSetAccessible=true to Java functions (#12624)
* [7474bbf7e4b](https://github.com/datastax/pulsar/commit/7474bbf7e4b) [pulsar-perf] Write histogram files for consume command (#12569)
* [9464408ac92](https://github.com/datastax/pulsar/commit/9464408ac92) Fix retention size policy delete too much ledgers (#11242)
* [7c9e4474c2b](https://github.com/datastax/pulsar/commit/7c9e4474c2b) suppress nashorn warning in JDK11 runtime
* [00e9eada3c3](https://github.com/datastax/pulsar/commit/00e9eada3c3) [Functions] Fix classloader leaks (#12973)
* [bb5bab54ae9](https://github.com/datastax/pulsar/commit/bb5bab54ae9) [Broker] Fix and improve topic ownership assignment (#13069)(#13117)
* [370b148df85](https://github.com/datastax/pulsar/commit/370b148df85) [Broker] Fix LeaderElectionService.getCurrentLeader and add support for empheralOwner in MockZooKeeper (#13066)
* [0a11d49287a](https://github.com/datastax/pulsar/commit/0a11d49287a) Remove -XX:-ResizePLAB JVM option which degrades performance on JDK11 (#12940)
* [d38ca782d6b](https://github.com/datastax/pulsar/commit/d38ca782d6b) [Functions][k8s] Expose function container metrics port (#12065)
* [96b3420cbb3](https://github.com/datastax/pulsar/commit/96b3420cbb3) Update command descriptions from old 'property/cluster/namespace' format to current 'tenant/namespace' format (#10485)
* [85166354742](https://github.com/datastax/pulsar/commit/85166354742) Don't create AvroData for each KafkaSourceRecord (#12859)
* [50db02ced2e](https://github.com/datastax/pulsar/commit/50db02ced2e) [OWASP] Address CVE-2020-29582 - upgrade kotlin-stdlib used by okhttp5
* [8db20a165af](https://github.com/datastax/pulsar/commit/8db20a165af) Fix wrong isEmpty method of ConcurrentOpenLongPairRangeSet (#12953)
 
## Luna Streaming Distribution 2.8.0 1.1.7

This release contains several bugfixes and improvements, most notably:
* Dedicated Netty EventLoopGroup for Protocol Handlers and Proxy extensions
* SchemaInfo.builder() API available again

List of most notable commits:

* [15d27662b19](https://github.com/datastax/pulsar/commit/15d27662b19) BookKeeper: use com.datastax.oss dependency and bump to 4.14.3.1.0.0
* [ab7f6c1b52b](https://github.com/datastax/pulsar/commit/ab7f6c1b52b) Disable stats recorder for built-in PulsarClient (#12217)
* [f09d0a99b29](https://github.com/datastax/pulsar/commit/f09d0a99b29) Bump BookKeeper 4.14.3 (#12906)
* [d7848da6fba](https://github.com/datastax/pulsar/commit/d7848da6fba) Fix log level config for pulsar-admin, pulsar-client and pulsar-perf
* [346745a6b7a](https://github.com/datastax/pulsar/commit/346745a6b7a) Fix Protocol Handlers and Proxy Extensions boot
* [306ae24a712](https://github.com/datastax/pulsar/commit/306ae24a712) Fix ProtocolHandlers
* [b743b765858](https://github.com/datastax/pulsar/commit/b743b765858) Fix boot of ProtocolHandlers and Proxy Extensions
* [8ea02d6573c](https://github.com/datastax/pulsar/commit/8ea02d6573c) Issue 12668: Protocol Handlers and Proxy Extensions: ability to use a dedicated EventLoopGroup for IO (#12692)
* [d51b0af62b2](https://github.com/datastax/pulsar/commit/d51b0af62b2) [Broker] Fix producer getting incorrectly removed from topic's producers map (#12846)
* [d5fe86f7c3b](https://github.com/datastax/pulsar/commit/d5fe86f7c3b) Fixed used after recycle issue in OpAddEntry (#12103)
* [8d9ab077984](https://github.com/datastax/pulsar/commit/8d9ab077984) Producer getting producer busy is removing existing producer from list (#11804)
* [b4a00834abd](https://github.com/datastax/pulsar/commit/b4a00834abd) [ServerCnx] Close connection after receiving unexpected SendCommand (#12780)
* [f46f54da368](https://github.com/datastax/pulsar/commit/f46f54da368) [Java Client] Let producer reconnect for state RegisteringSchema (#12781)
* [297fbd06a20](https://github.com/datastax/pulsar/commit/297fbd06a20) [Managed Ledger] Fix the incorrect total size when BrokerEntryMetadata is enabled (#12714)
* [643018ffef2](https://github.com/datastax/pulsar/commit/643018ffef2) Pulsar Client: restore SchemaInfo.builder() API (#12673)
* [6d94a427871](https://github.com/datastax/pulsar/commit/6d94a427871) [ML] Avoid passing OpAddEntry across a thread boundary in asyncAddEntry (#12606)
* [932a34cdb7d](https://github.com/datastax/pulsar/commit/932a34cdb7d) [Functions] Prevent NPE while stopping a non started Pulsar LogAppender (#12643)

## Luna Streaming Distribution 2.8.0 1.1.6

This release contains several bugfixes and improvements, most notably:

* Pulsar IO: Debezium upgrade to 1.7
* Pulsar IO: Datastax Cassandra Source Connector 0.2.10
* Better error handling for KCA based functions
* Improvements to ensure the production order of the messages
* Java artifacts are now available under the groupId `com.datastax.oss` (use `org.apache.pulsar` for Luna Streaming < 2.8.0.1.1.6)

List of most notable commits:

* [ae3cc95a406](https://github.com/datastax/pulsar/commit/ae3cc95a406) [ML] Add OpAddEntry to pendingAddEntries after the state check (#12570)
* [111ee2dc098](https://github.com/datastax/pulsar/commit/111ee2dc098) Fix cherry-pick issue
* [d4e5fb0da16](https://github.com/datastax/pulsar/commit/d4e5fb0da16) [managedledger] NPE on OpAddEntry while ManagedLedger is closing (#12364)
* [eb9c46c70d3](https://github.com/datastax/pulsar/commit/eb9c46c70d3) Replace orElse with orElseGet to avoid calling too many times. (#11542) (#11542)
* [36132a13b60](https://github.com/datastax/pulsar/commit/36132a13b60) [Branch-2.8]fix cherry-pick issue (#12397)
* [07d164ef6d8](https://github.com/datastax/pulsar/commit/07d164ef6d8) fix cherry-pick compile issue
* [ed6dc9fd3c6](https://github.com/datastax/pulsar/commit/ed6dc9fd3c6) [Java Client] Remove data race in MultiTopicsConsumerImpl to ensure correct message order (#12456)
* [0e62209dc75](https://github.com/datastax/pulsar/commit/0e62209dc75) [pulsar-java-client] Auto-recovery after exception like out of direct memory (#12170)
* [c9af4ab422b](https://github.com/datastax/pulsar/commit/c9af4ab422b) Avoid potentially blocking calls to metadata on critical threads (#12339)
* [beb75c00b68](https://github.com/datastax/pulsar/commit/beb75c00b68) Fix message being ignored when the non-persistent topic reader reconnect. (#12348)
* [ff16c9405c8](https://github.com/datastax/pulsar/commit/ff16c9405c8) Fix Pulsar Proxy to re-use authentication instance (#12245)
* [8c474585b29](https://github.com/datastax/pulsar/commit/8c474585b29) [Java Client] Use failPendingMessages to ensure proper cleanup (#12259)
* [18a4ae3c622](https://github.com/datastax/pulsar/commit/18a4ae3c622) Fix lost message issues 12221 (#12223)
* [c5936b27dda](https://github.com/datastax/pulsar/commit/c5936b27dda) Fix deadLetterPolicy is not working with key shared subscription under partitioned topic (#12148)
* [d467484f63d](https://github.com/datastax/pulsar/commit/d467484f63d) [Cherry-pick #11597] Use get instead of join to avoid getting stuck (#12110)
* [1c40034e12e](https://github.com/datastax/pulsar/commit/1c40034e12e) [Client] Fix ConcurrentModificationException in sendAsync (#11884)
* [4a31f8bc771](https://github.com/datastax/pulsar/commit/4a31f8bc771) [pulsar-functions] Pass `SubscriptionPosition` from `FunctionDetails` to `FunctionConfig` / `SinkConfig` (#11831)
* [c29ab1687f6](https://github.com/datastax/pulsar/commit/c29ab1687f6) [Issue 11936] forget to call SendCallback on producer close (#11939)
* [76c2bc136be](https://github.com/datastax/pulsar/commit/76c2bc136be) [function] enable protobuf-native schema support for function (#11868)
* [c9096c18221](https://github.com/datastax/pulsar/commit/c9096c18221) Fix seek at batchIndex level receive duplicated messages (#11826)
* [e2cd9f0a7da](https://github.com/datastax/pulsar/commit/e2cd9f0a7da) [Functions] ConcurrentHashMap should be used for caching producers (#11820)
* [b05b7660a33](https://github.com/datastax/pulsar/commit/b05b7660a33) Failed update partition of topic (#11683)
* [37be56ef338](https://github.com/datastax/pulsar/commit/37be56ef338) Fix race condition in concurrent schema deletion (#11606)
* [96a17c22c9e](https://github.com/datastax/pulsar/commit/96a17c22c9e) Stop OffsetStore when stopping the connector (#12457)
* [8dea755e3f3](https://github.com/datastax/pulsar/commit/8dea755e3f3) KCA doesn't handle unchecked unchecked ConnectException/KafkaException for the task, it may lead to the connector hanging (#12441)
* [f34a324eb3c](https://github.com/datastax/pulsar/commit/f34a324eb3c) Bugfix: Fix rackaware placement policy init error (#12097)
* [78984a515f4](https://github.com/datastax/pulsar/commit/78984a515f4) fix publish_time not set error when broker entry metadata enable without AppendBrokerTimestampMetadataInterceptor (#11014)
* [3cc06b58d39](https://github.com/datastax/pulsar/commit/3cc06b58d39) Avoid adding duplicated BrokerEntryMetadata (#12018)
* [0e95a1a1d85](https://github.com/datastax/pulsar/commit/0e95a1a1d85) Fix usage of seekAsync in MessageImpl.hasMessageAvailable and flaky-test (#10190)
* [38ee7e29c52](https://github.com/datastax/pulsar/commit/38ee7e29c52) ManagedLedger - EntryCacheImpl - move spammy log to TRACE level
* [9d2e30f13c7](https://github.com/datastax/pulsar/commit/9d2e30f13c7) Fix the dead lock when using hasMessageAvailableAsync and readNextAsync (#11183)
* [429c2be2d43](https://github.com/datastax/pulsar/commit/429c2be2d43) [function] fix update user config (#10731)
* [68534f6364d](https://github.com/datastax/pulsar/commit/68534f6364d) Upgrading Debezium to 1.7 (#12295)
* [fb31dcc054c](https://github.com/datastax/pulsar/commit/fb31dcc054c) [Proxy] set default httpProxyTimeout to 5 minutes (#12299)
* [375fa566cce](https://github.com/datastax/pulsar/commit/375fa566cce) [Issue-11966][pulsar-proxy] set default http proxy request timeout (#11971)
* [6c7d07bd874](https://github.com/datastax/pulsar/commit/6c7d07bd874) New distro groupId 'com.datastax.oss'
* [8442b563de6](https://github.com/datastax/pulsar/commit/8442b563de6) Use Public DataStax repo
* [aafcebbc805](https://github.com/datastax/pulsar/commit/aafcebbc805) Fixed ZKSessionTest.testReacquireLocksAfterSessionLost (#11886)



## Luna Streaming Distribution 2.8.0 1.1.5

This release contains some bugfixes and a couple of relevant improvements, most notably:
- New Debezium Oracle source
- [Pulsar Proxy extensions](https://github.com/apache/pulsar/wiki/PIP-99%3A-Pulsar-Proxy-Extensions) (from Apache Pulsar 2.9.0)
- Netty upgrade to 4.1.68.Final
- BookKeeper upgrade to 4.14.2 

List of most notable commits:

* [bad1f7057f9](https://github.com/datastax/pulsar/commit/bad1f7057f9) Update BK dependency to Apache 4.14.2
* [0660316ceca](https://github.com/datastax/pulsar/commit/0660316ceca) Upgrade netty to 4.1.68.Final (#12218)
* [dc7af79db0f](https://github.com/datastax/pulsar/commit/dc7af79db0f) [Pulsar IO] ElasticSearch Sink: support Fixed and ENUM datatypes
* [7b86934429f](https://github.com/datastax/pulsar/commit/7b86934429f) Debezium Oracle Source (#11520)
* [b3ddb476354](https://github.com/datastax/pulsar/commit/b3ddb476354) make KafkaSourceRecord ack() async to avoid deadlock (#11435)
* [2d42f0f35d1](https://github.com/datastax/pulsar/commit/2d42f0f35d1) [pulsar-io] pass the pulsar service url to debezium source for history database (#11251)
* [cb2ba71c30f](https://github.com/datastax/pulsar/commit/cb2ba71c30f) PIP-85: [pulsar-io] pass pulsar client via context to connector (#11056)
* [b3917afe046](https://github.com/datastax/pulsar/commit/b3917afe046) [Issue 11689][Client] Fixed block forever bug in Consumer.batchReceive (#11691)
* [84d78b4c091](https://github.com/datastax/pulsar/commit/84d78b4c091) Handle receiveAsync() failures in MultiTopicsConsumer (#11843)
* [96da2c4b663](https://github.com/datastax/pulsar/commit/96da2c4b663) [Client] Fix endless receiveAsync loop in MultiTopicsConsumer (#12044)
* [196cd08ae3e](https://github.com/datastax/pulsar/commit/196cd08ae3e) Fixed accessing MessageImpl after it was enqueued on user queue (#11824)
* [f4ef4f326a9](https://github.com/datastax/pulsar/commit/f4ef4f326a9) [Issue 11007]  add a version of AUTO_PRODUCE_BYTES that doesn't validate the message in `encode` (#11238)
* [1ec194cd07b](https://github.com/datastax/pulsar/commit/1ec194cd07b) Fixed KCA Sink handling of Json and Avro; support for kafka connectors that overload task.preCommit() directly (#11905)
* [7cbea875fa7](https://github.com/datastax/pulsar/commit/7cbea875fa7) Avoid to infinitely split bundle (#11937)
* [49be8b85ac2](https://github.com/datastax/pulsar/commit/49be8b85ac2) Fix wrong key-hash selector used for new consumers after all the previous consumers disconnected (#12035)
* [98ef811a699](https://github.com/datastax/pulsar/commit/98ef811a699) Fix the topic in fenced state and can not recover. (#11737)
* [10e74d9ecc0](https://github.com/datastax/pulsar/commit/10e74d9ecc0) fix parseMessageMetadata error cause by not skip broker entry metadata (#10968)
* [d4197345496](https://github.com/datastax/pulsar/commit/d4197345496) Forbid to read other topic's data in managedLedger layer (#11912)
* [7e99a6a86e1](https://github.com/datastax/pulsar/commit/7e99a6a86e1) Fixed Proxy leaking outbound connections (#11848)
* [42cf81bd613](https://github.com/datastax/pulsar/commit/42cf81bd613) PIP-99 Pulsar Proxy Protocol Handlers



## Luna Streaming Distribution 2.8.0 1.1.4

This is a bugfix release that allows you to run Pulsar while disabling non-TLS service ports and it fixes a problem with KEY_BASED BatchBulder in Pulsar IO.

List of most notable commits:

* [e97d53283a2](https://github.com/datastax/pulsar/commit/e97d53283a2) [Broker] Call .release() when discarding entry to prevent direct memory leak (#11748)
* [968432ca056](https://github.com/datastax/pulsar/commit/968432ca056) [Broker] Handle NPE when full key range isn't covered with active consumers (#11749)
* [79db72e9e3e](https://github.com/datastax/pulsar/commit/79db72e9e3e) [Functions] Support KEY_BASED batch builder for Java based functions and sources
* [a547b20b09c](https://github.com/datastax/pulsar/commit/a547b20b09c) [Broker] Support disabling non-TLS service ports (#11681)
* [550e6e1346a](https://github.com/datastax/pulsar/commit/550e6e1346a) [Transaction] Fix the transaction marker does not deleted as expect. (#11126)

## Luna Streaming Distribution 2.8.0 1.1.3

This is a bugfix release that upgrates Jetty to latest available version 9.4.43.v20210629.

List of most notable commits:

* [9140c12d79a](https://github.com/datastax/pulsar/commit/9140c12d79a) [Security] Upgrade Jetty to 9.4.43.v20210629 (#11660)

## Luna Streaming Distribution 2.8.0 1.1.2

This is a bugfix release that adds automatic updating (at build time) of Ubuntu system components in order to address security issues caused
by third party dependencies imported inside the docker images.

List of most notable commits:

* [e0b83008b28](https://github.com/datastax/pulsar/commit/e0b83008b28) [Security] Install Ubuntu updates while building docker image

## Luna Streaming Distribution 2.8.0 1.1.1

This is a bugfix release that fixes problems about Geo Replication.
It also includes the ALPHA version of the [OpenID Authentication plugin](https://github.com/datastax/pulsar-openid-connect-plugin).

List of most notable commits:

* [272c180f2da](https://github.com/datastax/pulsar/commit/272c180f2da) [Broker] Fix replicated subscriptions direct memory leak

## Luna Streaming Distribution 2.8.0 1.1.0

This release is based on the [Apache Pulsar 2.8.0 release](https://pulsar.apache.org/release-notes/#280-mdash-2021-06-12-a-id280a).

This is a major release on Luna Streaming 2.8.0 release line.

Most notably:
- It contains upgrades to third party libraries for known CVEs (Netty, Apache Commons Compress, OkHttp3)
- It fixes a problem with Bookies on TLS (anticipated from Apache BookKeeper 4.15.0-SNAPSHOT) 
- It upgrades Debezium to 1.5.4
- It fixes a problem on deploying Pulsar Functions with parallelism > 1
- It contains a BETA version of KOP (Kafka On Pulsar)

In addition to the contents of that release and of Luna Streaming 2.8.0 1.0.0, it includes the following notable commits:

* [ac9115b6625](https://github.com/datastax/pulsar/commit/ac9115b6625) Upgrade BookKeeper to DataStax version 4.14.1.1.0.1 - fix TLS issues on Pulsar
* [210b4d9cf6f](https://github.com/datastax/pulsar/commit/210b4d9cf6f) Fix issue with NarUnpacker that causes races and files getting overridden
* [180fc7ac013](https://github.com/datastax/pulsar/commit/180fc7ac013) Upgrade Netty tcnative to 2.0.40.Final which is compatible with 4.1.66.Final
* [f3bf0047eb2](https://github.com/datastax/pulsar/commit/f3bf0047eb2) [Security] Upgrade commons-compress to 1.21
* [32729193e9d](https://github.com/datastax/pulsar/commit/32729193e9d) Upgrade Netty to 4.1.66.Final
* [f08d76d1875](https://github.com/datastax/pulsar/commit/f08d76d1875) [broker] Fix issue that message ordering could be broken when redelivering messages on Key_Shared subscription (#10762)
* [f3e0c929560](https://github.com/datastax/pulsar/commit/f3e0c929560) Upgrade Debezium to v.1.5.4 (last buildable with Java 8)
* [246174afb2c](https://github.com/datastax/pulsar/commit/246174afb2c) Debezium: Make pulsar.auth.token optional (and make Integration Tests pass)
* [5445344cfd5](https://github.com/datastax/pulsar/commit/5445344cfd5) Debezium integration tests   - check for flush lsn updates
* [9574034675f](https://github.com/datastax/pulsar/commit/9574034675f) Implement createIndexIfNeeded option and upgrade ES container in tests
* [72bd887c495](https://github.com/datastax/pulsar/commit/72bd887c495) Fix ES Sink and remove debug
* [17cd5299931](https://github.com/datastax/pulsar/commit/17cd5299931) Fix Avro dep in ESSink
* [f5838dda8ab](https://github.com/datastax/pulsar/commit/f5838dda8ab) Include common-io in java function instance (#10939)
* [e8bd9a5bd8c](https://github.com/datastax/pulsar/commit/e8bd9a5bd8c) Add AVRO in compile scope
* [be81cd3ddc1](https://github.com/datastax/pulsar/commit/be81cd3ddc1) Port ElasticSearch Sink Tests from ASF Pulsar PR
* [d9f6a9de592](https://github.com/datastax/pulsar/commit/d9f6a9de592) Make MetadataCacheTest reliable. (#10877)
* [a7b274bb563](https://github.com/datastax/pulsar/commit/a7b274bb563) Add dependency management rule for com.squareup.okhttp3:logging-interceptor
* [7b00aa43956](https://github.com/datastax/pulsar/commit/7b00aa43956) Bump version to 2.8.0.1.0.1-SNAPSHOT
* [929050dce5a](https://github.com/datastax/pulsar/commit/929050dce5a) [Security] Upgrade OkHttp3 version to 5.0.0-alpha.2 to address CVE-2021-0341
* [359d6efad68](https://github.com/datastax/pulsar/commit/359d6efad68) LS-130 Pulsar SQL fails to start in lunastreaming-all:2.8.0_1.0.0
* [863bd9b9162](https://github.com/datastax/pulsar/commit/863bd9b9162) Enhanced ES-sink connector
* [827327d8f49](https://github.com/datastax/pulsar/commit/827327d8f49) [Broker] Fix the backlog issue with --precise-backlog=true (#10966)
* [21d19810f3c](https://github.com/datastax/pulsar/commit/21d19810f3c) Do not expose meaningless stats for consumer. (#11005)
* [07524f377ed](https://github.com/datastax/pulsar/commit/07524f377ed) Fixed using CommandSubscribe.getConsumerName() without checking (#11199)


## Luna Streaming Distribution 2.8.0 1.0.0

This release is based on the [Apache Pulsar 2.8.0 release](https://pulsar.apache.org/release-notes/#280-mdash-2021-06-12-a-id280a). In addition to the contents of that release, it includes the following notable commits:

* [66fb63324b4](https://github.com/datastax/pulsar/commit/66fb63324b4) Use Released DataStax BookKeeper 4.14.1.1.0.0 - with security updates
* [7544cfb65b3](https://github.com/datastax/pulsar/commit/7544cfb65b3) [Broker/Bookie] Set -Dio.netty.tryReflectionSetAccessible=true for pulsar processes
* [dfda03d5484](https://github.com/datastax/pulsar/commit/dfda03d5484) Add fsGroup to Pod context for function StatefulSet
* [2f3548cea4c](https://github.com/datastax/pulsar/commit/2f3548cea4c) Enable Function subscription naming workaround when activated
* [362b97b7bc5](https://github.com/datastax/pulsar/commit/362b97b7bc5) Revert "Changing default function subscription to be function name, not FQFN"
* [1d837c265f8](https://github.com/datastax/pulsar/commit/1d837c265f8) Add presto password authenticators plugin to enable password auth in Pulsar SQL
* [6725c4a26e3](https://github.com/datastax/pulsar/commit/6725c4a26e3) Docker image: add vim and nettools (netstat)
* [d8beb1fc107](https://github.com/datastax/pulsar/commit/d8beb1fc107) [Security] Use adoptopenjdk:11-jdk base image for Pulsar docker images
* [2f4fb58095a](https://github.com/datastax/pulsar/commit/2f4fb58095a) [issue 10989 ] Java Client: KeyValueSchema with AutoConsume component - make it work if the topic schema is still not set (#10995)
* [7fa88cce895](https://github.com/datastax/pulsar/commit/7fa88cce895) [Proxy] Limit replay buffer size in AdminProxyHandler (#10944)
* [a8b372e2a78](https://github.com/datastax/pulsar/commit/a8b372e2a78) [Security] Exclude grpc-okhttp dependency and set okhttp3 & okio version
* [321afb9b1ca](https://github.com/datastax/pulsar/commit/321afb9b1ca) [Broker] Fix direct memory leak in getLastMessageId (#10977)
* [f46815b83db](https://github.com/datastax/pulsar/commit/f46815b83db) Add AvroSchema UUID support
* [f1fe9c23486](https://github.com/datastax/pulsar/commit/f1fe9c23486) Fix peek message failure when broker entry metadata is enabled (#10924)
* [f66d03dc623](https://github.com/datastax/pulsar/commit/f66d03dc623) Fix issue where Key_Shared consumers could get stuck (#10920)
* [5ff33e5cf60](https://github.com/datastax/pulsar/commit/5ff33e5cf60) Fix the unit tests for the websocket and run tests under websocket group (#10921)
* [vd1b2ffed641](https://github.com/datastax/pulsar/commit/vd1b2ffed641) [Security] Upgrade vertx to 3.9.8 to address CVE-2019-17640
* [a4eb73bede4](https://github.com/datastax/pulsar/commit/a4eb73bede4) [Security] Exclude and remove freebuilder dependency
* [269ad60285b](https://github.com/datastax/pulsar/commit/269ad60285b) [Security] Upgrade bouncycastle version to 1.69
* [3ee7a371aca](https://github.com/datastax/pulsar/commit/3ee7a371aca) [Security] Upgrade k8s client-java to 12.0.1
* [0578136f930](https://github.com/datastax/pulsar/commit/0578136f930) [Security] Upgrade caffeine to 2.9.1
* [b3339feb1dd](https://github.com/datastax/pulsar/commit/b3339feb1dd) [Security] Upgrade commons-codec to 1.15
* [68349766567](https://github.com/datastax/pulsar/commit/68349766567) Remove the unwanted dependencies in the pulsar function's instance jar and make SchemaInfo an interface (#10878)
* [57f0deef837](https://github.com/datastax/pulsar/commit/57f0deef837) [Security] Upgrade Zookeeper to 3.6.3 (#10852)
* [389cbf9c858](https://github.com/datastax/pulsar/commit/389cbf9c858) Upgrade Jetty to 9.4.42.v20210604 (#10907)
* [4eb2321e6f2](https://github.com/datastax/pulsar/commit/4eb2321e6f2) Kafka connect sink adaptor to support non-primitive schemas (#10410)
* [bc737173b3c](https://github.com/datastax/pulsar/commit/bc737173b3c) Provide a flag to disable managed ledger metrics (#10885)
* [4f9364d34c9](https://github.com/datastax/pulsar/commit/4f9364d34c9) Make KeyValueSchema an interface visible in the public Schema API (#10888)
* [e1d474940b2](https://github.com/datastax/pulsar/commit/e1d474940b2) Introduce metrics servlet timeout setting (#10886)
* [10fb66cc56a](https://github.com/datastax/pulsar/commit/10fb66cc56a) #10882 use ObjectMapper to parse Sink/Source configs (#10883)
* [cd8a2808fe0](https://github.com/datastax/pulsar/commit/cd8a2808fe0) [Broker] Always let system topic TRANSACTION_BUFFER_SNAPSHOT be auto created (#10876)
* [b6217be1217](https://github.com/datastax/pulsar/commit/b6217be1217) [Issue 10860][pulsar-metadata] Ensure metadata cache consistency across brokers (#10862)
* [9f55556d363](https://github.com/datastax/pulsar/commit/9f55556d363) pulsar-perf: print total number of messages (#10765)
* [09290157d8b](https://github.com/datastax/pulsar/commit/09290157d8b) [Security] Upgrade Zookeeper to 3.6.3 (#10852)
* [1916324c8f0](https://github.com/datastax/pulsar/commit/1916324c8f0) Upgrade Jetty to 9.4.42.v20210604 (#10907)
* [5cfa70111ed](https://github.com/datastax/pulsar/commit/5cfa70111ed) Use LunaStreaming BookKeeper 4.14.1.1.0.0-SNAPSHOT
* [3505b98b7ea](https://github.com/datastax/pulsar/commit/3505b98b7ea) Kafka connect sink adaptor to support non-primitive schemas (#10410)
* [8252f9db7f2](https://github.com/datastax/pulsar/commit/8252f9db7f2) Provide a flag to disable managed ledger metrics (#10885)
* [1ecadd482ef](https://github.com/datastax/pulsar/commit/1ecadd482ef) Make KeyValueSchema an interface visible in the public Schema API (#10888)
* [a750f975799](https://github.com/datastax/pulsar/commit/a750f975799) Introduce metrics servlet timeout setting (#10886)
* [92aff2bbb83](https://github.com/datastax/pulsar/commit/92aff2bbb83) #10882 use ObjectMapper to parse Sink/Source configs (#10883)
* [e44be070d4b](https://github.com/datastax/pulsar/commit/e44be070d4b) [Broker] Always let system topic TRANSACTION_BUFFER_SNAPSHOT be auto created (#10876)
* [d280fad2b9f](https://github.com/datastax/pulsar/commit/d280fad2b9f) [Issue 10860][pulsar-metadata] Ensure metadata cache consistency across brokers (#10862)
* [263df0248ec](https://github.com/datastax/pulsar/commit/263df0248ec) pulsar-perf: print total number of messages (#10765)
* [1b44c32cc0e](https://github.com/datastax/pulsar/commit/1b44c32cc0e) [Issue 8751] Update Dockerfile for Pulsar and Dashboard to Create and Use pulsar User (nonroot user) (#8796)
* [32c313bca1c](https://github.com/datastax/pulsar/commit/32c313bca1c) Changing default function subscription to be function name, not FQFN
* [674508ae9b3](https://github.com/datastax/pulsar/commit/674508ae9b3) Always return from trigger even if read from output topic times out
* [ee864abc3d5](https://github.com/datastax/pulsar/commit/ee864abc3d5) update ds distro required io connectors
* [be602b9855b](https://github.com/datastax/pulsar/commit/be602b9855b) auth token for debezium and kafka connect adaptor
