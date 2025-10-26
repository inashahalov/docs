flowchart TD
    subgraph Sources
        A[Application Pods\n(stdout, files, HTTP)]
    end

    subgraph EdgeAgents
        B[Fluent Bit\n(DaemonSet)\n- lightweight\n- tail files]
        C[Vector\n(sidecar / host)\n- parsing\n- enrichment\n- routing]
    end

    subgraph AggregationLayer
        D[Vector\n(Aggregator)\n- disk buffering\n- deduplication\n- dynamic routing\n- observability]
    end

    subgraph Destinations
        E[Loki\n(logs)\n- labels\n- compaction]
        F[Elasticsearch\n(full-text, ML)\n- index templates\n- anomaly detection]
        G[Kafka\n(buffering tier)\n- replayable\n- decoupling]
    end

    subgraph Analytics
        H[ClickHouse\n(analytics)\n- Kafka Engine\n- materialized views]
    end

    subgraph UI
        I[Grafana\n(Unified UI)\n- Loki logs\n- ES dashboards\n- CH panels]
    end

    %% Connections
    A -->|raw logs| B
    A -->|structured/metrics| C
    B -->|forward| C
    C -->|structured, labeled| D

    D -->|logs| E
    D -->|searchable events| F
    D -->|high-throughput events| G

    G -->|stream| H

    E --> I
    F --> I
    H --> I

    %% Styling
    classDef source fill:#e6f3ff,stroke:#333;
    classDef agent fill:#d4f1e5,stroke:#333;
    classDef agg fill:#fff8dc,stroke:#333;
    classDef dest fill:#f0e6ff,stroke:#333;
    classDef analytics fill:#ffe6e6,stroke:#333;
    classDef ui fill:#fff0e6,stroke:#333;

    class A source
    class B,C agent
    class D agg
    class E,F,G dest
    class H analytics
    class I ui
