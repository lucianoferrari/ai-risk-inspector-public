```mermaid
flowchart LR
    A[GenAI System (LLM / Application)]
    B[Probe Execution Layer]
    C[Result Normalization]
    D[Risk Mapping Engine]
    E[Aggregation and Scoring]
    F[Reporting and Visualization]

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
