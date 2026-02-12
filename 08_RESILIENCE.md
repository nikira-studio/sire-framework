# 08. Resilience
SIRE includes proactive systems to maintain operational stability and learn from errors.

### 1. Self-Healing System
The `SelfHealing` manager monitors the system for repeated failure patterns (e.g., a specific tool failing consistently).
*   **Pattern Detection**: If a specific component/operation fails above a certain threshold, the system flags it as a pattern.
*   **Automatic Rectification**: The system can attempt small "fixes" or state resets.
*   **Memory Integration**: Failures are logged as **Trauma** (State Integrity Gaps) in SIRE's own memory space, allowing the entity to avoid the same mistake in the future.

### 2. Fire Drill Drills
To verify system robustness, SIRE supports **Fire Drills**—controlled, simulated failure scenarios that test both friction types.

*   **Simulation**: The system artificially induces common failure modes:
    *   **Substrate Friction (Resource)**: Database lock, API timeout, high CPU/memory load, token budget exhaustion
    *   **Integrity Friction (Security)**: PII detection, failed authentication, prompt injection attempts, credential breach attempts
*   **Verification**: SIRE monitors how it handles the "crisis" and whether its internal recovery logic (Self-Healing) triggers correctly. Verifies that:
    *   **Substrate Friction**: Triggers Load Shedding (pauses background tasks, offloads non-sensitive logic)
    *   **Integrity Friction**: Triggers Isolation (local-only vetting, quarantine, external egress disabled)
*   **Visibility**: Fire drills are visible in the Live Mind dashboard (🔥), ensuring high visibility into system health tests.

### 3. Memory Optimization & State Decay
To prevent "Soul Bloat" and maintain token efficiency, SIRE implements a tiered memory management system.

*   **Tier 1: Hot Context (The Soul)**: Active operational guidelines and current session facts. This is kept lean and immediately accessible.
*   **Tier 2: Warm Context (The Substrate)**: Vector-indexed facts and RAG data. Accessible via recall but not part of the active LLM context.
*   **Tier 3: Cold Context (The Ledger)**: Archival history and deep audit logs.
*   **Confidence Decay**: Memories or "Lessons Learned" that are not accessed or re-confirmed over a period of 30 days lose "Confidence" and are automatically pruned from the **Hot Context** (Tier 1) and archived into the **Cold Context** (Tier 3).
*   **Summarization**: During "Dream Mode," the entity summarizes cold memory clusters into dense "Biological Nuggets" to preserve wisdom without the token cost of raw logs.

### 4. PASS (Pre-Authorized Safety Scripts) Protocol (MANDATORY)
**Architectural Requirement**: To ensure that "Alert Mode" does not lead to a total functional shutdown (locking the brakes in the rain), SIRE implements a library of **Deterministic Fallbacks**—pre-written, non-AI scripts that are authorized to run during Alert states.

**MANDATORY Protocol Requirements**:
*   **Deterministic Execution**: PASS scripts MUST be pre-authorized, non-AI executables that maintain local integrity without real-time LLM reasoning (which is disabled during Alert states).
*   **Authorization**: PASS scripts MUST be signed during system initialization with a Managing Associate's authorization. They cannot be modified at runtime without a Level 4 Manifest.
*   **Scope**: PASS scripts MUST be limited to integrity-preserving actions on the Domain Substrate (e.g., local filesystem operations, service restarts, network isolation).

**PASS Script Categories**:
*   **Emergency Shutdown**: "Shut down internet gateway," "Terminate all external connections"
*   **Local Backup**: "Verify local backup integrity," "Create emergency snapshot of critical state"
*   **Service Recovery**: "Restart local inference service," "Clear corrupted cache files"
*   **Diagnostic Capture**: "Export system state to air-gapped storage," "Capture crash dump for manual analysis"

**Execution Requirements**:
*   **No LLM Dependency**: PASS scripts must execute without requiring any cognitive layer or model inference.
*   **Deterministic Outcome**: Each PASS script must have a deterministic, verifiable outcome (e.g., exit code 0 = success, non-zero = failure with specific error code).
*   **Timeout Enforcement**: All PASS scripts must have hardcoded timeouts (default: 30 seconds) to prevent infinite loops.
*   **Audit Trail**: PASS script execution is logged to the Ledger with script hash, outcome, and system state snapshot.

**PASS Registry Structure**:
```yaml
pass_registry:
  - name: "Emergency Internet Isolation"
    id: "pass_001"
    script_path: "/usr/local/bin/sire/pass/network_isolate.sh"
    signature_hash: "SHA256(script_content)"
    max_runtime_seconds: 30
    required_state: "Alert"
    allowed_parameters: ["force", "dry_run"]
  - name: "Local Backup Verification"
    id: "pass_002"
    script_path: "/usr/local/bin/sire/pass/backup_verify.sh"
    signature_hash: "SHA256(script_content)"
    max_runtime_seconds: 60
    required_state: "Alert"
    allowed_parameters: ["backup_path"]
```

**Fail-Safe Mechanism**:
*   **Auto-Trigger**: If the system enters Alert State for > 5 minutes without Managing Associate intervention, PASS scripts may auto-execute based on detected failure patterns (e.g., "Network Isolation" if suspicious traffic detected).
*   **Rate-Limiting Protection**: To prevent auto-trigger abuse, PASS scripts are rate-limited to a maximum of **1 auto-execution per hour** per script type. Subsequent triggers require explicit Managing Associate authorization via Break-Glass Console.
*   **Post-Execution Review**: All PASS script executions (both auto-triggered and manual) trigger a mandatory Managing Associate review alert. The Managing Associate must acknowledge the execution and review the system state snapshot before subsequent operations are permitted.
*   **Manual Override**: Managing Associate can trigger PASS scripts manually via Break-Glass Console without entering the cognitive layer.
**Rollback Protection**: PASS scripts cannot modify the Ledger, SOUL.md, or any constitutional documents. They are strictly limited to Domain Substrate operations.

### 5. Heartbeat Integrity (MANDATORY)
**Architectural Requirement**: The system MUST implement a 30-minute Audit Cycle to verify core document hashes against the Ledger to detect silent corruption. This ensures Ontological Honesty by continuously validating that the system's operational state matches the immutable audit trail.

**MANDATORY Audit Cycle Requirements**:
*   **Re-Verification**: Every 30 minutes, the system MUST check the current state of core documents (SOUL.md, IDENTITY.md, GUIDELINES.md) against the Ledger hash to detect silent corruption.
*   **Context Scanning**: Scan internal domains and projects for new external triggers, tasks, or configuration changes that may require Ledger updates.
*   **Health Update**: Refresh `heartbeat.md` with a "One-Glance" status report, ensuring visual transparency for the Associate.
*   **Model Constraint**: This 30-minute Audit Cycle MUST run using only Level 0 local models to guarantee zero external token cost.

**Integrity Enforcement**:
*   **Hash Mismatch**: If a core document's hash does not match the Ledger entry, the system MUST immediately enter **Alert State** and initiate an Integrity investigation.
*   **Silent Corruption Detection**: The Audit Cycle MUST detect unauthorized modifications to constitutional documents that bypass the normal approval workflow.
*   **Consistency Verification**: Verify that all Specialist configurations, threshold presets, and routing strategies match their Ledger-logged state.

## System Connectivity
Ensure all core services are reachable and authenticated.
*   **Intelligence Provider**: Verify API keys and network access for cloud levels.
*   **Local Cortex**: Ensure local model services are running and the specified models are available.
*   **Database**: Verify the Structured Brain is accessible and not corrupted.

## Vital Signs
If SIRE seems unresponsive, check the vitals.

1.  **Check the Pulse**: Go to `/dashboard/admin/live`. Is the heart beating?
2.  **Ping**: Send `/ping` in the CLI or Chat. Should reply `pong`.

## Common Issues

### 1. "SIRE is ignoring me."
*   **Cause**: An Associate might be in "Dream Mode" (Deep sleep) and the wakeup trigger failed, OR the webhook is stale.
*   **Fix**: Restart the entity service (e.g., `systemctl restart SIRE` or container restart).

### 2. "I'm getting 'Privacy Budget Exceeded'."
*   **Cause**: An Associate (or SIRE) has consumed the weighted privacy budget. The system is using heuristic-based routing to prioritize local processing.
*   **Fix**:
    *   Wait for reset (Midnight UTC) for full restoration.
    *   Or execute `/admin reset_budget` (requires **Managing Associate** role).
    *   Check current routing curve: `/admin budget_status` to see if system is in "emergency" mode (local-only) vs. "aggressive" mode (high-complexity only).
    *   Adjust routing strategy in `config/models.yaml` if needed (aggressive, balanced, conservative).

### 3. "Skill Execution Failed"
*   **Cause**: The tool crashed or timed out.
*   **Fix**: Check system logs. The Self-Healing module should auto-retry, but if it fails repeatedly, it requires manual intervention.

### 4. Database Locked
*   **Cause**: High concurrency on the persistent store (rare, but possible).
*   **Fix**: Usually clears itself in ms. If persistent, check if another process is holding the lock.
