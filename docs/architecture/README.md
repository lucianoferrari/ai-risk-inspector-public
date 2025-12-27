# High-Level Architecture

AI Risk Inspector is designed as a modular platform that separates **risk execution**, **risk interpretation**, and **reporting** concerns.

```mermaid
flowchart LR
    A[GenAI System<br/>(LLM / Application)] --> B[Probe Execution Layer]
    B --> C[Result Normalization]
    C --> D[Risk Mapping Engine]
    D --> E[Aggregation & Scoring]
    E --> F[Reporting & Visualization]
