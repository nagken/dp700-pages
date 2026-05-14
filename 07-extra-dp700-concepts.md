# Extra DP-700 Concepts - Edge Cases and Nuances

> Concepts that don't get a full domain page but show up on the exam.

## Spark - advanced tuning

- **AQE (Adaptive Query Execution)** - on by default in Fabric Spark. Re-optimizes plans at runtime based on actual stats. Helps with skew + small file shuffle.
- **Dynamic allocation** - Spark adds/removes executors based on load. Pair with autoscale pool for elastic cost.
- **Bucketing vs partitioning** - Fabric prefers Z-ORDER over bucketing for Delta tables.
- **Cache eviction** - when memory pressure rises, cached DataFrames evict in LRU order. Use `MEMORY_AND_DISK` for resilience.

## Delta deep cuts

- **Delta protocol versions** - newer features (column mapping, deletion vectors) require minReaderVersion / minWriterVersion bumps. Once bumped, older readers fail.
- **Time travel** - `VERSION AS OF n` or `TIMESTAMP AS OF '2026-01-01'`. Limited by VACUUM retention.
- **CHECKPOINTS** - every 10 commits, Delta writes a parquet checkpoint to speed up table reads.
- **Deletion vectors** - soft-delete rows instead of rewriting parquet. Faster MERGE/UPDATE but require modern reader.
- **Liquid clustering** (preview) - alternative to partitioning + Z-ORDER. Auto-clusters on chosen columns.

## KQL update policies and materialized views

- **Update policy** - runs a KQL transformation at ingest time, writing into a derived table. Like a streaming insert trigger.
- **Materialized view** - KQL-defined precomputed aggregate, served sub-second to dashboards.
- Update policies are **synchronous** by default (slow ingest if expensive); set asynchronous for high-throughput streams.

## Mirroring nuances

- Mirrored data lives in OneLake as **read-only Delta tables**.
- **No CDC available?** Some sources fall back to snapshot + polling intervals.
- **Schema drift** - adding columns at the source flows to Fabric automatically; renames break the mirror until reconfigured.
- Mirroring is **free for storage and compute** of the replication itself; downstream queries consume normal Fabric CU.

## Shortcut nuances

- **Cross-region shortcut** to ADLS/S3 incurs egress at the source.
- **OneLake-to-OneLake shortcut** is free and fast (within tenant).
- Shortcuts to **Dataverse** expose CRM tables as Delta without ETL.
- Shortcut **caching** (preview) reduces cross-cloud latency for read-heavy patterns.

## Capacity smoothing and bursting

- **Interactive operations** (Power BI queries, Direct Lake reads) are smoothed over **5 minutes**.
- **Background operations** (pipelines, Spark, refresh) are smoothed over **24 hours**.
- **Bursting** lets a single op exceed instantaneous CU briefly; the overage is repaid via smoothing.
- **Carry-forward / overages** - sustained over-consumption accumulates and eventually triggers throttling (Interactive Delay -> Interactive Reject -> Background Reject).

## Domains, gateways, deployment rules

- **Domain capacity assignment** - workspaces created in the domain inherit the domain's default capacity.
- **On-premises data gateway** - required for pipelines that read from on-prem SQL, file shares, etc.
- **Deployment rules** include:
  - Data source rules (rebind connection strings)
  - Parameter rules (override pipeline params)
  - Semantic model rules (rebind to new Lakehouse)
  - Lakehouse default rules (rebind default Lakehouse for notebooks)

## Notebook + pipeline patterns

- **Pipeline Notebook activity** vs **Run Notebook**: pipeline activity manages session reuse and parameter passing.
- **`%%configure`** - set Spark session properties from a notebook cell (must be first cell).
- **`mssparkutils`** - Fabric utility module for filesystem ops, secrets, notebook chaining (`runNotebook`).
- **`notebookutils`** - newer alias for `mssparkutils` in Fabric runtime >= 1.3.

## SQL endpoint quirks

- **Sync delay** - after writing to a Lakehouse table, the SQL endpoint may take **a few seconds** to reflect new data. Force a sync by querying `sys.tables` or via REST API.
- **Read-only** - no DML (INSERT/UPDATE/DELETE/MERGE) through the SQL endpoint of a Lakehouse. Use Spark or the Warehouse.
- **Cross-database queries** within a workspace use 3-part naming: `[Lakehouse_Sales].[dbo].[orders]`.

## Materialized views in Warehouse (preview)

- T-SQL CREATE MATERIALIZED VIEW WITH (DISTRIBUTION=...) - auto-refresh, query rewrite eligible.
- Different from KQL materialized views; same concept, different engine.

## Diagnostic settings - what flows where

- **Tenant-level diag** -> Log Analytics covers admin events, capacity events.
- **Workspace-level diag** -> can route per workspace.
- **Microsoft Purview** integrates for lineage + classification + policy enforcement across Fabric.

---

[<- References](06-references.md) - [Microsoft Learn Summaries ->](08-learn-summaries.md)
