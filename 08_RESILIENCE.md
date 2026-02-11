# 08. Resilience
SIRE includes proactive systems to maintain operational stability and learn from errors.

### 1. Self-Healing System
The `SelfHealing` manager monitors the system for repeated failure patterns (e.g., a specific tool failing consistently).
*   **Pattern Detection**: If a specific component/operation fails above a certain threshold, the system flags it as a pattern.
*   **Automatic Rectification**: The system can attempt small "fixes" or state resets.
*   **Memory Integration**: Failures are logged as **Trauma** (State Integrity Gaps) in SIRE's own memory space, allowing the entity to avoid the same mistake in the future.

### 2. Fire Drill Drills
To verify system robustness, SIRE supports **Fire Drills**—controlled, simulated failure scenarios.
*   **Simulation**: The system artificially induces common failure modes (e.g., database lock, API timeout).
*   **Verification**: SIRE monitors how it handles the "crisis" and whether its internal recovery logic (Self-Healing) triggers correctly.
*   **Visibility**: Fire drills are visible in the Live Mind dashboard (🔥), ensuring high visibility into system health tests.

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
*   **Cause**: An Associate (or SIRE) has made too many cloud calls today.
*   **Fix**:
    *   Wait for reset (Midnight UTC).
    *   Or execute `/admin reset_budget` (requires **Managing Associate** role).

### 3. "Skill Execution Failed"
*   **Cause**: The tool crashed or timed out.
*   **Fix**: Check system logs. The Self-Healing module should auto-retry, but if it fails repeatedly, it requires manual intervention.

### 4. Database Locked
*   **Cause**: High concurrency on the persistent store (rare, but possible).
*   **Fix**: Usually clears itself in ms. If persistent, check if another process is holding the lock.
