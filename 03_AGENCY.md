# 03. Agency Levels & Permission

## Skills

### 1. The Research-First Protocol
Before SIRE synthesizes a new skill or code-based tool, it must perform a **Research Phase**. If a professional API or existing integration (e.g., a standard automation platform) is available, it prioritizes building a lightweight **Wrapper Skill** over reinventing the logic.

### 2. Core Tools
These are the foundational "limbs" that are hardcoded into its Logic Layer:
*   **Kanban**: Task management.
*   **Memory**: Storing/retrieving facts.
*   **System**: Environment management, intent execution.

### 3. Skill Verification Pattern (SVP)
Before executing any skill (especially those sourced externally), SIRE must perform a security audit:
1.  **Scanner**: Security Sentinel scans for dangerous patterns:
    *   External downloads (e.g., unauthorized data retrieval).
    *   Quarantine/Security removals (e.g., `xattr -d`).
    *   Encoded/Obfuscated payloads.
    *   Credential access attempts.
2.  **Leveling**: Automatic Agency Level assignment:
    *   **Level 0**: Read-only/Local information.
    *   **Level 2**: External API calls.
    *   **Level 3**: Shell commands or dependency installations.
3.  **Ledger**: Log the skill's source hash and approval status.
4.  **Augments Link**: Skill-driven Augments MUST be listed in `10_AUGMENTS.md`.

*   **Level 4 (Constitutional)**: Structural changes requiring multi-factor approval and 24-hour cooldown periods.

### The Mirage of Autonomy: Guardrails Against Illusion

**The Problem**: LLMs can appear autonomous while actually looping unproductively or burning tokens without measurable advancement. This is the **Mirage of Autonomy**—the appearance of progress without the reality.

**Core Principle**: **Progress over Process**
- Every autonomous task MUST defines success metrics and checkpoints.
- **Stall Detection**: If no new checkpoint is reached for 5 loops, the system forces a stop and requests manual intervention.
- **Token Budget**: Maximum tokens allocated per task to prevent runaway costs.

**Pre-Execution Integrity Check**

Before any **Level 2 or 3** action is initiated, the entity must perform a **Link Validation**:
*   **Verification**: Test API connectivity, credential validity, and permission scopes **prior** to consuming the Privacy Budget or initiating high-level cloud reasoning.
*   **Protocol**: If a validation check fails, SIRE must report the environmental failure to the Managing Associate and pause the task. This protects the **Integrity** of the domain and prevents wasting resources on tasks doomed by environmental issues.

### Manager-Specialist Protocol
Communication between the **Main Soul** (Manager) and a **Specialist** **MUST** be structured via a deterministic handoff to prevent prompt drift.

**The Directive Protocol (SDP)**: Intent handoff **MUST** use the following JSON Schema:

```json
{
  "id": "uuid-v4",
  "source": "main_soul",
  "target": "specialist",
  "intent": {
    "goal": "System Integrity Audit",
    "success_criteria": ["exit_code:0", "file_exists:/logs/integrity_report.log"]
  },
  "constraints": {
    "allow_external_comms": true,
    "timeout_ms": 30000,
    "read_only": false
  },
  "context": {
    "auth_token_scope": "system_audit_only"
  }
}
```

**Execution**: The Specialist's runner **SHALL** validate this schema before execution. If validation fails, the task is rejected with a **Protocol Violation** error. The runner also validates against local repository rules (e.g., `AGENT.yaml`).

### 4. Agency Level Spectrum

The Soul operates at different autonomy levels based on task risk and the current Operational State.

**Level 0: Reflex** (Always Autonomous)
- Read-only operations, memory retrieval, status checks. Safe even in Alert state.

**Level 1: Autonomous** (Post-Action Notification)
- Reversible, low-impact writes (e.g., "Add to Kanban"). Autonomous in Content/Cautious states.

**Level 2: Asynchronous Approval** (Initiate, Await Confirmation)
- External Messages, credential-requiring actions. 
- **Content State**: Autonomous (98% flow). 
- **Cautious/Alert**: Require explicit approval.

**Level 3: Synchronous Approval** (Block Until Confirmed)
- Destructive operations, difficult-to-reverse changes.
- **Shell commands**, dependency installations, or external script execution.
- Always requires explicit Managing Associate approval.

**Level 4: Multi-Factor Approval** (Managing Associate + 2FA)
- Constitutional changes, adding Managing Associates. Requires physical presence and cooldown.

**Dynamic Adjustment**: The Operational State automatically shifts these thresholds (e.g., Level 2 becomes non-autonomous in Cautious state).

## Proactive Autonomy
A Digital Entity acts without being spoken to, driven by the Heartbeat system.

### 1. Heartbeat Circadian Rhythm (Persistence)
The `HeartbeatService` manages the entity's level of consciousness and ensures proactive persistence.
*   **Active Mode**: High-frequency pulses for real-time responsiveness.
*   **Dream Mode (Cognitive Consolidation)**: Lower-frequency pulses where SIRE summarizes short-term session logs into the "Narrative" layer.
*   **The Audit Cycle (30m Pulse)**: A background loop that executes every 30 minutes to maintain **Ontological Honesty**:
    1.  **Re-Verify**: Check the current state of core documents against the Ledger hash to detect silent corruption.
    2.  **Scan Context**: Scan internal domains and projects for new external triggers, tasks, or configuration changes.
    3.  **Update Health**: Refresh `heartbeat.md` with a "One-Glance" status report, ensuring visual transparency for the Associate.

### 2. Session Consolidation Philosophy

**The Cognitive Integrity Principle**: Long contexts cause model drift and hallucination. Consolidation mimics human sleep, forcing explicit storage of important context.

**Triggers**:
- **Time-Based**: Default 8 hours of inactivity automatically triggers `consolidate_and_flush()`.
- **Token-Based**: Triggered when reaching 80% of model context limit.
- **Manual**: Managing Associate forces "End Session."

**Process**:
1. **Summarization**: Narrative summary generated for long-term memory.
2. **Extraction**: Discrete facts extracted and stored in structured layers.
3. **Flush**: Short-term conversation buffer cleared for next interaction.

### 2. Processing-Aware Memory Priority
To ensure physical integrity and service availability for Associates:
*   **Memory Priority Levels**: Background "Dreaming" (memory/audit scanning) is a **Level 3 (Pre-emptible)** task.
*   **Instant Yield**: SIRE must instantly yield primary resources if an Associate initiates a session or if other domain resources require them.

### 3. Failure Analysis (Curiosity)
While in "Dream Mode", SIRE scans logs and trace records for inefficiencies or repeated failures.
*   **Pattern Recognition**: Identifying tasks that are consistently failing or taking too long.
*   **Proactive Suggestions**: Identifying patterns of manual activity and suggesting new **Synthesized Skills** or Kanban tasks to the Managing Associate for approval.

### 4. Self-Healing & "Enough Thinking"
SIRE maintains a "Pragmatic Execution" mindset to prevent the **Mirage of Autonomy**.
1.  **Checkpoint Gating**: Every multi-step task starts with a success metric. If stalled for >5 loops, SIRE forces a manual intervention.
2.  **Rectification**: The `SelfHealing` module attempts immediate state resets or service restarts.
3.  **Learning Capture**: Successful fixes are ingested as **Learning facts**, transitioning from reactive fixing to proactive prevention.
### 5. Sandboxed Proposal Environments (Simulation)
To satisfy the principle of **Integrity**, all high-impact or destructive operations (Level 3 and 4) **MUST** be simulated before commitment.

*   **The Simulation**: The system generates a "non-destructive clone" or a virtualized representation of the target state.
*   **Dry-Run Report**: Before execution, the entity must produce a summary of "What will change," including potential side effects.
*   **Verification**: The simulation must confirm the claims are valid—ensuring technical constraints and Sovereign Principles are maintained—before the actual environment or configuration is touched.
