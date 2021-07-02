# Release notes for DataStax Luna Streaming Distribution
Luna Streaming Distribution 2.8.0 is compatible with Apache Pulsar&trade; 2.8.0.

# Release notes for Luna Streaming Distribution 2.7.2
30 June 2021

## Component versions for Luna Streaming Distribution 2.7.2

   * Apache Pulsar 2.8.0
   * DataStax Pulsar Admin Console 1.0.0
   * DataStax Pulsar Heartbeat 1.0.2
   * DataStax Apache Pulsar Cassandra Sink 1.4.0
   * DataStax Apache Pulsar Cassandra Source 0.1.0
   * DataStax Burnell 1.0.0
   * Apache BookKeeper 14.1.1
 
This release adds these features to the original Apache Pulsar 2.8.0 release:
  
   * Stability improvements
   * Rootless Docker image
   * Third party libraries updates for security fixes
   * Docker images based on Ubuntu (instead of Debian based images in Pulsar 2.8.0, for security reasons)
   * Dependency upgrades (for security, stability and performances)
   * An Enhanced ElasticSearch Pulsar IO Sink  
   * An Enhanced version of Apache BookKeeper 4.14.1 with security fixes
 
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

## Source Code of Main Components

The source code for these versions of Apache Pulsar and Apache BookKeeper code is in
   
   * https://github.com/datastax/pulsar
   * https://github.com/datastax/bookkeeper

## Upgrade Considerations for Luna Streaming Distribution 2.7.2

As Luna Streming 2.7 servies, this Luna Streaming release that uses non-root containers for enhanced security. When upgrading from a previous version (for example, 2.6.2_1.0.1) files created while running that version will have root permissions and will not be readable by containers running the new version.

To fix this, you can manually log into the ZooKeeper, BookKeeper, and Function Worker containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs` directories are owned by UID 10000 (user pulsar). The group ID of the files should also be set to GID 10001 (group pulsar). Here is an example command:

```
chown -R 10000:10001 /pulsar/data
```

If you are are using the Luna Streaming Helm chart, you can enable automatic repair of the permissions using the `fixRootlessPermissions` setting. For more details on this setting, go [here](https://github.com/datastax/pulsar-helm-chart).

## Luna Streaming Distribution 2.8.0 1.0.0

This release is based on the [Apache Pulsar 2.8.2 release](https://pulsar.apache.org/release-notes/#280-mdash-2021-06-12-a-id280a). In addition to the contents of that release, it includes the following notable commits:

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

