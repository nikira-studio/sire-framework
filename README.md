# SIRE: Sovereign Constitutional Governance
**Version 1.0**

**A design pattern for building privacy-first AI assistants that actually remember who you are.**

---

## What This Is

This repository contains the architectural blueprints for building a **Digital Entity** - an AI assistant that:
- Runs in YOUR environment (not someone else's cloud)
- Remembers conversations across sessions
- Makes decisions based on clear governance rules
- Tracks everything it does in an audit log
- Adapts its behavior based on system load and security conditions

Think of it as a pattern language for AI assistants that respect your privacy and operate transparently.

---

## What This Isn't

- ❌ Not a ready-to-run application
- ❌ Not tied to a specific programming language
- ❌ Not a replacement for OpenClaw, Home Assistant, or other tools
- ❌ Not a commercial product

**This is a framework.** You implement it using whatever stack you prefer (e.g., JavaScript, Go, Rust, etc.).

---



## Why You Might Want This

**If you're building an AI assistant and you care about:**
- **Privacy**: Keep sensitive data local, not in someone else's API
- **Transparency**: Know exactly what your AI is doing and why
- **Memory**: Have your AI remember context across days, weeks, months
- **Governance**: Clear rules about what the AI can do autonomously vs what needs approval
- **Resilience**: AI that doesn't hallucinate or loop forever burning tokens

**Then this framework gives you the patterns to build that.**

---

## Core Concepts

### 1. **The Sovereign Core** (Constitutional Principles)
Four rules that govern every decision:
- **Sovereignty**: Your data stays on your controlled storage
- **Integrity**: Safety before features
- **Resilience**: Truth over speed
- **Evolution**: Purposeful growth, not random drift

### 2. **Operational State** (Adaptive Security with Bifurcated Friction)
The system adjusts its autonomy based on real conditions with distinct friction types:
- **Content** (normal): 98% autonomous, 2% asks permission
- **Cautious** (stressed): 
  - *Substrate Friction* (Resource): Load Shedding—pauses background tasks, offloads non-sensitive logic
  - *Integrity Friction* (Security): Isolation—local-only vetting, quarantine, disabled external egress
- **Alert** (critical): Minimal autonomy, maximum safety, external connections blocked

### 3. **Agency Levels** (What Can It Do Alone?)
5 levels of autonomy with Transactional Manifest Protocol:
- **Level 0**: Read-only (always autonomous)
- **Level 1**: Low-impact writes (autonomous unless stressed)
- **Level 2**: External actions (autonomous in normal state)
- **Level 3**: Destructive operations (requires Transactional Manifest with MFA approval)
- **Level 4**: Constitutional changes (requires Transactional Manifest with MFA + 24h cooldown)

### 4. **The Ledger** (Audit Everything)
Immutable log of every decision with:
- What happened
- Who triggered it
- Why it was allowed
- Whether data left the domain
- Tamper-evident hash chain with **JCS (JSON Canonicalization Scheme)** for cross-platform hash verification
- **Tiered Archival & Pruning**: Merkle Root preservation for long-term storage efficiency
- Impact-Based Thresholds determine logging requirements

### 5. **Privacy Budget** (Weighted Sovereignty Exposure)
Track when data leaves your domain with intelligent routing:
- Heuristic-based decision trees route tasks by category (Code Generation, Research, Finance, PII)
- Dynamic routing curves (aggressive, balanced, conservative) adjust behavior as budget depletes
- Prefer local processing for low-sensitivity tasks, preserve budget for high-complexity operations
- **Output-Side Sentinel Scans**: Prevent multi-tenant memory leaks in autonomous summaries
- **PASS Protocol**: Pre-Authorized Safety Scripts for Alert mode emergency fallbacks
- You control the budget and routing strategy

---

## The Constitution (The SIRE-10)

### 1. The Core (Laws & Identity)
1. **[The Constitution](01_CONSTITUTION.md)** - The Sovereign Core, Soul, and Governance Model.
2. **[Architecture](02_ARCHITECTURE.md)** - System design, Heartbeat, and Operational State.
3. **[Agency & Permission](03_AGENCY.md)** - The 5-Level Autonomy model and Stall Detection.

### 2. The Shield (Security & Audit)
4. **[The Ledger](04_LEDGER.md)** - Immutable Audit Protocol and Learning Capture.
5. **[Security](05_SECURITY.md)** - Sentinel, Privacy Budget, and Break-Glass Protocol.

### 3. The Hands (Interface & Config)
6. **[Interfaces](06_INTERFACES.md)** - Dashboard, CLI, and visual signaling.
7. **[Configuration](07_CONFIGURATION.md)** - Abstract environment and Specialist Registry setup.

### 4. Reference
8. **[Resilience](08_RESILIENCE.md)** - Resolving state deadlocks and integrity failures.
9. **[Compliance](09_COMPLIANCE.md)** - The Sovereignty Test Suite (Verification).
10. **[Augments](10_AUGMENTS.md)** - The gateway to extending the core with new faculties.

---

## Quick Example: Weighted Privacy Budget in Action

```
Normal Day (Budget 0-50%):
  - User asks question
  - Heuristic evaluation: Code Generation (Low Sensitivity/High Complexity)
  - Routing: Cloud model preferred (fast, high-quality)
  - Track in privacy budget: 2,500 tokens used

Budget at 75% (Conservative Curve):
  - Heuristic evaluation: Code Generation (Low Sensitivity/High Complexity)
  - Routing: Cloud allowed (complexity threshold met)
  - Heuristic evaluation: Research (Low-Medium Sensitivity/Medium Complexity)
  - Routing: Local preferred (budget conservation)
  - Heuristic evaluation: Personal Finance (High Sensitivity/Low Complexity)
  - Routing: Local always (regardless of budget)

Budget at 100% (Emergency Curve):
  - All tasks route to local models (except high-complexity in aggressive mode)
  - External calls blocked OR require explicit Managing Associate override
  - Check `/admin budget_status` to see current routing mode
```

---

## Example Implementations

### Example A: Script-Based + Local Files
```
- Level 0: Local Inference Engine
- Level 1-3: Cloud Intelligence Provider
- Database: Persistent Structured Store (SQL)
- Interface: Private Messaging Client
- Deployment: Environmental Isolation
```

### Example B: Web-Based + Enterprise Services
```
- Level 0: Native Runtime Inference
- Level 1-3: Enterprise Cloud Intelligence
- Database: Vector-Enabled Database
- Interface: Corporate Messaging Interface
- Deployment: Managed Environment
```

**The framework works with both.** Same constitutional guarantees, different tech stacks. Augments (Doc 10) provide the interface for connecting specialized tools to the Sovereign Core.

## Deployment Scenarios

The SIRE framework is designed for any scenario where an AI entity interacts with a private domain:

*   **Single-User Domain**: Personal environments where a single Associate maintains full sovereignty over all data and decisions. Suitable for individual productivity, research, or local automation with strict privacy guarantees.

*   **Multi-Tenant Environment**: Collaborative environments where multiple Associates interact with the same Soul within defined boundaries. Memory isolation and scoped access ensure that sensitive data remains segregated while enabling shared knowledge and coordinated workflows.

*   **High-Availability Node**: Mission-critical deployments requiring strict deterministic guardrails, comprehensive audit trails, and minimal downtime. Suitable for edge-computing resources, configuration management, and automated workflows with fail-safe mechanisms.

> **Note**: This repository currently contains the framework documentation only. Reference implementations in various languages are welcome contributions. If you build one, let us know in Discussions!

---

## Getting Started

### 1. Read the Framework
Start with [01_CONSTITUTION.md](01_CONSTITUTION.md)

### 2. Check the Checklist
Review the [Constitutional Guarantee Checklist](05_SECURITY.md#constitutional-guarantee-checklist) to understand what you're building toward

### 3. Pick Your Stack
Choose tools you know (JS, Go, Rust, or any language)

### 4. Implement the Patterns
- Security Sentinel (scan inputs for sensitive data)
- Operational State Monitor (track system health)
- Agency Level routing (decide what needs approval)
- Ledger logging (audit everything)
- Privacy Budget tracking (count external calls)

### 5. Verify Constitutional Compliance
Use the checklist to make sure you've implemented the core patterns

---

## SIRE Lite Quick-Start (Low-Friction First Deployment)

For developers, hobbyists, or rapid prototyping, use the **SIRE Lite** preset to minimize friction while maintaining core constitutional guarantees.

### Quick Configuration Changes

**1. Set Threshold Preset in `config/threshold_presets.yaml`**:

```yaml
threshold_presets:
  active_preset: "sire_lite"
  
  sire_lite:
    name: "SIRE Lite"
    mfa_trigger_score: 0.9          # Only very high-impact requires MFA
    ledger_trigger_score: 0.7        # Higher threshold before logging
    level_3_manifest_score: 0.8   # More permissive for destructive ops
    auto_approve_level_3_threshold: 0.4  # Auto-approve Level 3 for low-impact (S < 0.4)
```

**2. Set Privacy Budget Routing Strategy in `config/models.yaml`**:

```yaml
routing_strategy:
  mode: "aggressive"  # Prefer cloud models for most tasks
  budget_tracking: "token-based"
  heuristics:
    code_generation_complexity_threshold: 0.7
    research_sensitivity_threshold: 0.3
```

### What This Gives You

| Feature | SIRE Lite | High-Integrity |
|--------|-----------|----------------|
| **MFA Required** | Only for S ≥ 0.9 | For S ≥ 0.3 |
| **Ledger Logging** | For S ≥ 0.7 | For S ≥ 0.1 |
| **Level 3 Manifests** | Auto-approve for S < 0.4 | Always required |
| **Privacy Budget** | Aggressive routing | Conservative routing |
| **Best For** | Development, prototyping, trusted environments | Production, high-security, audit requirements |

### SIRE Lite Deployment Checklist

- ✅ Threshold preset set to `sire_lite` in `threshold_presets.yaml`
- ✅ Routing strategy set to `aggressive` in `models.yaml`
- ✅ Privacy budget monitoring enabled (optional for development)
- ✅ Security Sentinel configured for input/output-side scans
- ✅ Ledger initialized with JCS canonicalization

### When to Upgrade

Upgrade from SIRE Lite to **Balanced** or **High-Integrity** presets when:
- Moving to production deployment
- Handling sensitive data (PII, credentials, financial)
- Multi-tenant environment with Associate isolation
- Require strict audit trails for compliance

---


---

## Contributing

This framework is still evolving. We welcome:

- **Pattern improvements**: Better ways to implement the core concepts
- **Implementation examples**: Reference implementations in different languages
- **Documentation fixes**: Typos, unclear explanations, missing details
- **Use cases**: How you're using the framework
- **Roadmap feedback**: Ideas for future features

**What we're NOT looking for:**
- Feature requests that violate the Sovereign Core principles
- Tech-stack-specific code (this is a framework, not an app)
- Contributions that make the framework more complex without clear benefit

### How to Contribute

**GitHub Issues** - Use for:
- Documentation bugs, typos, broken links
- Unclear or missing explanations
- Errors in the framework patterns

**GitHub Discussions** - Use for:
- Implementation questions ("How do I build X?")
- Pattern feedback ("Have you considered Y approach?")
- Sharing your implementations
- Use cases and success stories
- General questions about the framework

---

## FAQ

**Q: Is this production-ready?**  
A: The framework is. Your implementation needs to be built and tested.

**Q: What tech stack should I use?**  
A: Whatever you know best. The framework is implementation-agnostic.

**Q: Do I need all the roadmap features?**  
A: No. The core framework (docs 01-10) is complete. Extensions are optional.

**Q: Can I use this commercially?**  
A: Yes. This is public domain (The Unlicense). Build whatever you want.

**Q: Is this just for personal assistants?**  
A: No. The patterns work for any AI system where privacy, transparency, and governance matter.

**Q: How is this different from AutoGPT/LangChain/etc?**  
A: Those are execution frameworks. This is a governance and privacy framework. You could use LangChain as part of your implementation.

---

## License

This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or distribute this software, either in source code form or as a compiled binary, for any purpose, commercial or non-commercial, and by any means.

See [UNLICENSE](UNLICENSE) for full details.

---

## Acknowledgments

Built with feedback from builders tired of AI assistants that forget everything, leak data, and make decisions without explanation.

Inspired by the need for AI systems that respect sovereignty, maintain transparency, and operate under clear constitutional rules.

---

**The goal: AI assistants you can trust because you can verify exactly what they're doing and why.**
