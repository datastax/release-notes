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

# Releases

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