# Pitfalls and Exam Traps - DP-700

> The 12 most common mistakes and trap distinctions on DP-700.

## 1. Lakehouse SQL endpoint is read-only

The SQL endpoint of a Lakehouse cannot run `INSERT / UPDATE / DELETE / MERGE`. Use **Spark** or write through the **Warehouse**.

## 2. Mirroring vs Shortcut confusion

- **Mirroring** = continuous CDC replication into a Fabric-owned read-only Delta copy. Sources: Cosmos / Snowflake / Azure SQL DB / Fabric SQL DB.
- **Shortcut** = symbolic link to existing data (ADLS / S3 / GCS / Dataverse / OneLake). No copy.

## 3. Direct Lake silently falls back to DirectQuery

Unsupported data types, missing V-Order, or large queries trigger fallback. Power BI users see "DirectQuery" in the model and worse perf. Verify V-Order is on and column types are supported.

## 4. Domain != security boundary

Domain is business metadata. Permissions are still set per **workspace**.

## 5. Workspace role vs item permission

A **Viewer** in the workspace can still be granted item-level **ReadAll** to consume a Power BI report on a Lakehouse via Direct Lake. Don't conflate the two layers.

## 6. DDM is not encryption

Dynamic Data Masking is a presentation-layer mask. Users with `UNMASK` permission see real values. For cryptographic protection, use **Always Encrypted** or column encryption.

## 7. VACUUM with low retention breaks time travel

Default 7 days. Going lower needs a flag override and a real reason. After VACUUM, time travel can no longer reach versions older than retention.

## 8. Deployment pipelines do not require Git, and vice versa

They solve different problems (source control vs stage promotion). Most teams use both. The exam often presents one without the other.

## 9. Pipeline Copy activity != Copy job

- **Copy activity** is one task inside a pipeline.
- **Copy job** is a standalone item with simpler scheduling for bulk migration.

## 10. Capacity throttling order

**Interactive Delay -> Interactive Reject -> Background Reject.** Pipelines fail under Background Reject before users notice slow reports. Watch the **Throttling tab** in the Capacity Metrics app.

## 11. Eventstream destination matters

- `-> Lakehouse` lands data as Delta - query with Spark / SQL endpoint / Direct Lake.
- `-> Eventhouse / KQL DB` lands data for KQL queries / Real-Time dashboards / Activator.

Pick the destination that matches your query engine.

## 12. Spark starter pool vs custom pool

Starter pool = warm, shared, fast start. Custom pool = isolated, configurable nodes / libraries, but ~2-3 min cold start. Pick based on latency requirement.

## 13. Variable library is the modern way to parameterize

Old patterns put per-environment values in pipeline parameters or notebook config. The exam favors **variable libraries** for cross-item, per-stage variables.

## 14. Sync delay on Lakehouse SQL endpoint

After writing a Lakehouse table, the SQL endpoint may take a few seconds to reflect new rows. Force a refresh by querying `sys.tables` or via REST API if a downstream T-SQL step depends on it.

## 15. Dataflow Gen2 needs a destination

Without a destination configured, the data is computed but not stored. A Dataflow Gen2 with no destination produces no output table.

---

[<- Flashcards](13-flashcards.md) - [Hands-on Labs ->](15-hands-on-labs.md)
