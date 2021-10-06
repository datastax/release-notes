# Release notes for DataStax Luna Streaming Distribution
Luna Streaming Distribution 2.8.0 is compatible with Apache Pulsar&trade; 2.8.0.

# Release notes for Luna Streaming Distribution 2.8.0
30 June 2021

## Component versions for Luna Streaming Distribution 2.8.0

   * Apache Pulsar 2.8.0
   * DataStax Pulsar Admin Console 1.0.0
   * DataStax Pulsar Heartbeat 1.0.2
   * DataStax Apache Pulsar Cassandra Sink 1.5.0
   * DataStax Apache Pulsar Cassandra Source 0.2.5
   * DataStax Burnell 1.0.0
   * Apache BookKeeper 4.14.2
 
This release adds these features to the original Apache Pulsar 2.8.0 release:
  
   * Stability improvements
   * Rootless Docker image
   * Third party libraries updates for security fixes
   * Docker images based on Ubuntu (instead of Debian based images in Pulsar 2.8.0, for security reasons)
   * Dependency upgrades (for security, stability and performances)
   * An Enhanced ElasticSearch Pulsar IO Sink  
   * An Enhanced version of Apache BookKeeper 4.14.2 with security fixes
   * Pulsar IO source for Debezium Oracle
   * [Pulsar Proxy extensions](https://github.com/apache/pulsar/wiki/PIP-99%3A-Pulsar-Proxy-Extensions) feature 
 
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

## Source Code of Main Components

The source code for these versions of Apache Pulsar and Apache BookKeeper code is in
   
   * https://github.com/datastax/pulsar
   * https://github.com/datastax/bookkeeper

## Upgrade Considerations for Luna Streaming Distribution 2.8.0

As with Luna Streaming 2.7, this release uses non-root containers for enhanced security. When upgrading from a previous version (for example, 2.6.2_1.0.1) files created while running that version will have root permissions and will not be readable by containers running the new version.

To fix this, you can manually log into the ZooKeeper, BookKeeper, and Function Worker containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs` directories are owned by UID 10000 (user pulsar). The group ID of the files should also be set to GID 10001 (group pulsar). Here is an example command:

```
chown -R 10000:10001 /pulsar/data
```

If you are are using the Luna Streaming Helm chart, you can enable automatic repair of the permissions using the `fixRootlessPermissions` setting. For more details on this setting, go [here](https://github.com/datastax/pulsar-helm-chart).

## Upgrade Considerations for custom Pulsar Functions and Pulsar IO Connectors

If you are upgrading from Apache Pulsar 2.7.0 or Luna Streaming 2.7.2 you may need to recompile your Pulsar Functions or Pulsar IO Connectors using Apache Pulsar 2.8.0 as a dependency in certain cases.
This is because there is a breaking API change in Apache Pulsar 2.8.0 (and so in Luna Streaming 2.8.0) related to the SchemaInfo java class.
More context [here](https://github.com/apache/pulsar/issues/11338).

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
