# 07. Configuration

## The `data/` Directory
All state for the specific SIRE instance lives in `/app/data` (mapped to `data/` locally).

*   `config/SOUL.md`: Personality definition and evolutionary state.
*   `config/identity.yaml`: System identity (Timezone, Domain Name).
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
domain_name: "Local"
timezone: "UTC"
version: "1.0.0"
memory_priority: "shared" # Options: shared, hybrid, exclusive

# Operational State Monitoring
monitoring:
  heartbeat_seconds: 60
  state_thresholds:
    cautious:
      # Substrate Friction (Resource) Thresholds
      memory_utilization: 0.60
      processing_load: 0.70
      token_budget_percentage: 0.70
      error_rate: 0.05
      # Integrity Friction (Security) Thresholds
      pii_detection_count: 5
      failed_auth_attempts: 3
      unusual_traffic_threshold: 2.0
    alert:
      # Substrate Friction (Resource) Thresholds
      memory_utilization: 0.90
      processing_load: 0.90
      token_budget_percentage: 0.90
      # Integrity Friction (Security) Thresholds
      security_events_threshold: 3
      prompt_injection_detected: true
      credential_breach_attempt: true
```

## Specialist Registry (`specialists.yaml`)
Define specialized sub-agents and their directory jails.

```yaml
specialists:
  - name: "Operations Specialist"
    role: "ops_lead"
    level: 2
    base_dir: "/app/domain-configs" # Directory Jail
    augments: ["domain_access", "state_mgmt"]
  - name: "Information Specialist"
    role: "data_intel"
    level: 1
    base_dir: "/mnt/data/reports"
    augments: ["read_only", "batch_process"]

## Intelligence Level Configuration (`models.yaml`)
Define the intelligence tiers and dynamic routing strategy.

```yaml
intelligence_levels:
  level_0:
    name: "Reflex"
    model_type: "local"
    max_tokens: 2048
    use_case: ["heartbeat", "pii_scan", "background_maintenance"]
  
  level_1:
    name: "Workhorse"
    model_type: "cloud"
    max_tokens: 4096
    use_case: ["proactive_tasks", "summaries"]
  
  level_2:
    name: "Specialist"
    model_type: "cloud"
    max_tokens: 8192
    use_case: ["research", "coding", "analysis"]
  
  level_3:
    name: "Architect"
    model_type: "cloud"
    max_tokens: 16384
    use_case: ["high_stakes_decisions", "soul_updates"]

# Weighted Privacy Budget Configuration
routing_strategy:
  mode: "balanced"  # Options: aggressive, balanced, conservative
  budget_tracking: "token-based"  # Options: token-based, dollar-based, action-based
  
  # Heuristic-Based Routing Thresholds
  heuristics:
    code_generation_complexity_threshold: 0.7
    research_sensitivity_threshold: 0.3
    summarization_sensitivity_threshold: 0.2
  
  # Dynamic Routing Curves
  curves:
    aggressive:
      0_50: "standard"
      50_70: "standard"
      70_90: "conservative"
      90_100: "emergency"
    balanced:
      0_50: "standard"
      50_70: "conservative"
      70_90: "aggressive"
      90_100: "emergency"
    conservative:
      0_30: "standard"
      30_50: "conservative"
      50_100: "aggressive"
```

## Threshold Presets Configuration (`threshold_presets.yaml`)
Define universal governance thresholds that replace user profiles.

```yaml
threshold_presets:
  # SIRE Lite Preset (Adoption-focused with minimal friction)
  sire_lite:
    name: "SIRE Lite"
    mfa_trigger_score: 0.9
    ledger_trigger_score: 0.7
    level_3_manifest_score: 0.8
    auto_approve_level_3_threshold: 0.4
    description: "Developer/hobbyist preset with low-friction. Auto-approves Level 3 for low-impact (S < 0.4). Suitable for experimentation and rapid prototyping."
  
  # Low-Friction Preset (Minimal approvals for low-impact operations)
  low_friction:
    name: "Low-Friction Threshold"
    mfa_trigger_score: 0.7
    ledger_trigger_score: 0.5
    level_3_manifest_score: 0.6
    description: "Suitable for single-user domains with trusted environment. All Level 3/4 require manifests. More friction than SIRE Lite but maintains strong governance."
  
  # Balanced Preset (Moderate approvals for mixed operations)
  balanced:
    name: "Balanced Threshold"
    mfa_trigger_score: 0.5
    ledger_trigger_score: 0.3
    level_3_manifest_score: 0.4
    description: "Suitable for multi-tenant environments with diverse operations"
  
  # High-Integrity Preset (Strict approvals for all operations)
  high_integrity:
    name: "High-Integrity Threshold"
    mfa_trigger_score: 0.3
    ledger_trigger_score: 0.1
    level_3_manifest_score: 0.2
    description: "Suitable for high-availability nodes with strict audit requirements"

# Universal Enforcement Rules (Apply to all presets)
universal_enforcement:
  # High-impact operations always trigger Ledger and MFA
  min_score_for_always_log: 0.5
  min_score_for_always_mfa: 0.5
```

## Context Triggers (Knowledge Injection)
To prevent "Memory Drift" and ensure the entity always has the correct Single Source of Truth, SIRE supports **Context Triggers**.

*   **Goal**: Automatically inject relevant documentation based on task keywords.
*   **Mechanism**: A local Level 0 scan of Associate input.
*   **The Registry**: Defined in `config/triggers.yaml`.
*   **Example**:
    ```yaml
    triggers:
      - keywords: ["virtualization", "isolation", "orchestration"]
        inject: ["skills/SYSTEM_STANDARDS.md"]
      - keywords: ["security", "connectivity", "communications"]
        inject: ["skills/SEC_OPS.md"]
    ```
*   **The Result**: The Specialist's context window is automatically "pre-loaded" with the required manual, ensuring they never operate on generic (potentially hallucinated) knowledge.

## Environment Variables (`.env`)
Runtime secrets and domain settings.

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
