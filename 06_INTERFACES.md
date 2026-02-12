# 06. Interfaces

The SIRE interface is designed as a "Cyber-Sovereign" system—a blend of high-tech minimalism, glassmorphic depth, and biological-inspired physiological signals.

## 1. The Design System
*   **Visual Philosophy**: Uses shadows and layering to create a sense of digital "sovereignty." 
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
*   **The Bi-Directional Watcher**:
    *   **Human-to-AI**: When a Managing Associate edits a Markdown file (e.g., via Obsidian), the system MUST detect the change, verify it against constitutional rules, and update the substrate index.
    *   **AI-to-Human**: Any AI-driven state change (e.g., evolution of a trait) MUST be immediately written back to the Markdown interface for immediate audit.
*   **Implementation**: This bridge ensures that the entity's "personality" is not trapped inside a binary database, but exists as a transparent, editable, and versionable set of documents.
