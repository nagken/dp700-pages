# Microsoft Learn Summaries - DP-700

> One-paragraph summary of each Microsoft Learn module on the DP-700 path. Skim before deeper reading.

## Foundation

**Get started with Microsoft Fabric.** Introduces the unified SaaS analytics platform, the F-SKU capacity model, and the seven workloads (Data Engineering, Data Factory, Data Science, Data Warehouse, Real-Time Intelligence, Power BI, Industry Solutions). Workspaces are the unit of governance; OneLake is the single tenant-wide lake under all workloads.

**Administer Microsoft Fabric.** Capacity SKUs and CU economics; admin portal tenant settings; domains and workspaces; auditing and lineage; gateways and on-prem connectivity.

## Implement and Manage (Domain 1)

**Implement security in Microsoft Fabric.** Workspace roles (Admin, Member, Contributor, Viewer); item permissions (Read, ReadAll, Write, Share); RLS in Power BI semantic models and in Warehouse; OLS in semantic models; CLS via T-SQL GRANT/DENY; DDM in Warehouse; sensitivity labels via Microsoft Purview.

**Implement CI/CD in Microsoft Fabric.** Git integration with Azure DevOps or GitHub; per-workspace branch model; deployment pipelines (Dev / Test / Prod) with deployment rules and parameter rebinding; variable libraries for environment-specific values; Fabric REST APIs for automation.

**Manage the analytics development lifecycle.** Workspace-as-code patterns; promotion strategies; testing approaches (data validation, contract tests on Delta); capacity sizing for non-prod environments; backup and recovery patterns.

## Ingest and Transform (Domain 2)

**Ingest data with Microsoft Fabric.** Pipelines (control flow, activities, parameters), Dataflows Gen2 (Power Query M, destinations), Eventstream (real-time), Mirroring (CDC for Cosmos / Snowflake / Azure SQL DB / Fabric SQL DB), OneLake shortcuts (symbolic links to ADLS / S3 / Dataverse), Copy job for bulk migration, Notebook-based ingestion via Spark.

**Get started with Real-Time Intelligence in Fabric.** Eventhouse + KQL Database; ingest via Eventstream; query with KQL; dashboards; Activator alerts. Update policies for ingest-time transforms; materialized views for sub-second aggregates.

**Use Apache Spark to work with files in a lakehouse.** Lakehouse Files vs Tables; reading and writing Delta with PySpark and Spark SQL; the `MERGE INTO` pattern; partitioning and bucketing tradeoffs; notebook authoring; pipeline notebook activities.

**Get started with Data Warehouse in Microsoft Fabric.** Cross-database queries; T-SQL stored procedures; multi-table transactions; the relationship between Lakehouse SQL endpoint (read-only) and Warehouse (full DML); patterns for SCD Type 2 and incremental loading.

**Mirroring in Microsoft Fabric.** Continuous CDC replication into OneLake as read-only Delta; supported sources (Cosmos DB, Snowflake, Azure SQL DB, Fabric SQL DB); schema drift behavior; storage cost (free for replicated data).

**OneLake shortcuts.** Reference data without copying; supported targets (ADLS Gen2, S3, GCS, Dataverse, OneLake); permission inheritance from source; cross-region considerations.

## Monitor and Optimize (Domain 3)

**Monitor activities in Microsoft Fabric.** Monitoring hub for cross-workspace runs; per-item run history; pipeline run insights; integration with Real-Time hub for streaming; diagnostic settings to Log Analytics.

**Use the Microsoft Fabric Capacity Metrics app.** F-SKU CU consumption visualization; throttling states (Interactive Delay -> Interactive Reject -> Background Reject); operation breakdown per item; smoothing windows (5 min interactive, 24 h background).

**Optimize a Lakehouse for analytics.** V-Order (Fabric Parquet sort for Direct Lake reads); OPTIMIZE (file compaction); VACUUM (old version cleanup); partitioning best practices; Z-ORDER for range scans; Auto Compaction and Optimize Write defaults.

**Tune Apache Spark in Microsoft Fabric.** Starter pool vs custom pools (cold start trade-off); autoscale and dynamic allocation; broadcast joins; AQE; cache and persist; shuffle partition tuning; skew handling.

**Get started with Data Activator.** Rule-based alerting on Eventstreams, Power BI metrics, KQL outputs; trigger Power Automate flows, Teams notifications, custom HTTP endpoints; complex conditions over time windows.

---

[<- Extra Concepts](07-extra-dp700-concepts.md) - [Architectures ->](09-arch-dp700.md)
