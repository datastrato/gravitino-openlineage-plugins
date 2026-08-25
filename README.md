# Gravitino OpenLineage plugins

## Gravitino Spark OpenLineage plugin

Gravitino Spark OpenLineage plugin could transform OpenLineage dataset identifier to Gravitino dataset identifier, please refer to [Gravitino Spark Lineage page](https://gravitino.apache.org/docs/latest/lineage/gravitino-spark-lineage) for more details.

- New Features
  - Added the ability to extract Gravitino datasets from GVFS.
  - Enabled extraction of Gravitino datasets from Gravitino-managed Hive, JDBC, Iceberg, and Paimon tables.
- Behavior Changes
  - For Hive, JDBC, and Iceberg tables not managed by Gravitino, the dataset can now be converted into a Gravitino dataset identifier via configuration.

#### Changelog

- 1.31.0-datastrato-1
  - Based on OpenLineage 1.31.0.
  - Supports Gravitino Spark connector and non-Gravitino Spark connector.
  - Supports extract Gravitino dataset from GVFS.
  - Supports extract Gravitino dataset from Gravitino managed Hive, JDBC, Iceberg, Paimon tables.
  - Supports transform to Gravitino dataset from non-Gravitino managed Hive, JDBC, Iceberg tables.

## Gravitino Flink OpenLineage plugin

Gravitino Flink OpenLineage plugin extracts data lineage from Flink SQL and DataStream jobs and transforms dataset identifiers to Gravitino format (`namespace=metalake, name=catalog.db.table`), please refer to [Gravitino Flink Lineage page](https://gravitino.apache.org/docs/latest/lineage/gravitino-flink-lineage) for more details.

Two plugin variants are provided:

| JAR | Plugin | Flink Version | Capabilities |
|-----|--------|---------------|--------------|
| `openlineage-flink2-<version>.jar` | Flink2 plugin | Flink 2.x or Flink 1.20+ with FLIP-314 | SQL + DataStream lineage, zero code change |
| `openlineage-flink1-<version>.jar` | Flink1 plugin | Flink 1.18 / 1.19 / 1.20 (native) | DataStream lineage only, requires `registerJobListener` |

- New Features
  - Table-level lineage for Flink SQL jobs (Flink2 plugin, connector-agnostic).
  - DataStream lineage for Kafka, JDBC, Iceberg, Hive connectors.
  - Physical address resolution in `symlinks` facet (from DDL options and Gravitino REST API).
  - Deterministic run ID derived from Flink Job ID (START and COMPLETE/FAIL events correlate).
  - Configurable checkpoint tracking disable to reduce excessive RUNNING events.
  - ABORT event for canceled jobs.
  - Supports Kafka, HTTP, and Console transports.
  - Supports Gravitino Basic auth for metadata resolution.

#### Changelog

- 1.45.0-datastrato-1
  - Based on OpenLineage 1.45.0.
  - Flink2 plugin: SQL lineage + DataStream lineage for Flink 2.x / Flink 1.20+ with FLIP-314.
  - Flink1 plugin: DataStream lineage for native Flink 1.18-1.20.
  - Supports Gravitino Flink Connector (`GravitinoCatalogStore` mode) and non-Gravitino catalogs.
  - Supports physical address in `symlinks` facet (Kafka topic/broker, JDBC URL, Paimon warehouse, Hive metastore URI).
  - Fix: terminal events (COMPLETE/FAIL/ABORT) now emitted correctly via deterministic run ID.
  - Fix: temporary table catalog resolution from dataset name instead of CatalogContext.
  - Fix: FlinkConfigParser handles dotted Kafka properties correctly.
  - Fix: defensive listener initialization prevents SQL execution failures.
  - Feature: `openlineage.flink.disableCheckpointTracking` to suppress RUNNING events.
  - Feature: CANCELED jobs emit ABORT event (OpenLineage community PR #4615).
