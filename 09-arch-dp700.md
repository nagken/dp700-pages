# Reference Architectures - DP-700

> Canonical Fabric architectures you should be able to draw on a whiteboard.

## 1. Medallion Lakehouse (batch ETL)

```mermaid
flowchart LR
    SRC[Source<br/>Azure SQL DB / SaaS / Files]
    SRC --> PL[Pipeline + Copy / Dataflow Gen2]
    PL --> BR[Bronze<br/>Lakehouse Files + raw Delta]
    BR --> NB1[Notebook Spark<br/>clean + dedupe]
    NB1 --> SLV[Silver<br/>cleaned Delta]
    SLV --> NB2[Notebook Spark<br/>conform + aggregate]
    NB2 --> GLD[Gold<br/>star schema Delta]
    GLD --> SM[Direct Lake semantic model]
    SM --> PBI[Power BI report]
```

## 2. Real-time intelligence (streaming)

```mermaid
flowchart LR
    DEV[Devices / IoT / app events]
    DEV --> EH[Azure Event Hubs / Kafka]
    EH --> ES[Eventstream]
    ES --> EHO[Eventhouse / KQL DB]
    EHO --> MV[Materialized view]
    MV --> RTD[Real-Time Dashboard]
    EHO --> ACT[Activator rule]
    ACT --> ALR[Teams / Email / Power Automate]
```

## 3. Mirroring + Direct Lake (zero-ETL analytics)

```mermaid
flowchart LR
    OPS[(Cosmos DB /<br/>Snowflake /<br/>Azure SQL DB)]
    OPS -->|Mirror CDC| MIR[Mirrored DB in Fabric]
    MIR --> SQL[SQL endpoint]
    SQL --> SM[Direct Lake semantic model]
    SM --> PBI[Power BI report]
```

## 4. Hybrid: Lakehouse + Warehouse

```mermaid
flowchart LR
    SRC[Source] --> PL[Pipeline] --> LH[Lakehouse<br/>Bronze + Silver]
    LH -->|Cross-DB query| WH[Warehouse<br/>Gold + dims/facts]
    WH --> SM[Direct Lake semantic model]
    SM --> PBI[Power BI]

    LH --> NB[Notebook<br/>data science]
    NB --> ML[ML model]
```

## 5. CI/CD with Git + Deployment Pipelines

```mermaid
flowchart LR
    Dev[Workspace: Dev] -- Git --> Repo[(Azure DevOps / GitHub)]
    Repo -- Pull --> Test[Workspace: Test]
    Test -- Deployment Pipeline + rules --> Prod[Workspace: Prod]
    VL[Variable Library] -.-> Dev
    VL -.-> Test
    VL -.-> Prod
```

## 6. Cross-cloud lake federation via shortcuts

```mermaid
flowchart LR
    S3[(AWS S3 lake)]
    ADLS[(Azure ADLS Gen2)]
    OL[(Other tenant OneLake)]

    S3 -. shortcut .-> LH[Lakehouse]
    ADLS -. shortcut .-> LH
    OL -. shortcut .-> LH

    LH --> NB[Notebook Spark<br/>unified query]
    LH --> SM[Direct Lake semantic model]
    SM --> PBI[Power BI]
```

## 7. Ingest from on-premises

```mermaid
flowchart LR
    OnP[(On-prem SQL Server)]
    OnP --- GW[On-premises data gateway]
    GW --> PL[Data Factory pipeline<br/>Copy activity]
    PL --> LH[Lakehouse]
    LH --> WH[Warehouse]
    WH --> SM[Semantic model]
    SM --> PBI[Power BI]
```

## 8. Secure data sharing across business units

```mermaid
flowchart LR
    LHA[Lakehouse: Sales] -. shortcut .-> LHB[Lakehouse: Marketing]
    RLS[RLS on semantic model] -.-> SM[Marketing semantic model]
    LHB --> SM
    SM --> PBI[Marketing Power BI<br/>filtered by region]
    SL[Sensitivity Label: Confidential] -.-> LHA
    SL -.-> SM
```

## 9. Activator end-to-end (operational alerting)

```mermaid
flowchart LR
    METRIC[Power BI metric<br/>Failed Orders %]
    KQL[KQL output<br/>Sensor anomaly]
    ES[Eventstream]

    METRIC --> ACT[Activator rule]
    KQL --> ACT
    ES --> ACT

    ACT --> A1[Teams channel post]
    ACT --> A2[Power Automate flow]
    ACT --> A3[Custom HTTP endpoint]
```

## 10. Capacity isolation strategy

```mermaid
flowchart TD
    F8P[F8 capacity - Prod<br/>BI + nightly ETL]
    F4D[F4 capacity - Dev/Test<br/>devs experimenting]
    F2D[F2 capacity - Sandbox<br/>POCs]

    WSP[Prod workspaces] --> F8P
    WSD[Dev/Test workspaces] --> F4D
    WSS[Sandbox workspaces] --> F2D

    NOTE[Why isolate:<br/>dev throttling won't hurt prod<br/>budgets are per-capacity<br/>pause non-prod overnight]
```

---

[<- Learn Summaries](08-learn-summaries.md) - [Microsoft Resources ->](11-microsoft-resources.md)
