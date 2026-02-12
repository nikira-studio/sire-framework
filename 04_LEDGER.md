# 04. The Ledger

The **Ledger** is the central nervous system of accountability. It is an immutable, crypto-verified audit log that records every state change, decision, and action taken by the entity.

## 1. Immutable Audit Protocol

A SIRE implementation **MUST** fulfill the following cryptographic requirements for its audit log:

### The Hash Chain
To prevent history rewriting (gaslighting or cover-ups), the Ledger implements a **SHA-256 Hash Chain**:
*   **Structure**: `Entry(N).hash` = `SHA256(Entry(N).canonical_content + Entry(N-1).hash)`
*   **Verification**: The system must validate the chain integrity on startup.
*   **Tamper Response**: If the hash chain is broken, the system **MUST** immediately enter **Alert State** and lock down all autonomy until the Managing Associate intervenes.

### Canonical Serialization (Deterministic Hashing)
To ensure the audit log remains verifiable across different programming languages (e.g., a Python implementation verifying a Rust Ledger), all entries **MUST** be serialized into a **Canonical Format** before hashing:
*   **Key Sorting**: Dictionary/Map keys must be sorted alphabetically.
*   **No Whitespace**: All optional whitespace (spaces, tabs, newlines) between tokens must be removed.
*   **Standard Encoding**: Content must be encoded as `UTF-8`.
*   **Consistency**: A `SIRE-v1` compliant Ledger must produce identical hashes for identical data regardless of implementation stack.

### Single Source of Truth
*   **Requirement**: All components—including Extensions, **Specialists**, and external webhooks—**MUST** pipe their operational logs to the Main Ledger.
*   **Prohibition**: Independent, siloed log files that bypass the Ledger are strictly prohibited to ensure a unified **Sovereign Audit**.

### Semantic Conflict Resolution
To maintain **Deterministic Integrity** in a multi-specialist environment, the system must handle write collisions:
*   **The Problem**: Multiple **Specialists** or external pulses may attempt to update system state or the Ledger simultaneously.
*   **The Protocol**: The Manager (The Cortex) performs a **Semantic Diff** before hashing an entry. If a collision is detected, the Manager must resolve the conflict based on **Constitutional Priority** (e.g., a Security Sentinel log overrides a Skill utility log) to ensure the SHA-256 chain remains linear and uncorrupted.

## 2. Event Log Specification

Every entry in the Ledger must contain:
1.  **Timestamp** (ISO-8601 UTC)
2.  **Actor** (Soul ID, Specialist ID, or System Process)
3.  **Action** (The specific tool or decision executed)
4.  **Justification** (Link to a Sovereign Core pillar: Sovereignty, Integrity, Resilience, Evolution)
5.  **Hash** (SHA-256 verification string)

## 3. Learning Capture Pattern (The Loop)

The Ledger is not just a log; it is a learning mechanism. When a tool fails or self-healing occurs, the entry must capture:
*   **Trauma**: The specific error or failure condition.
*   **Root Cause**: Why it happened.
*   **Correction**: The remedial action taken.
*   **Lesson**: An abstracted rule to prevent recurrence.

### Genetic Patching (Self-Healing Docs)
To prevent "Instruction Drift," SIRE periodically reviews "Trauma" logs:
*   **Proposal**: The Manager proposes specific updates to a **Specialist's handbook** (`AGENT.md`) to codify lessons learned.
*   **Evolution**: The Managing Associate approves these "Genetic Patches," permanently upgrading the system's baseline competence.
## 4. Point-in-Time Recovery (PITR)
To maintain **Integrity** and **Resilience**, the Ledger protocol **MUST** support the restoration of previous valid states.

*   **Requirement**: The system must be capable of reverting its entire cognitive and operational state to any previous hash-verified Ledger entry.
*   **Soul Rollback**: This provides a native mechanism to reverse "Instruction Drift," catastrophic reasoning errors, or "Trauma" by returning to a baseline of known truth.
*   **Audit**: A PITR event is itself a recorded action, preserving the timeline of the entity's evolution even through a recovery event.
