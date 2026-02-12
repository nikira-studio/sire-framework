# 03. Agency Levels & Permission

## Skills

### 1. The Research-First Protocol
Before SIRE synthesizes a new skill or code-based tool, it must perform a **Research Phase**. If a professional API or existing integration (e.g., Home Assistant) is available, it prioritizes building a lightweight **Wrapper Skill** over reinventing the logic.

### 2. Core Tools
These are the foundational "limbs" that are hardcoded into its Logic Layer:
*   **Kanban**: Task management.
*   **Memory**: Storing/retrieving facts.
*   **System**: Container management, Shell execution.

### 3. Skill Verification Pattern (SVP)
Before executing any skill (especially those sourced externally), SIRE must perform a security audit:
1.  **Scanner**: Security Sentinel scans for dangerous patterns:
    *   External downloads (e.g., `curl | bash`, `wget`).
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
*   **Protocol**: If a validation check fails, SIRE must report the environmental failure to the Managing Associate and pause the task. This protects the **Integrity** of the host and prevents wasting resources on tasks doomed by infrastructure issues.

### Manager-Technician Contract

Communication between the **Main Soul** (Manager) and a **Staff Associate** (Technician) **MUST** be structured via a deterministic handoff to prevent prompt drift.

**The Directive Protocol (SDP)**: Intent handoff **MUST** use the following JSON Schema:

```json
{
  "id": "uuid-v4",
  "source": "main_soul",
  "target": "network_technician",
  "intent": {
    "goal": "Backup NAS Constraints",
    "success_criteria": ["exit_code:0", "file_exists:/backup/nas_config.tar.gz"]
  },
  "constraints": {
    "allow_network": true,
    "timeout_ms": 30000,
    "read_only": false
  },
  "context": {
    "auth_token_scope": "nas_backup_only"
  }
}
```

**Execution**: The Technician's runner **SHALL** validate this schema before execution. If validation fails, the task is rejected with a **Protocol Violation** error. The runner also validates against local repository rules (e.g., `AGENT.yaml`).

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

### 1. Heartbeat Circadian Rhythm
The `HeartbeatService` manages the entity's level of consciousness.
*   **Active Mode**: High-frequency pulses for real-time responsiveness.
*   **Dream Mode (Cognitive Consolidation)**: Lower-frequency pulses where SIRE summarizes short-term session logs into the "Narrative" layer. Provides the scheduling socket for future **Sensory Pulses** (Vision/Voice audit).

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

### 2. GPU-Aware VRAM Priority
To ensure hardware integrity and service availability for Associates:
*   **VRAM Priority Levels**: Background "Dreaming" (memory/audit scanning) is a **Level 3 (Pre-emptible)** task.
*   **Instant Yield**: SIRE must instantly yield the host GPU if an Associate initiates a session or if other host resources require them.

### 3. Failure Analysis (Curiosity)
While in "Dream Mode", SIRE scans logs and trace records for inefficiencies or repeated failures.
*   **Pattern Recognition**: Identifying tasks that are consistently failing or taking too long.
*   **Proactive Suggestions**: Identifying patterns of manual activity and suggesting new **Synthesized Skills** or Kanban tasks to the Managing Associate for approval.

### 4. Self-Healing & "Enough Thinking"
SIRE maintains a "Pragmatic Execution" mindset to prevent the **Mirage of Autonomy**.
1.  **Checkpoint Gating**: Every multi-step task starts with a success metric. If stalled for >5 loops, SIRE forces a manual intervention.
2.  **Rectification**: The `SelfHealing` module attempts immediate state resets or service restarts.
3.  **Learning Capture**: Successful fixes are ingested as **Learning facts**, transitioning from reactive fixing to proactive prevention.
