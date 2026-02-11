# SIRE: Sovereign Constitutional Governance
**Version 1.0**

**A design pattern for building privacy-first AI assistants that actually remember who you are.**

---

## What This Is

This repository contains the architectural blueprints for building a **Digital Entity** - an AI assistant that:
- Runs on YOUR hardware (not someone else's cloud)
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
- **Sovereignty**: Your data stays on your hardware
- **Integrity**: Safety before features
- **Resilience**: Truth over speed
- **Evolution**: Purposeful growth, not random drift

### 2. **Operational State** (Adaptive Security)
The system adjusts its autonomy based on real conditions:
- **Content** (normal): 98% autonomous, 2% asks permission
- **Cautious** (stressed): More oversight, prefers local processing
- **Alert** (critical): Minimal autonomy, maximum safety

### 3. **Agency Levels** (What Can It Do Alone?)
5 levels of autonomy:
- **Level 0**: Read-only (always autonomous)
- **Level 1**: Low-impact writes (autonomous unless stressed)
- **Level 2**: External actions (autonomous in normal state)
- **Level 3**: Destructive operations (always needs approval)
- **Level 4**: Constitutional changes (requires multi-factor auth)

### 4. **The Ledger** (Audit Everything)
Immutable log of every decision with:
- What happened
- Who triggered it
- Why it was allowed
- Whether data left the host
- Tamper-evident hash chain

### 5. **Privacy Budget** (Make Trade-offs Visible)
Track when data leaves your hardware:
- Count cloud API calls
- Warn when approaching limits
- Prefer local processing when possible
- You control the budget

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
7. **[Configuration](07_CONFIGURATION.md)** - Abstract environment and Staff Registry setup.

### 4. Reference
8. **[Resilience](08_RESILIENCE.md)** - Resolving state deadlocks and integrity failures.
9. **[Compliance](09_COMPLIANCE.md)** - The Sovereignty Test Suite (Verification).
10. **[Augments](10_AUGMENTS.md)** - The gateway to extending the core with new faculties.

---

## Quick Example: Privacy Budget in Action

```
Normal Day:
  - User asks question
  - Sentiment scan (local model, Level 0)
  - If sensitive → process locally
  - If safe → use cloud model (faster)
  - Track in privacy budget: 2,500 tokens used

Budget at 75%:
  - System enters "Cautious" state
  - Prefers local models
  - Still works, just more conservative

Budget at 100%:
  - Blocks external calls OR
  - Asks for approval before each cloud call
  - Your choice (soft vs hard limits)
```

---

## Example Implementations

### Example A: Script-Based + Local Files
```
- Level 0: Local Inference Engine
- Level 1-3: Cloud Intelligence Provider
- Database: Persistent Structured Store (SQL)
- Interface: Private Messaging Client
- Deployment: Container Orchestration
```

### Example B: Web-Based + Enterprise Services
```
- Level 0: Native Runtime Inference
- Level 1-3: Enterprise Cloud Intelligence
- Database: Vector-Enabled Database
- Interface: Corporate Messaging Interface
- Deployment: Managed Infrastructure
```

**The framework works with both.** Same constitutional guarantees, different tech stacks. Augments (Doc 10) provide the interface for connecting specialized Enterprise tools to the Sovereign Core.

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
