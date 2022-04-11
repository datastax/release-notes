# Release notes for DataStax Luna Streaming Distribution
 
## About DataStax Luna Streaming Distribution
Luna Streaming Distribution 2.8.3 is compatible with Apache Pulsar&trade; 2.8.0 and subsequent releases.

### Components

   * Datastax Luna Streaming (Apache Pulsar 2.8.3 fork)
   * DataStax Pulsar Admin Console
   * DataStax Pulsar Heartbeat
   * DataStax Apache Pulsar Cassandra Sink
   * DataStax Apache Pulsar Cassandra Source
   * DataStax Burnell
   * Datastax BookKeeper (Apache BookKeeper fork)
 
This release adds these features to the original Apache Pulsar 2.8.3 release:
  
   * Stability improvements
   * Rootless Docker image
   * Third party libraries updates for security fixes
   * Docker images based on Ubuntu (instead of Debian based images in Pulsar 2.8.0, for security reasons)
   * Dependency upgrades (for security, stability and performances)
   * An enhanced ElasticSearch Pulsar IO Sink
   * An enhanced version of Apache BookKeeper with security fixes
   * Pulsar IO source for Debezium Oracle
   * [Pulsar Proxy extensions](https://github.com/apache/pulsar/wiki/PIP-99%3A-Pulsar-Proxy-Extensions) feature 
   * [Starlight for RabbitMQ](https://www.datastax.com/starlight/rabbitmq)
 
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

### Source Code of Main Components

The source code for these versions of Apache Pulsar and Apache BookKeeper code is available here:
   
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


### Upgrade considerations for Luna Streaming Distribution 2.8.3

As with Luna Streaming 2.7, this release uses non-root containers for enhanced security. When upgrading from a previous version (for example, 2.6.2_1.0.1), files created while running that version will have root permissions and will not be readable by containers running the new version.

To fix this, manually log into the ZooKeeper, BookKeeper, and Function Worker containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs` directories are owned by UID 10000 (user pulsar). The group ID of the files should also be set to GID 10001 (group pulsar). Here is an example command:

```
chown -R 10000:10001 /pulsar/data
```

If you are using the Luna Streaming Helm chart, you can enable automatic repair of the permissions using the `fixRootlessPermissions` setting to solve this problem. For more details on this setting, go [here](https://github.com/datastax/pulsar-helm-chart).

If you are upgrading from Luna Streaming Distribution 2.8.0, you don't have to do any particular action.

### Upgrade considerations for custom Pulsar Functions and Pulsar IO Connectors

If you are upgrading from Apache Pulsar 2.7.0 or Luna Streaming 2.7.2 you may need to recompile your Pulsar Functions or Pulsar IO Connectors using Apache Pulsar 2.8.0 as a dependency.
This is because there is a breaking API change in Apache Pulsar 2.8.0 (and therefore in Luna Streaming 2.8.0) related to the `SchemaInfo` java class.
More context [here](https://github.com/apache/pulsar/issues/11338).

If you are upgrading from Luna Streaming Distribution 2.8.0, you don't have to do any particular action.

### Packaging

Luna Streaming Distribution comes with different packages tooled for different purposes. 
The distributions are available as Docker images and tarballs, and both methods follow the same packaging patterns.

#### Patterns

* **lunastreaming**: the basic Luna Streaming Distribution **including Pulsar SQL** feature.
* **lunastreaming-core**: the basic Luna Streaming Distribution **without Pulsar SQL** feature. Pick this distribution if you don't need Pulsar SQL features.
* **lunastreaming-all**: contains the Core Luna Streaming Distribution, including **Pulsar Offloaders** and the **Datastax Pulsar IO Connectors** listed above. Pick this distribution if you want the Datastax connectors or the offloading feature.

# Releases

## Luna Streaming Distribution 2.8.3 1.0.7
This is a maintenance release containing important security updates.
### Most notable commits
* [b6d1967c60a](https://github.com/datastax/pulsar/commit/b6d1967c60a) Add KeyStore support in WebSocket, Function Worker HTTPS Servers
* [e0072ba5afe](https://github.com/datastax/pulsar/commit/e0072ba5afe) [Proxy] Exit if proxy service fails to start (#15076)
* [386e0a810a8](https://github.com/datastax/pulsar/commit/386e0a810a8) Use tlsCertRefreshCheckDurationSec instead of 0 for refresh value (#15075)
* [3bf6f405b36](https://github.com/datastax/pulsar/commit/3bf6f405b36) Ignore case when obfuscating passwords in python configuration scripts (#15077)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.4.nar
* pulsar-io-data-generator-2.8.3.1.0.7.nar
* pulsar-io-debezium-mongodb-2.8.3.1.0.7.nar
* pulsar-io-debezium-mssql-2.8.3.1.0.7.nar
* pulsar-io-debezium-mysql-2.8.3.1.0.7.nar
* pulsar-io-debezium-oracle-2.8.3.1.0.7.nar
* pulsar-io-debezium-postgres-2.8.3.1.0.7.nar
* pulsar-io-elastic-search-2.8.3.1.0.7.nar
* pulsar-io-jdbc-clickhouse-2.8.3.1.0.7.nar
* pulsar-io-jdbc-mariadb-2.8.3.1.0.7.nar
* pulsar-io-jdbc-postgres-2.8.3.1.0.7.nar
* pulsar-io-jdbc-sqlite-2.8.3.1.0.7.nar
* pulsar-io-kafka-2.8.3.1.0.7.nar
* pulsar-io-kinesis-2.8.3.1.0.7.nar
* pulsar-snowflake-connector-0.1.9.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.18.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.18.nar

## Luna Streaming Distribution 2.8.3 1.0.6
This is a maintenance release containing important stability and security updates.
### Most notable commits
* [4f09d3daa5c](https://github.com/datastax/pulsar/commit/4f09d3daa5c) Add pulsar_subscription_consumers_count metric Fix #15032
* [fcaa26aebc9](https://github.com/datastax/pulsar/commit/fcaa26aebc9) [fix][elasticseach] ElasticSearch sink: client 'close' method is never called (#14995)
* [335d28a4354](https://github.com/datastax/pulsar/commit/335d28a4354) KCA Sink to handle KeyValue<GenericRecord, GenericRecord>
* [106302663de](https://github.com/datastax/pulsar/commit/106302663de) Add FULL_MESSAGE_IN_JSON_EXPAND_VALUE message format to Kinesis sink (#52)
* [2de66504178](https://github.com/datastax/pulsar/commit/2de66504178) handle whatever KeyValue getNativeObject() returns: org.apache.pulsar.io.core.KeyValue or org.apache.pulsar.common.schema.KeyValue (#61)
* [57762dcd540](https://github.com/datastax/pulsar/commit/57762dcd540) [ML] Fix race condition in updating lastMarkDeleteEntry field (#15031)
* [eca591a5cee](https://github.com/datastax/pulsar/commit/eca591a5cee) [branch-2.8] Fix delete namespace issue
* [9e22643c11b](https://github.com/datastax/pulsar/commit/9e22643c11b) Revert "Fix delete namespace issue. (#14619)"
* [0828d655954](https://github.com/datastax/pulsar/commit/0828d655954) [kca] Fix kca cherry-pick issue (#63)
* [24f4d6f14bc](https://github.com/datastax/pulsar/commit/24f4d6f14bc) [fix][broker] Fix potential NPE in Replicator (#15003)
* [808728bc0d9](https://github.com/datastax/pulsar/commit/808728bc0d9) [fix][client] ConsumerBuilderImpl can not set null to deadLetterPolicy (#14980)
* [fc6ee9cdae5](https://github.com/datastax/pulsar/commit/fc6ee9cdae5) [CI] Upgrade zlib version to 1.2.12 (#14964)
* [36602790c70](https://github.com/datastax/pulsar/commit/36602790c70) [fix][broker] Fix wrong state for non-durable cursor (#14869)
* [4b4978a8cfc](https://github.com/datastax/pulsar/commit/4b4978a8cfc) [fix][broker] Fix topic policy reader close bug. (#14897)
* [e9dfffb4c05](https://github.com/datastax/pulsar/commit/e9dfffb4c05) [fix][admin] Fix NPE in PulsarAdminBuilder when the service is not set (#14769)
* [60fc0863b3b](https://github.com/datastax/pulsar/commit/60fc0863b3b) [fix][broker] Fix cannot delete namespace with system topic (#14730)
* [611de95bd25](https://github.com/datastax/pulsar/commit/611de95bd25) [fix][admin-cli]: Remove the trust certs check (#14764)
* [646d9c7b8ee](https://github.com/datastax/pulsar/commit/646d9c7b8ee) Process maxRedeliverCount is 0 of DeadLeddterPolicy (#14706)
* [08d7485fcaf](https://github.com/datastax/pulsar/commit/08d7485fcaf) Provide an accurate error message when set ``autoTopicCreation `` (#14684)
* [9c77c25a62a](https://github.com/datastax/pulsar/commit/9c77c25a62a) [pulsar-functions] fix some IOExceptions when create functions from package URL (#14553)
* [1dc8e6062d2](https://github.com/datastax/pulsar/commit/1dc8e6062d2) [Broker] Optimize RawReader#create when using Compactor (#14447)
* [c7f53072eb2](https://github.com/datastax/pulsar/commit/c7f53072eb2) Fixes NPE - ``ReplicatedSubscriptionsController`` send marker message when enable deduplicated. (#14017)
* [8cd2aaa30d0](https://github.com/datastax/pulsar/commit/8cd2aaa30d0) Set splitNamespaceBundle with `readonly=false`. (#14680)
* [3c0f869cf67](https://github.com/datastax/pulsar/commit/3c0f869cf67) [security] Allow to config web server's cipher and protocols (#13354)
* [09ec366082e](https://github.com/datastax/pulsar/commit/09ec366082e) Include circe-checksum in pulsar-client dependency (#60)
* [72aae1521a1](https://github.com/datastax/pulsar/commit/72aae1521a1) [feat][broker] Full-support set ssl provider, ciphers and protocols (#14569)
* [e5e49511a36](https://github.com/datastax/pulsar/commit/e5e49511a36) [pulsar-proxy] Fix auto-cert refresh when proxy connects to broker (#14130)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.4.nar
* pulsar-io-data-generator-2.8.3.1.0.6.nar
* pulsar-io-debezium-mongodb-2.8.3.1.0.6.nar
* pulsar-io-debezium-mssql-2.8.3.1.0.6.nar
* pulsar-io-debezium-mysql-2.8.3.1.0.6.nar
* pulsar-io-debezium-oracle-2.8.3.1.0.6.nar
* pulsar-io-debezium-postgres-2.8.3.1.0.6.nar
* pulsar-io-elastic-search-2.8.3.1.0.6.nar
* pulsar-io-jdbc-clickhouse-2.8.3.1.0.6.nar
* pulsar-io-jdbc-mariadb-2.8.3.1.0.6.nar
* pulsar-io-jdbc-postgres-2.8.3.1.0.6.nar
* pulsar-io-jdbc-sqlite-2.8.3.1.0.6.nar
* pulsar-io-kafka-2.8.3.1.0.6.nar
* pulsar-io-kinesis-2.8.3.1.0.6.nar
* pulsar-snowflake-connector-0.1.8.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.17.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.17.nar

## Luna Streaming Distribution 2.8.3 1.0.5

This release is based on the [Apache Pulsar 2.8.3 release](https://pulsar.apache.org/release-notes/#283). In addition to the contents of that release, it includes the following notable commits:

* [7548eac686e](https://github.com/datastax/pulsar/commit/7548eac686e) [elasticsearch] Option to disable SSL certificate validation (#56)
* [c6cd49eb707](https://github.com/datastax/pulsar/commit/c6cd49eb707) handle null offsets from kafka connector (#53)
* [55add94d03f](https://github.com/datastax/pulsar/commit/55add94d03f) Offloader: add API to scan objects on Tiered Storage: Move to JAX-RS StreamingOutput
* [549fa14e703](https://github.com/datastax/pulsar/commit/549fa14e703) Offloader: add API to scan objects on Tiered Storage
* [3650318d34f](https://github.com/datastax/pulsar/commit/3650318d34f) [fix][kinesis] Remove internal dependency: pulsar-functions-instance (#14925)
* [123fa447b6f](https://github.com/datastax/pulsar/commit/123fa447b6f) [Java Client] Improve consumer listener logic (#13273)
* [9b3e06e8d43](https://github.com/datastax/pulsar/commit/9b3e06e8d43) TieredStorage: add debug information (#14907)
* [ac9b66d24a1](https://github.com/datastax/pulsar/commit/ac9b66d24a1) [elasticsearch] support token based auth (#46)
* [0d4ec74a1a9](https://github.com/datastax/pulsar/commit/0d4ec74a1a9) ElasticSearch Sink: handle concurrent index creation requests (#51)
* [0ae0fcb18b5](https://github.com/datastax/pulsar/commit/0ae0fcb18b5) [fix][auth] Athenz: do not use uber-jar and bump to 1.10.50
* [145a3888390](https://github.com/datastax/pulsar/commit/145a3888390) [fix][security] Upgrade jackson and jackson-databind (2.13.2.1) to get rid of CVE-2020-36518
* [c6a5969c62e](https://github.com/datastax/pulsar/commit/c6a5969c62e) [security] Upgrade PostGre driver to 42.3.3 to get rid of CVE-2022-26520
* [662565bf1d6](https://github.com/datastax/pulsar/commit/662565bf1d6) ServerCnx] Improve error logging for topic not found (#13950) (#14892)
* [57a1c40d695](https://github.com/datastax/pulsar/commit/57a1c40d695) [Broker] Fix NPE when subscription is already removed (#14363)
* [3c98f3e1ebf](https://github.com/datastax/pulsar/commit/3c98f3e1ebf) [refactor][proxy] Refactor Proxy code and fix connection stalling by switching to auto read mode (#14713)
* [f1f6121a79b](https://github.com/datastax/pulsar/commit/f1f6121a79b) [Proxy] Log warning when opening connection to broker fails (#14710)
* [456b1aaf634](https://github.com/datastax/pulsar/commit/456b1aaf634) [fix][broker] Fixed duplicated delayed messages when all consumers disconnect (#14740)
* [5dc8ed27f94](https://github.com/datastax/pulsar/commit/5dc8ed27f94) [fix][broker]: cancel offload tasks when managed ledger closed. (#14744)
* [2fbf49f4f15](https://github.com/datastax/pulsar/commit/2fbf49f4f15) Handle kafka sinks that return immutable maps as configs (#14780)
* [bf0f862c1e0](https://github.com/datastax/pulsar/commit/bf0f862c1e0) Switch BlobStoreManagedLedgerOffloader to use removeBlob
* [90e3db35c5e](https://github.com/datastax/pulsar/commit/90e3db35c5e) Upgrade Zookeeper to 3.8.0 (#14601)
* [936ef17b6e3](https://github.com/datastax/pulsar/commit/936ef17b6e3) Drop provided scope for the pulsar-functions-instance in kinesis sink (#41)
* [37b2c81e521](https://github.com/datastax/pulsar/commit/37b2c81e521) Fixed 404 error msg not being returned correctly using http lookup. (#14677)
* [989d3fdbc36](https://github.com/datastax/pulsar/commit/989d3fdbc36) [ Issue 14633] [pulsar-broker] Fix metadata store deadlock when checking BacklogQuota (#14634)
* [fd8e4f8a8a9](https://github.com/datastax/pulsar/commit/fd8e4f8a8a9) [Broker] Ignore the print the log that the topic does not exist (#13535)
* [f839ea2500c](https://github.com/datastax/pulsar/commit/f839ea2500c) Fail proxy startup if brokerServiceURL is missing scheme (#14682)
* [b8c0fbcb7ea](https://github.com/datastax/pulsar/commit/b8c0fbcb7ea) [pulsar-io] Elasticsearch sink support for Elastic 8 - switch to java-client (#35)
* [67b9aa1dc32](https://github.com/datastax/pulsar/commit/67b9aa1dc32) Set the ignoreUnsupportedFields default to false
* [a598d9d857a](https://github.com/datastax/pulsar/commit/a598d9d857a) Add support of PrometheusRawMetricsProvider for the Pulsar-Proxy
* [f519f9e4785](https://github.com/datastax/pulsar/commit/f519f9e4785) Fix lost message issue due to ledger rollover. (#14664)
* [e15abdcaaa7](https://github.com/datastax/pulsar/commit/e15abdcaaa7) [Branch-2.8] Fix Broker HealthCheck Endpoint Exposes Race Conditions. (#14618)
* [d32c13424ab](https://github.com/datastax/pulsar/commit/d32c13424ab) Fix delete namespace issue. (#14619)
* [0b25dd5d4b8](https://github.com/datastax/pulsar/commit/0b25dd5d4b8) Fix PulsarRecordCursor deserialize issue. (#14615)
* [2899f2ba080](https://github.com/datastax/pulsar/commit/2899f2ba080) Fix ConsumerBuilderImpl#subscribeAsync blocks calling thread. (#14614)
* [c0f3e9640f5](https://github.com/datastax/pulsar/commit/c0f3e9640f5) [Branch-2.8] Fix validateGlobalNamespaceOwnership wrap exception issue. (#14612)
* [b739e06ba18](https://github.com/datastax/pulsar/commit/b739e06ba18) [Broker] Fixed wrong behaviour caused by not cleaning up topic policy service state. (#14503)
* [cd260c662f8](https://github.com/datastax/pulsar/commit/cd260c662f8) [C++] Fix wrong unit of Access Token Response's `expires_in` field (#14554)
* [f7ac6311ab5](https://github.com/datastax/pulsar/commit/f7ac6311ab5) [Functions] Pass configured metricsPort to k8s runtime (#14502)
* [5b6f360c03f](https://github.com/datastax/pulsar/commit/5b6f360c03f) Revert "kubernetesRuntime read metricsPort from kuberbetesRuntimeFactoryConfig"
* [2ec00c5d02e](https://github.com/datastax/pulsar/commit/2ec00c5d02e) [pulsar-io] throw exceptions when kafka offset backing store failed to start (#14491)
* [a27a50f78c7](https://github.com/datastax/pulsar/commit/a27a50f78c7) fix npe in ManagedLedgerImpl (#14481)
* [768c7fb0c35](https://github.com/datastax/pulsar/commit/768c7fb0c35) [pulsar-broker] Fix avg-messagePerEntry metrics for consumer (#14330)
* [fc960a6a2ca](https://github.com/datastax/pulsar/commit/fc960a6a2ca) Validate rack name (#14336)
* [8bec08bbaec](https://github.com/datastax/pulsar/commit/8bec08bbaec) Fix can't read the latest message of the compacted topic (#14449)
* [7ecf51ed694](https://github.com/datastax/pulsar/commit/7ecf51ed694) Fixing get functions for output topic and serde classname (#14103)
* [e9897eaa986](https://github.com/datastax/pulsar/commit/e9897eaa986) Added Debezium Source for MS SQL Server (#12256)
* [959db2ee768](https://github.com/datastax/pulsar/commit/959db2ee768) KCA: Option to sanitize topic name for the conenctors that cannot handle pulsar topic names
* [0138f6e16d0](https://github.com/datastax/pulsar/commit/0138f6e16d0) Allow Pulsar Functions localrun to exit on error (#12278)
* [3b31de285ec](https://github.com/datastax/pulsar/commit/3b31de285ec) Allow Pulsar Functions / Sinks to pool messages (#11618)
* [75cec6d9816](https://github.com/datastax/pulsar/commit/75cec6d9816) [Transaction] Fix topicTransactionBuffer handle null snapshot (#12758)
* [d13ef6dce16](https://github.com/datastax/pulsar/commit/d13ef6dce16) Update command descriptions from old 'property/cluster/namespace' format to current 'tenant/namespace' format (#10485)
* [48204dfd0db](https://github.com/datastax/pulsar/commit/48204dfd0db) KCA doesn't handle unchecked unchecked ConnectException/KafkaException for the task, it may lead to the connector hanging (#12441)
* [1938b7cd084](https://github.com/datastax/pulsar/commit/1938b7cd084) PIP-85: [pulsar-io] pass pulsar client via context to connector (#11056)
* [b3e2ec0478a](https://github.com/datastax/pulsar/commit/b3e2ec0478a) Remove --illegal-access errors resulting from Google Guice - Pulsar IO, Offloaders and Pulsar SQL - Bump Guice to 5.1.0 (#14300)
* [2289d687afa](https://github.com/datastax/pulsar/commit/2289d687afa) Fix NoClassDefFoundError: com/google/inject/AbstractModule in pulsar-io/batch-data-generator and Jcloud offloader (#14150)
* [56eff2fa4a2](https://github.com/datastax/pulsar/commit/56eff2fa4a2) Remove --illegal-access errors resulting from Google Guice (upgrade to 5.0.1) (#13810)
* [9e612d545bf](https://github.com/datastax/pulsar/commit/9e612d545bf) KCA: Option to sanitize topic name for the conenctors that cannot handle pulsar topic names (#14475)
* [c4f65cb626a](https://github.com/datastax/pulsar/commit/c4f65cb626a) [tools] Pulsar Client: add ability to produce KV messages (#11303)
* [baa8ba47839](https://github.com/datastax/pulsar/commit/baa8ba47839) Functions: add -Dio.netty.tryReflectionSetAccessible=true to Java functions (#12624)
* [a61a38f0de5](https://github.com/datastax/pulsar/commit/a61a38f0de5) [Issue 13651][elastic-search] Fix Elasticsearch Sink Invalid type for uuid encoded as logical types #13652
* [44c624c6794](https://github.com/datastax/pulsar/commit/44c624c6794) [function] fix update user config (#10731)
* [df5f9264b84](https://github.com/datastax/pulsar/commit/df5f9264b84) Issue 12668: Protocol Handlers and Proxy Extensions: ability to use a dedicated EventLoopGroup for IO (#12692)
* [95471cc6ac8](https://github.com/datastax/pulsar/commit/95471cc6ac8) Update PIP-99 rename Proxy Protocol Handler to ProxyExtension
* [997d0c87381](https://github.com/datastax/pulsar/commit/997d0c87381) PIP-93 Pulsar Proxy Protocol Handlers
* [896303cbb3a](https://github.com/datastax/pulsar/commit/896303cbb3a) [Functions] Prevent NPE while stopping a non started Pulsar LogAppender (#12643)
* [62620758889](https://github.com/datastax/pulsar/commit/62620758889) [Issue 11007]  add a version of AUTO_PRODUCE_BYTES that doesn't validate the message in `encode` (#11238)
* [a6e645ee4ac](https://github.com/datastax/pulsar/commit/a6e645ee4ac) Fixed KCA Sink handling of Json and Avro; support for kafka connectors that overload task.preCommit() directly (#11905)
* [5c497c3ab8f](https://github.com/datastax/pulsar/commit/5c497c3ab8f) Include common-io in java function instance (#10939)
* [0af5718d58f](https://github.com/datastax/pulsar/commit/0af5718d58f) [issue 10989 ] Java Client: KeyValueSchema with AutoConsume component - make it work if the topic schema is still not set (#10995)
* [c9a5e19b41d](https://github.com/datastax/pulsar/commit/c9a5e19b41d) [Proxy] Limit replay buffer size in AdminProxyHandler (#10944)
* [1f735343347](https://github.com/datastax/pulsar/commit/1f735343347) Don't create AvroData for each KafkaSourceRecord (#12859)
* [74ca44fba6b](https://github.com/datastax/pulsar/commit/74ca44fba6b) Remove -XX:-ResizePLAB JVM option which degrades performance on JDK11 (#12940)
* [ee3183e3663](https://github.com/datastax/pulsar/commit/ee3183e3663) [pulsar-broker] handle NPE when check active consumer in stats (#12214)
* [7b2022798b2](https://github.com/datastax/pulsar/commit/7b2022798b2) Upgrade debezium to 1.7.1 (#12644)
* [da8bd6f296c](https://github.com/datastax/pulsar/commit/da8bd6f296c) [Client]Allow to override PULSAR_MEM settings via PULSAR_EXTRA_OPS #13381
* [5311ef88da6](https://github.com/datastax/pulsar/commit/5311ef88da6) Function: add possibility to pass additional JVM arguments to the function JVM (additionalJavaRuntimeArguments) (#13282)
* [acbe5e26dd4](https://github.com/datastax/pulsar/commit/acbe5e26dd4) Option to not upload builtin connectors to BK for k8s runtime (#12947)
* [1fb017205e9](https://github.com/datastax/pulsar/commit/1fb017205e9) [configuration]exposeBunlesMetricsInPrometheus (#13460)
* [514938d6148](https://github.com/datastax/pulsar/commit/514938d6148) Non-persistent topic subscription metrics #13827
* [1789e4036b3](https://github.com/datastax/pulsar/commit/1789e4036b3) Fix bundle metrics would overwrite loadbalance metrics (#13641)
* [331db6076a3](https://github.com/datastax/pulsar/commit/331db6076a3) Expose broker bundles  metrics to prometheus (#12366)
* [8aa98f1cd14](https://github.com/datastax/pulsar/commit/8aa98f1cd14) [security] pulsar-io-kafka: upgrade jakarta.el to 3.0.4 to get rid of CVE-2021-28170 #13943
* [265eb12e69e](https://github.com/datastax/pulsar/commit/265eb12e69e) [security] pulsar-io-kafka: upgrade jersey-bean-validation to get rid CVE-2017-7536 (brought in by Hibernate Validator 5.x) (#13868)
* [2a391fe96b6](https://github.com/datastax/pulsar/commit/2a391fe96b6) [security] remove Jackson ASL from kafka-connect-avro-converter-shaded (#13894)
* [c1aa7c6283b](https://github.com/datastax/pulsar/commit/c1aa7c6283b) [Security] Use dependencyManagement to enforce snakeyaml version to 1.30 (#13722)
* [6e6d978568e](https://github.com/datastax/pulsar/commit/6e6d978568e) Updating dependencies (guava and what brought in older guava) to get rid of the guava-related CVE-2018-10237 and CVE-2020-8908 (#13716)
* [79f99a08139](https://github.com/datastax/pulsar/commit/79f99a08139) Upgraded ElasticSearch to get rid of CVEs (and switched client to OpenSearch one) (#13867)
* [5939f8956ca](https://github.com/datastax/pulsar/commit/5939f8956ca) [security] Offloaders - get rid of several CVEs (Log4J included) (#13746)
* [a459761e068](https://github.com/datastax/pulsar/commit/a459761e068) Updating dependencies to get rid of CVEs brought in with kafka and log4j-1.2 libs (#13726)
* [7e6c5f2a516](https://github.com/datastax/pulsar/commit/7e6c5f2a516) Fix the default maxRetries=-1 (#22)
* [f397fd7f1aa](https://github.com/datastax/pulsar/commit/f397fd7f1aa) Add a copyPkFields option to the ES sink (#20)
* [ff10093c3c9](https://github.com/datastax/pulsar/commit/ff10093c3c9) Close the replicator and replication client when delete cluster. (#11342)
* [d316b3c3218](https://github.com/datastax/pulsar/commit/d316b3c3218) Include correct bookkeeper jars in pulsar-client jar (#16)
* [1e8f0a1afa9](https://github.com/datastax/pulsar/commit/1e8f0a1afa9) Upgrade BookKeeper to 4.14.4.1.0.0
* [fb6e0ee1948](https://github.com/datastax/pulsar/commit/fb6e0ee1948) Updated dependencies to get rid of pulsar-io/jdbc related CVE-2020-13692 (#13753)
* [02628b5d0f9](https://github.com/datastax/pulsar/commit/02628b5d0f9) Prevent StackOverFlowException in KEY_SHARED subscription (#14121)
* [e11b6363d87](https://github.com/datastax/pulsar/commit/e11b6363d87) Pulsar IO: implement --retain-key-ordering (KEY_SHARED subscription) for Sinks
* [42b31669879](https://github.com/datastax/pulsar/commit/42b31669879) kubernetesRuntime read metricsPort from kuberbetesRuntimeFactoryConfig
* [e2e575f3c62](https://github.com/datastax/pulsar/commit/e2e575f3c62) Use numeric uid in Dockerfile's USER to overcome issue with runAsNonRoot
* [dd74c86248d](https://github.com/datastax/pulsar/commit/dd74c86248d) [Broker] Fix race condition in stopping replicator while it is starting
* [349218606af](https://github.com/datastax/pulsar/commit/349218606af) [Java Client] Improve state changes to Connecting
* [91c6dc9f5ba](https://github.com/datastax/pulsar/commit/91c6dc9f5ba) suppress nashorn warning in JDK11 runtime
* [d46b3e9e898](https://github.com/datastax/pulsar/commit/d46b3e9e898) fix compile due to different grpc versions from Pulsar and BookKeeper
* [2df9cbff473](https://github.com/datastax/pulsar/commit/2df9cbff473) BookKeeper: use com.datastax.oss dependency and bump to 4.14.3.1.0.0
* [c2ef2de5659](https://github.com/datastax/pulsar/commit/c2ef2de5659) ManagedLedger - EntryCacheImpl - move spammy log to TRACE level
* [dd4aacf1f05](https://github.com/datastax/pulsar/commit/dd4aacf1f05) Debezium Oracle Source (#11520)
* [a815516416c](https://github.com/datastax/pulsar/commit/a815516416c) New distro groupId 'com.datastax.oss'
* [408902fee70](https://github.com/datastax/pulsar/commit/408902fee70) [Pulsar IO] ElasticSearch Sink: support Fixed and ENUM datatypes
* [49f83be16d8](https://github.com/datastax/pulsar/commit/49f83be16d8) Upgrade Debezium to v.1.5.4 (last buildable with Java 8)
* [aa4f8780111](https://github.com/datastax/pulsar/commit/aa4f8780111) Debezium: Make pulsar.auth.token optional (and make Integration Tests pass)
* [9a273f439e8](https://github.com/datastax/pulsar/commit/9a273f439e8) Remove Pulsar Standalone Docker image builder
* [122ec123fba](https://github.com/datastax/pulsar/commit/122ec123fba) Remove Pulsar Dashboard
* [e4e26a1c122](https://github.com/datastax/pulsar/commit/e4e26a1c122) [Issue 8751] Update Dockerfile for Pulsar and Dashboard to Create and Use pulsar User (nonroot user) (#8796)
* [cbbd1f02151](https://github.com/datastax/pulsar/commit/cbbd1f02151) Implement createIndexIfNeeded option and upgrade ES container in tests
* [5a4b98c5a08](https://github.com/datastax/pulsar/commit/5a4b98c5a08) Enhanced ES-sink connector
* [fc1b6d57e8c](https://github.com/datastax/pulsar/commit/fc1b6d57e8c) Add fsGroup to Pod context for function StatefulSet
* [624df376e84](https://github.com/datastax/pulsar/commit/624df376e84) Enable Function subscription naming workaround when activated
* [f9994912191](https://github.com/datastax/pulsar/commit/f9994912191) function container run as group 10001 mount function user token from k8s secret as 400 permission for rootless container
* [3e2aea21ab2](https://github.com/datastax/pulsar/commit/3e2aea21ab2) Add presto password authenticators plugin to enable password auth in Pulsar SQL
* [c8e4920c50e](https://github.com/datastax/pulsar/commit/c8e4920c50e) upgrade presto version to 334 and JDK11
* [17dc4ee4328](https://github.com/datastax/pulsar/commit/17dc4ee4328) Docker image: add vim and nettools (netstat)
* [af59594f77a](https://github.com/datastax/pulsar/commit/af59594f77a) Always return from trigger even if read from output topic times out
* [bc54b6a688a](https://github.com/datastax/pulsar/commit/bc54b6a688a) auth token for debezium and kafka connect adaptor

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-1.0.3.nar
* pulsar-io-data-generator-2.8.3.1.0.5.nar
* pulsar-io-debezium-mongodb-2.8.3.1.0.5.nar
* pulsar-io-debezium-mssql-2.8.3.1.0.5.nar
* pulsar-io-debezium-mysql-2.8.3.1.0.5.nar
* pulsar-io-debezium-oracle-2.8.3.1.0.5.nar
* pulsar-io-debezium-postgres-2.8.3.1.0.5.nar
* pulsar-io-elastic-search-2.8.3.1.0.5.nar
* pulsar-io-jdbc-clickhouse-2.8.3.1.0.5.nar
* pulsar-io-jdbc-mariadb-2.8.3.1.0.5.nar
* pulsar-io-jdbc-postgres-2.8.3.1.0.5.nar
* pulsar-io-jdbc-sqlite-2.8.3.1.0.5.nar
* pulsar-io-kafka-2.8.3.1.0.5.nar
* pulsar-io-kinesis-2.8.3.1.0.5.nar
* pulsar-snowflake-connector-0.1.7.nar
* pulsar-protocol-handler-kafka-2.8.0.1.0.16.nar
* starlight-rabbitmq-2.8.0.1.1.27-ls-1.nar
* pulsar-kafka-proxy-2.8.0.1.0.16.nar
