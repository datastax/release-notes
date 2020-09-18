# Release notes for 6.8.4



## 6.8.4 DSE Compaction

* Fixes compaction getting stuck on acquiring references for non-existing sstables. (DB-4290)


## 6.8.4 DSE CQL

* Distributes Netty connections more uniformly across TPC cores (DB-4683)


## 6.8.4 DSE MessagingService

* Distributes Netty connections more uniformly across TPC cores (DB-4683)


## 6.8.4 DSE Deprecated: Core

* Adds TTL and TimeWindowCompactionStrategy (TWCS) to system_distributed.repair_history and system_distributed.parent_repair_history tables. (DB-2009)
