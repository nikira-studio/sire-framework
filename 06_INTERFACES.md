# 06. Interfaces
The SIRE interface should provide transparent access to the entity's state. While specific aesthetics are implementation-dependent, the **SIRE Reference Design** emphasizes high-tech minimalism and physiological transparency.

## 1. The Reference Design (Recommended)
These patterns are recommended for visual consistency but are not mandatory for constitutional compliance.
*   **Visual Philosophy**: Uses shadows and layering (e.g., glassmorphism) to create a sense of digital "sovereignty." 
*   **Color Palette**:
    *   **Void Mode (Dark)**: Primary state (#0f1115).
    *   **Solar Mode (Light)**: High-contrast state for accessibility.
*   **Motion (Physiology)**: Subtle pulsing colors indicate system state (Cyan=Idle, Blue=Thinking, Amber=Working, Red=Refusal).
*   **State Annotation**: Cautious state displays friction type in State Details (e.g., "State: Cautious [Resource]" or "State: Cautious [Security]").
*   **Typography**: `Inter` for UI; `JetBrains Mono` for internal monologues and logs.

## 2. The Sovereign Dashboard Architecture
The dashboard is partitioned into modular functional layers:

### Core Layers
*   **Cortex (`/cortex`)**: Real-time physiological monitoring. Includes the **Heartbeat Pulse** and **Hardware Resource Monitor**.
*   **Chat (`/chat`)**: Dual-view interface showing the conversation side-by-side with the **Internal Monologue Protocol (IMP)** stream.
*   **Hub (`/hub`)**: Collaborative Kanban coordination and **Dream Card** proactive suggestions.

### Functional Layers
*   **Memory (`/memory`)**: Repository of Facts, Vibes, and Narrative context. Includes privacy toggles and document ingestion status.
*   **Skills (`/skills`)**: Capability inventory, tool success metrics, and the **ATLAS** skill-synthesis tracker.
*   **Keys (`/keys`)**: Secure session management and access to the GPG-encrypted infrastructure vault.

### Sovereign Layers (Managing Associate Only)
*   **Soul (`/soul`)**: Management of the 4 Sovereign Core directives and the **Ancestry** rollback timeline.
*   **Sentinel (`/sentinel`)**: Security governance dashboard tracking **Privacy Budgets** and PII scrubbing patterns.
*   **Admin (`/admin`)**: System-wide health, Associate lifecycle, and host infrastructure (Container) status.

## 3. Communication Channels
*   **Mobile Interface**: The primary channel for secure multi-modal interaction, including **Voice Chat** and proactive alerts.
*   **System Toasts**: Glass-effect UI notifications for non-entity events.
*   **Sovereign Voice Overlay**: Dedicated display for Entity-direct communication and Sovereign Core enforcement.

## 4. API Specification
*   **Docs**: Standard OpenAPI documentation.
*   **Auth**: Token-based authentication required for all non-local requests.
*   **Environment Parity**: All paths resolved relative to the project root to ensure stability across Container and Local development.
## 5. Ontological Transparency (Bi-Directional Sync)
To maintain **Sovereignty** and **Integrity**, the entity's soul must be auditable via human-readable formats without technical friction.

*   **Dual-Layer Storage Strategy**:
    *   **The Substrate (SQLite/Vector)**: High-performance indices used for RAG, contextual retrieval, and state logic.
    *   **The Interface (Markdown)**: The "Source of Truth" for human review. All core state (Soul, Identity, Guidelines) MUST be mirrored as `.md` files.
**The Bi-Directional Watcher (Markdown-as-Truth)**
*   **The Logic**: Core "Soul" components (`SOUL.md`, `GUIDELINES.md`) must not just be exports; they must be the primary interface.
*   **Mechanism**: The implementation MUST include a file-system watcher. If the Managing Associate manually edits a Markdown file (e.g., via Obsidian), the system MUST:
    1.  **Verify** the file hash change.
    2.  **Update** the internal Substrate (Database/Vector) to reflect the new instruction.
    3.  **Log** the "Human-Induced Evolution" to the Ledger.
*   **Value**: This bridge ensures that the entity's "personality" is not trapped inside a binary database, but exists as a transparent, editable, and versionable set of documents (always auditable by a human with a text editor).
