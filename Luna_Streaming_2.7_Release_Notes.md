# Release notes for DataStax Luna Streaming Distribution
Luna Streaming Distribution 2.7.2 is compatible with Apache Pulsar&trade; 2.7.2.

# Release notes for Luna Streaming Distribution 2.7.2
11 June 2021

## Component versions for Luna Streaming Distribution 2.7.2

   * Apache Pulsar 2.7.2
   * DataStax Pulsar Admin Console 1.0.0
   * DataStax Pulsar Heartbeat 1.0.2
   * DataStax Apache Pulsar Cassandra Sink 1.4.0
   * DataStax Apache Pulsar Cassandra Source 0.2.8
   * DataStax Burnell 1.0.0
 
This release adds these features to the original Apache Pulsar 2.7.2 release:
  
   * Stability improvements
   * Rootless Docker image
   * Schema API and Pulsar IO API improvements ported from Apache Pulsar 2.8.0
   * Dependency upgrades (for security, stability and performances)
   * An Enhanced ElasticSearch Pulsar IO Sink  
 
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.

## Upgrade Considerations for Luna Streaming Distribution 2.7.2

This is the first Luna Streaming release that uses non-root containers for enhanced security. When upgrading from a previous version (for example, 2.6.2_1.0.1) files created while running that version will have root permissions and will not be readable by containers running the new version.

To fix this, you can manually log into the ZooKeeper, BookKeeper, and Function Worker containers and make sure that all files in the `/pulsar/data/` and `pulsar/logs` directories are owned by UID 10000 (user pulsar). The group ID of the files should also be set to GID 10001 (group pulsar). Here is an example command:

```
chown -R 10000:10001 /pulsar/data
```

If you are are using the Luna Streaming Helm chart, you can enable automatic repair of the permissions using the `fixRootlessPermissions` setting. For more details on this setting, go [here](https://github.com/datastax/pulsar-helm-chart).

## Luna Streaming Distribution 2.7.2 1.1.8

This release contains mainly a new release of Cassandra Source Connector.

List of most notable commits:

* [b1c80e79894](https://github.com/datastax/pulsar/commit/b1c80e79894) [function] fix update user config (#10731)
* [1ffa32c0c83](https://github.com/datastax/pulsar/commit/1ffa32c0c83) Remove pulsar-standalone docker image


## Luna Streaming Distribution 2.7.2 1.1.7

This release allows Datastax to publish Luna Streaming artifacts with the proprietary groupId "com.datastax.oss"; also it contains bugfixes and lib updates.

List of most notable commits:

* [1e4b53bbc52](https://github.com/datastax/pulsar/commit/1e4b53bbc52) Upgrading Debezium to 1.7 (#12295)
* [f741cade4f2](https://github.com/datastax/pulsar/commit/f741cade4f2) New distro groupId 'com.datastax.oss'
* [df2ac59e5e2](https://github.com/datastax/pulsar/commit/df2ac59e5e2) [Proxy] set default httpProxyTimeout to 5 minutes (#12299)
* [2a31adc2089](https://github.com/datastax/pulsar/commit/2a31adc2089) [Issue-11966][pulsar-proxy] set default http proxy request timeout (#11971)

## Luna Streaming Distribution 2.7.2 1.1.6

This is a bugfix release and enhance the support for some Pulsar IO connectors with the usage of native Avro Schema.

List of most notable commits:

* [a931bf276a5](https://github.com/datastax/pulsar/commit/a931bf276a5) Remove Pulsar Dashboard
* [8d0a967ff25](https://github.com/datastax/pulsar/commit/8d0a967ff25) [Pulsar IO] ElasticSearch Sink: support Fixed and ENUM datatypes
* [4f7c838a160](https://github.com/datastax/pulsar/commit/4f7c838a160) ElasticSearch Sink: handle Cassandra cql_varint and cql_decimal logical types - add support for dealing with custom logical types 'cql_varint' and 'cql_decimal' - add test case for 'cql_duration'
* [c1c297f916c](https://github.com/datastax/pulsar/commit/c1c297f916c) [Issue 11007]  add a version of AUTO_PRODUCE_BYTES that doesn't validate the message in `encode` (#11238)
* [49874b2937c](https://github.com/datastax/pulsar/commit/49874b2937c) Forbid to read other topic's data in managedLedger layer (#11912)


## Luna Streaming Distribution 2.7.2 1.1.5

This is a bugfix release that allows you to run Pulsar while disabling non-TLS service ports and it fixes a problem with KEY_BASED BatchBulder in Pulsar IO.

List of most notable commits:

* [e365009b561](https://github.com/datastax/pulsar/commit/e365009b561) [Broker] Call .release() when discarding entry to prevent direct memory leak (#11748)
* [cffa69d5215](https://github.com/datastax/pulsar/commit/cffa69d5215) [Broker] Handle NPE when full key range isn't covered with active consumers (#11749)
* [e1498a0a86b](https://github.com/datastax/pulsar/commit/e1498a0a86b) [Broker] Support disabling non-TLS service ports (#11681)
* [36312027240](https://github.com/datastax/pulsar/commit/36312027240) Support setting KEY_BASED batch builder for Pulsar Sinks

## Luna Streaming Distribution 2.7.2 1.1.4

This is a bugfix release that upgrades a third party library, Jetty, to the latest version 9.4.43.v20210629.

List of most notable commits:

* [c76d7d20b01](https://github.com/datastax/pulsar/commit/c76d7d20b01) [Security] Upgrade Jetty to 9.4.43.v20210629 (#11660)

## Luna Streaming Distribution 2.7.2 1.1.3

This is a bugfix release that adds automatic updating (at build time) of Ubuntu system components in order to address security issues caused
by third party dependencies imported inside the docker images.

List of most notable commits:

* [00b4dd439fc](https://github.com/datastax/pulsar/commit/00b4dd439fc) [Security] Install Ubuntu updates while building docker image

## Luna Streaming Distribution 2.7.2 1.1.2

This is a bugfix release that fixes problems about Geo Replication and it contains the upgrade of Debezium library

List of most notable commits:

* [b09ad5a3712](https://github.com/datastax/pulsar/commit/b09ad5a3712) [Broker] Fix replicated subscriptions direct memory leak
* [0f4b69129fd](https://github.com/datastax/pulsar/commit/0f4b69129fd) Upgrade Debezium to v.1.5.4 (last buildable with Java 8) (#6)

## Luna Streaming Distribution 2.7.2 1.1.1

This is a bugfix release that fixes problems around Pulsar Functions, Data Retention, the Enhanced ElasticSearch Sink, Key_Shared Subscriptions and Performances on JDK11. 

List of most notable commits:

* [bfa30dd49d0](https://github.com/datastax/pulsar/commit/bfa30dd49d0) [broker] Fix issue that message ordering could be broken when redelivering messages on Key_Shared subscription (#10762)
* [278e217726b](https://github.com/datastax/pulsar/commit/278e217726b) Fix issue with NarUnpacker that causes races and files getting overridden
* [e1bc601c73c](https://github.com/datastax/pulsar/commit/e1bc601c73c) Fix retention size policy delete too much ledgers (#11242)
* [7ba63e3a673](https://github.com/datastax/pulsar/commit/7ba63e3a673) Add stripNulls setting to avoid null in Elasticsearch (#5)
* [255a96f0394](https://github.com/datastax/pulsar/commit/255a96f0394) [Broker/Bookie] Set -Dio.netty.tryReflectionSetAccessible=true for pulsar processes (#11138)

## Luna Streaming Distribution 2.7.2 1.1.0

This is a major release for 2.7.2 release line.
From this version the base docker image is adoptopenjdk:11-jdk that is based on Ubuntu
in order to have a better security baseline for OS libraries.
We are also upgrading Python from 3.7 to 3.8.

List of most notable commits:

* [21a93e98f89](https://github.com/datastax/pulsar/commit/21a93e98f89) Postgres WAL does not truncate / confirmed_flush_lsn dows not change. Downgrading debezium to the same version as apache. (#4)
* [282f8319c8e](https://github.com/datastax/pulsar/commit/282f8319c8e) Use the subscription name defined in function details in the Pulsar Functions Python instance
* [b2e95a64572](https://github.com/datastax/pulsar/commit/b2e95a64572) Enable Function subscription naming workaround when activated
* [653aeca2739](https://github.com/datastax/pulsar/commit/653aeca2739) Revert "Changing default function subscription to be function name, not FQFN"
* [105a1d3ecb0](https://github.com/datastax/pulsar/commit/105a1d3ecb0) [Security] Use adoptopenjdk:11-jdk base image for Pulsar docker images

## Luna Streaming Distribution 2.7.2 1.0.1

This is a bugfix release that fixes problems around Memory usage in the Debezium connector, Pulsar Functions and
in automatic stuck subscription recovery. 

List of most notable commits:

* [318295e2c56](https://github.com/datastax/pulsar/commit/318295e2c56) Java Client: KeyValueSchema with AutoConsume component - make it work if the topic is still not initialized
* [a40bcce12cd](https://github.com/datastax/pulsar/commit/a40bcce12cd) [pulsar-broker] Handle NPE in unblock stuck subscrption task when dispatcher is not created (#10430)
* [70556e58c02](https://github.com/datastax/pulsar/commit/70556e58c02) [Broker] Fix direct memory leak in getLastMessageId (#10977)

## Luna Streaming Distribution 2.7.2 1.0.0

This release is based on the [Apache Pulsar 2.7.2 release](https://pulsar.apache.org/release-notes/#272-mdash-2021-05-11-a-id272a). In addition to the contents of that release, it includes the following notable commits:

* [24787c7902d](https://github.com/datastax/pulsar/commit/24787c7902d) function container run as group 10001 mount function user token from k8s secret as 400 permission for rootless container
* [b3271b3ef34](https://github.com/datastax/pulsar/commit/b3271b3ef34) Add workaround for failing PulsarFunctionsJavaProcessTest on JDK11 (#10566)
* [a742d138b46](https://github.com/datastax/pulsar/commit/a742d138b46) PulsarFunctionsTests - use InstanceUtils.getDefaultSubscriptionName instead of an hardcoded subscription name
* [96afcf94d5d](https://github.com/datastax/pulsar/commit/96afcf94d5d) Docker image: add vim and nettools (netstat)
* [1d34fa639b1](https://github.com/datastax/pulsar/commit/1d34fa639b1) Revert "[Schema] Support consume multiple schema types messages by AutoConsumeSchema (#10604)"
* [bfb25df7a14](https://github.com/datastax/pulsar/commit/bfb25df7a14) Fix compile issue in AutoConsumeSchemaTest.java
* [432f0960ff4](https://github.com/datastax/pulsar/commit/432f0960ff4) [ML] Cancel scheduled tasks as the first step in closing (#10739)
* [cb0dfd7cc6d](https://github.com/datastax/pulsar/commit/cb0dfd7cc6d) [ML] Fix solution for preventing race conditions between timeout and completion (#10740)
* [063040dfd38](https://github.com/datastax/pulsar/commit/063040dfd38) Release OpAddEntry.data when entry is copied and discarded (#10773)
* [9f30951139b](https://github.com/datastax/pulsar/commit/9f30951139b) [Broker] Fix possible data race in getFirstAvailableConsumerPermits (#10831)
* [58a19fd6ce6](https://github.com/datastax/pulsar/commit/58a19fd6ce6) Fix the out of index issue when dispatch messages based on the avgBatchSizePerMsg. (#10828)
* [f508ff14dd2](https://github.com/datastax/pulsar/commit/f508ff14dd2) Fix consumer stuck issue due to reuse entry wrapper. (#10824)
* [7513f3e8e06](https://github.com/datastax/pulsar/commit/7513f3e8e06) [Schema] Fix AutoConsumeSchema decode null schema version data (#10811)
* [e21c03884c1](https://github.com/datastax/pulsar/commit/e21c03884c1) AutoConsumeSchema: use decode(payload, schemaversion) (#10700)
* [3398e3f74dc](https://github.com/datastax/pulsar/commit/3398e3f74dc) [Schema] Support consume multiple schema types messages by AutoConsumeSchema (#10604)
* [66deda48eb8](https://github.com/datastax/pulsar/commit/66deda48eb8) ReflectionUtils use Class.forName in order to properly discover classes in Functions Runtime while using DefaultImplementation
* [0d530108233](https://github.com/datastax/pulsar/commit/0d530108233) Move full pulsar-client-original in Pulsar IO classpath, as in 2.8.0 - this change allows to use KeyValueSchema and RecordSchemaBuilder in Pulsar Sinks
* [0c62e0b412a](https://github.com/datastax/pulsar/commit/0c62e0b412a) AutoConsumeSchema: use decode(payload, schemaversion) (#10700)
* [2bde8b20e14](https://github.com/datastax/pulsar/commit/2bde8b20e14) [Schema] Support consume multiple schema types messages by AutoConsumeSchema (#10604)
* [305db0e4e55](https://github.com/datastax/pulsar/commit/305db0e4e55) Support writing general records to Pulsar sink (#9590)
* [b6977c06aee](https://github.com/datastax/pulsar/commit/b6977c06aee) Fix usage of seekAsync in MessageImpl.hasMessageAvailable and flaky-test (#10190)
* [1f222bc77a3](https://github.com/datastax/pulsar/commit/1f222bc77a3) Support get topic applied policy for message TTL (#9225)
* [5d252e4c4a4](https://github.com/datastax/pulsar/commit/5d252e4c4a4) Ensure read-lock is not continuously held on a section while iterating over concurrent maps (#9787)
* [bedc715392b](https://github.com/datastax/pulsar/commit/bedc715392b) Branch-2.7: getListOfNamespaces does not fail with non-existant tenant
* [4b9d2eede3d](https://github.com/datastax/pulsar/commit/4b9d2eede3d) [Performance] Use single instance of parser (#10664)
* [66a7d55993e](https://github.com/datastax/pulsar/commit/66a7d55993e) Fix ConcurrentOpenLongPairRangeSet remove all range (#10656)
* [7dd67603d13](https://github.com/datastax/pulsar/commit/7dd67603d13) Ensure all the ReadHandle gets properly closed on cache invalidation (#10659)
* [6e0a03243aa](https://github.com/datastax/pulsar/commit/6e0a03243aa) Add metrics for nonContiguousDeletedMessagesRange (#10638)
* [2c27f2c0db8](https://github.com/datastax/pulsar/commit/2c27f2c0db8) [C++] Avoid sending flow requests with zero permits (#10506)
* [3ebd2d8b3b0](https://github.com/datastax/pulsar/commit/3ebd2d8b3b0) [Issue-10611] consumer related topic stats only available while consumer or reader are connected
* [ed1f33e8304](https://github.com/datastax/pulsar/commit/ed1f33e8304) More fixes about running tests on JDK11 (#9893)
* [79ddf32144e](https://github.com/datastax/pulsar/commit/79ddf32144e) make ledger rollover check task internal (#8946)
* [c979b25736d](https://github.com/datastax/pulsar/commit/c979b25736d) Fix writing/encoding of GenericJsonRecord (#9608)
* [5d4ad98933a](https://github.com/datastax/pulsar/commit/5d4ad98933a) Upgrade to Apache Avro 1.10.2 (#9898)
* [f270964367f](https://github.com/datastax/pulsar/commit/f270964367f) [Security] Upgrade junit version to 4.13.1 to resolve CVE-2020-15250 and fix test dependency leak (#10147)
* [8d006468a9e](https://github.com/datastax/pulsar/commit/8d006468a9e) [Schema] Add schemaType field in SchemaHash (#10573)
* [545edcb7412](https://github.com/datastax/pulsar/commit/545edcb7412) Enhanced ES-sink connector
* [0f11747c8e5](https://github.com/datastax/pulsar/commit/0f11747c8e5) [CLIENT] fixed NPE in GenericJsonRecord (#10482)
* [bf008053ef3](https://github.com/datastax/pulsar/commit/bf008053ef3) [Issue 8751] Update Dockerfile for Pulsar and Dashboard to Create and Use pulsar User (nonroot user) (#8796)
* [bec07ebaa02](https://github.com/datastax/pulsar/commit/bec07ebaa02) Pulsar Admin: return a better error message
* [0ad9b90a5aa](https://github.com/datastax/pulsar/commit/0ad9b90a5aa) Comment lo4j2 script in order to save resources in pulsar-admin (#9309)
* [203b67b366f](https://github.com/datastax/pulsar/commit/203b67b366f) Ensure that temporary directories are deleted during tests (#9263)
* [0b9509a6fe6](https://github.com/datastax/pulsar/commit/0b9509a6fe6) Changes required to backport PR 7266 to 2.7 branch
* [d6027a8ea58](https://github.com/datastax/pulsar/commit/d6027a8ea58) [pulsar-broker] Dispatch batch messages according consumer permits (#7266)
* [bcb849e0a01](https://github.com/datastax/pulsar/commit/bcb849e0a01) Fixed missed ZK caching when fetching list of namespaces for a tenant (#10594)
* [6f6dc57c6f0](https://github.com/datastax/pulsar/commit/6f6dc57c6f0) [Issue 10010][Client] fixed memory leak (#10028)
* [5d7ef69f156](https://github.com/datastax/pulsar/commit/5d7ef69f156) [pulsar-broker] Dispatch batch messages according consumer permits (#7266)
* [d5aeb665c9d](https://github.com/datastax/pulsar/commit/d5aeb665c9d) Add AvroSchema UUID support
* [1a94bbcdc7b](https://github.com/datastax/pulsar/commit/1a94bbcdc7b) [Build] Specify release in maven-compiler-plugin configuration on JDK11 (#10343)
* [5dee3ebe51e](https://github.com/datastax/pulsar/commit/5dee3ebe51e) Use Message.getReaderSchema() in Pulsar IO Sinks when possible (#10557)
* [7e1f9f06f2a](https://github.com/datastax/pulsar/commit/7e1f9f06f2a) Allow to build Pulsar with JDK11 and -Dmaven.compiler.release=8 (#9580)
* [e7670be4055](https://github.com/datastax/pulsar/commit/e7670be4055) Upgrade Lombok to 1.18.20 (#10259)
* [e2c52457d27](https://github.com/datastax/pulsar/commit/e2c52457d27) Made OpAddEntry.toString() more robust to nulls to prevent NPEs (#10548)
* [a26de54f1bf](https://github.com/datastax/pulsar/commit/a26de54f1bf) [pulsar-broker] Dispatch messaages to consumer with permits (#10417)
* [83d10a140f2](https://github.com/datastax/pulsar/commit/83d10a140f2) [Broker] Make Persistent*DispatcherMultipleConsumers.readMoreEntries synchronized (#10413)
* [a1e1388111f](https://github.com/datastax/pulsar/commit/a1e1388111f) [pulsar-broker] Allow broker to discover and unblock stuck subscription (#9789)
* [7e57cbe5de2](https://github.com/datastax/pulsar/commit/7e57cbe5de2) Add streaming dispatcher. (#9056)
* [c73cdae681f](https://github.com/datastax/pulsar/commit/c73cdae681f) AutoConsumeSchema: handle schema NONE as BYTES (#10277)
* [4acd720eb2a](https://github.com/datastax/pulsar/commit/4acd720eb2a) PIP-85 Add Schema Information to Message in Java Client API (#10476)
* [56c2f6b3f95](https://github.com/datastax/pulsar/commit/56c2f6b3f95) cleaned some code in GenericJsonRecord (#10527)
* [b1ee56c5ce6](https://github.com/datastax/pulsar/commit/b1ee56c5ce6) Add JsonRecordBuilder implementation (#10052)
* [2932b1057a2](https://github.com/datastax/pulsar/commit/2932b1057a2) Add Schema.getNativeSchema (#10076)
* [1264c476223](https://github.com/datastax/pulsar/commit/1264c476223) [Java client] Fix behaviour of Schema.AUTO_CONSUME() with KeyValueSchema and multi versions (#10492)
* [fe980e72bd4](https://github.com/datastax/pulsar/commit/fe980e72bd4) Add JsonRecordBuilder implementation (#10052)
* [ea5b676372f](https://github.com/datastax/pulsar/commit/ea5b676372f) [Security] Upgrade vertx to 3.9.7, addresses CVE-2018-12541 (#10261)
* [ff5924492d7](https://github.com/datastax/pulsar/commit/ff5924492d7) Java Client: MessageImpl - ensure that AutoConsumeSchema downloaded the schema before decoding the payload (#10248)
* [ec3ad85d1b8](https://github.com/datastax/pulsar/commit/ec3ad85d1b8) Sink<GenericObject> unwrap internal AutoConsumeSchema and allow to handle topics with KeyValue schema (#10211)
* [72295b67bee](https://github.com/datastax/pulsar/commit/72295b67bee) GenericObject: handle KeyValue with SEPARATED encoding and add more tests (#10186)
* [b116efd0944](https://github.com/datastax/pulsar/commit/b116efd0944) Pulsar IO: Allow to develop Sinks that support Schema but without setting it at build time (Sink<GenericObject>) (#10034)
* [ab3caca169c](https://github.com/datastax/pulsar/commit/ab3caca169c) GenericObject - support KeyValue in Message#getValue() (#10107)
* [23b28593899](https://github.com/datastax/pulsar/commit/23b28593899) Implement GenericObject - Allow GenericRecord to wrap any Java Object (#10057)
* [6fe93f50a8c](https://github.com/datastax/pulsar/commit/6fe93f50a8c) Add presto password authenticators plugin to enable password auth in Pulsar SQL
* [5bc23c6aead](https://github.com/datastax/pulsar/commit/5bc23c6aead) Enable Conscrypt for Jetty in the Broker and in the Proxy (#10541)
* [e275813efc7](https://github.com/datastax/pulsar/commit/e275813efc7) Bump Debezium version to latest in series
* [56e127d30d9](https://github.com/datastax/pulsar/commit/56e127d30d9) [Branch-2.7] Fix deadlock on Monitoring thread blocked by LeaderService.isLeader() (#10512)
* [421fd828a02](https://github.com/datastax/pulsar/commit/421fd828a02) [pulsar-functions] enhance kubernetes manifest customizer with default options (#9445)
* [186e63b27bf](https://github.com/datastax/pulsar/commit/186e63b27bf) Changing default function subscription to be function name, not FQFN
* [b56a6d86f9d](https://github.com/datastax/pulsar/commit/b56a6d86f9d) Always return from trigger even if read from output topic times out
* [c9e071cca72](https://github.com/datastax/pulsar/commit/c9e071cca72) Update path for TTL config in Java 11
* [830d79803e3](https://github.com/datastax/pulsar/commit/830d79803e3) Switch Docker image to Java 11
* [d6f953893fa](https://github.com/datastax/pulsar/commit/d6f953893fa) upgrade presto version to 334 and JDK11
* [65a1acd7334](https://github.com/datastax/pulsar/commit/65a1acd7334) auth token for debezium and kafka connect adaptor
