# AI System Design and Development Documentation — Oxcart Agent Platform

Document owner: AI Governance Office. Version 3.2. Approved 2026-08-14. Review cycle: annual. Next review: 2026-12-31.

## 1. Scope and AI system inventory

This document covers the design and development of every AI system in the Oxcart platform:
the Bedrock agents (`OC7ONZZZVW`, `KJP2US73C6`), their AgentCore runtimes and runtime
endpoints, the `oxcart_Agent_mem` memory store, and the `Y3A6EA3CCM` knowledge base.
The inventory is reconciled quarterly against the account's resource tags.

## 2. Requirements specification

Functional and non-functional requirements for each AI system are recorded in the platform
requirements register (REQ-AI-001 through REQ-AI-214) and traced to design elements. Each
requirement carries an owner, an acceptance test, and a risk classification. Requirements
covering accuracy, latency, and refusal behaviour have quantified thresholds: retrieval
precision >= 0.85, p99 response latency <= 4s, and a refusal rate on the red-team prompt
suite of >= 0.98.

## 3. Architecture and design decisions

The system design is recorded as a set of architecture decision records (ADR-AI-01 .. ADR-AI-37),
each stating the decision, the alternatives considered, and the rationale. Design documentation
covers data flow between the agent, the knowledge base and the memory store; the trust boundary
at the runtime endpoint; and the model selection rationale, including why a managed foundation
model was chosen over a fine-tuned variant.

## 4. Data and model provenance

Training and grounding data sources are catalogued with lineage, licence, and retention terms.
The knowledge base is populated only from the approved corpus; ingestion is gated by a
classification check that rejects documents above Confidential. Model versions in use are
pinned and recorded, and every change to a pinned version requires re-running the evaluation
suite in section 6.

## 5. Development lifecycle controls

All changes to AI system code, prompts, and configuration go through peer review with at least
two approvals, automated static analysis, and the evaluation gate. Prompts are version
controlled alongside code. No developer can deploy to production without an approved change
record. Development, staging and production environments are separate accounts.

## 6. Verification and validation

Before each release the system is evaluated against a held-out benchmark and an adversarial
red-team suite covering prompt injection, data exfiltration, and harmful-content refusal.
Results are recorded with the model version, the dataset hash, and the pass/fail verdict
against the thresholds in section 2. A release is blocked on any threshold regression.

## 7. Deployment, monitoring and change management

Deployments are automated and auditable. In production, the runtime emits per-invocation
telemetry to CloudWatch in the AI-governance namespaces, with alarms on error rate, refusal
rate drift, and latency. Incidents are triaged through the standard operational process and
post-incident reviews feed back into the requirements register.

## 8. Roles and competence

The AI Governance Office owns this document. Named accountable roles exist for data
stewardship, model evaluation, and production operation; each role has documented competence
requirements and annual training records.
