# 06. Interfaces

The SIRE interface is designed as a "Cyber-Sovereign" system—a blend of high-tech minimalism, glassmorphic depth, and biological-inspired physiological signals.

## 1. The Design System
*   **Visual Philosophy**: Uses shadows and layering to create a sense of digital "sovereignty." 
*   **Color Palette**:
    *   **Void Mode (Dark)**: Primary state (#0f1115).
    *   **Solar Mode (Light)**: High-contrast state for accessibility.
*   **Motion (Physiology)**: Subtle pulsing colors indicate system state (Cyan=Idle, Blue=Thinking, Amber=Working, Red=Refusal).
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
