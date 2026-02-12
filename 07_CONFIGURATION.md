# 07. Configuration

## The `data/` Directory
All state for the specific SIRE instance lives in `/app/data` (mapped to `data/` locally).

*   `config/SOUL.md`: Personality definition and evolutionary state.
*   `config/identity.yaml`: System identity (Timezone, Server Name).
*   `config/models.yaml`: Intelligence Level configuration (Levels 0-3).
*   `db/`: Structured databases (SIRE "Brain").
*   `memory/`: Vector stores and session transcripts.
*   `secure/`: Encrypted credential vault.
*   `skills/`: Associate-defined Markdown skills.

## Bootstrap Sequence (First Run)
When initializing a new Soul instance for the first time, follow this sequence:

1.  **Genesis**: Create `config/SOUL.md` (Name, Version, Managing Associate ID).
2.  **Ledger Init**: Create the first immutable log entry ("System Birth").
3.  **State Baseline**: Set Operational State to **Content** (Default).
4.  **Validation**: Run the **Pre-Execution Validation** checklist (db, keys, permissions).
5.  **Confirm**: Log "Bootstrap Complete" to Ledger.

## Identity Configuration (`identity.yaml`)
Define the physical grounding of the entity.

```yaml
system_name: "SIRE"
server_name: "Host"
timezone: "UTC"
version: "1.0.0"
vram_priority: "shared" # Options: shared, hybrid, exclusive

# Operational State Monitoring
monitoring:
  heartbeat_seconds: 60
  state_thresholds:
    cautious:
      vram_utilization: 0.60
      cpu_load: 0.70
      error_rate: 0.05
    alert:
      vram_utilization: 0.90
      cpu_load: 0.90
      security_events_threshold: 3

## Staff Registry (`staff.yaml`)
Define specialized sub-agents and their directory jails.

```yaml
staff:
  - name: "Network Technician"
    role: "network_ops"
    level: 2
    base_dir: "/opt/network-configs" # Directory Jail
    augments: ["ssh", "container_mgmt"]
  - name: "Business Analyst"
    role: "biz_intel"
    level: 1
    base_dir: "/mnt/data/reports"
    augments: ["read_only", "batch_process"]
```

## Context Triggers (Knowledge Injection)
To prevent "Memory Drift" and ensure the entity always has the correct Single Source of Truth, SIRE supports **Context Triggers**.

*   **Goal**: Automatically inject relevant documentation based on task keywords.
*   **Mechanism**: A local Level 0 scan of Associate input.
*   **The Registry**: Defined in `config/triggers.yaml`.
*   **Example**:
    ```yaml
    triggers:
      - keywords: ["docker", "container", "compose"]
        inject: ["skills/DOCKER_STANDARDS.md"]
      - keywords: ["firewall", "vyatta", "routing"]
        inject: ["skills/NETWORK_SOP.md"]
    ```
*   **The Result**: The Technician's context window is automatically "pre-loaded" with the required manual, ensuring they never operate on generic (potentially hallucinated) knowledge.

## Environment Variables (`.env`)
Runtime secrets and infrastructure settings.

*   `LLM_PROVIDER_KEY`: Access to high-level intelligence.
*   `MESSAGING_PLATFORM_TOKEN`: Nervous system access.
*   `DATABASE_PATH`: Location of the Structured Brain.
*   `SIRE_SKILLS_DIR`: Location of the skill registry.

## User & Interface Configuration
Specific preferences are managed via the **Settings Dashboard (`/settings`)**.
*   **Persona**: User-specific communication style, verbosity, and tone.
*   **Circadian Bounds**: Prevents proactive notifications during defined sleep cycles.
*   **A2UI Styling**: Customization of glassmorphic effects and biometric UI behaviors.

## Modifying the Soul
The Managing Associate can edit `SOUL.md` at any time, or use the **Soul Dashboard** for versioning and rollbacks.
