# High-Level Architecture

AI Risk Inspector is designed as a modular platform that separates risk execution, risk interpretation, and reporting concerns.

```mermaid
flowchart LR
    A[GenAI System]
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
```

## Architectural Principles

- Separation of concerns
- Extensible risk probes and categories
- Repeatable and auditable assessments
- Security-first output handling
