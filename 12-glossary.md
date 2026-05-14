# Glossary - DP-700

> Alphabetical. Acronyms expanded inline.

| Term | Definition |
|---|---|
| **Activator (Data Activator / Reflex)** | Fabric service for rule-based alerting on streams, KQL output, or Power BI metrics. Triggers Power Automate, Teams, or HTTP endpoints. |
| **AQE** | Adaptive Query Execution - Spark feature that re-optimizes plans at runtime based on actual stats. |
| **Bursting** | Capacity feature letting a single op briefly exceed CU; repaid via smoothing. |
| **Capacity (F-SKU)** | Compute + billing boundary in Fabric. F2, F4, F8, ..., F2048. |
| **CDC** | Change Data Capture - source-side log of inserts/updates/deletes used by Mirroring. |
| **CLS** | Column-Level Security - T-SQL GRANT/DENY on specific columns. |
| **Copy job** | Standalone Fabric item for bulk data movement with simple mapping. |
| **CU** | Capacity Unit - Fabric's unit of compute consumption. |
| **Dataflow Gen2** | Power Query M low-code transformation tool. Outputs to Lakehouse / Warehouse / KQL / SQL DB. |
| **DDM** | Dynamic Data Masking - column-level presentation mask in Warehouse / SQL DB. |
| **Delta Lake** | Open-source table format on Parquet with ACID transactions, time travel, schema enforcement. Native to Fabric. |
| **Deployment pipeline** | Built-in Fabric tool to promote artifacts Dev -> Test -> Prod with deployment rules. |
| **Direct Lake** | Power BI semantic model mode that reads OneLake parquet at query time without import or refresh. |
| **DirectQuery** | Power BI mode that issues live queries to source. |
| **Domain** | Business grouping of workspaces in a Fabric tenant. Not a security boundary. |
| **Eventhouse** | Container for one or more KQL Databases in Real-Time Intelligence. |
| **Eventstream** | No-code stream processor that ingests from Event Hubs, IoT Hub, Kafka, custom apps to Eventhouse / Lakehouse. |
| **F-SKU** | Pay-as-you-go or reserved Fabric capacity SKU (F2, F4, ...). |
| **Git integration** | Per-workspace branch-based source control to Azure DevOps or GitHub. |
| **Import (semantic model)** | In-memory cached Power BI model with scheduled refresh. |
| **KQL** | Kusto Query Language - read-optimized query language for telemetry / time-series. |
| **Lakehouse** | Fabric item combining Files + Tables (Delta) area. Multi-engine (Spark + SQL endpoint + KQL via shortcut). |
| **Materialized view** | Precomputed aggregate served sub-second. Available in Warehouse (preview) and KQL. |
| **MERGE** | SQL/Spark statement that performs upsert (INSERT + UPDATE + DELETE) in one pass. |
| **Mirroring** | Continuous CDC replication of Cosmos / Snowflake / Azure SQL DB / Fabric SQL DB into Fabric as read-only Delta. |
| **Monitoring hub** | Tenant-wide cross-workspace view of pipeline / notebook / dataflow runs. |
| **Notebook** | Interactive code experience for PySpark / Spark SQL / Scala / R in Fabric. |
| **OLS** | Object-Level Security - hide tables / columns at semantic model level. |
| **OneLake** | Single tenant-wide data lake under all Fabric workloads. ADLS Gen2-compatible. |
| **OneLake shortcut** | Symbolic link from a Lakehouse to external data (ADLS, S3, GCS, Dataverse, OneLake). |
| **OPTIMIZE** | Delta command that compacts many small files into ~1 GB target files. |
| **Pipeline (Data Factory)** | Orchestration item with activities, control flow, parameters, and schedule. |
| **Real-Time Dashboard** | KQL-backed sub-second visualization. |
| **Real-Time hub** | Centralized view of all streams across the tenant. |
| **Reflex** | See Activator. |
| **Result-set cache** | Warehouse feature that caches identical SELECT results until source data changes. |
| **RLS** | Row-Level Security - filter rows by user identity. DAX role on semantic model OR T-SQL CREATE SECURITY POLICY in Warehouse. |
| **SCD Type 2** | Slowly Changing Dimension that keeps historical rows with current-flag + start/end dates. |
| **Semantic model** | Power BI tabular model. Modes: Direct Lake / Import / DirectQuery / Composite. |
| **Sensitivity label** | Microsoft Purview classification (Confidential, Highly Confidential, ...) that propagates through Fabric items and exports. |
| **Service principal** | Entra app identity for non-interactive automation. |
| **Shortcut** | See OneLake shortcut. |
| **Smoothing** | Fabric capacity feature that averages CU usage over time (5 min interactive, 24 h background). |
| **Spark pool** | Compute fleet for notebooks. Starter pool (warm, shared) vs custom pool (cold, isolated). |
| **SQL endpoint** | Read-only T-SQL interface over a Lakehouse. |
| **Update policy (KQL)** | Ingest-time KQL transform that writes into a derived table. |
| **VACUUM** | Delta command that removes old file versions older than retention threshold (default 7 days). |
| **Variable library** | Reusable, environment-specific variables consumed by pipelines, dataflows, notebooks. |
| **V-Order** | Fabric Parquet write-time sort that accelerates Direct Lake / VertiPaq reads. |
| **Warehouse** | Full T-SQL multi-table-transactional store in Fabric. |
| **Workspace** | Permissions + governance unit. Assigned to one capacity. Holds items. |
| **Workspace identity** | Workspace-owned managed identity for accessing Azure resources without per-user grants. |
| **Z-ORDER** | Delta technique that co-locates rows with similar values in the same files for faster range scans. |

---

[<- Microsoft Resources](11-microsoft-resources.md) - [Flashcards ->](13-flashcards.md)
