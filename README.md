flowchart TD
    subgraph Критерий
        A1["Язык реализации"]
        A2["Потребление памяти"]
        A3["Поддержка парсинга"]
        A4["Fault tolerance"]
        A5["Observability"]
        A6["Поддержка выходов"]
        A7["Гибкость конфигурации"]
    end

    subgraph Beats__Elastic_
        B1["Go"]
        B2["~50–100 MB"]
        B3["Ограниченная (через LS)"]
        B4["DLQ (в Logstash)"]
        B5["Через ES/Kibana"]
        B6["ES, Kafka, Logstash"]
        B7["Низкая"]
    end

    subgraph Fluent_Bit__CNCF_
        C1["C"]
        C2["~1–5 MB"]
        C3["Встроенные парсеры"]
        C4["Mem/FS buffer"]
        C5["Prometheus endpoint"]
        C6["80+ (ES, Loki, S3…)"]
        C7["Средняя"]
    end

    subgraph Vector__Datadog_
        D1["Rust"]
        D2["~10–30 MB"]
        D3["Rich transforms"]
        D4["Disk buffer + ACK"]
        D5["Встроенная (metrics, logs)"]
        D6["60+ (включая OTLP)"]
        D7["Высокая (YAML + DSL)"]
    end

    A1 --> B1
    A2 --> B2
    A3 --> B3
    A4 --> B4
    A5 --> B5
    A6 --> B6
    A7 --> B7

    A1 --> C1
    A2 --> C2
    A3 --> C3
    A4 --> C4
    A5 --> C5
    A6 --> C6
    A7 --> C7

    A1 --> D1
    A2 --> D2
    A3 --> D3
    A4 --> D4
    A5 --> D5
    A6 --> D6
    A7 --> D7

    classDef header fill:#e0e0e0,stroke:#333;
    classDef col1 fill:#f9f,stroke:#333;
    classDef col2 fill:#cff,stroke:#333;
    classDef col3 fill:#cfc,stroke:#333;

    class A1,A2,A3,A4,A5,A6,A7 header
    class B1,B2,B3,B4,B5,B6,B7 col1
    class C1,C2,C3,C4,C5,C6,C7 col2
    class D1,D2,D3,D4,D5,D6,D7 col3
