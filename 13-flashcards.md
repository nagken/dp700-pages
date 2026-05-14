# Flashcards: Active Recall - DP-700

> Click any card to reveal the answer. Use the **Domain pager bottom-right** to switch between exam areas.

<section class="fc-section" data-fc-title="Implement and Manage">
<h2>1 - Implement and Manage</h2>

<div class="flashcard-grid">

<div class="flashcard"><div class="fc-q">Name the four Fabric workspace roles in order of decreasing power.</div><div class="fc-a"><strong>Admin -> Member -> Contributor -> Viewer.</strong></div></div>

<div class="flashcard"><div class="fc-q">Which workspace role can edit items but not add new users?</div><div class="fc-a"><strong>Contributor.</strong></div></div>

<div class="flashcard"><div class="fc-q">What is the security boundary in Fabric: capacity, workspace, or domain?</div><div class="fc-a"><strong>Workspace.</strong> Capacity is billing/compute; domain is organizational metadata.</div></div>

<div class="flashcard"><div class="fc-q">Difference between a Fabric domain and a workspace?</div><div class="fc-a"><strong>Domain</strong> = business grouping for discovery + endorsement. <strong>Workspace</strong> = permissions + governance unit holding items.</div></div>

<div class="flashcard"><div class="fc-q">How do you give a workspace access to ADLS Gen2 without per-user grants?</div><div class="fc-a">Use the <strong>workspace identity</strong> (or a service principal) and grant it the appropriate role on the storage account.</div></div>

<div class="flashcard"><div class="fc-q">RLS vs OLS vs CLS vs DDM - which one masks part of a value?</div><div class="fc-a"><strong>DDM</strong> (Dynamic Data Masking). RLS filters rows; OLS hides columns/tables in the semantic model; CLS hides columns in the Warehouse via GRANT/DENY.</div></div>

<div class="flashcard"><div class="fc-q">Is DDM cryptographic encryption?</div><div class="fc-a"><strong>No.</strong> DDM is a presentation-layer mask. Privileged users with UNMASK see real values.</div></div>

<div class="flashcard"><div class="fc-q">Do you need Git integration to use deployment pipelines?</div><div class="fc-a"><strong>No.</strong> They are independent. Git = source control; deployment pipelines = stage promotion. Most teams use both.</div></div>

<div class="flashcard"><div class="fc-q">What does a deployment rule do?</div><div class="fc-a">Rebinds connections, parameters, semantic model bindings, or Lakehouse references between stages so Dev settings don't ship to Prod.</div></div>

<div class="flashcard"><div class="fc-q">Where do you store environment-specific connection strings outside item code?</div><div class="fc-a"><strong>Variable library.</strong></div></div>

</div>
</section>

<section class="fc-section" data-fc-title="Ingest and Transform">
<h2>2 - Ingest and Transform</h2>

<div class="flashcard-grid">

<div class="flashcard"><div class="fc-q">Continuous CDC replication of Cosmos DB into Fabric - which feature?</div><div class="fc-a"><strong>Mirroring.</strong></div></div>

<div class="flashcard"><div class="fc-q">Symbolic reference to existing ADLS / S3 data without copying - which feature?</div><div class="fc-a"><strong>OneLake shortcut.</strong></div></div>

<div class="flashcard"><div class="fc-q">Real-time stream of IoT events into Fabric - which feature?</div><div class="fc-a"><strong>Eventstream -> Eventhouse / KQL DB.</strong></div></div>

<div class="flashcard"><div class="fc-q">Low-code Power Query transformation - which Fabric tool?</div><div class="fc-a"><strong>Dataflow Gen2.</strong></div></div>

<div class="flashcard"><div class="fc-q">Multi-step orchestrated ETL with parameters and schedule - which Fabric tool?</div><div class="fc-a"><strong>Data Factory pipeline.</strong></div></div>

<div class="flashcard"><div class="fc-q">Lakehouse vs Warehouse - which supports SQL DML (INSERT/UPDATE/DELETE/MERGE)?</div><div class="fc-a"><strong>Warehouse.</strong> Lakehouse SQL endpoint is read-only; write via Spark or Warehouse.</div></div>

<div class="flashcard"><div class="fc-q">Mirrored data in Fabric - read-only or read-write?</div><div class="fc-a"><strong>Read-only.</strong></div></div>

<div class="flashcard"><div class="fc-q">Name the medallion layers in order.</div><div class="fc-a"><strong>Bronze -> Silver -> Gold.</strong> Raw -> cleaned/conformed -> aggregated/star schema.</div></div>

<div class="flashcard"><div class="fc-q">In KQL Real-Time Intelligence, what does an <em>update policy</em> do?</div><div class="fc-a">Runs a KQL transform at ingest time, writing into a derived table. Like a streaming insert trigger.</div></div>

<div class="flashcard"><div class="fc-q">Which engine should you pick for streaming aggregations on telemetry?</div><div class="fc-a"><strong>KQL</strong> in Eventhouse, with materialized views for sub-second serving.</div></div>

</div>
</section>

<section class="fc-section" data-fc-title="Monitor and Optimize">
<h2>3 - Monitor and Optimize</h2>

<div class="flashcard-grid">

<div class="flashcard"><div class="fc-q">Tool for cross-workspace pipeline run history?</div><div class="fc-a"><strong>Monitoring hub.</strong></div></div>

<div class="flashcard"><div class="fc-q">Tool for capacity CU consumption + throttling diagnosis?</div><div class="fc-a"><strong>Capacity Metrics app.</strong></div></div>

<div class="flashcard"><div class="fc-q">Three throttling states in order of severity?</div><div class="fc-a"><strong>Interactive Delay -> Interactive Reject -> Background Reject.</strong></div></div>

<div class="flashcard"><div class="fc-q">What does V-Order do?</div><div class="fc-a">Fabric-specific Parquet write-time sort that accelerates Direct Lake / VertiPaq reads. ~15% extra write CPU, large read win.</div></div>

<div class="flashcard"><div class="fc-q">OPTIMIZE vs VACUUM - what does each do?</div><div class="fc-a"><strong>OPTIMIZE</strong> compacts small files. <strong>VACUUM</strong> removes old versions past retention (default 7 days).</div></div>

<div class="flashcard"><div class="fc-q">Smoothing window for interactive vs background ops?</div><div class="fc-a"><strong>5 minutes</strong> interactive; <strong>24 hours</strong> background.</div></div>

<div class="flashcard"><div class="fc-q">Spark notebook OOM on a join with a small dim - fix?</div><div class="fc-a">Use <strong>broadcast(small_df)</strong> to avoid shuffling the large side.</div></div>

<div class="flashcard"><div class="fc-q">Skewed key in Spark causing one task to run long - fix?</div><div class="fc-a"><strong>Salt the key</strong> + repartition; or enable AQE skew handling.</div></div>

<div class="flashcard"><div class="fc-q">Activator can trigger which channels?</div><div class="fc-a"><strong>Power Automate, Teams, custom HTTP endpoint.</strong> (Email comes via Power Automate.)</div></div>

<div class="flashcard"><div class="fc-q">Where do you send Fabric audit logs for SIEM correlation?</div><div class="fc-a"><strong>Diagnostic settings -> Log Analytics</strong> (or Event Hubs / Storage).</div></div>

<div class="flashcard"><div class="fc-q">How do you reduce capacity cost when dev is idle outside business hours?</div><div class="fc-a"><strong>Pause the capacity</strong> on a schedule. Storage is still billed; compute is not.</div></div>

</div>
</section>

---

[<- Glossary](12-glossary.md) - [Pitfalls ->](14-pitfalls.md)
