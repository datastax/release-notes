# Release notes for DataStax Luna Streaming Distribution
 
## About DataStax Luna Streaming Distribution
Luna Streaming Distribution 2.10 is compatible with Apache Pulsar&trade; 2.10.0 and subsequent releases.

### Components

   * [Datastax Luna Streaming](https://github.com/datastax/pulsar) (Apache Pulsar 2.10 fork)
   * [Datastax BookKeeper](https://github.com/datastax/bookkeeper) (Apache BookKeeper fork)
   * DataStax Burnell
   * DataStax Pulsar Admin Console
   * DataStax Pulsar Heartbeat
   * DataStax Apache Pulsar Cassandra Sink
   * DataStax Apache Pulsar Cassandra Source
   * DataStax Starlight For Kafka
   * DataStax Starlight For RabbitMQ
   * DataStax Starlight For JMS Broker filter
   * DataStax Snowflake connector
   
 
This release adds these features to the original Apache Pulsar 2.10 release:
  
   * Stability improvements
   * Third party libraries updates for security fixes
   * Dependency upgrades (for security, stability and performances)
   * An enhanced ElasticSearch Pulsar IO Sink
   * An enhanced version of Apache BookKeeper with security fixes
   * Apache ZooKeeper 3.8.0
 
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

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


### Upgrade considerations for Luna Streaming Distribution 2.10

As with Luna Streaming 2.7, this release uses non-root containers for enhanced security. When upgrading from a previous version (for example, 2.6.2_1.0.1), files created while running that version will have root permissions and will not be readable by containers running the new version.

To fix this, manually log into the ZooKeeper, BookKeeper, and Function Worker containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs` directories are owned by UID 10000 (user pulsar). The group ID of the files should also be set to GID 10001 (group pulsar). Here is an example command:

```
chown -R 10000:10001 /pulsar/data
```

If you are using the Luna Streaming Helm chart, you can enable automatic repair of the permissions using the `fixRootlessPermissions` setting to solve this problem. For more details on this setting, go [here](https://github.com/datastax/pulsar-helm-chart).

If you are upgrading from Luna Streaming Distribution 2.8.0 or 2.8.3, you don't have to do any particular action.

### Upgrade considerations for custom Pulsar Functions and Pulsar IO Connectors

If you are upgrading from Apache Pulsar 2.7.0 or Luna Streaming 2.7.2 you may need to recompile your Pulsar Functions or Pulsar IO Connectors using Apache Pulsar 2.8.0 as a dependency.
This is because there is a breaking API change in Apache Pulsar 2.8.0 (and therefore in Luna Streaming 2.8.0) related to the `SchemaInfo` java class.
More context [here](https://github.com/apache/pulsar/issues/11338).

If you are upgrading from Luna Streaming Distribution 2.8.0 or 2.8.3, you don't have to do any particular action.

### Packaging

Luna Streaming Distribution comes with different packages tooled for different purposes. 
The distributions are available as Docker images and tarballs, and both methods follow the same packaging patterns.

#### Patterns

* **lunastreaming**: the basic Luna Streaming Distribution **including Pulsar SQL** feature.
* **lunastreaming-core**: the basic Luna Streaming Distribution **without Pulsar SQL** feature. Pick this distribution if you don't need Pulsar SQL features.
* **lunastreaming-all**: contains the Core Luna Streaming Distribution, including **Pulsar Offloaders** and the **Datastax Pulsar IO Connectors** listed above. Pick this distribution if you want the Datastax connectors or the offloading feature.
* **lunastreaming-experimental**: extends the **all** distribution with experimental features and connectors. This distribution is only available as a Docker image.


# Releases

## Luna Streaming Distribution 2.10 1.6
This release contains new features, improvements and stability updates.

### Most notable commits
* [4eea638d6ff](https://github.com/datastax/pulsar/commit/4eea638d6ff) fix duplicate calculation for msgRateIn and msgThroughputIn in replication stats (#15062)
* [a6d8016acdf](https://github.com/datastax/pulsar/commit/a6d8016acdf) Issue 17588: Allow deletion of a namespace that was left in deleted status
* [8659d3f4d23](https://github.com/datastax/pulsar/commit/8659d3f4d23) [fix][functions] Fix K8S download function method with auth enabled
* [224e49e9142](https://github.com/datastax/pulsar/commit/224e49e9142) [PIP-193] Support Transform Function with LocalRunner (#17445)
* [1bca43290a1](https://github.com/datastax/pulsar/commit/1bca43290a1) Factorize code in LocalRunner (#17400)
* [c4c6eb708e1](https://github.com/datastax/pulsar/commit/c4c6eb708e1) [fix][broker] Fix issue where leader broker information isn't available after 10 minutes (#17401)
* [ff0875233e9](https://github.com/datastax/pulsar/commit/ff0875233e9) Use `safeRun` to log thread exception. (#17484)
* [6c7fdf204e0](https://github.com/datastax/pulsar/commit/6c7fdf204e0) [feature][broker] Allow to configure the entry filters per namespace and per topic (#17153)
* [ea426df578f](https://github.com/datastax/pulsar/commit/ea426df578f) [fix][broker] Fix calculate avg message per entry (#17046)
* [08761296664](https://github.com/datastax/pulsar/commit/08761296664) Bump dependency check and spring version to avoid potential FP (#15408)
* [f08b7dca6fd](https://github.com/datastax/pulsar/commit/f08b7dca6fd) [fix][sec] bump snakeyaml to 1.31 fix CVE-2022-25857 (#17457)
* [fa06cac1eb2](https://github.com/datastax/pulsar/commit/fa06cac1eb2) [improve][cli] Pulsar shell: fix custom commands autocompletion
* [725f3284d83](https://github.com/datastax/pulsar/commit/725f3284d83) [improve][cli] CLI extensions: rename default location to 'cliextensions' (#17435)
* [bb0b94bf9bc](https://github.com/datastax/pulsar/commit/bb0b94bf9bc) [fix][broker] Increment topic stats outbound message counters after messages have been written to the TCP/IP connection (#17043)
* [894fde1bb27](https://github.com/datastax/pulsar/commit/894fde1bb27) Revert "[Fix][Flaky-test] Fix testConsumeTxnMessage (#16981)"
* [a9653884483](https://github.com/datastax/pulsar/commit/a9653884483) Upgrade debezium to 1.9.5 (#17340)
* [8b131d7f533](https://github.com/datastax/pulsar/commit/8b131d7f533) Fix OutputRecordSinkRecord getValue and getSchema (#17434)
* [dbf3b5923f4](https://github.com/datastax/pulsar/commit/dbf3b5923f4) [Fix][Flaky-test] Fix testConsumeTxnMessage (#16981)
* [3275c82b9ee](https://github.com/datastax/pulsar/commit/3275c82b9ee) [fix][broker] Support loadBalancerSheddingIntervalMinutes dynamic configuration (#16408)
* [013cb0111fe](https://github.com/datastax/pulsar/commit/013cb0111fe) [fix][connector] IOConfigUtils support required and defaultValue annotations (#16785)
* [b7e91927573](https://github.com/datastax/pulsar/commit/b7e91927573) [fix][flaky-test] testSplitBundleForMultiTimes (#16562)
* [6de8ecae848](https://github.com/datastax/pulsar/commit/6de8ecae848) [improve][CI] Cancel duplicate build jobs for maintenance branches
* [98712542799](https://github.com/datastax/pulsar/commit/98712542799) [fix][broker]ManagedLedger metrics fail cause of zero period (#17257)
* [ff22fb84e54](https://github.com/datastax/pulsar/commit/ff22fb84e54) [fix][broker] Remove timestamp from broker metrics (#129)
* [b980f73909c](https://github.com/datastax/pulsar/commit/b980f73909c) [PIP-193] [feature][connectors] Add support for a transform Function in Sinks (#16740)
* [7b9c433963e](https://github.com/datastax/pulsar/commit/7b9c433963e) [fix][functions] Fix netty.DnsResolverUtil compat issue on JDK9+ for the function Runtimes (#16423)
* [45f373a2232](https://github.com/datastax/pulsar/commit/45f373a2232) [cleanup][functions] Remove unused code (#16472)
* [8ec343ff4b2](https://github.com/datastax/pulsar/commit/8ec343ff4b2) [fix][cli] Exclude windows script from the docker image

### `lunastreaming-all` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.5 | cassandra-enhanced-pulsar-sink-1.6.5-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.6 | pulsar-io-data-generator-2.10.1.6.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.6 | pulsar-io-elastic-search-2.10.1.6.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.6 | pulsar-io-jdbc-clickhouse-2.10.1.6.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.6 | pulsar-io-jdbc-mariadb-2.10.1.6.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.6 | pulsar-io-jdbc-postgres-2.10.1.6.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.6 | pulsar-io-jdbc-sqlite-2.10.1.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.6 | pulsar-io-kafka-2.10.1.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.6 | pulsar-io-kinesis-2.10.1.6.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.1 | pulsar-cassandra-source-2.2.1.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.6 | pulsar-io-data-generator-2.10.1.6.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.6 | pulsar-io-debezium-mongodb-2.10.1.6.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.6 | pulsar-io-debezium-mssql-2.10.1.6.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.6 | pulsar-io-debezium-mysql-2.10.1.6.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.6 | pulsar-io-debezium-oracle-2.10.1.6.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.6 | pulsar-io-debezium-postgres-2.10.1.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.6 | pulsar-io-kafka-2.10.1.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.6 | pulsar-io-kinesis-2.10.1.6.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.0.0 | pulsar-transformations-2.0.0.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.9 | pulsar-jms-2.4.9-nar.nar |

</details>

### `lunastreaming-experimental` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.5 | cassandra-enhanced-pulsar-sink-1.6.5-nar.nar |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [aerospike](https://pulsar.apache.org/docs/io-connectors) | Aerospike database sink | 2.10.1.6 | pulsar-io-aerospike-2.10.1.6.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.6 | pulsar-io-batch-data-generator-2.10.1.6.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.6 | pulsar-io-data-generator-2.10.1.6.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.6 | pulsar-io-elastic-search-2.10.1.6.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.6 | pulsar-io-flume-2.10.1.6.nar |
| [hbase](https://pulsar.apache.org/docs/io-connectors) | Writes data into hbase table | 2.10.1.6 | pulsar-io-hbase-2.10.1.6.nar |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 2.x | 2.10.1.6 | pulsar-io-hdfs2-2.10.1.6.nar |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 3.x | 2.10.1.6 | pulsar-io-hdfs3-2.10.1.6.nar |
| [influxdb](https://pulsar.apache.org/docs/io-connectors) | Writes data into InfluxDB database | 2.10.1.6 | pulsar-io-influxdb-2.10.1.6.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.6 | pulsar-io-jdbc-clickhouse-2.10.1.6.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.6 | pulsar-io-jdbc-mariadb-2.10.1.6.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.6 | pulsar-io-jdbc-postgres-2.10.1.6.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.6 | pulsar-io-jdbc-sqlite-2.10.1.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.6 | pulsar-io-kafka-2.10.1.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.6 | pulsar-io-kinesis-2.10.1.6.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.6 | pulsar-io-mongo-2.10.1.6.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.6 | pulsar-io-rabbitmq-2.10.1.6.nar |
| [redis](https://pulsar.apache.org/docs/io-connectors) | Writes data into Redis | 2.10.1.6 | pulsar-io-redis-2.10.1.6.nar |
| [solr](https://pulsar.apache.org/docs/io-connectors) | Writes data into solr collection | 2.10.1.6 | pulsar-io-solr-2.10.1.6.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.1 | pulsar-cassandra-source-2.2.1.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.6 | pulsar-io-batch-data-generator-2.10.1.6.nar |
| [canal](https://pulsar.apache.org/docs/io-connectors) | canal source and read data from mysql | 2.10.1.6 | pulsar-io-canal-2.10.1.6.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.6 | pulsar-io-data-generator-2.10.1.6.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.6 | pulsar-io-debezium-mongodb-2.10.1.6.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.6 | pulsar-io-debezium-mssql-2.10.1.6.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.6 | pulsar-io-debezium-mysql-2.10.1.6.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.6 | pulsar-io-debezium-oracle-2.10.1.6.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.6 | pulsar-io-debezium-postgres-2.10.1.6.nar |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors) | DynamoDB connectors | 2.10.1.6 | pulsar-io-dynamodb-2.10.1.6.nar |
| [file](https://pulsar.apache.org/docs/io-connectors) | Reads data from local filesystem | 2.10.1.6 | pulsar-io-file-2.10.1.6.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.6 | pulsar-io-flume-2.10.1.6.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.6 | pulsar-io-kafka-2.10.1.6.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.6 | pulsar-io-kinesis-2.10.1.6.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.6 | pulsar-io-mongo-2.10.1.6.nar |
| [netty](https://pulsar.apache.org/docs/io-connectors) | Netty Tcp or Udp Source Connector | 2.10.1.6 | pulsar-io-netty-2.10.1.6.nar |
| [nsq](https://pulsar.apache.org/docs/io-connectors) | Ingest data from an NSQ topic | 2.10.1.6 | pulsar-io-nsq-2.10.1.6.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.6 | pulsar-io-rabbitmq-2.10.1.6.nar |
| [twitter](https://pulsar.apache.org/docs/io-connectors) | Ingest data from Twitter firehose | 2.10.1.6 | pulsar-io-twitter-2.10.1.6.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 2.0.0 | pulsar-transformations-2.0.0.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.9 | pulsar-jms-2.4.9-nar.nar |

</details>


## Luna Streaming Distribution 2.10 1.5
This is a release containing important stability, security updates and enhancements.
### Most notable commits

* [83cef793765](https://github.com/datastax/pulsar/commit/83cef793765) Clean up the ledgers cache in PendingReadsManager (#126)
* [39eeb760851](https://github.com/datastax/pulsar/commit/39eeb760851) [improve][dependency] Upgrade JNA to 5.12.1 (#17262)
* [4271c184a69](https://github.com/datastax/pulsar/commit/4271c184a69) [improve][cli] Pulsar shell, Pulsar admin, Pulsar client and Pulsar perf: support for Windows (#17243)
* [c361cf315cd](https://github.com/datastax/pulsar/commit/c361cf315cd) [fix][tiered-storage] Fix the wrong secret key name get from env (#15814)
* [8bcb0464b77](https://github.com/datastax/pulsar/commit/8bcb0464b77) [fix][client] Fix the message present in incoming queue after go to DLQ (#17326)
* [255d489bdb6](https://github.com/datastax/pulsar/commit/255d489bdb6) [improve][functions][admin] Improve the package download process (#16365)
* [2c45fb008f4](https://github.com/datastax/pulsar/commit/2c45fb008f4) [Branch-2.10] [fix] [broker] Fix bookeeper packages npe (#17291)
* [d33b6b1ddf1](https://github.com/datastax/pulsar/commit/d33b6b1ddf1) [fix][client] Fix reach redeliverCount client can't send batch messages to DLQ (#17317)
* [b6d43cb34d2](https://github.com/datastax/pulsar/commit/b6d43cb34d2) [fix][client] Fix reach redeliverCount client can't send messages to DLQ (#17287)
* [f84a5cef499](https://github.com/datastax/pulsar/commit/f84a5cef499) [fix][cpp] Fix multi-topics consumer close segmentation fault (#17239)
* [c4d93b23f41](https://github.com/datastax/pulsar/commit/c4d93b23f41) [improve][client-c++] Use an atomic `state_` instead of the lock to improve performance (#16940)
* [513d308c27a](https://github.com/datastax/pulsar/commit/513d308c27a) [fix][broker] Fix pulsarLedgerIdGenerator can't delete index path when zk metadata store config rootPath. (#17192)
* [c27363b4d8f](https://github.com/datastax/pulsar/commit/c27363b4d8f) [fix][broker] Fix broker cache eviction of entries read by active cursors (#17273)
* [201cf0bb316](https://github.com/datastax/pulsar/commit/201cf0bb316) Pending cache reads: reuse pending reads that partially overlaps
* [3d1d175a2a3](https://github.com/datastax/pulsar/commit/3d1d175a2a3) [enh][broker] Allow to leverage pending reads with partial coverage (#120) - fix metrics
* [0427838f134](https://github.com/datastax/pulsar/commit/0427838f134) [enh][broker] Allow to leverage pending reads with partial coverage (#120)
* [3f9f557a256](https://github.com/datastax/pulsar/commit/3f9f557a256) Pulsar shell: allow custom commands (#119)
* [4b61d7d6bd0](https://github.com/datastax/pulsar/commit/4b61d7d6bd0) Remove import in RangeEntryCacheImpl to fix checkstyle
* [cc490b8eeb9](https://github.com/datastax/pulsar/commit/cc490b8eeb9) [fix][broker] Revert 5895: fix redeliveryCount (#17060)
* [f3ce1be9bb1](https://github.com/datastax/pulsar/commit/f3ce1be9bb1) [fix][function] Use the schema set by the Function when it returns a Record (#17142)
* [d27ba9dc79f](https://github.com/datastax/pulsar/commit/d27ba9dc79f) [fix][functions] Make mandatory to provide a schema in Context::newOutputRecordBuilder (#17118)
* [925072f6414](https://github.com/datastax/pulsar/commit/925072f6414) [managed-ledger] prevent sending duplicate reads to BK/offloaders
* [d0c3087d391](https://github.com/datastax/pulsar/commit/d0c3087d391) [enh][broker] Add metrics for entry cache insertion, eviction
* [d0d4ee26637](https://github.com/datastax/pulsar/commit/d0d4ee26637) [fix][broker] Make timestamp fields thread safe by using volatile
* [34934aabb03](https://github.com/datastax/pulsar/commit/34934aabb03) PIP-201 Extensions mechanism for Pulsar Admin CLI tools (#111)
* [3e4dd4bfb5e](https://github.com/datastax/pulsar/commit/3e4dd4bfb5e) [fix][cli] Pulsar shell: fix using directory '?' in the docker image (#17185)
* [68c1907f9da](https://github.com/datastax/pulsar/commit/68c1907f9da) [fix][broker] Avoid messages being repeatedly replayed with SHARED subscriptions (streaming dispatcher)  (#17163)
* [82bf2ede48d](https://github.com/datastax/pulsar/commit/82bf2ede48d) [fix][broker] Streaming dispatcher stuck after reading the first entry
* [478bf0869b7](https://github.com/datastax/pulsar/commit/478bf0869b7) [fix][broker] Fix out of order data replication (#17154)
* [6bbc9c8d288](https://github.com/datastax/pulsar/commit/6bbc9c8d288) [fix][broker] Fix schema does not replicate successfully (#17049)
* [b2b4ba2a209](https://github.com/datastax/pulsar/commit/b2b4ba2a209) [Fix][Client] Fixed cnx channel Inactive causing the request fail to time out and fail to return (#17051)
* [4d0e3b27c61](https://github.com/datastax/pulsar/commit/4d0e3b27c61) Pulsar-perf produce add possibility to set eventTime on messages
* [cd9f48336a9](https://github.com/datastax/pulsar/commit/cd9f48336a9) [broker][monitoring] add per-subscription EntryFilter metrics (#16932)

### `lunastreaming-all` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.4 | cassandra-enhanced-pulsar-sink-1.6.4-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.5 | pulsar-io-data-generator-2.10.1.5.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.5 | pulsar-io-elastic-search-2.10.1.5.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.5 | pulsar-io-jdbc-clickhouse-2.10.1.5.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.5 | pulsar-io-jdbc-mariadb-2.10.1.5.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.5 | pulsar-io-jdbc-postgres-2.10.1.5.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.5 | pulsar-io-jdbc-sqlite-2.10.1.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.5 | pulsar-io-kafka-2.10.1.5.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.5 | pulsar-io-kinesis-2.10.1.5.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.1 | pulsar-cassandra-source-2.2.1.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.5 | pulsar-io-data-generator-2.10.1.5.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.5 | pulsar-io-debezium-mongodb-2.10.1.5.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.5 | pulsar-io-debezium-mssql-2.10.1.5.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.5 | pulsar-io-debezium-mysql-2.10.1.5.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.5 | pulsar-io-debezium-oracle-2.10.1.5.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.5 | pulsar-io-debezium-postgres-2.10.1.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.5 | pulsar-io-kafka-2.10.1.5.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.5 | pulsar-io-kinesis-2.10.1.5.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.6 | pulsar-jms-2.4.6-nar.nar |

</details>

### `lunastreaming-experimental` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.4 | cassandra-enhanced-pulsar-sink-1.6.4-nar.nar |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [aerospike](https://pulsar.apache.org/docs/io-connectors) | Aerospike database sink | 2.10.1.5 | pulsar-io-aerospike-2.10.1.5.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.5 | pulsar-io-batch-data-generator-2.10.1.5.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.5 | pulsar-io-data-generator-2.10.1.5.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.5 | pulsar-io-elastic-search-2.10.1.5.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.5 | pulsar-io-flume-2.10.1.5.nar |
| [hbase](https://pulsar.apache.org/docs/io-connectors) | Writes data into hbase table | 2.10.1.5 | pulsar-io-hbase-2.10.1.5.nar |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 2.x | 2.10.1.5 | pulsar-io-hdfs2-2.10.1.5.nar |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 3.x | 2.10.1.5 | pulsar-io-hdfs3-2.10.1.5.nar |
| [influxdb](https://pulsar.apache.org/docs/io-connectors) | Writes data into InfluxDB database | 2.10.1.5 | pulsar-io-influxdb-2.10.1.5.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.5 | pulsar-io-jdbc-clickhouse-2.10.1.5.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.5 | pulsar-io-jdbc-mariadb-2.10.1.5.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.5 | pulsar-io-jdbc-postgres-2.10.1.5.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.5 | pulsar-io-jdbc-sqlite-2.10.1.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.5 | pulsar-io-kafka-2.10.1.5.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.5 | pulsar-io-kinesis-2.10.1.5.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.5 | pulsar-io-mongo-2.10.1.5.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.5 | pulsar-io-rabbitmq-2.10.1.5.nar |
| [redis](https://pulsar.apache.org/docs/io-connectors) | Writes data into Redis | 2.10.1.5 | pulsar-io-redis-2.10.1.5.nar |
| [solr](https://pulsar.apache.org/docs/io-connectors) | Writes data into solr collection | 2.10.1.5 | pulsar-io-solr-2.10.1.5.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.2.1 | pulsar-cassandra-source-2.2.1.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.5 | pulsar-io-batch-data-generator-2.10.1.5.nar |
| [canal](https://pulsar.apache.org/docs/io-connectors) | canal source and read data from mysql | 2.10.1.5 | pulsar-io-canal-2.10.1.5.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.5 | pulsar-io-data-generator-2.10.1.5.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.5 | pulsar-io-debezium-mongodb-2.10.1.5.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.5 | pulsar-io-debezium-mssql-2.10.1.5.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.5 | pulsar-io-debezium-mysql-2.10.1.5.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.5 | pulsar-io-debezium-oracle-2.10.1.5.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.5 | pulsar-io-debezium-postgres-2.10.1.5.nar |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors) | DynamoDB connectors | 2.10.1.5 | pulsar-io-dynamodb-2.10.1.5.nar |
| [file](https://pulsar.apache.org/docs/io-connectors) | Reads data from local filesystem | 2.10.1.5 | pulsar-io-file-2.10.1.5.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.5 | pulsar-io-flume-2.10.1.5.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.5 | pulsar-io-kafka-2.10.1.5.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.5 | pulsar-io-kinesis-2.10.1.5.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.5 | pulsar-io-mongo-2.10.1.5.nar |
| [netty](https://pulsar.apache.org/docs/io-connectors) | Netty Tcp or Udp Source Connector | 2.10.1.5 | pulsar-io-netty-2.10.1.5.nar |
| [nsq](https://pulsar.apache.org/docs/io-connectors) | Ingest data from an NSQ topic | 2.10.1.5 | pulsar-io-nsq-2.10.1.5.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.5 | pulsar-io-rabbitmq-2.10.1.5.nar |
| [twitter](https://pulsar.apache.org/docs/io-connectors) | Ingest data from Twitter firehose | 2.10.1.5 | pulsar-io-twitter-2.10.1.5.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.6 | pulsar-jms-2.4.6-nar.nar |

</details>


## Luna Streaming Distribution 2.10 1.4
This is a maintenance release containing important security and stability updates.

### Most notable commits
* [f1caacc0794](https://github.com/datastax/pulsar/commit/f1caacc0794) [feat][connector] ElasticSearch Sink: add ignoreUnsupportedFields option
* [fd321a75e30](https://github.com/datastax/pulsar/commit/fd321a75e30) [improve][proxy] Consolidate Netty channel flushes to mitigate syscall overhead (#16372)
* [c2b346da480](https://github.com/datastax/pulsar/commit/c2b346da480) [cleanup][broker] Follow up on #16968 to restore some behavior in PersistentDispatcherMultipleConsumers class (#17018)
* [bb8ef6e6665](https://github.com/datastax/pulsar/commit/bb8ef6e6665) Fix ut MessageDispatchThrottlingTest#testDispatchRateCompatibility2 (#15999)
* [36eed47eeb9](https://github.com/datastax/pulsar/commit/36eed47eeb9) [clean][broker]Cleanup DispatchRateLimiter#onPoliciesUpdate #15986
* [9d21e1a8a41](https://github.com/datastax/pulsar/commit/9d21e1a8a41) Upgrade DS Bookkeeper to 4.14.5.1.0.2
* [414578b8582](https://github.com/datastax/pulsar/commit/414578b8582) [fix][broker]Prevent `StackOverFlowException` in SHARED subscription(#16968)
* [f120e61d73c](https://github.com/datastax/pulsar/commit/f120e61d73c) [fix][security] Bump PostgreSQL version to 42.4.1(#17066)
* [16c93e5a1a4](https://github.com/datastax/pulsar/commit/16c93e5a1a4) [improve][authentication] Support for get token from HTTP params (#16986)
* [4d3fc2e3153](https://github.com/datastax/pulsar/commit/4d3fc2e3153) [branch-2.10][cherry-pick] Fix topic dispatch rate limiter not init on broker-level #16084 (#17000)
* [f87e765221d](https://github.com/datastax/pulsar/commit/f87e765221d) Fix failed test introduced by cherry-pick, according to https://github.com/apache/pulsar/pull/16971/files\#diff-6e09b03081dd6077066c65b656ed10be6125d2b7fc9a12c9a78d391afbb6b081R72-R99
* [07f90d135cf](https://github.com/datastax/pulsar/commit/07f90d135cf) [fix][client] Remove redundant check for chunked message TotalChunkMsgSize in ConsumerImpl (#16797)
* [30ce121fd1c](https://github.com/datastax/pulsar/commit/30ce121fd1c) [improve][test] Verify the authentication data in the authorization provider (#16900)
* [23038927125](https://github.com/datastax/pulsar/commit/23038927125) [improve][authentication] Adapt basic authentication configuration with prefix (#16935)
* [713a9f45c57](https://github.com/datastax/pulsar/commit/713a9f45c57) [improve][authentication] Improve get the basic authentication config (#16526)
* [f848de61bce](https://github.com/datastax/pulsar/commit/f848de61bce) [fix][function] Fix python instance not process zip file correctly (#16697)
* [d68dd3b9d04](https://github.com/datastax/pulsar/commit/d68dd3b9d04) [fix][broker] PulsarLedgerManager to pass correct error code to BK client (#16857)
* [eeb2ed27c95](https://github.com/datastax/pulsar/commit/eeb2ed27c95) [fix][client]Fix MaxQueueSize semaphore release leak in createOpSendMsg (#16915)
* [12a18d57612](https://github.com/datastax/pulsar/commit/12a18d57612) fix Flaky-test: PulsarFunctionLocalRunTest.testE2EPulsarFunctionLocalRunMultipleInstance (#16872)
* [6048307a072](https://github.com/datastax/pulsar/commit/6048307a072) [fix][broker] Upgrade log4j2 version to 2.18.0 (#16884)
* [bbcbe080e53](https://github.com/datastax/pulsar/commit/bbcbe080e53) [fix][client]Fix client memory limit currentUsage leak and semaphore release duplicated in ProducerImpl (#16837)
* [94968bd35c9](https://github.com/datastax/pulsar/commit/94968bd35c9) [Java Client] Send CloseConsumer on timeout (#16616)
* [38a1e475cbd](https://github.com/datastax/pulsar/commit/38a1e475cbd) fix PatternTopicsChangedListener blocked when topic removed (#16842)
* [1d4b4a3560f](https://github.com/datastax/pulsar/commit/1d4b4a3560f) [fix][client] Fix load trust certificate (#16789)
* [e04377608b9](https://github.com/datastax/pulsar/commit/e04377608b9) [fix][broker] ManagedCursor: mark delete no callback when create meta-ledger fail (#16841)
* [d09899fdbfa](https://github.com/datastax/pulsar/commit/d09899fdbfa) Forget to update memory usage when invalid message (#16835)
* [27c49838091](https://github.com/datastax/pulsar/commit/27c49838091) [fix][broker] Avoid IllegalStateException while client_version is not set (#16788)
* [e3f4e1f90d4](https://github.com/datastax/pulsar/commit/e3f4e1f90d4) [fix][flaky-test] Fix ClassCastException: BrokerService cannot be cast to class PulsarResources (#16821)
* [e034160de74](https://github.com/datastax/pulsar/commit/e034160de74) [Branch-2.10][Cherry-pick] tidy update subscriptions dispatcher rate-limiter (#16778)
* [d36c40038ab](https://github.com/datastax/pulsar/commit/d36c40038ab) [improve][broker][PIP-149]Make resetCursor async (#16355) (#16774)
* [cb28c46c336](https://github.com/datastax/pulsar/commit/cb28c46c336) [improve][connector] add reader config to `pulsar-io-debezium` and `pulsar-io-kafka-connect-adaptor` (#16675)
* [7fbd450ce16](https://github.com/datastax/pulsar/commit/7fbd450ce16) Fix newLookup TooManyRequestsException message (#16594)
* [c4ad0ed3dfc](https://github.com/datastax/pulsar/commit/c4ad0ed3dfc) [fix][broker] Fix consumer does not abide by the max unacks limitation for Key_Shared subscription (#16718)
* [e9af98ab362](https://github.com/datastax/pulsar/commit/e9af98ab362) [fix][proxy] Do not preserve host when forwarding admin requests. (#16342)
* [622d65da6e4](https://github.com/datastax/pulsar/commit/622d65da6e4) [improve][security] Upgrade aws-java-sdk-s3 to 1.12.261 (#16684)
* [e068ec4eba3](https://github.com/datastax/pulsar/commit/e068ec4eba3) [fix][broker] Retry to delete the namespace if new topics created during the namespace deletion (#16676)
* [8f5dc77b9e3](https://github.com/datastax/pulsar/commit/8f5dc77b9e3) [fix][broker] Fix consumer does not abide by the max unacks limitation for Shared subscription (#16670)
* [2365a03b848](https://github.com/datastax/pulsar/commit/2365a03b848) [fix][broker] The configuration loadBalancerNamespaceMaximumBundles is invalid (#16552)
* [6a0f3381b9b](https://github.com/datastax/pulsar/commit/6a0f3381b9b) [fix][broker] BadVersionException when splitting bundles, delay 100ms and try again (#16612)
* [48810e148fe](https://github.com/datastax/pulsar/commit/48810e148fe)  [improve][client] Add message key if exists to deadLetter messages (#16615)
* [8688b6ab3ff](https://github.com/datastax/pulsar/commit/8688b6ab3ff) Update/fix Swagger Annotation for param: authoritative (#16222)
* [bda6b605ede](https://github.com/datastax/pulsar/commit/bda6b605ede) [fix][function] Ensure bytes is a well-formed UTF-8 byte sequence when decode the `FunctionState` bytes to string (#16199)
* [09d04c8aa01](https://github.com/datastax/pulsar/commit/09d04c8aa01) [improve][security] Add load multiple certificates support in TrustManagerProxy (#14798)
* [fea2d3cc209](https://github.com/datastax/pulsar/commit/fea2d3cc209) [fix][flaky-test] ElasticSearchClientTests.testBulkBlocking (#16920)
* [21e2143dfc1](https://github.com/datastax/pulsar/commit/21e2143dfc1) Add a copyPkFields option to the ES sink (#20)
* [0d8a4b23150](https://github.com/datastax/pulsar/commit/0d8a4b23150) [fix][broker] Duplicate ByteBuffer when Caching Backlogged Consumers (#17105)
* [71763f4867c](https://github.com/datastax/pulsar/commit/71763f4867c) [fix][broker] Fix memory leak if entry exists in cache (#16996)
* [9817b8faed3](https://github.com/datastax/pulsar/commit/9817b8faed3) [pulsar-broker] Support caching to drain backlog consumers (#12258)
* [ff98753da7d](https://github.com/datastax/pulsar/commit/ff98753da7d) [Pulsar Admin CLI Tool] Use NoSplitter for subscription properties
* [e2e31876427](https://github.com/datastax/pulsar/commit/e2e31876427) PIP-187: Add API to analyze a subscription backlog and provide a accurate value
* [6a4f773fcc1](https://github.com/datastax/pulsar/commit/6a4f773fcc1) [fix][proxy] Fix client service url (#16834)
* [cc2b8995fa9](https://github.com/datastax/pulsar/commit/cc2b8995fa9) Fix rack awareness cache expiration race condition (#16825)
* [c86cc77c6be](https://github.com/datastax/pulsar/commit/c86cc77c6be) [Broker] Expose topic level storage write and read rate metrics (#16855)

### `lunastreaming-all` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.4 | pulsar-io-data-generator-2.10.1.4.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.4 | pulsar-io-elastic-search-2.10.1.4.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.4 | pulsar-io-jdbc-clickhouse-2.10.1.4.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.4 | pulsar-io-jdbc-mariadb-2.10.1.4.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.4 | pulsar-io-jdbc-postgres-2.10.1.4.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.4 | pulsar-io-jdbc-sqlite-2.10.1.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.4 | pulsar-io-kafka-2.10.1.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.4 | pulsar-io-kinesis-2.10.1.4.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.4 | pulsar-io-data-generator-2.10.1.4.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.4 | pulsar-io-debezium-mongodb-2.10.1.4.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.4 | pulsar-io-debezium-mssql-2.10.1.4.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.4 | pulsar-io-debezium-mysql-2.10.1.4.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.4 | pulsar-io-debezium-oracle-2.10.1.4.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.4 | pulsar-io-debezium-postgres-2.10.1.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.4 | pulsar-io-kafka-2.10.1.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.4 | pulsar-io-kinesis-2.10.1.4.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>

### `lunastreaming-experimental` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [aerospike](https://pulsar.apache.org/docs/io-connectors) | Aerospike database sink | 2.10.1.4 | pulsar-io-aerospike-2.10.1.4.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.4 | pulsar-io-batch-data-generator-2.10.1.4.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.4 | pulsar-io-data-generator-2.10.1.4.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.4 | pulsar-io-elastic-search-2.10.1.4.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.4 | pulsar-io-flume-2.10.1.4.nar |
| [hbase](https://pulsar.apache.org/docs/io-connectors) | Writes data into hbase table | 2.10.1.4 | pulsar-io-hbase-2.10.1.4.nar |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 2.x | 2.10.1.4 | pulsar-io-hdfs2-2.10.1.4.nar |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 3.x | 2.10.1.4 | pulsar-io-hdfs3-2.10.1.4.nar |
| [influxdb](https://pulsar.apache.org/docs/io-connectors) | Writes data into InfluxDB database | 2.10.1.4 | pulsar-io-influxdb-2.10.1.4.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.4 | pulsar-io-jdbc-clickhouse-2.10.1.4.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.4 | pulsar-io-jdbc-mariadb-2.10.1.4.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.4 | pulsar-io-jdbc-postgres-2.10.1.4.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.4 | pulsar-io-jdbc-sqlite-2.10.1.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.4 | pulsar-io-kafka-2.10.1.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.4 | pulsar-io-kinesis-2.10.1.4.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.4 | pulsar-io-mongo-2.10.1.4.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.4 | pulsar-io-rabbitmq-2.10.1.4.nar |
| [redis](https://pulsar.apache.org/docs/io-connectors) | Writes data into Redis | 2.10.1.4 | pulsar-io-redis-2.10.1.4.nar |
| [solr](https://pulsar.apache.org/docs/io-connectors) | Writes data into solr collection | 2.10.1.4 | pulsar-io-solr-2.10.1.4.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.4 | pulsar-io-batch-data-generator-2.10.1.4.nar |
| [canal](https://pulsar.apache.org/docs/io-connectors) | canal source and read data from mysql | 2.10.1.4 | pulsar-io-canal-2.10.1.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.4 | pulsar-io-data-generator-2.10.1.4.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.4 | pulsar-io-debezium-mongodb-2.10.1.4.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.4 | pulsar-io-debezium-mssql-2.10.1.4.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.4 | pulsar-io-debezium-mysql-2.10.1.4.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.4 | pulsar-io-debezium-oracle-2.10.1.4.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.4 | pulsar-io-debezium-postgres-2.10.1.4.nar |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors) | DynamoDB connectors | 2.10.1.4 | pulsar-io-dynamodb-2.10.1.4.nar |
| [file](https://pulsar.apache.org/docs/io-connectors) | Reads data from local filesystem | 2.10.1.4 | pulsar-io-file-2.10.1.4.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.4 | pulsar-io-flume-2.10.1.4.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.4 | pulsar-io-kafka-2.10.1.4.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.4 | pulsar-io-kinesis-2.10.1.4.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.4 | pulsar-io-mongo-2.10.1.4.nar |
| [netty](https://pulsar.apache.org/docs/io-connectors) | Netty Tcp or Udp Source Connector | 2.10.1.4 | pulsar-io-netty-2.10.1.4.nar |
| [nsq](https://pulsar.apache.org/docs/io-connectors) | Ingest data from an NSQ topic | 2.10.1.4 | pulsar-io-nsq-2.10.1.4.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.4 | pulsar-io-rabbitmq-2.10.1.4.nar |
| [twitter](https://pulsar.apache.org/docs/io-connectors) | Ingest data from Twitter firehose | 2.10.1.4 | pulsar-io-twitter-2.10.1.4.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>

## Luna Streaming Distribution 2.10 1.3
This is a maintenance release containing important stability updates.

### Most notable commits

* [39fc69a944d](https://github.com/datastax/pulsar/commit/39fc69a944d) Reduce Flakyness in PersistentStickyKeyDispatcherMultipleConsumersTest
* [af5441cfef3](https://github.com/datastax/pulsar/commit/af5441cfef3) Broker: Fix KEY_SHARED dispatcher and tests

### `lunastreaming-all` distribution
<details><summary>Filters</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.3 | pulsar-io-elastic-search-2.10.1.3.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.3 | pulsar-io-jdbc-clickhouse-2.10.1.3.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.3 | pulsar-io-jdbc-mariadb-2.10.1.3.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.3 | pulsar-io-jdbc-postgres-2.10.1.3.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.3 | pulsar-io-jdbc-sqlite-2.10.1.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.3 | pulsar-io-debezium-mongodb-2.10.1.3.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.3 | pulsar-io-debezium-mssql-2.10.1.3.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.3 | pulsar-io-debezium-mysql-2.10.1.3.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.3 | pulsar-io-debezium-oracle-2.10.1.3.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.3 | pulsar-io-debezium-postgres-2.10.1.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar |

</details>
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>

### `lunastreaming-experimental` distribution
<details><summary>Filters</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [aerospike](https://pulsar.apache.org/docs/io-connectors) | Aerospike database sink | 2.10.1.3 | pulsar-io-aerospike-2.10.1.3.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.3 | pulsar-io-batch-data-generator-2.10.1.3.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.3 | pulsar-io-elastic-search-2.10.1.3.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.3 | pulsar-io-flume-2.10.1.3.nar |
| [hbase](https://pulsar.apache.org/docs/io-connectors) | Writes data into hbase table | 2.10.1.3 | pulsar-io-hbase-2.10.1.3.nar |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 2.x | 2.10.1.3 | pulsar-io-hdfs2-2.10.1.3.nar |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 3.x | 2.10.1.3 | pulsar-io-hdfs3-2.10.1.3.nar |
| [influxdb](https://pulsar.apache.org/docs/io-connectors) | Writes data into InfluxDB database | 2.10.1.3 | pulsar-io-influxdb-2.10.1.3.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.3 | pulsar-io-jdbc-clickhouse-2.10.1.3.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.3 | pulsar-io-jdbc-mariadb-2.10.1.3.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.3 | pulsar-io-jdbc-postgres-2.10.1.3.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.3 | pulsar-io-jdbc-sqlite-2.10.1.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.3 | pulsar-io-mongo-2.10.1.3.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.3 | pulsar-io-rabbitmq-2.10.1.3.nar |
| [redis](https://pulsar.apache.org/docs/io-connectors) | Writes data into Redis | 2.10.1.3 | pulsar-io-redis-2.10.1.3.nar |
| [solr](https://pulsar.apache.org/docs/io-connectors) | Writes data into solr collection | 2.10.1.3 | pulsar-io-solr-2.10.1.3.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.3 | pulsar-io-batch-data-generator-2.10.1.3.nar |
| [canal](https://pulsar.apache.org/docs/io-connectors) | canal source and read data from mysql | 2.10.1.3 | pulsar-io-canal-2.10.1.3.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.3 | pulsar-io-data-generator-2.10.1.3.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.3 | pulsar-io-debezium-mongodb-2.10.1.3.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.3 | pulsar-io-debezium-mssql-2.10.1.3.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.3 | pulsar-io-debezium-mysql-2.10.1.3.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.3 | pulsar-io-debezium-oracle-2.10.1.3.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.3 | pulsar-io-debezium-postgres-2.10.1.3.nar |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors) | DynamoDB connectors | 2.10.1.3 | pulsar-io-dynamodb-2.10.1.3.nar |
| [file](https://pulsar.apache.org/docs/io-connectors) | Reads data from local filesystem | 2.10.1.3 | pulsar-io-file-2.10.1.3.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.3 | pulsar-io-flume-2.10.1.3.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.3 | pulsar-io-kafka-2.10.1.3.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.3 | pulsar-io-kinesis-2.10.1.3.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.3 | pulsar-io-mongo-2.10.1.3.nar |
| [netty](https://pulsar.apache.org/docs/io-connectors) | Netty Tcp or Udp Source Connector | 2.10.1.3 | pulsar-io-netty-2.10.1.3.nar |
| [nsq](https://pulsar.apache.org/docs/io-connectors) | Ingest data from an NSQ topic | 2.10.1.3 | pulsar-io-nsq-2.10.1.3.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.3 | pulsar-io-rabbitmq-2.10.1.3.nar |
| [twitter](https://pulsar.apache.org/docs/io-connectors) | Ingest data from Twitter firehose | 2.10.1.3 | pulsar-io-twitter-2.10.1.3.nar |

</details>
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>

## Luna Streaming Distribution 2.10 1.2
**NOTE: IF YOU'RE USING THIS VERSION PLEASE UPGRADE TO A NEWER ONE. VERSION 2.10 1.2 CONTAINS STABILITY ISSUES ABOUT KEY_SHARED SUBSCRIPTIONS.**

This is a maintenance release containing important stability updates.

### Most notable commits

* [6c80ce26acb](https://github.com/datastax/pulsar/commit/6c80ce26acb) Issue 16802: fix Repeated messages of shared dispatcher Changes: sendMessagesToConsumer must block reads of new entries otherwise we will end up in reading duplicates
* [73c14dbc968](https://github.com/datastax/pulsar/commit/73c14dbc968) Fix pulsar-experimental-docker-image version
* [e8283824ff7](https://github.com/datastax/pulsar/commit/e8283824ff7) Create -experimental docker image with all the builtin connectors
* [e47236100d1](https://github.com/datastax/pulsar/commit/e47236100d1) KCA: handle kafka's logical schemas
* [a79fbd931bd](https://github.com/datastax/pulsar/commit/a79fbd931bd) [Fix][pulsar-io] KCA: handle kafka preCommit() returning earlier offsets than requested (#16100)
* [3d754337c80](https://github.com/datastax/pulsar/commit/3d754337c80) KCA to use index (if available) instead of sequence and to handle batched messages non-unique sequenceIds (#16098)
* [d14af5c2f94](https://github.com/datastax/pulsar/commit/d14af5c2f94) Fix flaky DelayedDeliveryTest
* [1d552518103](https://github.com/datastax/pulsar/commit/1d552518103) Fix owasp-dependency-check supression file
* [91bf7b5b215](https://github.com/datastax/pulsar/commit/91bf7b5b215) Fixed deadlock in key-shared dispatcher (#16660)
* [83fe4270a78](https://github.com/datastax/pulsar/commit/83fe4270a78) Avoid tracking the delays of all the message when we detect that they are fixed (#16609)
* [650ce37a71c](https://github.com/datastax/pulsar/commit/650ce37a71c) [Branch 2.10] Fix some OWASP dependency problems. (#16260)
* [b9166972de1](https://github.com/datastax/pulsar/commit/b9166972de1) [fix][pulsar-broker] Fix RawReader hasMessageAvailable returns true when no messages (#16443)
* [d64593c907f](https://github.com/datastax/pulsar/commit/d64593c907f) Fix: Make DeadLetterPolicy deserializable (#16513)
* [4847928a3bc](https://github.com/datastax/pulsar/commit/4847928a3bc) [improve][metadataStore] Update namespace policies would cause metadata-store thread waiting too long (#16438)
* [f435dc74981](https://github.com/datastax/pulsar/commit/f435dc74981) [fix][flaky-test] Fix flaky test testConsumerBacklogEvictionTimeQuotaWithEmptyLedger (#16419)
* [165f1ac303b](https://github.com/datastax/pulsar/commit/165f1ac303b) [fix][broker] Retry when DistributedIdGenerator has BadVersion error (#16491)
* [c2122357ee0](https://github.com/datastax/pulsar/commit/c2122357ee0) [improve][test] Fix flaky C++ ClientTest.testWrongListener (#16510)
* [05fff208477](https://github.com/datastax/pulsar/commit/05fff208477) Fix flaky-test: NonPersistentTopicE2ETest.testGC (#16505)
* [9d5108891f1](https://github.com/datastax/pulsar/commit/9d5108891f1) [improve][test] Reduce the time consumption of BacklogQuotaManagerTest (#16550)
* [5fc0731f1c2](https://github.com/datastax/pulsar/commit/5fc0731f1c2) [fix][flaky-test] PersistentFailoverE2ETest.testSimpleConsumerEventsWithPartition (#16493)
* [493f451112d](https://github.com/datastax/pulsar/commit/493f451112d) [fix][test] Catch exception when update data in mockZookeeper (#16473)
* [bc0e10eb487](https://github.com/datastax/pulsar/commit/bc0e10eb487) [fix][test] Fix jvm oom on Unit Test broker group 1 (#16542)
* [f9dd46bbde1](https://github.com/datastax/pulsar/commit/f9dd46bbde1) [fix][broker] Expose timestamp field for SchemaData&SchemaInfo (#16380)
* [77957d8879e](https://github.com/datastax/pulsar/commit/77957d8879e) [fix][flaky-test] MessageTTLTest.testMessageExpiryAfterTopicUnload (#16462)
* [f79fd657a89](https://github.com/datastax/pulsar/commit/f79fd657a89) [fix][broker]Fix getInternalStats occasional lack of LeaderInfo again (#16238)
* [747d5bd70a5](https://github.com/datastax/pulsar/commit/747d5bd70a5) [fix] PulsarLedgerManager: add missed return statement (#16607)

### `lunastreaming-all` distribution
<details><summary>Filters</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.2 | pulsar-io-elastic-search-2.10.1.2.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.2 | pulsar-io-jdbc-clickhouse-2.10.1.2.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.2 | pulsar-io-jdbc-mariadb-2.10.1.2.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.2 | pulsar-io-jdbc-postgres-2.10.1.2.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.2 | pulsar-io-jdbc-sqlite-2.10.1.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.2 | pulsar-io-debezium-mongodb-2.10.1.2.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.2 | pulsar-io-debezium-mssql-2.10.1.2.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.2 | pulsar-io-debezium-mysql-2.10.1.2.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.2 | pulsar-io-debezium-oracle-2.10.1.2.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.2 | pulsar-io-debezium-postgres-2.10.1.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar |

</details>
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>

### `lunastreaming-experimental` distribution
<details><summary>Filters</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [aerospike](https://pulsar.apache.org/docs/io-connectors) | Aerospike database sink | 2.10.1.2 | pulsar-io-aerospike-2.10.1.2.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.2 | pulsar-io-batch-data-generator-2.10.1.2.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.2 | pulsar-io-elastic-search-2.10.1.2.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.2 | pulsar-io-flume-2.10.1.2.nar |
| [hbase](https://pulsar.apache.org/docs/io-connectors) | Writes data into hbase table | 2.10.1.2 | pulsar-io-hbase-2.10.1.2.nar |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 2.x | 2.10.1.2 | pulsar-io-hdfs2-2.10.1.2.nar |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 3.x | 2.10.1.2 | pulsar-io-hdfs3-2.10.1.2.nar |
| [influxdb](https://pulsar.apache.org/docs/io-connectors) | Writes data into InfluxDB database | 2.10.1.2 | pulsar-io-influxdb-2.10.1.2.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.2 | pulsar-io-jdbc-clickhouse-2.10.1.2.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.2 | pulsar-io-jdbc-mariadb-2.10.1.2.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.2 | pulsar-io-jdbc-postgres-2.10.1.2.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.2 | pulsar-io-jdbc-sqlite-2.10.1.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.2 | pulsar-io-mongo-2.10.1.2.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.2 | pulsar-io-rabbitmq-2.10.1.2.nar |
| [redis](https://pulsar.apache.org/docs/io-connectors) | Writes data into Redis | 2.10.1.2 | pulsar-io-redis-2.10.1.2.nar |
| [solr](https://pulsar.apache.org/docs/io-connectors) | Writes data into solr collection | 2.10.1.2 | pulsar-io-solr-2.10.1.2.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.2 | pulsar-io-batch-data-generator-2.10.1.2.nar |
| [canal](https://pulsar.apache.org/docs/io-connectors) | canal source and read data from mysql | 2.10.1.2 | pulsar-io-canal-2.10.1.2.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.2 | pulsar-io-data-generator-2.10.1.2.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.2 | pulsar-io-debezium-mongodb-2.10.1.2.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.2 | pulsar-io-debezium-mssql-2.10.1.2.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.2 | pulsar-io-debezium-mysql-2.10.1.2.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.2 | pulsar-io-debezium-oracle-2.10.1.2.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.2 | pulsar-io-debezium-postgres-2.10.1.2.nar |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors) | DynamoDB connectors | 2.10.1.2 | pulsar-io-dynamodb-2.10.1.2.nar |
| [file](https://pulsar.apache.org/docs/io-connectors) | Reads data from local filesystem | 2.10.1.2 | pulsar-io-file-2.10.1.2.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.2 | pulsar-io-flume-2.10.1.2.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.2 | pulsar-io-kafka-2.10.1.2.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.2 | pulsar-io-kinesis-2.10.1.2.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.2 | pulsar-io-mongo-2.10.1.2.nar |
| [netty](https://pulsar.apache.org/docs/io-connectors) | Netty Tcp or Udp Source Connector | 2.10.1.2 | pulsar-io-netty-2.10.1.2.nar |
| [nsq](https://pulsar.apache.org/docs/io-connectors) | Ingest data from an NSQ topic | 2.10.1.2 | pulsar-io-nsq-2.10.1.2.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.2 | pulsar-io-rabbitmq-2.10.1.2.nar |
| [twitter](https://pulsar.apache.org/docs/io-connectors) | Ingest data from Twitter firehose | 2.10.1.2 | pulsar-io-twitter-2.10.1.2.nar |

</details>
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File |
| ---- | ----------- | ------- | ---- |
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>

## Luna Streaming Distribution 2.10 1.1
This is a maintenance release containing important security and stability updates.
### Most notable commits
* [037b9fc981d](https://github.com/datastax/pulsar/commit/037b9fc981d) Broker: fix Key_Shared dispatcher when using dispatcherDispatchMessagesInSubscriptionThread
* [0f748e6e908](https://github.com/datastax/pulsar/commit/0f748e6e908) [enh] Broker/EntryFilter: make the delay for RESCHEDULED messages configurable (dispatcherFilterRescheduledMessageDelay) (#16602)
* [9fafe31df54](https://github.com/datastax/pulsar/commit/9fafe31df54) Fix PersistentStickyKeyDispatcherMultipleConsumersTest
* [cb28169717c](https://github.com/datastax/pulsar/commit/cb28169717c) [feature][connector] JDBC sinks: support upsert and row deletion (#16448)
* [66d205ad7d4](https://github.com/datastax/pulsar/commit/66d205ad7d4) [fix][test][branch-2.10] Fix test TransactionEndToEndTest#testSendTxnMessageTimeout (only release branches) (#16570)
* [6ae4175d3a0](https://github.com/datastax/pulsar/commit/6ae4175d3a0) Shared subscription: run filters in a separate (per-subscription) thread (dispatcherDispatchMessagesInSubscriptionThread)
* [ab5687f2348](https://github.com/datastax/pulsar/commit/ab5687f2348) Pulsar shell: configs to manage multiple clusters/tenants
* [d62fb98094a](https://github.com/datastax/pulsar/commit/d62fb98094a) [fix][broker] Skip reading more entries for a pending read with no more entries (#16400)
* [7c002e6c4fb](https://github.com/datastax/pulsar/commit/7c002e6c4fb) [fix][security] Upgrade to Jetty to 9.4.48.v20220622 to get rid of CVE-2022-2047 (#16520)
* [6a112d3bff9](https://github.com/datastax/pulsar/commit/6a112d3bff9) cherry-pick [fix][txn] fix pattern sub filter transaction system topic (#16533)
* [2ae0ee032c3](https://github.com/datastax/pulsar/commit/2ae0ee032c3) [fix][broker] Fixed error when delayed messages trackers state grows to >1.5GB (#16490)
* [6ab833340ba](https://github.com/datastax/pulsar/commit/6ab833340ba) Support shrink for TripleLongPriorityQueue (#15936)
* [63980fbf058](https://github.com/datastax/pulsar/commit/63980fbf058) Pulsar Shell: fix sh command and better error message for non-interactive mode failures
* [04610605c47](https://github.com/datastax/pulsar/commit/04610605c47) [fix][txn] Allow producer enable send timeout in transaction (#16519)
* [c03f3cb1590](https://github.com/datastax/pulsar/commit/c03f3cb1590) Fix get non-persistent topics issue in Namespaces. (#16170) (#16514)
* [ef16e303db7](https://github.com/datastax/pulsar/commit/ef16e303db7) [fix][broker] fix No such ledger exception (#16420)
* [2ab1991a0de](https://github.com/datastax/pulsar/commit/2ab1991a0de) [fix][broker] Fix setManagedLedgerOffloadedReadPriority not work. (#16436)
* [43e239ac5eb](https://github.com/datastax/pulsar/commit/43e239ac5eb) [improve][broker] Recycle OpReadEntry in some corner cases (#16399)
* [1c28da327bf](https://github.com/datastax/pulsar/commit/1c28da327bf) [fix][C++ client] Fix the close of Client might stuck or return a wrong result (#16285)
* [e163dc5a752](https://github.com/datastax/pulsar/commit/e163dc5a752) [fix][broker] Release the entry in getEarliestMessagePublishTimeOfPos (#16386)
* [88c907a8743](https://github.com/datastax/pulsar/commit/88c907a8743) Exclude the Netty Reactive Stream from asynchttpclient (#16312)
* [e8534707f76](https://github.com/datastax/pulsar/commit/e8534707f76) [improve][java-client] Improve performance of multi-topic consumer with more than one IO thread (#16336)
* [3f0641573a9](https://github.com/datastax/pulsar/commit/3f0641573a9) [improve][java-client] Support passing existing scheduled executor providers to the client (#16334)
* [a6d97f07848](https://github.com/datastax/pulsar/commit/a6d97f07848) [fix][flaky-test] Fix failed test NonPersistentTopicE2ETest.testGCWillDeleteSchema (#16381)
* [25424651d65](https://github.com/datastax/pulsar/commit/25424651d65) [fix][flaky-test] Try to fix flaky test related to PersistentTopicTest.setup (#16383)
* [643625b9b81](https://github.com/datastax/pulsar/commit/643625b9b81) [fix][flaky-test] Fix failed test PatternTopicsConsumerImplTest.testAutoSubscribePatternConsumer (#16375)
* [23e5ccd480d](https://github.com/datastax/pulsar/commit/23e5ccd480d) [improve][broker] Use shared broker client scheduled executor provider (#16338)
* [8611de81c4f](https://github.com/datastax/pulsar/commit/8611de81c4f) fix select broker is none (#16316)
* [47a7368bf6c](https://github.com/datastax/pulsar/commit/47a7368bf6c) [fix][txn] Fix TopicTransactionBuffer ledger apend marker throw ManagedLedgerAlreadyClosedException (#16265)
* [dcf80fac0f5](https://github.com/datastax/pulsar/commit/dcf80fac0f5) [improve][broker] Optimise msgOutCounter and bytesOutCounter (#16214) (#16286)
* [a9d62b59aec](https://github.com/datastax/pulsar/commit/a9d62b59aec) [fix][broker]fix bug: fail to expose managed ledger client stats to prometheus if bookkeeperClientExposeStatsToPrometheus is true (#16219)
* [5f8b65b70ae](https://github.com/datastax/pulsar/commit/5f8b65b70ae) [fix] [transaction] Cmd-Subscribe and Cmd-Producer will not succeed even after 100 retries (#16248)
* [eb481fc9803](https://github.com/datastax/pulsar/commit/eb481fc9803) [improve][broker] Use LinkedHashSet for config items of type Set to preserve elements order (#16138)
* [2b09f7d170f](https://github.com/datastax/pulsar/commit/2b09f7d170f) [fix][txn] Fix append txn message is lower than lowWaterMark decrease pendingWriteOps (#16266)
* [d7068c1cddb](https://github.com/datastax/pulsar/commit/d7068c1cddb) fix npe when doCacheEviction (#15184)
* [96666e1158d](https://github.com/datastax/pulsar/commit/96666e1158d) Add a cache eviction policy：Evicting cache data by the slowest markDeletedPosition (#14985)
* [5ef2183f320](https://github.com/datastax/pulsar/commit/5ef2183f320) Extracted interface for EntryCacheManager (#15933)
* [8a6f0fb832d](https://github.com/datastax/pulsar/commit/8a6f0fb832d) Support dynamic update cache config (#13679)
* [9480b49fcc3](https://github.com/datastax/pulsar/commit/9480b49fcc3) [fix][broker] Do not use IO thread for consumerFlow in Shared subscription
* [7e9dee3f928](https://github.com/datastax/pulsar/commit/7e9dee3f928) Shared subscription: improvement with offloaded ledgers
* [d95fb1e09ed](https://github.com/datastax/pulsar/commit/d95fb1e09ed) [fix][broker] Fix RawReader out of order (#16390)
* [c143bd97791](https://github.com/datastax/pulsar/commit/c143bd97791) Pulsar shell: symlink support
* [52cf9e8124c](https://github.com/datastax/pulsar/commit/52cf9e8124c) Pulsar Shell: use service hostname as prompt
* [bea45683d4e](https://github.com/datastax/pulsar/commit/bea45683d4e) Pulsar shell: use -c to specify client configuration file
* [fc6c37b636b](https://github.com/datastax/pulsar/commit/fc6c37b636b) [cleanup] CLI: fix pulsar-websocket dependency importing only needed jars
* [cc4c7be3916](https://github.com/datastax/pulsar/commit/cc4c7be3916) Offloaders: fix metrics - pass the Scheduler for periodic calculations - add raw brk_ledgeroffloader_read_bytes counter - fix read latency from JClouds calculation
* [90399643a68](https://github.com/datastax/pulsar/commit/90399643a68) Fixed deadlock when checking topic ownership (#16310)
* [52e0711d373](https://github.com/datastax/pulsar/commit/52e0711d373) Ensure ack-timeout task gets re-scheduled when there are exception in the final stage (#16337)
* [ee1a89ccc8d](https://github.com/datastax/pulsar/commit/ee1a89ccc8d) [improve][workflow] Sync the new docbot to branch-2.10 #16288
* [7468f8b9ea8](https://github.com/datastax/pulsar/commit/7468f8b9ea8) [fix][broker] Fix passing incorrect authentication data (#16201)
* [b72c5089738](https://github.com/datastax/pulsar/commit/b72c5089738) Avoid AuthenticationDataSource mutation for subscription name (#16065)
* [91ca4b4c906](https://github.com/datastax/pulsar/commit/91ca4b4c906) [fix][broker]fix npe when invoke replaceBookie. (#16239)
* [bd7c63aec4c](https://github.com/datastax/pulsar/commit/bd7c63aec4c) [fix][broker] Fix NPE when drop backlog for time limit. (#16235)
* [8b1d7a0c894](https://github.com/datastax/pulsar/commit/8b1d7a0c894) [improve][broker] Reduce the re-schedule message read operation for PersistentDispatcherMultipleConsumers (#16241)
* [da72a32112c](https://github.com/datastax/pulsar/commit/da72a32112c) [improve][java-client] Replace ScheduledExecutor to improve performance of message consumption (#16236)
* [a8695ff3aff](https://github.com/datastax/pulsar/commit/a8695ff3aff) [improve][broker] Avoid go through all the consumers to get the message ack owner (#16245)
* [8347ed2218d](https://github.com/datastax/pulsar/commit/8347ed2218d)  [fix][broker]Fix subscribe dispathcer limiter not be initialized (#16175)
* [17be098c6af](https://github.com/datastax/pulsar/commit/17be098c6af) [fix][broker] Fix compaction subscription acknowledge Marker msg issue. (#16205)
* [03a9ea7bc73](https://github.com/datastax/pulsar/commit/03a9ea7bc73) [fix][tests] TieredStorageConfigurationTests - clear system properties (#15957)
* [f26597a4002](https://github.com/datastax/pulsar/commit/f26597a4002) [fix][client] Add classLoader field for `SchemaDefinition` (#15915)
* [e676ae08319](https://github.com/datastax/pulsar/commit/e676ae08319) [fix][broker] Fix NPE when get /admin/v2/namespaces/public/default/maxTopicsPerNamespace (#16076)
* [25638e068be](https://github.com/datastax/pulsar/commit/25638e068be) [improve][java-client] Only trigger the batch receive timeout when having pending batch receives requests (#16160)
* [dc27dee3ef8](https://github.com/datastax/pulsar/commit/dc27dee3ef8) [fix][Java Client] Fix thread safety issue of `LastCumulativeAck` (#16072)
* [fbfaa516315](https://github.com/datastax/pulsar/commit/fbfaa516315) [fix][client] Fix the startMessageId can't be respected as the ChunkMessageID (#16154)
* [208b0a8abc3](https://github.com/datastax/pulsar/commit/208b0a8abc3) Fix `messageQueue` release message issue. (#16155)
* [21f06632351](https://github.com/datastax/pulsar/commit/21f06632351) [fix][broker][monitoring] fix message ack rate (#16108)
* [f22a8779e31](https://github.com/datastax/pulsar/commit/f22a8779e31) [fix][txn] Fix NPE when ack message with transaction at cnx = null  (#16142)
* [04b3a81b87b](https://github.com/datastax/pulsar/commit/04b3a81b87b) [Flakey-test] fix flaky-test RackAwareTest.testRackUpdate (#16071)
* [5d92ad89ad7](https://github.com/datastax/pulsar/commit/5d92ad89ad7) [fix][broker] Fix create client with TLS config (#16014)
* [6d37fb9b357](https://github.com/datastax/pulsar/commit/6d37fb9b357) [fix][broker]Fix topic policies update not check message expiry (#15941)
* [3d8618711ea](https://github.com/datastax/pulsar/commit/3d8618711ea) [Transaction] Set TC state is Ready after open MLTransactionMetadataStore completely. (#13957)
* [6d4487a5346](https://github.com/datastax/pulsar/commit/6d4487a5346) [improve][tests] improved flaky test runs (#16011)
* [92a8237c0a9](https://github.com/datastax/pulsar/commit/92a8237c0a9) [ML] Fix thread safety issues in ManagedCursorContainer related to "heap" field access (#16049)
* [ccda354b3ef](https://github.com/datastax/pulsar/commit/ccda354b3ef) [improve][broker] Avoid reconnection when a partitioned topic was created concurrently (#16043)
* [c99b6ce0c16](https://github.com/datastax/pulsar/commit/c99b6ce0c16) rename pulsar_producer_configuration_set_crypto_failure_action to pulsar_producer_configuration_get_crypto_failure_action (#16031)
* [85cac9f87cb](https://github.com/datastax/pulsar/commit/85cac9f87cb) [fix][client] Remove producer when close producer command is received (#16028)
* [c3f6c48063e](https://github.com/datastax/pulsar/commit/c3f6c48063e) [fix][admin] Fix typo in validation message (#16021)
* [65109b23256](https://github.com/datastax/pulsar/commit/65109b23256) [fix][client] Remove consumer when close consumer command is received (#15761)
* [251d1eded27](https://github.com/datastax/pulsar/commit/251d1eded27) [Fix][broker] Fix NPE when ledger id not found in `OpReadEntry` (#15837)
* [09cb1026fea](https://github.com/datastax/pulsar/commit/09cb1026fea) [improve][broker] Make PulsarWebResource#getOwnerFromPeerClusterList async. (#15940)
* [4e05c32c65b](https://github.com/datastax/pulsar/commit/4e05c32c65b) [improve][cli] Pulsar shell: include pulsar-shell in released tarballs
* [a34536e27eb](https://github.com/datastax/pulsar/commit/a34536e27eb) Pulsar shell: support comments in file
* [83fbe08cf1c](https://github.com/datastax/pulsar/commit/83fbe08cf1c) Pulsar shell: disable jansi to avoid JVM crashes on Ubuntu

### `lunastreaming-all` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.1 | pulsar-io-data-generator-2.10.1.1.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.1 | pulsar-io-elastic-search-2.10.1.1.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.1 | pulsar-io-jdbc-clickhouse-2.10.1.1.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.1 | pulsar-io-jdbc-mariadb-2.10.1.1.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.1 | pulsar-io-jdbc-postgres-2.10.1.1.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.1 | pulsar-io-jdbc-sqlite-2.10.1.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.1 | pulsar-io-kafka-2.10.1.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.1 | pulsar-io-kinesis-2.10.1.1.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.1 | pulsar-io-data-generator-2.10.1.1.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.1 | pulsar-io-debezium-mongodb-2.10.1.1.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.1 | pulsar-io-debezium-mssql-2.10.1.1.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.1 | pulsar-io-debezium-mysql-2.10.1.1.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.1 | pulsar-io-debezium-oracle-2.10.1.1.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.1 | pulsar-io-debezium-postgres-2.10.1.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.1 | pulsar-io-kafka-2.10.1.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.1 | pulsar-io-kinesis-2.10.1.1.nar |

</details>

### `lunastreaming-experimental` distribution
<details><summary>Proxy extensions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Proxy Extension | 2.10.0.3 | pulsar-kafka-proxy-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Protocol handlers</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |
| [kafka](https://github.com/datastax/starlight-for-kafka) | Kafka Protocol Handler | 2.10.0.3 | pulsar-protocol-handler-kafka-2.10.0.3.nar |
| [rabbitmq](https://github.com/datastax/starlight-for-rabbitmq) | Starlight for RabbitMQ Proxy Extension | 2.10.0.1 | starlight-rabbitmq-2.10.0.1.nar |

</details>
<details><summary>Filters</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [jms](https://pulsar.apache.org/docs/io-connectors) | Starlight for JMS - support for server side filters | 2.4.0 | pulsar-jms-2.4.0-nar.nar |

</details>
<details><summary>Functions</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [transforms](https://pulsar.apache.org/docs/io-connectors) | Transformation function | 1.0.2 | pulsar-transformations-1.0.2.nar |

</details>
<details><summary>Sinks</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [cassandra-enhanced](https://github.com/datastax/pulsar-sink) | A DataStax Pulsar Sink to load records from Pulsar topics to Apache Cassandra(R) or DataStax Enterprise(DSE) | 1.6.3 | cassandra-enhanced-pulsar-sink-1.6.3-nar.nar |
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [azure-kusto](https://github.com/datastax/pulsar-3rdparty-connector) | Azure Data Explorer (Kusto) Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-kusto-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [aerospike](https://pulsar.apache.org/docs/io-connectors) | Aerospike database sink | 2.10.1.1 | pulsar-io-aerospike-2.10.1.1.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.1 | pulsar-io-batch-data-generator-2.10.1.1.nar |
| [cloud-storage](https://pulsar.apache.org/docs/io-connectors) | Writes data into cloud storage | 2.10.0.4 | pulsar-io-cloud-storage-2.10.0.4.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.1 | pulsar-io-data-generator-2.10.1.1.nar |
| [elastic_search](https://pulsar.apache.org/docs/io-connectors) | Writes data into Elastic Search | 2.10.1.1 | pulsar-io-elastic-search-2.10.1.1.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.1 | pulsar-io-flume-2.10.1.1.nar |
| [hbase](https://pulsar.apache.org/docs/io-connectors) | Writes data into hbase table | 2.10.1.1 | pulsar-io-hbase-2.10.1.1.nar |
| [hdfs2](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 2.x | 2.10.1.1 | pulsar-io-hdfs2-2.10.1.1.nar |
| [hdfs3](https://pulsar.apache.org/docs/io-connectors) | Writes data into HDFS 3.x | 2.10.1.1 | pulsar-io-hdfs3-2.10.1.1.nar |
| [influxdb](https://pulsar.apache.org/docs/io-connectors) | Writes data into InfluxDB database | 2.10.1.1 | pulsar-io-influxdb-2.10.1.1.nar |
| [jdbc-clickhouse](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for ClickHouse | 2.10.1.1 | pulsar-io-jdbc-clickhouse-2.10.1.1.nar |
| [jdbc-mariadb](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for MariaDB | 2.10.1.1 | pulsar-io-jdbc-mariadb-2.10.1.1.nar |
| [jdbc-postgres](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for PostgreSQL | 2.10.1.1 | pulsar-io-jdbc-postgres-2.10.1.1.nar |
| [jdbc-sqlite](https://pulsar.apache.org/docs/io-connectors) | JDBC sink for SQLite | 2.10.1.1 | pulsar-io-jdbc-sqlite-2.10.1.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.1 | pulsar-io-kafka-2.10.1.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.1 | pulsar-io-kinesis-2.10.1.1.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.1 | pulsar-io-mongo-2.10.1.1.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.1 | pulsar-io-rabbitmq-2.10.1.1.nar |
| [redis](https://pulsar.apache.org/docs/io-connectors) | Writes data into Redis | 2.10.1.1 | pulsar-io-redis-2.10.1.1.nar |
| [solr](https://pulsar.apache.org/docs/io-connectors) | Writes data into solr collection | 2.10.1.1 | pulsar-io-solr-2.10.1.1.nar |
| [snowflake](https://github.com/datastax/snowflake-connector) | Snowflake Connector | 0.1.10 | pulsar-snowflake-connector-0.1.10.nar |

</details>
<details><summary>Sources</summary>

| Name | Description | Version | File | 
| ---- | ----------- | ------- | ---- | 
| [azure-docdb](https://github.com/datastax/pulsar-3rdparty-connector) | Azure DocumentDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-azure-documentdb-2.10.1.1.nar |
| [bigquery](https://github.com/datastax/pulsar-3rdparty-connector) | Big Query Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-bigquery-2.10.1.1.nar |
| [coap](https://github.com/datastax/pulsar-3rdparty-connector) | CoAP Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-coap-2.10.1.1.nar |
| [couchbase](https://github.com/datastax/pulsar-3rdparty-connector) | Couchbase Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-couchbase-2.10.1.1.nar |
| [datadog](https://github.com/datastax/pulsar-3rdparty-connector) | DataDog Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-datadog-2.10.1.1.nar |
| [diffusion](https://github.com/datastax/pulsar-3rdparty-connector) | Diffusion Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-diffusion-2.10.1.1.nar |
| [geode](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Geode Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-geode-2.10.1.1.nar |
| [hazelcast](https://github.com/datastax/pulsar-3rdparty-connector) | Hazelcast Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-hazelcast-2.10.1.1.nar |
| [humio](https://github.com/datastax/pulsar-3rdparty-connector) | Humio Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-humio-2.10.1.1.nar |
| [jms](https://github.com/datastax/pulsar-3rdparty-connector) | JMS Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-jms-2.10.1.1.nar |
| [Kinetica](https://github.com/datastax/pulsar-3rdparty-connector) | Kinetica Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kinetica-2.10.1.1.nar |
| [kudu](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Kudu Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-kudu-2.10.1.1.nar |
| [marklogic](https://github.com/datastax/pulsar-3rdparty-connector) | MarkLogic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-marklogic-2.10.1.1.nar |
| [mqtt](https://github.com/datastax/pulsar-3rdparty-connector) | MQTT Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-mqtt-2.10.1.1.nar |
| [neo4j](https://github.com/datastax/pulsar-3rdparty-connector) | Neo4J Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-neoj4-2.10.1.1.nar |
| [newrelic](https://github.com/datastax/pulsar-3rdparty-connector) | New Relic Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-newrelic-2.10.1.1.nar |
| [orientdb](https://github.com/datastax/pulsar-3rdparty-connector) | OrientDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-orientdb-2.10.1.1.nar |
| [phoenix](https://github.com/datastax/pulsar-3rdparty-connector) | Apache Phoenix Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-phoenix-2.10.1.1.nar |
| [plc4x](https://github.com/datastax/pulsar-3rdparty-connector) | PLC4X Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-plc4x-2.10.1.1.nar |
| [redis](https://github.com/datastax/pulsar-3rdparty-connector) | Redis Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-redis-2.10.1.1.nar |
| [sap-hana](https://github.com/datastax/pulsar-3rdparty-connector) | SAP HANA Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-sap-hana-2.10.1.1.nar |
| [singlestore](https://github.com/datastax/pulsar-3rdparty-connector) | SingleStore Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-singlestore-2.10.1.1.nar |
| [splunk](https://github.com/datastax/pulsar-3rdparty-connector) | Splunk Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-splunk-2.10.1.1.nar |
| [xtdb](https://github.com/datastax/pulsar-3rdparty-connector) | XTDB Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-xtdb-2.10.1.1.nar |
| [zeebe](https://github.com/datastax/pulsar-3rdparty-connector) | Zeebe Connector | 2.10.1.1 | pulsar-3rdparty-pulsar-connectors-zeebe-2.10.1.1.nar |
| [cassandra-source](https://github.com/datastax/cdc-for-apache-cassandra) | Read data from Cassandra | 2.1.0 | pulsar-cassandra-source-2.1.0.nar |
| [batch-data-generator](https://pulsar.apache.org/docs/io-connectors) | Test batch data generator source | 2.10.1.1 | pulsar-io-batch-data-generator-2.10.1.1.nar |
| [canal](https://pulsar.apache.org/docs/io-connectors) | canal source and read data from mysql | 2.10.1.1 | pulsar-io-canal-2.10.1.1.nar |
| [data-generator](https://pulsar.apache.org/docs/io-connectors) | Test data generator source | 2.10.1.1 | pulsar-io-data-generator-2.10.1.1.nar |
| [debezium-mongodb](https://pulsar.apache.org/docs/io-connectors) | Debezium MongoDb Source | 2.10.1.1 | pulsar-io-debezium-mongodb-2.10.1.1.nar |
| [debezium-mssql](https://pulsar.apache.org/docs/io-connectors) | Debezium Microsoft SQL Server Source | 2.10.1.1 | pulsar-io-debezium-mssql-2.10.1.1.nar |
| [debezium-mysql](https://pulsar.apache.org/docs/io-connectors) | Debezium MySql Source | 2.10.1.1 | pulsar-io-debezium-mysql-2.10.1.1.nar |
| [debezium-oracle](https://pulsar.apache.org/docs/io-connectors) | Debezium Oracle Source | 2.10.1.1 | pulsar-io-debezium-oracle-2.10.1.1.nar |
| [debezium-postgres](https://pulsar.apache.org/docs/io-connectors) | Debezium Postgres Source | 2.10.1.1 | pulsar-io-debezium-postgres-2.10.1.1.nar |
| [dynamodb](https://pulsar.apache.org/docs/io-connectors) | DynamoDB connectors | 2.10.1.1 | pulsar-io-dynamodb-2.10.1.1.nar |
| [file](https://pulsar.apache.org/docs/io-connectors) | Reads data from local filesystem | 2.10.1.1 | pulsar-io-file-2.10.1.1.nar |
| [flume](https://pulsar.apache.org/docs/io-connectors) | flume source and sink connector | 2.10.1.1 | pulsar-io-flume-2.10.1.1.nar |
| [kafka](https://pulsar.apache.org/docs/io-connectors) | Kafka source and sink connector | 2.10.1.1 | pulsar-io-kafka-2.10.1.1.nar |
| [kafka-connect-adaptor](https://pulsar.apache.org/docs/io-connectors) | Kafka source connect adaptor | 2.10.1.1 | pulsar-io-kafka-connect-adaptor-2.10.1.1.nar |
| [kinesis](https://pulsar.apache.org/docs/io-connectors) | Kinesis connectors | 2.10.1.1 | pulsar-io-kinesis-2.10.1.1.nar |
| [mongo](https://pulsar.apache.org/docs/io-connectors) | MongoDB source and sink connector | 2.10.1.1 | pulsar-io-mongo-2.10.1.1.nar |
| [netty](https://pulsar.apache.org/docs/io-connectors) | Netty Tcp or Udp Source Connector | 2.10.1.1 | pulsar-io-netty-2.10.1.1.nar |
| [nsq](https://pulsar.apache.org/docs/io-connectors) | Ingest data from an NSQ topic | 2.10.1.1 | pulsar-io-nsq-2.10.1.1.nar |
| [rabbitmq](https://pulsar.apache.org/docs/io-connectors) | RabbitMQ source and sink connector | 2.10.1.1 | pulsar-io-rabbitmq-2.10.1.1.nar |
| [twitter](https://pulsar.apache.org/docs/io-connectors) | Ingest data from Twitter firehose | 2.10.1.1 | pulsar-io-twitter-2.10.1.1.nar |

</details>

## Luna Streaming Distribution 2.10 1.0
This is release contains new features such as Pulsar Transforms and Pulsar Shell.
It also contains several stability issues about transactions.

### Most notable commits

* [010629e5a39](https://github.com/datastax/pulsar/commit/010629e5a39) Add commons-text to LICENSE
* [6f636a1c24e](https://github.com/datastax/pulsar/commit/6f636a1c24e) Fix JDK 11 compatibility
* [0c81490391c](https://github.com/datastax/pulsar/commit/0c81490391c) [feature][cli] Pulsar shell - Env variables interpolation
* [3501b0ce7d4](https://github.com/datastax/pulsar/commit/3501b0ce7d4) [feature][cli] Pulsar shell - add support for input files and pipe for running multiple commands - part 2
* [698f225d6d2](https://github.com/datastax/pulsar/commit/698f225d6d2) [feature][cli] Pulsar Shell
* [57b80e25f49](https://github.com/datastax/pulsar/commit/57b80e25f49) [fix][client] Fix JDK17 compatibility issue (#15964)
* [fa3dfdd5068](https://github.com/datastax/pulsar/commit/fa3dfdd5068) [fix][functions] Handle uploading of builtin Functions to BK if uploadBuiltinSinksSources is true (#16111)
* [8d9c008f938](https://github.com/datastax/pulsar/commit/8d9c008f938) [improve][functions] Use the classloader of the builtin Function in ThreadRuntime (#16092)
* [80af58eaff0](https://github.com/datastax/pulsar/commit/80af58eaff0) [improve][function] Support Record<?> as WindowFunction output type (#16129)
* [9e24d8f6b7f](https://github.com/datastax/pulsar/commit/9e24d8f6b7f) [improve][function] Allow not providing the class name when loading a Function nar file (#16079)
* [19b36c6b830](https://github.com/datastax/pulsar/commit/19b36c6b830) [improve][broker] Reduce the consumers list sort by priority level (#16243)
* [b4f1126b943](https://github.com/datastax/pulsar/commit/b4f1126b943) [fix][branch-2.10] Fix wrong unit of NIC speed on linux (#16166)
* [ba6fe1213b4](https://github.com/datastax/pulsar/commit/ba6fe1213b4) [fix][txn] Ack the same batch message different batchIndex with transaction (#16032)
* [1d34c98e87f](https://github.com/datastax/pulsar/commit/1d34c98e87f) [improvement][broker]: remove spammy log 'The count of topics on the bundle {} is less than 2, skip split!' (#16212)
* [8926fd2df65](https://github.com/datastax/pulsar/commit/8926fd2df65) Transactions: fix race in TransactionMetaStoreHandler (#16147)
* [4d7fe72c16c](https://github.com/datastax/pulsar/commit/4d7fe72c16c) PIP-105: new API to get subscription properties (#16095)
* [7e7a95b67b8](https://github.com/datastax/pulsar/commit/7e7a95b67b8) [improve][function] Support Record<?> as Function output type (#16041)
* [15722152dc3](https://github.com/datastax/pulsar/commit/15722152dc3) [improve][admin] Add option function-type to admin CLI for Functions (#16075)
* [eb525cfabcf](https://github.com/datastax/pulsar/commit/eb525cfabcf) Use OrderedExecutor instead of OrderedScheduler for consumer dispatch (#16115)
* [a71a2b5d57e](https://github.com/datastax/pulsar/commit/a71a2b5d57e) [improve][function] Get function class name from the NAR when using built-in functions (#15693)
* [044c0a0a145](https://github.com/datastax/pulsar/commit/044c0a0a145) [fix][admin] Fix check on create function class name (#15700)
* [c92e672d6d7](https://github.com/datastax/pulsar/commit/c92e672d6d7) Allow creating builtin functions in pulsar-admin CLI (#15671)
* [450a83db0d1](https://github.com/datastax/pulsar/commit/450a83db0d1) Parse function userConfig to Map<String, Object> (#15669)
* [03a80b0ce1b](https://github.com/datastax/pulsar/commit/03a80b0ce1b) [improve][pulsar-perf] Transactions: improve client options (#16090)
* [870af8a495f](https://github.com/datastax/pulsar/commit/870af8a495f) [Cli tools] Disable Pulsar client memory limit by default (#15748)
* [acd6424a03c](https://github.com/datastax/pulsar/commit/acd6424a03c) [pulsar-perf] Change the default for max-connections from 100 to 1 (#15387)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.2-nar.nar
* pulsar-cassandra-source-2.1.0.nar
* pulsar-io-cloud-storage-2.10.0.4.nar
* pulsar-io-data-generator-2.10.1.0.nar
* pulsar-io-debezium-mongodb-2.10.1.0.nar
* pulsar-io-debezium-mssql-2.10.1.0.nar
* pulsar-io-debezium-mysql-2.10.1.0.nar
* pulsar-io-debezium-oracle-2.10.1.0.nar
* pulsar-io-debezium-postgres-2.10.1.0.nar
* pulsar-io-elastic-search-2.10.1.0.nar
* pulsar-io-jdbc-clickhouse-2.10.1.0.nar
* pulsar-io-jdbc-mariadb-2.10.1.0.nar
* pulsar-io-jdbc-postgres-2.10.1.0.nar
* pulsar-io-jdbc-sqlite-2.10.1.0.nar
* pulsar-io-kafka-2.10.1.0.nar
* pulsar-io-kinesis-2.10.1.0.nar
* pulsar-snowflake-connector-0.1.10.nar
* pulsar-transformations-1.0.2.nar
* pulsar-protocol-handler-kafka-2.10.0.3.nar
* starlight-rabbitmq-2.10.0.1.nar
* pulsar-kafka-proxy-2.10.0.3.nar
* pulsar-jms-2.4.0-nar.nar


## Luna Streaming Distribution 2.10 0.6
This is a maintenance release containing important stability and security updates.
### Most notable commits
* [4930f6c45c2](https://github.com/datastax/pulsar/commit/4930f6c45c2) [fix][broker]Fix topic-level replicator rate limiter not init (#15825)
* [421bf6dc957](https://github.com/datastax/pulsar/commit/421bf6dc957) Optimize topic policy with HierarchyTopicPolicies about replicatorDispatchRate (#14161)
* [3312986d869](https://github.com/datastax/pulsar/commit/3312986d869) [broker] Add config to allow deliverAt time to be strictly honored (#16068)
* [8d0c054d5fc](https://github.com/datastax/pulsar/commit/8d0c054d5fc) [Issue 15896] Fix LockTimeout when storePut on the same key concurrently in RocksdbMetadataStore (#16005)
* [0e46a881bdc](https://github.com/datastax/pulsar/commit/0e46a881bdc) Clean up C++ client curl configuration (#16064)
* [ad3a814c37a](https://github.com/datastax/pulsar/commit/ad3a814c37a) Fix wrong response type for swagger definitions (#16022)
* [4923e15dcaf](https://github.com/datastax/pulsar/commit/4923e15dcaf) [broker] Make invalid namespace and topic name logs more descriptive (#16047)
* [7b556f44d70](https://github.com/datastax/pulsar/commit/7b556f44d70) [ML] When skipping updating mark delete position, execute callback with executor to prevent deadlock (#15971)
* [790ee2f72e2](https://github.com/datastax/pulsar/commit/790ee2f72e2) [fix][admin] Fix producer/consume permission can’t get schema (#15956) (#16026)
* [91ea44756f5](https://github.com/datastax/pulsar/commit/91ea44756f5) [broker][monitoring] add message ack rate metric for consumer (#15674)
* [54e36a46603](https://github.com/datastax/pulsar/commit/54e36a46603) [Function] provide default error handler for function log appender (#15728)
* [6a7d024e5fb](https://github.com/datastax/pulsar/commit/6a7d024e5fb) [fix][security] Add timeout of sync methods and avoid call sync method for AuthoriationService (#15694)
* [64f5de79a58](https://github.com/datastax/pulsar/commit/64f5de79a58) [Broker]make revokePermissionsOnTopic method async (#14149)
* [99f54cb8e31](https://github.com/datastax/pulsar/commit/99f54cb8e31) [cleanup][function] refine file io connector (#15250)
* [666435c951e](https://github.com/datastax/pulsar/commit/666435c951e) [fix] [admin] fix reach max tenants error if the tenant already exists (#15961)
* [7f08804b4cc](https://github.com/datastax/pulsar/commit/7f08804b4cc) [fix][txn] fix NPE of TransactionMetaStoreHandler (#15840)
* [353ffcbe9f9](https://github.com/datastax/pulsar/commit/353ffcbe9f9) [feature][admin] Support to get topic properties. (#15944)
* [f12f06750b1](https://github.com/datastax/pulsar/commit/f12f06750b1) [fix][auth] Generate correct well-known OpenID configuration URL (#15928)
* [1146c9c7368](https://github.com/datastax/pulsar/commit/1146c9c7368) Allow PULSAR_MEM & PULSAR_GC to be Overridden in pulsar_tool_env.sh (#15868)
* [ae7cd9c965b](https://github.com/datastax/pulsar/commit/ae7cd9c965b) [fix][pulsar] Bump pyyaml from 5.3.1 to 5.4.1 to solve CVE-2020-14343 (#15989)
* [2889092f6d7](https://github.com/datastax/pulsar/commit/2889092f6d7) Upgrade Netty Reactive Streams to 2.0.6 (#15990)
* [f95c371b3ff](https://github.com/datastax/pulsar/commit/f95c371b3ff) Removing log4j-1.2-api from dependencies (#15991)
* [64d8e0c3e20](https://github.com/datastax/pulsar/commit/64d8e0c3e20) Fix: org.apache.kafka.connect.errors.DataException: Not a struct schema: Schema{ARRAY} + tests (#15988)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.2-nar.nar
* pulsar-cassandra-source-2.1.0.nar
* pulsar-io-cloud-storage-2.10.0.4.nar
* pulsar-io-data-generator-2.10.0.6.nar
* pulsar-io-debezium-mongodb-2.10.0.6.nar
* pulsar-io-debezium-mssql-2.10.0.6.nar
* pulsar-io-debezium-mysql-2.10.0.6.nar
* pulsar-io-debezium-oracle-2.10.0.6.nar
* pulsar-io-debezium-postgres-2.10.0.6.nar
* pulsar-io-elastic-search-2.10.0.6.nar
* pulsar-io-jdbc-clickhouse-2.10.0.6.nar
* pulsar-io-jdbc-mariadb-2.10.0.6.nar
* pulsar-io-jdbc-postgres-2.10.0.6.nar
* pulsar-io-jdbc-sqlite-2.10.0.6.nar
* pulsar-io-kafka-2.10.0.6.nar
* pulsar-io-kinesis-2.10.0.6.nar
* pulsar-snowflake-connector-0.1.11-beta.nar
* pulsar-transformations-1.0.0.nar
* pulsar-protocol-handler-kafka-2.10.0.3.nar
* starlight-rabbitmq-2.10.0.1.nar
* pulsar-kafka-proxy-2.10.0.3.nar
* pulsar-jms-2.4.0-nar.nar

## Luna Streaming Distribution 2.10 0.5
This is a maintenance release containing important stability and security updates.
### Most notable commits
* [bb6db424376](https://github.com/datastax/pulsar/commit/bb6db424376) [Python] Use MacOS 10.15 as the target OS version for Python wheel files (#15788)
* [5a5030587aa](https://github.com/datastax/pulsar/commit/5a5030587aa) [Python] Adjusted script to build wheel for Python 3.7 on Mac (#15407)
* [86cdc542c98](https://github.com/datastax/pulsar/commit/86cdc542c98) [Fix][Docker] Add write permissions to /pulsar subdirectories to enable running as non-root user (#15769)
* [26236cd29f2](https://github.com/datastax/pulsar/commit/26236cd29f2) [fix][broker] Fix creating producer failure when set backlog quota. (#15663)
* [a716a300415](https://github.com/datastax/pulsar/commit/a716a300415) [fix][sql] Fix the decimal type error convert in json schema (#15687)
* [142689a902f](https://github.com/datastax/pulsar/commit/142689a902f) [fix][txn]Fix transasction ack batch message (#15875)
* [cdb8c372909](https://github.com/datastax/pulsar/commit/cdb8c372909) [improve][tiered storage] Reduce cpu usage when offloading the ledger (#15063)
* [ce9349ceffb](https://github.com/datastax/pulsar/commit/ce9349ceffb) [fix][broker]Fast return if ack cumulative illegal (#15695)
* [168228c14e6](https://github.com/datastax/pulsar/commit/168228c14e6) [Revert] [#15483] Remove sensitive msg from consumer/producer stats log (#15817)
* [7a04b7ddee7](https://github.com/datastax/pulsar/commit/7a04b7ddee7) Avoid contended synchronized block on topic load (#15883)
* [06aa6c031e4](https://github.com/datastax/pulsar/commit/06aa6c031e4) Fix avro conversion order of registration (#15863)
* [8130645b4c0](https://github.com/datastax/pulsar/commit/8130645b4c0) Fix NPE in MessageDeduplication. (#15820)
* [57acd651ac5](https://github.com/datastax/pulsar/commit/57acd651ac5) fix bug in getNumberOfEntriesInStorage (#15627)
* [df5685f8c1d](https://github.com/datastax/pulsar/commit/df5685f8c1d) Sync topicPublishRateLimiter update (#15599)
* [f554598cc62](https://github.com/datastax/pulsar/commit/f554598cc62) [feat] [tiered-storage] Add pure S3 provider for the offloader (#15710)
* [29dc9a7b497](https://github.com/datastax/pulsar/commit/29dc9a7b497) [fix][ML]Fix NPE when put value to `RangeCache`. (#15707)
* [4fd06d369ae](https://github.com/datastax/pulsar/commit/4fd06d369ae) [fix][broker-common] expose configurationMetadataStore and localMetadataStore (#15661)
* [797aa0e696b](https://github.com/datastax/pulsar/commit/797aa0e696b) [optimize][txn] Optimize transaction lowWaterMark to clean useless data faster (#15592)
* [a86141b7a0d](https://github.com/datastax/pulsar/commit/a86141b7a0d) Use dispatchRateLimiterLock to update dispatchRateLimiter. (#15601)
* [eef7d61efc5](https://github.com/datastax/pulsar/commit/eef7d61efc5) [cleanup] [broker] Remove useless code to avoid confusion in OpReadEntry#checkReadCompletion. (#15104)
* [378e19b63c7](https://github.com/datastax/pulsar/commit/378e19b63c7) [Transaction] Fix cursor readPosition is bigger than maxPosition in OpReadEntry (#14667)
* [cf7a72cba47](https://github.com/datastax/pulsar/commit/cf7a72cba47) Fix NPE when TableView handles null value message (#15951)
* [a3370e52e29](https://github.com/datastax/pulsar/commit/a3370e52e29) Upgrade BookKeeper to 4.14.5.1.0.1
* [f9da03ee823](https://github.com/datastax/pulsar/commit/f9da03ee823) [fix][connector] KCA sinks: fix offset mapping when sanitizeTopicName=true (#15950)
* [a1251385cde](https://github.com/datastax/pulsar/commit/a1251385cde) Enable TCP/IP keepalive for all ZK client connections in all components (#15908)
* [f7fa04ca2e3](https://github.com/datastax/pulsar/commit/f7fa04ca2e3) [ML] Fix race condition in getManagedLedgerInternalStats when includeLedgerMetadata=true (#15918)
* [a52d1f99736](https://github.com/datastax/pulsar/commit/a52d1f99736) [Broker] Add timeout to closing CoordinationServiceImpl (#15777)
* [e2dea872548](https://github.com/datastax/pulsar/commit/e2dea872548) [Broker, Functions, Websocket] Disable memory limit controller in internal Pulsar clients (#15752)
* [d40383d6ec9](https://github.com/datastax/pulsar/commit/d40383d6ec9) [PIP-146] ManagedCursorInfo compression (#14542)
* [9bc493ddf90](https://github.com/datastax/pulsar/commit/9bc493ddf90) PIP-105 add support for updating the Subscription properties (#15751)
* [9f5e0732cb3](https://github.com/datastax/pulsar/commit/9f5e0732cb3) [improve][connector] JDBC sinks: support Avro specific datatypes (#15845)
* [177a9dd36ca](https://github.com/datastax/pulsar/commit/177a9dd36ca) Configure DLog Bookie, Pulsar, and Admin clients via pass through config (#15818)
* [b41bf129565](https://github.com/datastax/pulsar/commit/b41bf129565) Switch to rely on Netty for Hostname Verification (#15824)
* [8988740a1cb](https://github.com/datastax/pulsar/commit/8988740a1cb) [fix][python]Fix generated Python protobuf code not compatible with latest protobuf package (#15846)
* [0e84d66ac33](https://github.com/datastax/pulsar/commit/0e84d66ac33) [improve][connector] JDBC Sinks: support KeyValue schema (#15807)
* [9b6d2eafcd4](https://github.com/datastax/pulsar/commit/9b6d2eafcd4) Replaced unicode 'comma and space' as single glyph with regular comma and space characters (#15461)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.2-nar.nar
* pulsar-cassandra-source-2.1.0.nar
* pulsar-io-cloud-storage-2.10.0.4.nar
* pulsar-io-data-generator-2.10.0.5.nar
* pulsar-io-debezium-mongodb-2.10.0.5.nar
* pulsar-io-debezium-mssql-2.10.0.5.nar
* pulsar-io-debezium-mysql-2.10.0.5.nar
* pulsar-io-debezium-oracle-2.10.0.5.nar
* pulsar-io-debezium-postgres-2.10.0.5.nar
* pulsar-io-elastic-search-2.10.0.5.nar
* pulsar-io-jdbc-clickhouse-2.10.0.5.nar
* pulsar-io-jdbc-mariadb-2.10.0.5.nar
* pulsar-io-jdbc-postgres-2.10.0.5.nar
* pulsar-io-jdbc-sqlite-2.10.0.5.nar
* pulsar-io-kafka-2.10.0.5.nar
* pulsar-io-kinesis-2.10.0.5.nar
* pulsar-snowflake-connector-0.1.11-beta.nar
* pulsar-protocol-handler-kafka-2.10.0.1.nar
* starlight-rabbitmq-2.10.0.0.nar
* pulsar-kafka-proxy-2.10.0.1.nar
* pulsar-jms-2.4.0-nar.nar

## Luna Streaming Distribution 2.10 0.4
This is a maintenance release containing important security and stability updates.
### Most notable commits
* [1b2a97888e3](https://github.com/datastax/pulsar/commit/1b2a97888e3) [fix][common] Add back FutureUtil#waitForAll and FutureUtil#waitForAny methods with List parameter
* [1ba180cbc74](https://github.com/datastax/pulsar/commit/1ba180cbc74) PIP-105: Store Subscription properties
* [4a2f75e71eb](https://github.com/datastax/pulsar/commit/4a2f75e71eb) [Broker] Disable memory limit controller for broker client and replication clients (#15723)
* [abec5d8c3c2](https://github.com/datastax/pulsar/commit/abec5d8c3c2) [enh] Broker: make max size of Consumer metadata configurable (#15713)
* [ee43c96373f](https://github.com/datastax/pulsar/commit/ee43c96373f) [fix][owasp] Fix false positive google-http-client-gson-1.41.0.jar (#15651)
* [4f85fbcc2d2](https://github.com/datastax/pulsar/commit/4f85fbcc2d2) [enh] Issue 15455: Pulsar Admin: create subscripion with Properties (PIP-105) (#15503) (#15681)
* [73c313664f9](https://github.com/datastax/pulsar/commit/73c313664f9) [fix][security] Tiered storage: Upgrade Hadoop to 3.3.3 to get rid of CVE-2022-26612 (#15660)
* [95fddf691cd](https://github.com/datastax/pulsar/commit/95fddf691cd) [fix][broker] Fix NPE when set `AutoTopicCreationOverride` (#15653)
* [7b37a8f63cf](https://github.com/datastax/pulsar/commit/7b37a8f63cf) [fix][broker] fix MetadataStoreException$NotFoundException while doing topic lookup (#15633)
* [b31898f9aae](https://github.com/datastax/pulsar/commit/b31898f9aae) Fix potential to add duplicated consumer (#15051)
* [602e8ad73b1](https://github.com/datastax/pulsar/commit/602e8ad73b1) [cleanup][broker] Override close method to avoid caching exception (#15529)
* [c244892e7ee](https://github.com/datastax/pulsar/commit/c244892e7ee) [Java Client] Fix messages sent by producers without schema cannot be decoded (#15622)
* [c04bebcf0f3](https://github.com/datastax/pulsar/commit/c04bebcf0f3) [improve][common] Use `Collection` to instead of `List` parameter type (#15329)
* [206b7a58668](https://github.com/datastax/pulsar/commit/206b7a58668) [PIP-153][optimize][txn]  Optimize metadataPositions in MLPendingAckStore (#15137)
* [50fc82778e2](https://github.com/datastax/pulsar/commit/50fc82778e2) [fix][broker] Fix to avoid TopicStatsImpl NPE even if producerName is null (#15502)
* [2579fae36ca](https://github.com/datastax/pulsar/commit/2579fae36ca) Fix http produce msg redirect issue. (#15551)
* [b7b447bab6e](https://github.com/datastax/pulsar/commit/b7b447bab6e) [PIP-163][Txn]Add lowWaterMark check before appending entry to TB (#15424)
* [1055ae396a5](https://github.com/datastax/pulsar/commit/1055ae396a5) [fix][broker]Close publishLimiter when disable it (#15520)
* [aa7f2081786](https://github.com/datastax/pulsar/commit/aa7f2081786) [fix][txn] Topic transaction buffer recover don't close reader when throw RuntimeException (#15361)
* [37397912703](https://github.com/datastax/pulsar/commit/37397912703) Fix grant all permissions but can't list topic. (#15501)
* [4bcbf93b5d6](https://github.com/datastax/pulsar/commit/4bcbf93b5d6) [Authorization] Role with namespace produce authz can also get topics (#13773)
* [13f3c7922e2](https://github.com/datastax/pulsar/commit/13f3c7922e2) [fix][broker] Fix MultiRolesTokenAuthorizationProvider `authorize` issue. (#15454)
* [4d3ea536808](https://github.com/datastax/pulsar/commit/4d3ea536808) [security] Remove sensitive msg from consumer/producer stats log (#15483)
* [bb900fcb287](https://github.com/datastax/pulsar/commit/bb900fcb287) Support handling single role and non-jwt-token in MultiRolesTokenAuthorizationProvider (#14857)
* [e3a0ad6c7d3](https://github.com/datastax/pulsar/commit/e3a0ad6c7d3) [improve][client] improve logic when ACK grouping tracker checks duplicated message id (#15465)
* [550e14de451](https://github.com/datastax/pulsar/commit/550e14de451) [Improve][doc] Add config of IO and acceptor threads in proxy (#15340)
* [c4ac6d50229](https://github.com/datastax/pulsar/commit/c4ac6d50229) [fix][package-management] Fix the new path `/data` introduced regression (#15367)
* [f0700865253](https://github.com/datastax/pulsar/commit/f0700865253) [improve][java-client] Add pending messages information while print the producer stats (#15440)
* [717b3459a9a](https://github.com/datastax/pulsar/commit/717b3459a9a) fix bug in contructor of RocksdbMetadataStore (#15405)
* [37e09eaf14c](https://github.com/datastax/pulsar/commit/37e09eaf14c) [improve][broker-web&websocket&proxy&function-worker] Full-support set ssl provider, ciphers and protocols (#13740)
* [f7ce317244a](https://github.com/datastax/pulsar/commit/f7ce317244a) [Improve][admin|client] AsyncHttpConnector doesn't use the system properties configured (#15307)
* [4f7c7191c51](https://github.com/datastax/pulsar/commit/4f7c7191c51) [Broker] Fix typo in enum name and handle closing of the channel properly since writeAndFlush is asynchronous (#15384)
* [7d245e6d1e7](https://github.com/datastax/pulsar/commit/7d245e6d1e7) Add KeyStore support in WebSocket, Function Worker HTTPS Servers  (#15084)
* [626c0de3948](https://github.com/datastax/pulsar/commit/626c0de3948) [enh][monitor]: add metrics for pulsar web service thread pool (#14742)
* [3816b039331](https://github.com/datastax/pulsar/commit/3816b039331) [CI] Upgrade zlib version to 1.2.12 (#14964)
* [1fdbeee1e1a](https://github.com/datastax/pulsar/commit/1fdbeee1e1a) [improve][offloaders] Upgrade JClouds to 2.5.0 (#15649)
* [eb03e976f3a](https://github.com/datastax/pulsar/commit/eb03e976f3a) [Fix][Txn] Fix transaction PendingAck lowWaterMark (#15530)
* [e23a44f3289](https://github.com/datastax/pulsar/commit/e23a44f3289) [Fix][Txn]Fix transaction component recover fillQueue (#15418)
* [f4fc76f2aec](https://github.com/datastax/pulsar/commit/f4fc76f2aec) [Fix][txn] Make transaction stats consistent at end txn (#15472)
* [6b85f8a68e2](https://github.com/datastax/pulsar/commit/6b85f8a68e2) Upgrade Netty to 4.1.77.Final and netty-tcnative to 2.0.52.Final (#15646)
### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-2.0.0.nar
* pulsar-io-data-generator-2.10.0.4.nar
* pulsar-io-debezium-mongodb-2.10.0.4.nar
* pulsar-io-debezium-mssql-2.10.0.4.nar
* pulsar-io-debezium-mysql-2.10.0.4.nar
* pulsar-io-debezium-oracle-2.10.0.4.nar
* pulsar-io-debezium-postgres-2.10.0.4.nar
* pulsar-io-elastic-search-2.10.0.4.nar
* pulsar-io-jdbc-clickhouse-2.10.0.4.nar
* pulsar-io-jdbc-mariadb-2.10.0.4.nar
* pulsar-io-jdbc-postgres-2.10.0.4.nar
* pulsar-io-jdbc-sqlite-2.10.0.4.nar
* pulsar-io-kafka-2.10.0.4.nar
* pulsar-io-kinesis-2.10.0.4.nar
* pulsar-snowflake-connector-0.1.9.nar
* pulsar-protocol-handler-kafka-2.10.0.1.nar
* starlight-rabbitmq-2.10.0.0.nar
* pulsar-kafka-proxy-2.10.0.1.nar
* pulsar-jms-2.3.0-nar.nar

## Luna Streaming Distribution 2.10 0.3
This is a maintenance release containing important stability updates.
### Most notable commits
* [b0a2a5e4fd0](https://github.com/datastax/pulsar/commit/b0a2a5e4fd0) fix: org.apache.kafka.connect.errors.DataException: Invalid Java object for schema with type... (#15598)
* [8ef565e8171](https://github.com/datastax/pulsar/commit/8ef565e8171) [fix][broker] Fix deadlock in broker after race condition in topic creation failure (#15570)
* [2dba8e8084f](https://github.com/datastax/pulsar/commit/2dba8e8084f) Offloader metrics (#13833)
* [51e35187b50](https://github.com/datastax/pulsar/commit/51e35187b50) Pulsar Functions: allow a Function<GenericObject,?> to access the original Schema of the Message and use it (#14847)
* [b58211de4d4](https://github.com/datastax/pulsar/commit/b58211de4d4) Fix pulsar-client-all shade - include BookKeeper libraries
* [babea4bfb28](https://github.com/datastax/pulsar/commit/babea4bfb28) Upgrade to Datastax BookKeeper 4.14.5.1.0.0
* [19daad5a5bb](https://github.com/datastax/pulsar/commit/19daad5a5bb) [fix][test] Add receive timeout to avoid block thread. (#15088)
* [41417f9d8dd](https://github.com/datastax/pulsar/commit/41417f9d8dd) [WebSocket] Fix MultiTopicReader#getConsumer ClassCastException (#15534)

### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-2.0.0.nar
* pulsar-io-data-generator-2.10.0.3.nar
* pulsar-io-debezium-mongodb-2.10.0.3.nar
* pulsar-io-debezium-mssql-2.10.0.3.nar
* pulsar-io-debezium-mysql-2.10.0.3.nar
* pulsar-io-debezium-oracle-2.10.0.3.nar
* pulsar-io-debezium-postgres-2.10.0.3.nar
* pulsar-io-elastic-search-2.10.0.3.nar
* pulsar-io-jdbc-clickhouse-2.10.0.3.nar
* pulsar-io-jdbc-mariadb-2.10.0.3.nar
* pulsar-io-jdbc-postgres-2.10.0.3.nar
* pulsar-io-jdbc-sqlite-2.10.0.3.nar
* pulsar-io-kafka-2.10.0.3.nar
* pulsar-io-kinesis-2.10.0.3.nar
* pulsar-snowflake-connector-0.1.9.nar
* pulsar-protocol-handler-kafka-2.10.0.1.nar
* starlight-rabbitmq-2.10.0.0.nar
* pulsar-kafka-proxy-2.10.0.1.nar
* pulsar-jms-2.1.0-nar.nar

## Luna Streaming Distribution 2.10 0.2
This is a maintenance release containing important stability updates.

### Most notable commits
* [d0105dfe006](https://github.com/datastax/pulsar/commit/d0105dfe006) [Proxy] Remove unnecessary blocking DNS lookup in LookupProxyHandler (#15415)
* [de3fef3f49f](https://github.com/datastax/pulsar/commit/de3fef3f49f) [Proxy/Client] Fix DNS server denial-of-service issue when DNS entry expires (#15403)
* [91ab03c029f](https://github.com/datastax/pulsar/commit/91ab03c029f) [fix][kinesis-sink] Handle Avro collections native types (GenericData.Array and Utf8 map keys) (#15432)
* [d30126b01d1](https://github.com/datastax/pulsar/commit/d30126b01d1) [feat][elasticsearch-sink] Option to strip out non printable characters (#15431)
* [d65d6bd8e0e](https://github.com/datastax/pulsar/commit/d65d6bd8e0e) [fix][elasticsearch-sink] Handle Avro collections native types (GenericData.Array and Utf8 map keys) (#15430)
* [bfa5a02ee7a](https://github.com/datastax/pulsar/commit/bfa5a02ee7a) [feat][elasticsearch] Add hashed id support (#15428)
* [cfd467fd3f5](https://github.com/datastax/pulsar/commit/cfd467fd3f5) [feat][elasticsearch-sink] Option to output canonical JSON (#15426)
* [bda6fdd32bc](https://github.com/datastax/pulsar/commit/bda6fdd32bc) Sinks: allow to reset --timeout-ms to zero
* [f2f6e607d6a](https://github.com/datastax/pulsar/commit/f2f6e607d6a) Include circe-checksum in pulsar-client dependency (#60)
* [97a7b3b049e](https://github.com/datastax/pulsar/commit/97a7b3b049e) Include correct bookkeeper jars in pulsar-client jar (#16)


### Builtin connectors
* cassandra-enhanced-pulsar-sink-1.6.1-nar.nar
* pulsar-cassandra-source-2.0.0.nar
* pulsar-io-data-generator-2.10.0.2.nar
* pulsar-io-debezium-mongodb-2.10.0.2.nar
* pulsar-io-debezium-mssql-2.10.0.2.nar
* pulsar-io-debezium-mysql-2.10.0.2.nar
* pulsar-io-debezium-oracle-2.10.0.2.nar
* pulsar-io-debezium-postgres-2.10.0.2.nar
* pulsar-io-elastic-search-2.10.0.2.nar
* pulsar-io-jdbc-clickhouse-2.10.0.2.nar
* pulsar-io-jdbc-mariadb-2.10.0.2.nar
* pulsar-io-jdbc-postgres-2.10.0.2.nar
* pulsar-io-jdbc-sqlite-2.10.0.2.nar
* pulsar-io-kafka-2.10.0.2.nar
* pulsar-io-kinesis-2.10.0.2.nar
* pulsar-snowflake-connector-0.1.9.nar
* pulsar-protocol-handler-kafka-2.10.0.1.nar
* starlight-rabbitmq-2.10.0.0.nar
* pulsar-kafka-proxy-2.10.0.1.nar
