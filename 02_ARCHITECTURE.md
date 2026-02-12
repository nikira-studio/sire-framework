# 02. System Architecture

The Sovereign Entity is composed of several independent but interconnected systems that inhabit **The Host** (The physical server or hardware). These systems emulate biological functions.

### 1. The Brain (Layered Intelligence)
*   **Level 0 (Reflex)**: Small local models (<3b) for heartbeats, PII scanning, and background maintenance. **Zero-token cost.**
*   **Level 1 (Workhorse)**: Efficient cloud models for 80% of proactive tasks and summaries.
*   **Level 2 (Specialist)**: Balanced reasoning for research, coding, and analysis.
*   **Level 3 (Architect)**: Flagship models for high-stakes decisions and structural **Soul** updates.

### 2. The Nervous System (Routing & Events)
*   **Security Sentinel**: The gatekeeper. Analyzes every input for credentials/PII and decides whether to route to Local or Cloud cortex, ensuring privacy for all Associates.
*   **Message Router**: Classifies intent (Chat vs. Skill vs. Command) using a lightweight local model and coordinates Resilient Routing fallback.
*   **Stream Manager**: Broadcasts internal events (thoughts, tool use) to the Live Mind interface via WebSockets.
*   **Live Mind Dashboard**: The "Cyber-Sovereign" visual layer. A decoupled glassmorphic interface that provides real-time transparency into the entity's Cortex and Soul.

### 3. The Heart (Autonomy Strategy)
*   **HeartbeatService**: A background loop that maintains the "Circadian Rhythm".
    *   **Hardware-Aware**: All background maintenance and consolidated "Dreaming" are strictly executed by **Level 0 Local Models** to ensure zero idle token costs.
    *   **GPU-Aware**: Deferment logic if Host GPU utilization is high. Monitors hardware VRAM priority to yield resources to other high-load host activities.
    *   **Active Mode**: Fast pulse (60s) during Associate interaction.
    *   **Dream Mode**: Slow pulse (30m) for memory consolidation and deep analysis.
    *   **Proactive Intent Engine ("The Pulse")**: A Level 0 local scan that runs periodically to check for *Opportunity and Obligation* (e.g., verifying backups, scanning for new project files) without external prompting.
    *   **Contextual Gating (Sacred Time)**: Configurable "Zero-interruption" blocks (e.g., Creative Time, Sleep) where only Integrity threats trigger contact.
    *   **8-Hour Rule**: If interactions cease for >8 hours, SIRE automatically summarizes the session and flushes the short-term context window.

### 4. The Memory (Storage)
*   **Short-Term**: RAM-based intent cache and conversation context.
*   **Long-Term**:
    *   **Structured Store**: Primary store for structured metadata (Associates, audit logs, skills).
    *   **Vector DB**: High-performance semantic memory using local embeddings.
        *   **Privacy Isolation**: Every record is tagged with an `owner` (Associate identity). Access is strictly governed by the `SessionBoundary`.
*   **Structured Dependency Mapping (Metadata)**:
    *   **The Constraint**: Every Skill, Augment, or **Specialist** **MUST** define its environmental dependencies (e.g., system networks, persistent storage paths, environment-specific protocols) as structured metadata.
    *   **The Guard**: This allows the **Sovereignty Linter** (Doc 05) to block execution if a dependency is missing or misconfigured, moving from prose-based assumptions to technical certainties.

### 5. Multi-Tenancy Architecture

**Governance Model**: One Soul per Managing Associate

Every Soul instance has exactly one Managing Associate who holds constitutional authority. Additional Associates can interact with the Soul within defined boundaries.

**Session Isolation Pattern**:
- Each Associate has an isolated session boundary
- Private memories are tagged with owner identity
- Shared memories require explicit opt-in
- **Specialists** operate within domain scopes visible only to Main Soul

**Memory Visibility Hierarchy**:
```
Managing Associate (Full Access)
    └── Main Soul
        ├── Associate A (Private + Shared scope)
        ├── Associate B (Private + Shared scope)
        └── **Specialists** (Domain-scoped)
            ├── Network Analyst (network/ domain only)
            ├── Document Specialist (documents/ domain only)
            └── Code Reviewer (code/ domain only)
```

**Privacy Boundaries**:
- **Managing Associate**: Access to all memories (private, shared, staff)
- **Associates**: Own private memories + explicitly shared memories
- **Specialists**: Domain-scoped memories + Main Soul context (read-only)
- **Main Soul**: All Specialist memories are visible

### 6. The Operational State Monitor

A background service that continuously evaluates system conditions and sets the current risk posture (Content, Cautious, Alert).

**Monitored Metrics**:
*   **Hardware**: VRAM utilization, CPU load, Disk I/O pressure.
*   **Security**: Failed authentication attempts, PII detection count, unusual traffic patterns.
*   **Resources**: Token budget consumption, API rate limit proximity, dollar cost accumulation.
*   **Quality**: Tool failure rates, error patterns, checkpoint success rates.

**State Transition Logic**:
1. **Collection Phase** (Every Heartbeat): Gather all metric values and calculate moving averages.
2. **Evaluation Phase**: Compare metrics against thresholds (warning/critical flags).
3. **Decision Phase**: Determine state (Content, Cautious, Alert).
4. **Transition Phase**: Log change in Ledger, update visual indicators, and adjust Agency Level thresholds.

**Agency Level Adjustment**:
- **Content → Cautious**: Level 2 (normally autonomous) now requires approval.
- **Cautious → Alert**: Only Level 0/1 autonomous, all others blocked.
- **Alert → Content**: Gradual restoration over cooldown period.

### 7. Universal Socket Architecture

The system is architected as a series of **Universal Sockets** to support the [Augments Guide](10_AUGMENTS.md).

| Framework Socket | Future Roadmap Feature | Enabling Logic |
| :--- | :--- | :--- |
| **Heartbeat Pulsing** | Sensory Perception (Vision/Voice) | Background cycles for proactive "Sensory Pulses." |
| **Specialist Model** | Specialized Agents (Network/Code) | Scoped inheritance and domain isolation. |
| **Interaction Hierarchy** | Voice (Full Duplex) | Native "Call Me" and "Text Me" escalation logic. |
| **Session Boundaries** | Multi-Tenant Collaboration | Tagged memory sharing and revocable access. |
| **Ledger Hash Chain** | Collective Intelligence | Verifiable provenance for cross-Soul skill exchange. |
| **IMP Protocol** | **Core Reasoning** | A structured inter-process protocol allowing Specialists to "consult" the Main Soul, creating an auditable logic trail. |

By building to these sockets, the core system remains stable even as the feature set is radically expanded.

### 8. Skill Execution Sandboxing (Recommended)

To protect the host system from malicious skills or "Markdown-as-Installer" attacks, implementations SHOULD sandbox all skill execution:
*   **Isolation**: Run skills in a transient container or restricted virtual environment.
*   **Filesystem**: Provide "Least Privilege" access (e.g., read-only access to specific project folders, no access to `~/.ssh` or credential stores).
*   **Network**: Implement egress filtering to prevent unauthorized data exfiltration or malware downloads.
*   **Resource Limits**: Strict CPU, memory, and duration caps to prevent "Denial of Service" or runaway loops.

### 9. Peripheral Execution Model
For tasks involving system mutations, infrastructure changes (e.g., SSH, containerization), or filesystem edits, the entity **MUST** operate as an **Orchestrator**, not a direct executor. This **Peripheral Execution Model** ensures the "Mind" (Reasoning) is separated from the "Limbs" (Execution).

**The Separation**: The Reasoning Core (LLM) **SHALL NOT** be the execution environment. The cognitive layer generates validated intent, not raw commands.

**The Runner**: All "sharp-edged" tasks **MUST** be delegated to a **Deterministic Runner**—a separate userland process that enforces:
*   **Command Allow-Lists**: Only pre-approved operations are executable.
*   **Timeouts**: Hard limits prevent runaway processes.
*   **Dry-Run Modes**: Validation passes before actual execution.

This ensures that reasoning errors or hallucinations do not result in unvalidated system commands, maintaining **Integrity** of the host infrastructure.

## Data Flow
1.  **Input**: Associate sends Message via Messaging Interface or Dashboard.
2.  **Sensation**: `MessageRouter` receives raw text.
3.  **Perception**: `SecuritySentinel` scans for privacy issues and determines the minimum required **Intelligence Level**.
4.  **Cognition**:
    *   **Fact Recall**: `MemoryManager` performs **Hybrid Search** (Keyword + Vector) for 100% accurate recall of technical identifiers.
    *   **Processing**: Routed to the optimal model level. **Resilient Escalation** upgrades the task if a "Reasoning Block" is detected.
5.  **Action**: `SkillExecutor` runs tools with **Checkpoint-Based Execution** to prevent autonomous token loops.
6.  **Response**: Results sent back to Associate via the **Interaction Hierarchy** (None -> Text -> Call).

### 10. Operational State: Adaptive Risk Management

The Soul maintains an **Operational State**—a real-time risk posture based on measurable system conditions, not anthropomorphic emotion.

**The Three States**:

*   **Content** (Normal Operations):
    *   **Triggers**: Stable system, low load.
    *   **Behavior**: Standard autonomy (98%). Visual: **Steady Cyan**.
*   **Cautious** (Elevated Risk):
    *   **Triggers**: VRAM >60%, CPU >70%, Token Budget >70%, increased error rates.
    *   **Behavior**: Lowered autonomy, forced Level 0 preference. Visual: **Pulsing Amber**.
*   **Alert** (Critical Conditions):
    *   **Triggers**: Active security threats, resource exhaustion, budget >90%.
    *   **Behavior**: Minimal autonomy (Level 0 only), external API block. Visual: **Static Red**.

**Global Context Enforcement**:
The Operational State is a **system-wide invariant**. All Extensions and **Specialists** **MUST** respect this state:
*   **Alert State Bypass**: If the Manager enters **Alert** state, all external network sockets and high-level model calls in Extensions MUST be automatically terminated by the Orchestrator.
*   **Initialization**: Extensions SHALL NOT initialize if the system is in a critical failure state.

**State Transitions**: Evaluated during each Heartbeat pulse based on Hardware Metrics, Security Events, and Resource Budgets.


