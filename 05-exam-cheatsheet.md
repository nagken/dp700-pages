# DP-700 Exam Decision Reference (Cheatsheet)

> Single-page "when X then Y" lookup. Print this. Skim 60 minutes before the test.

## Pick the Fabric store

| Question wording | Pick |
|---|---|
| "T-SQL devs, multi-table transactions, stored procs" | **Warehouse** |
| "Data scientists, PySpark, files + tables, ML" | **Lakehouse** |
| "Streaming logs, time-series, KQL" | **Eventhouse / KQL Database** |
| "Live OLTP analytics without ETL (Cosmos / Snowflake / Azure SQL DB)" | **Mirroring** |
| "Reference external lake without copying" | **OneLake shortcut** |

## Pick the ingestion tool

| Wording | Pick |
|---|---|
| "Continuous events / IoT / Kafka / sub-second" | **Eventstream** |
| "Replicate operational DB live" | **Mirroring** |
| "Symlink to ADLS / S3 / Dataverse / OneLake" | **Shortcut** |
| "Self-service Power Query, Excel-style" | **Dataflow Gen2** |
| "Multi-step ETL with control flow + parameters + schedules" | **Data Factory pipeline** |
| "Bulk one-time copy / migration with simple mapping" | **Copy job** |
| "Custom Python / large-scale transform" | **Notebook (Spark)** |

## Pick the transform engine

| Wording | Pick |
|---|---|
| "PySpark / Spark SQL / Delta MERGE / ML libraries" | **Notebook** |
| "T-SQL stored proc, multi-table TX" | **Warehouse** |
| "Power Query M, citizen developer" | **Dataflow Gen2** |
| "Streaming aggregation, materialized view, telemetry" | **KQL update policy** |

## Pick the security feature

| Wording | Pick |
|---|---|
| "Limit which workspace items the user touches" | **Workspace role** (Admin / Member / Contributor / Viewer) |
| "Filter rows by user identity" | **Row-Level Security (RLS)** |
| "Hide entire columns / tables from a role" | **Object-Level Security (OLS)** or T-SQL **CLS** (GRANT/DENY) |
| "Mask part of a value (last 4 digits)" | **Dynamic Data Masking (DDM)** |
| "Tag dataset Confidential and propagate" | **Sensitivity label** |
| "Workspace-owned identity to access ADLS / KV" | **Workspace identity** |
| "Non-human automated identity" | **Service principal** |

## Power BI semantic-model mode

| Need | Pick |
|---|---|
| Hits OneLake parquet at query time, no refresh | **Direct Lake** |
| In-memory cache, scheduled refresh | **Import** |
| Live source query, no cache | **DirectQuery** |
| Mix Import + DirectQuery | **Composite** |

## Lifecycle / CI/CD

| Need | Pick |
|---|---|
| Source-control item definitions in repo | **Git integration** |
| Promote artifacts Dev -> Test -> Prod with rules | **Deployment pipelines** |
| Parameterize per-environment values | **Variable library** |
| Bulk provision / automate workspaces | **Fabric REST API + PowerShell / Python SDK** |

## Performance - Lakehouse / Delta

| Symptom | Fix |
|---|---|
| Many small files after streaming append | **OPTIMIZE** + **VACUUM** |
| Direct Lake falls back to DirectQuery | Enable **V-Order**; check supported types |
| Range filter on a few columns slow | **Z-ORDER BY col1, col2** |
| Skewed partitions, tiny per-partition file count | Re-partition by higher-cardinality column |

## Performance - Warehouse

| Symptom | Fix |
|---|---|
| Bad cardinality estimates | **UPDATE STATISTICS** |
| Repeated identical SELECT slow | **Result-set cache** (on by default) |
| Frequent aggregation on big fact | **Materialized view** |

## Performance - Spark

| Symptom | Fix |
|---|---|
| Cold start ~2-3 min | Use **starter pool** for short jobs |
| OOM on join | **Broadcast** small dim |
| Skewed key | Salt + repartition |
| Reuses df many times | **df.cache()** |

## Performance - KQL

| Symptom | Fix |
|---|---|
| Dashboard query slow on hot range | **Caching policy** for last N days |
| Aggregation rebuilt every query | **Materialized view** |
| Append heavy + transform | **Update policy** at ingest |

## Monitoring - where to look

| Need | Tool |
|---|---|
| Cross-workspace pipeline runs | **Monitoring hub** |
| Capacity CU consumption + throttling | **Capacity Metrics app** |
| Eventstream / KQL ingestion lag | **Real-Time hub** |
| Rule-based alerts on KPIs / streams | **Activator (Reflex)** |
| Audit logs to SIEM | **Diagnostic settings -> Log Analytics** |

## Cost

| Need | Action |
|---|---|
| Steady-state prod | **Reserved F-SKU** (1y / 3y) |
| Dev/test idle hours | **Pause capacity** |
| Dev throttling prod | **Workload isolation** (separate capacity) |
| Logs / soft-deleted versions piling up | **Retention policy** + **VACUUM** |

## 60-second pre-exam reset

1. Read the question. Underline the verb (ingest / transform / serve / monitor / secure / deploy).
2. Map verb -> Fabric tool family.
3. Within family, map wording -> specific feature.
4. Cross-check: would another tool also work? Pick the **most specific Fabric-native** one.
5. For security: which **granularity** is asked (workspace / item / row / column / value)?

---

[<- Monitor and Optimize](03-monitor-optimize.md) - [References ->](06-references.md)
