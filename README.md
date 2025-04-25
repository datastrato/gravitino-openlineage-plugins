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
