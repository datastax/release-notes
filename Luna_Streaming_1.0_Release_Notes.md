# Release notes for DataStax Luna Streaming Distribution
Luna Streaming Distribution 1.0.x is compatible with Apache Pulsar&trade; 2.6.2.

# Release notes for Luna Streaming Distribution 1.0.0
27 January 2021

## Component versions for Luna Streaming Distribution 1.0.0

   * Apache Pulsar 2.6.2
   * DataStax Pulsar Admin Console 1.0.0
   * DataStax Pulsar Heartbeat 1.0.0
   * DataStax Apache Pulsar Connector 1.4.0
   * DataStax Burnell 1.0.0
   
*Note:* The DataStax Luna Streaming Distribution is designed for Java 11. However, because the product releases Docker images, you do not need to install Java (8 or 11) in advance. Java 11 is bundled in the Docker image.   

## Luna Streaming Distribution 1.0.0

This is the initial release of the DataStax Luna Streaming Distribution. This release contains all of the commits included in the Apache Pulsar v2.6.2 release plus the following changes specific to Luna Streaming:


* [cc5b83663d2](https://github.com/datastax/pulsar/commit/cc5b83663d2) - update LICENSE for presto 334 upversion
* [cebcc97f33a](https://github.com/datastax/pulsar/commit/cebcc97f33a) - suppress nashorn warning in JDK11 runtime
* [da22685e074](https://github.com/datastax/pulsar/commit/da22685e074) - upgrade presto version to 334 and JDK11
* [57578c32e3a](https://github.com/datastax/pulsar/commit/57578c32e3a) - Issue 9130: Pulsar-admin sinks create: bad error message "java.lang.NullPointerException: path is 'null'." in case of missing "--name" parameter
* [b6410dcdaa4](https://github.com/datastax/pulsar/commit/b6410dcdaa4) - Fix checkstyle
* [c50dee2f18b](https://github.com/datastax/pulsar/commit/c50dee2f18b) - Fix master broker while subscribe to non-persistent partitioned topic without topic auto-creation.
* [5c070704cce](https://github.com/datastax/pulsar/commit/5c070704cce) - Getting the stats of a non-persistent topic that has been cleaned causes it to re-appear (#9029)
* [f4fdc0c1cc5](https://github.com/datastax/pulsar/commit/f4fdc0c1cc5) - fix expiring messages after topic unload
* [b82dc34b753](https://github.com/datastax/pulsar/commit/b82dc34b753) - update ds distro required io connectors
* [13c35538fa1](https://github.com/datastax/pulsar/commit/13c35538fa1) - Switch Docker image to Java 11
* [341f7a9897a](https://github.com/datastax/pulsar/commit/341f7a9897a) - Update path for TTL config in Java 11
* [f8a1b826c45](https://github.com/datastax/pulsar/commit/f8a1b826c45) - auth token for debezium and kafka connect adaptor
* [d5b70adb742](https://github.com/datastax/pulsar/commit/d5b70adb742) - Always return from trigger even if read from output topic times out
* [81710076ff4](https://github.com/datastax/pulsar/commit/81710076ff4) - Update command descriptions from old 'property/cluster/namespace' format to current 'tenant/namespace' format
* [dbe1feeb394](https://github.com/datastax/pulsar/commit/dbe1feeb394) - Update "sample" tenant on standalone to stop using old property/cluster/namespace naming convention.
* [4bb90560ad7](https://github.com/datastax/pulsar/commit/4bb90560ad7) - Changing default function subscription to be function name, not FQFN
