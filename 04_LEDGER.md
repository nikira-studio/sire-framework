# 04. The Ledger

The **Ledger** is the central nervous system of accountability. It is an immutable, crypto-verified audit log that records every state change, decision, and action taken by the entity.

## 1. Immutable Audit Protocol

A SIRE implementation **MUST** fulfill the following cryptographic requirements for its audit log:

### The Hash Chain (MANDATORY)
To prevent history rewriting (gaslighting or cover-ups), the Ledger implements a **SHA-256 Hash Chain**:
*   **Architectural Requirement**: The Ledger MUST implement a cryptographically secure SHA-256 hash chain where `Entry(N).hash` = `SHA256(Entry(N).canonical_content + Entry(N-1).hash)`.
*   **Verification**: The system MUST validate the chain integrity on startup before allowing any operations.
*   **Tamper Response**: If the hash chain is broken, the system **MUST** immediately enter **Alert State** and lock down all autonomy until the Managing Associate intervenes.

### Canonical Serialization (MANDATORY - JCS Standard)
**Architectural Requirement**: To ensure the audit log remains verifiable across different programming languages (e.g., a Python implementation verifying a Rust Ledger), all entries **MUST** be serialized into a **Canonical Format** using the **JSON Canonicalization Scheme (RFC 8785)** before hashing. This ensures cross-platform hash consistency and allows implementations in any language to verify the same Ledger.

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

### Execution Lineage Contract (MANDATORY)
To ensure audits, recovery, and observability are comparable across SIRE implementations, the Ledger **MUST** enforce a canonical runtime lineage contract for all operational transitions (e.g., from request to job to runtime task).

**Mandatory Lineage Entities**:
Every externally visible action and cross-system transition event **MUST** capture the following minimum fields in its Ledger payload:
*   `request_id`: The originating intent or Associate input.
*   `job_id`: The structured chunk of work responding to the request.
*   `correlation_id`: The global thread tying multiple jobs or operations together.
*   `causation_id`: The immediate preceding event ID that triggered the current event.
*   `actor`: The specific process, Specialist, or Associate initiating the transition.
*   `system_from` / `system_to`: The boundary transition (e.g., `router` -> `specialist_a`).
*   `event_type`: The nature of the change (e.g., `task_queued`, `task_executing`, `task_complete`).
*   `sequence_num`: The chronological order of the event within the correlation thread.
*   `visibility`: Whether the event is public to the Associate, or internal to the Core.
*   `delivery_status`: The projected delivery outcome (e.g., `pending_delivery`, `delivered`, `failed`).

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
## 5. Tiered Archival & Pruning (Checkpoint Protocol - MANDATORY)
**Architectural Requirement**: To prevent "Soul Bloat" and performance degradation while maintaining **Integrity**, the Ledger MUST implement a **Checkpoint Protocol** for tiered archival.

**MANDATORY Protocol Requirements**:
*   **Cold Segment Compression**: After a configurable period (default: 90 days), "Cold" segments of the hash chain MUST be compressed into a single **Consolidated Checkpoint Entry**.
*   **Merkle Root Preservation**: The consolidated entry MUST contain the Merkle Root of all archived entries, preserving the audit trail without requiring the full raw history in active memory.
*   **Verification Continuity**: The checkpoint entry itself MUST be hashed and linked into the active chain, ensuring cryptographic continuity from genesis to present.

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

## 6. Point-in-Time Recovery (The Sovereign Restore)
**Architectural Requirement**: To maintain **Integrity** and **Resilience**, the SIRE protocol **MUST** support the restoration of previous valid states. This is the entity's **"Undo" button**.

*   **Constitutional Rollback Protocol**: Any change to the Sovereign Core (Identity, Soul, Guidelines, Associates) MUST create a restorable snapshot in the Ledger.
*   **MANDATORY Requirement**: The system MUST be capable of reverting its entire cognitive and operational state to any previous hash-verified Ledger entry (including checkpoint boundaries).
*   **Sovereign Restore**: If a change results in a "Trauma" event, a constitutional deadlock, or an unwanted identity shift, the Managing Associate MUST be able to trigger a **Sovereign Restore** to the last "Known Good" hash state.
*   **Constitutional Recoveries (Auto-Restore)**: If the system's Heartbeat detects an out-of-band edit to the 5 Sovereign Core files without a valid Ledger manifest, it MUST automatically execute a Sovereign Restore to the active snapshot and log the event as a "Constitutional Recovery" to track tamper attempts.
*   **Audit**: A restore event MUST be recorded as a Level 4 Ledger entry, preserving the timeline of the entity's evolution even through a recovery event.

## 7. The Provenance Manifest (MANIFEST.md)
To prevent "Instruction Drift" or unauthorized file injection, the system must link its file-system state to the Ledger.

*   **Architectural Requirement**: The system MUST maintain a signed **Manifest of Hashes** for every file in the `/config` and `/skills` directories.
*   **Verification**: On every **Heartbeat** (Doc 02) and **Audit Cycle** (Doc 08), the system MUST verify the current file hashes against the `MANIFEST.md`.
*   **Shadow Change Detection**: If a skill file or identity file has been modified without a corresponding Ledger entry or MFA approval, the system MUST immediately enter **Alert State** and disable the cognitive layer.
*   **The Logic**: This ensures that every capability and identity trait has a "Chain of Custody" back to an authorized Managing Associate action.
