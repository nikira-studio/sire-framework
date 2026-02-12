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
To ensure the audit log remains verifiable across different programming languages (e.g., a Python implementation verifying a Rust Ledger), all entries **MUST** be serialized into a **Canonical Format** using the **JSON Canonicalization Scheme (JCS)** before hashing.

**The JCS Standard (RFC 8785)**:
*   **Key Sorting**: Dictionary/Map keys must be sorted alphabetically (ASCII order).
*   **No Whitespace**: All optional whitespace (spaces, tabs, newlines) between tokens must be removed.
*   **Standard Encoding**: Content must be encoded as `UTF-8`.
*   **Numeric Format**: Numbers must be represented in their most compact form (no trailing zeros, no leading zeros except for zero itself).
*   **Unicode Escaping**: Only characters that MUST be escaped (e.g., `"`, `\`, control characters) may be escaped; all other Unicode characters are represented directly.
*   **Consistency**: A `SIRE-v1.0` compliant Ledger must produce identical hashes for identical data regardless of implementation stack.

**Test Case (Verification Standard)**:
*   **Input Data**:
    ```json
    {"actor": "soul_01", "impact": 0.5, "pillar": "S"}
    ```
*   **Expected Canonical String**:
    ```
    {"actor":"soul_01","impact":0.5,"pillar":"S"}
    ```
*   **Expected SHA-256 Hash**:
    ```
    c142dff728132640d1cd3844158fdbcda1cc9f31b59ec26ffdb0e0791978610b
    ```
*   **Implementation Requirement**: All SIRE implementations MUST pass this test case during initialization to verify canonicalization compliance.

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

## 3. Impact-Based Thresholds

To eliminate situational profiling and enforce universal governance, SIRE uses **Impact-Based Thresholds** to determine which actions require Manifest Approval, MFA, and Ledger logging.

### Weighted Impact Score (S)

Every operation is evaluated using a **Weighted Impact Score**:

```
S = 0.5 × Persistence + 0.3 × Reach + 0.2 × Sensitivity
```

**Component Scoring**:
- **Persistence** (0 = Ephemeral, 1 = Immutable): How long the change persists.
- **Reach** (0 = Local, 1 = External Egress): Whether the action affects internal or external systems.
- **Sensitivity** (0 = Generic, 1 = PII/Private): The sensitivity of the data or operation.

### Threshold Presets

Implementations MUST support **Threshold Presets** instead of user profiles:

| Preset | MFA Trigger | Ledger Trigger | Level 3 Manifest |
| :--- | :--- | :--- | :--- |
| **Low-Friction** | S ≥ 0.7 | S ≥ 0.5 | S ≥ 0.6 |
| **Balanced** | S ≥ 0.5 | S ≥ 0.3 | S ≥ 0.4 |
| **High-Integrity** | S ≥ 0.3 | S ≥ 0.1 | S ≥ 0.2 |

**Universal Enforcement**: High-impact operations (S ≥ 0.5) trigger Ledger logging and MFA regardless of threshold preset. This ensures critical actions are always audited.

**Examples**:
- **Local cache clear**: Persistence=0, Reach=0, Sensitivity=0 → **S=0.0** (No approval)
- **Send email**: Persistence=0, Reach=1, Sensitivity=0.5 → **S=0.4** (Level 2, Balanced: Approval)
- **Delete user account**: Persistence=1, Reach=0, Sensitivity=0.5 → **S=0.6** (Level 3 Manifest + MFA, all presets)
- **Export PII to cloud**: Persistence=1, Reach=1, Sensitivity=1 → **S=1.0** (Level 4 Manifest + MFA + Cooldown, all presets)

## 4. Learning Capture Pattern (The Loop)

The Ledger is not just a log; it is a learning mechanism. When a tool fails or self-healing occurs, the entry must capture:
*   **Trauma**: The specific error or failure condition.
*   **Root Cause**: Why it happened.
*   **Correction**: The remedial action taken.
*   **Lesson**: An abstracted rule to prevent recurrence.

### Genetic Patching (Self-Healing Docs)
To prevent "Instruction Drift," SIRE periodically reviews "Trauma" logs:
*   **Proposal**: The Manager proposes specific updates to a **Specialist's handbook** (`AGENT.md`) to codify lessons learned.
*   **Evolution**: The Managing Associate approves these "Genetic Patches," permanently upgrading the system's baseline competence.
## 5. Tiered Archival & Pruning (Checkpoint Protocol)
To prevent "Soul Bloat" and performance degradation while maintaining **Integrity**, the Ledger implements a **Checkpoint Protocol** for tiered archival.

**The Protocol**:
*   **Cold Segment Compression**: After a configurable period (default: 90 days), "Cold" segments of the hash chain are compressed into a single **Consolidated Checkpoint Entry**.
*   **Merkle Root Preservation**: The consolidated entry contains the Merkle Root of all archived entries, preserving the audit trail without requiring the full raw history in active memory.
*   **Verification Continuity**: The checkpoint entry itself is hashed and linked into the active chain, ensuring cryptographic continuity from genesis to present.

**Checkpoint Entry Structure**:
```json
{
  "checkpoint_id": "uuid-v4",
  "type": "consolidated_checkpoint",
  "timestamp": "ISO-8601-UTC",
  "period_start": "ISO-8601-UTC",
  "period_end": "ISO-8601-UTC",
  "entry_count": 15420,
  "merkle_root": "SHA256_hash_of_all_archived_entries",
  "archival_signature": "SHA256(checkpoint_id + merkle_root + timestamp)",
  "compression_algorithm": "zstd",
  "compression_ratio": 0.85
}
```

**Performance Requirements**:
*   **Active Memory**: Only the most recent 90 days of Ledger entries must be kept in active memory for real-time verification.
*   **Cold Storage**: Archived segments may be stored in compressed form with optional tiered storage (e.g., SSD for recent checkpoints, HDD for deep archives).
*   **Query Performance**: PITR requests for archived segments must resolve within 5 seconds (including decompression time).

## 6. Point-in-Time Recovery (PITR)
To maintain **Integrity** and **Resilience**, the Ledger protocol **MUST** support the restoration of previous valid states.

*   **Requirement**: The system must be capable of reverting its entire cognitive and operational state to any previous hash-verified Ledger entry (including checkpoint boundaries).
*   **Soul Rollback**: This provides a native mechanism to reverse "Instruction Drift," catastrophic reasoning errors, or "Trauma" by returning to a baseline of known truth.
*   **Audit**: A PITR event is itself a recorded action, preserving the timeline of the entity's evolution even through a recovery event.
