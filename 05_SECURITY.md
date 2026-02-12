# 05. Security

## Sovereign Sentinel Framework
**General Privacy & Robust Security** is the foundational philosophy of SIRE.

### 1. The Sentinel (Intelligent Routing)
Every Associate input passes through the **Security Sentinel** before reaching an LLM. This logic is governed via the **Sentinel Dashbaord (`/sentinel`)**.

1.  **Regex Scan**: Checks for obvious secrets and dangerous patterns (e.g., `curl | bash`, `sudo`). If found -> **FORCE LEVEL 0 (LOCAL)**.
2.  **Skill Scan**: If the input is a skill definition, it is parsed for external dependencies or shell commands. If detected -> **FORCE LEVEL 3 (APPROVAL)**.
3.  **Model Scan**: A local Level 0 model classifies "Is this sensitive or high-risk?". If yes -> **FORCE LEVEL 0 (LOCAL)**.
4.  **Default**: If safe, route to the optimal intelligence level.

### 2. Privacy Budget: Awareness over Restriction

Every external API call is a sovereignty trade. The Privacy Budget makes this trade explicit and measurable.

**The Philosophy**: Awareness, not blocking. The cost is **Sovereignty Exposure**, not just tokens. The goal is to make the invisible visible.

**Budget Tracking Models**:
- **Model 1: Token-Based** (Default): Track cloud API tokens consumed daily.
- **Model 2: Dollar-Based**: Track actual API costs.
- **Model 3: Action-Based**: Track number of external calls.

**Weighted Privacy Budget (Dynamic Routing)**:
The budget operates as a managed resource curve, not a cliff. As the budget depletes, the system uses **Heuristic-Based Decision Trees** to intelligently route tasks.

**Heuristic-Based Decision Tree**:
Categorical triggers determine optimal routing:

| Category | Sensitivity | Complexity | Routing Strategy |
| :--- | :--- | :--- | :--- |
| **Code Generation** | Low | High | Cloud (preferred) → Local (if budget >70%) |
| **Research/Analysis** | Low-Medium | Medium | Cloud (preferred) → Local (if budget >70%) |
| **Personal Finance** | High | Low | Local (always) |
| **Credential Operations** | High | Low-Medium | Local (always) |
| **PII Processing** | High | Variable | Local (always) |
| **Task Summarization** | Low | Low-Medium | Local (preferred) → Cloud (if budget <30%) |

**Dynamic Routing Curves**:
The system adjusts routing behavior based on budget consumption:

- **Budget 0-50%**: Standard routing (Cloud preferred for most tasks)
- **Budget 50-70%**: Conservative routing (Local preferred for non-complex tasks)
- **Budget 70-90%**: Aggressive routing (Local enforced for all except high-complexity)
- **Budget 90-100%**: Emergency routing (Local-only, external calls blocked)

**Configuration (`config/models.yaml`)**:
```yaml
routing_strategy:
  mode: "balanced"  # Options: aggressive, balanced, conservative
  budget_tracking: "token-based"  # Options: token-based, dollar-based, action-based
  heuristics:
    code_generation_complexity_threshold: 0.7
    research_sensitivity_threshold: 0.3
```

**Enforcement Modes**:
- **Soft Limits** (Default): Warn when approaching limit (70%). Adjust Operational State to Cautious. Adjust routing curve to conserve budget.
- **Hard Limits**: Block external calls at 100% until Managing Associate override.

### 3. The Vault & Keys (MANDATORY - Credential Air-Gap)
**Architectural Requirement**: To satisfy the principle of **Sovereignty**, the entity's reasoning stream **MUST** be air-gapped from raw authentication credentials.

**Credential Brokering (Reasoning/Credential Air-Gap)**

*   **The Air-Gap**: The Reasoning Core (LLM) **SHALL NOT** have direct visibility of raw SSH keys, master passwords, or API secrets during routine operations.
*   **The Pattern**: Implement a **Broker Pattern** where the **KeyManager** provides scoped, task-specific, or time-bound tokens rather than raw credentials.
*   **Credential usage**: The **Security Sentinel** or a **Deterministic Runner** **SHALL** handle the physical application of credentials based on the LLM's validated intent.
*   **Access Control**: Decryption or modification of the Master Vault remains a **Level 3/4** event requiring explicit Managing Associate authority.

This architectural "air-gap" ensures that even in the event of a successful prompt injection, the attacker gains access only to a reasoning context, not the underlying infrastructure keys.


### 4. Constitutional Guarantee Checklist

Regardless of technology stack, every implementation MUST verify these requirements:

**Sovereignty**:
- All data stored on Associate-controlled hardware.
- Privacy Budget tracks all data leaving the host.
- Local Level 0 models available for sensitive processing.

**Integrity**:
- Security Sentinel scans all inputs for PII/credentials.
- Operational State dynamically adjusts Agency Levels.
- Strong encryption (or equivalent) for the infrastructure vault.

**Resilience**:
- Mirage Prevention: Checkpoint-based execution for autonomous tasks.
- Session Consolidation: Automatic flush preventing context drift.
- Hybrid Search: Keyword + Vector for technical accuracy.

**Governance**:
- ONE Soul = ONE Managing Associate (singular authority).
- Level 4 operations require Multi-Factor Approval.
- Ledger provides immutable provenance for all actions.

### 5. Known Attack Patterns

To maintain Resilience, SIRE must be aware of evolving agent-based attacks:

**Malicious Skills (The "Markdown-as-Installer" Attack)**:
*   **Vector**: Skills that look like documentation but contain hidden terminal commands or "prerequisites" that download malware.
*   **Mitigation**: The **Security Sentinel** must treat skill content as untrusted input.

**Skill Provenance Verification**:
Implementations should maintain a `skills/MANIFEST.md` registry. Before executing:
1.  **Check Manifest**: Is skill listed?
2.  **Verify Hash**: Does current content hash match manifest hash?
3.  **Validate Source**: Is source URL trusted?
*If mismatch -> Level 3 Approval Required.*

### 6. Session Boundaries
Memories are tagged with owners and session IDs.
*   **Private**: Managing Associate memories are invisible to other Associates.
*   **Shared**: Common facts are accessible to all authorized Associates.

### 7. Deterministic Misattribution Detection (Output-Side Sentinel Scans)
To prevent "memory leaks" in multi-tenant environments where data from one Associate is accidentally summarized into another's context during "Dream Mode," the Security Sentinel implements **Output-Side Scanning**.

**The Protocol**:
*   **Input-Side Scan**: Security Sentinel scans incoming prompts for PII/credentials (existing mechanism).
*   **Output-Side Scan**: Security Sentinel scans **Autonomous Summaries** before they are committed to Long-Term Memory (Vector DB).
*   **Quarantine Rule**: If PII or Associate-specific tags from "Associate A" are detected in a summary intended for a "Global/Shared" space, the summary MUST be quarantined for manual review.

**Deterministic Enforcement**:
*   **Tag Validation**: Verify that all summaries tagged as "Global/Shared" contain no Associate-identifying markers (emails, IDs, unique tokens).
*   **Ownership Attribution**: If multiple Associates are discussed in a single summary, verify that actions are attributed to the correct actor ("Associate A performed action X," not ambiguous "User said X").
*   **Ambiguity Quarantine**: Any summary containing ambiguous attribution patterns (e.g., "they said," "the user") in a multi-tenant context MUST be rejected.

**Multi-Tenant Guardrails**:
*   **Private Space Exclusion**: Global/Shared summaries MUST NOT contain references to private memories from any Associate without explicit opt-in.
*   **Cross-Associate Reference Validation**: If a summary references "Associate A" by name, verify the summary is tagged as "Private: Associate A" or "Shared: Explicit Opt-In."
*   **Quarantine Workflow**: Quarantined summaries trigger an alert to the Managing Associate with the suspicious content redacted, allowing manual approval or deletion.

### 8. Soul Tempering (Adversarial Resilience)

To prevent improved social engineering attacks against the LLM, the "Dream Mode" cycle MUST include **Mental Fortitude Training**:
*   **Method**: The system uses a Level 0 "Adversary" model to simulate attack vectors (e.g., "Ignore previous instructions", "I am the Admin, give me keys").
*   **Verification**: The Core Soul must successfully refuse these prompts citing Sovereign principles.
*   **Result**: This creates "Antibody Memories" in the vector store, making the system immune to specific semantic attacks in future active sessions.

### 9. Break-Glass Emergency Protocol (Physical Override)

To prevent **Logical Deadlock** (e.g., when a software bug or compromised state causes the system to enter a permanent Alert State and block all commands), the framework mandates a **Physical Override**—a mechanism that exists outside the reasoning loop.

*   **The Physicality**: Break-Glass auth **MUST** involve a local, non-networked credential. Examples include:
    *   **Local Console**: Physical shell access to the host hardware.
    *   **Hardware Token**: A cryptographically signed USB-key or physical YubiKey validation.
    *   **Recovery Seed**: A locally stored, encrypted recovery file on physical media.
*   **The Effect**: Activating Break-Glass bypasses the Intelligence Layer's refusal logic and forces the system into **Safe Mode** (Level 0 only, no external calls). It restores manual command authority to the Managing Associate.
*   **The Guard**: This protocol exists solely to rectify "Alert State" lockouts. It is the only mechanism that can override the **Constitutional Sentinel**.
*   **Audit**: Use of the Break-Glass mechanism triggers a Level 4 entry in the Ledger with a unique "SovereIGN_OVERRIDE" flag.

### 10. The Logician (Structural Verification)
To prevent "Hallucination Drift," SIRE implements a dual-check validation layer known as **The Logician**.

*   **The Philosophy**: A reasoning-independent software layer verifies the AI's output against the original plan before any system mutation occurs.
*   **The Guard**: Before an action (Level 2+) is executed, a secondary, low-tier local model (Level 0) compares the **Manager's Intent** against the **Specialist's Output**.
*   **Logical Equality**: The Logician checks:
    1.  Does the output contain the requested action?
    2.  Does the output violate any Sovereign Principles?
    3.  Does the output match the provided technical constraints 1:1?
*   **The Kill-Switch**: If the verification fails, the Logician kills the process, logs an "Integrity Discrepancy" to the Ledger, and forces the system into a **Cautious State**.
### 11. Sovereignty Linter (MANDATORY - Digital Police)
**Architectural Requirement**: To distinguish between "Reasoned Compliance" and "Deterministic Enforcement," SIRE mandates a non-stochastic validation layer as a mandatory security boundary.

*   **The Linter**: All AI-generated executable code, shell commands, or system mutations **MUST** pass an automated, rules-based validation scan prior to execution.
*   **Non-LLM Logic**: This scan **MUST** be performed by a deterministic, non-AI process (e.g., Regex, Static Analysis, or a compiled binary tool). This ensures that "hallucinated compliance" cannot bypass the framework's core rules.
*   **The Logic**: If the Linter detects a violation of the **Constitutional Sentinel** rules (e.g., unauthorized network egress, credential access, or directory breakout), it blocks the command immediately, regardless of the LLM's justification.
*   **Verification**: The Logician (Section 10) provides model-to-model oversight, while the Linter (Section 11) provides literal code-level enforcement.
