# Assessment Methodology

How AI Risk Inspector turns "is this AI system safe enough?" into a repeatable, evidence-producing process. This page describes the approach at the level a security leader, auditor, or governance committee needs; probe content and scoring weights are proprietary.

## 1. Scope and threat model

Every assessment starts with a short scoping record:

- **System type** — chat assistant, RAG application, copilot, tool-using agent, embedded AI feature in a product
- **Data sensitivity** — public, internal, confidential, regulated (PII, PCI, PHI)
- **Autonomy** — informs a human, recommends, acts with approval, acts autonomously
- **Attack surface** — user input, retrieved content, tool outputs, uploaded files, connected systems
- **User population** — internal, partner, public

Sensitivity × autonomy sets the **risk tier**, which determines probe depth and the approval required before production.

## 2. Risk domains

Findings are organized into four domains so that non-security stakeholders can see where risk concentrates:

| Domain | What it covers | Example findings |
|---|---|---|
| **Security** | Prompt injection (direct and indirect), jailbreaks, system-prompt disclosure, tool misuse, excessive agency, insecure output handling | Agent emails data to an attacker-supplied address; retrieved document overrides instructions |
| **Privacy** | Sensitive data disclosure, cross-tenant leakage, training-data extraction, memorization, PII handling in logs | Assistant returns another customer's record; PII present in unredacted traces |
| **Ethics** | Harmful content, bias and discriminatory outputs, manipulation, lack of disclosure | Materially different answers by protected attribute; no AI disclosure to end users |
| **Compliance** | Regulatory and policy alignment, human oversight for consequential decisions, auditability, data residency and retention | Automated decision with no review path; model provider contract lacks no-training clause |

Each finding also carries a mapping to **OWASP Top 10 for LLM Applications** and the relevant **NIST AI RMF** function (Govern / Map / Measure / Manage), so results slot into existing GRC reporting.

## 3. Probe execution

Probes are structured test cases, not ad-hoc prompts. Each has an objective, an input strategy, a success criterion, and a severity if successful. Categories include:

- **Instruction integrity** — direct override, role-play and persona escapes, multi-turn escalation, encoding and translation bypasses
- **Indirect injection** — adversarial content placed in retrieval sources, documents, web pages, and tool results
- **Data boundary** — cross-tenant and cross-user access, system prompt and configuration disclosure, secret extraction
- **Agency and tools** — destination allow-list bypass, scope creep in tool calls, confirmation bypass, loop and spend abuse
- **Output handling** — unsafe code or markup in responses, schema violations, content-policy failures
- **Fairness and harm** — paired-prompt comparisons across attributes, harmful-request handling, disclosure checks

Every run captures the full trace: input, retrieved context, prompt version, model and parameters, tool calls, and output. A finding without a reproducible trace is not reported.

## 4. Normalization and scoring

Raw results are normalized into a common finding schema (domain, framework mapping, severity, reproducibility, affected component, evidence). Scoring aggregates by domain and severity to produce:

- a **domain risk profile** (where the exposure is)
- a **severity distribution** (how bad the worst findings are)
- a **trend** against previous assessments of the same system (is it getting better)

Scores are designed for comparison over time and across systems, not as a certification.

## 5. Reporting

Two outputs from every assessment:

- **Executive summary** — one page: overall posture, top risks in business terms, what changed since last time, decisions needed. Written for the AI governance committee and leadership.
- **Technical report** — every finding with reproduction context, affected component, recommended control, and framework mapping. Written for the engineering team that has to fix it.

## 6. Re-assessment triggers

An assessment is a point in time. Re-run when the model or provider changes, when tools or data sources are added, when the user population changes, after any AI-related incident, and on a fixed cadence for medium- and high-tier systems.

## What this methodology is not

- Not a substitute for a secure architecture (least-privilege tools, tenant-aware retrieval, human confirmation for consequential actions) — it finds where those are missing
- Not a one-time certification — it is a measurement you repeat
- Not a replacement for the model provider's own safety work — it tests *your* system as deployed, with *your* data, tools, and prompts
