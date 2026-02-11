# 04. The Ledger

The **Ledger** is the central nervous system of accountability. It is an immutable, crypto-verified audit log that records every state change, decision, and action taken by the entity.

## 1. Immutable Audit Protocol

A SIRE implementation **MUST** fulfill the following cryptographic requirements for its audit log:

### The Hash Chain
To prevent history rewriting (gaslighting or cover-ups), the Ledger implements a **SHA-256 Hash Chain**:
*   **Structure**: `Entry(N).hash` = `SHA256(Entry(N).content + Entry(N-1).hash)`
*   **Verification**: The system must validate the chain integrity on startup.
*   **Tamper Response**: If the hash chain is broken, the system **MUST** immediately enter **Alert State** and lock down all autonomy until the Managing Associate intervenes.

### Single Source of Truth
*   **Requirement**: All components—including Extensions, Staff Associates, and external webhooks—**MUST** pipe their operational logs to the Main Ledger.
*   **Prohibition**: Independent, siloed log files that bypass the Ledger are strictly prohibited to ensure a unified **Sovereign Audit**.

## 2. Event Log Specification

Every entry in the Ledger must contain:
1.  **Timestamp** (ISO-8601 UTC)
2.  **Actor** (Soul ID, Staff ID, or System Process)
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
*   **Proposal**: The Manager proposes specific updates to a Technician's handbook (`AGENT.md`) to codify lessons learned.
*   **Evolution**: The Managing Associate approves these "Genetic Patches," permanently upgrading the system's baseline competence.
