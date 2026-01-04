# Azure Red Team Abuse Scenarios (AZ-900 Aligned)

> **Attacker-focused cloud tradecraft for Azure environments**  
> Identity abuse • RBAC escalation • Lateral movement • Persistence • OPSEC

---

## Author

**BackdoorAli**  
GitHub: https://github.com/BackdoorAli

---

## What This Project Is

This repository documents **realistic Azure attack paths** from a **red team / attacker perspective**.

It focuses on *how Azure environments are actually abused after access is obtained*, emphasizing:

- Identity over exploitation
- Authorisation over authentication
- Control-plane abuse over host compromise
- Stealth, OPSEC, and attacker decision-making

This is **not a tool repository**.  
This is a **tradecraft and reasoning repository**.

---

## Who This Is For

- Red teamers and pentesters moving into cloud
- Security professionals with AZ-900 / Security+ background
- Blue teamers studying attacker behavior
- Recruiters and interviewers evaluating cloud offensive skills

If you know *what Azure is* but want to understand *how Azure gets abused*, this repo is for you.

---

## Core Design Philosophy

- Scenario-driven, not tool-driven  
- Diagrams before commands  
- Attacker logic and tradeoffs  
- OPSEC-aware throughout  
- Ethical and lab-safe  

All scenarios assume **AUTHORISED testing or lab environments only**.

---

## Repository Structure

```text
scenarios/        → Attacker abuse scenarios
diagrams/         → Visual attack flows and decision logic
decision-trees/   → Attacker tradeoff models
ethics-and-scope.md
```

---

## Scenario Coverage

### Identity Abuse
- Token abuse and replay
- OAuth application consent abuse
- Guest user → internal tenant pivoting
- Conditional Access blind spots

### Authorisation & Privilege Escalation
- RBAC role chaining
- Subscription boundary hopping
- Management group inheritance abuse

### Lateral Movement (Cloud-Native)
- Managed identity abuse
- Key Vault pivot chains
- Resource-to-resource identity movement

### Persistence
- Service principal persistence
- Automation and application camouflage
- Non-interactive durable access

### OPSEC & Detection
- Common cloud OPSEC failures
- Detection gaps attackers exploit
- Why real-world attackers get caught

A full index is available in [`scenarios/README.md`](scenarios/README.md).

---

## Diagrams & Visuals

Each major scenario is paired with:
- Attack flow diagrams
- Trust boundary visualizations
- Decision logic models

See [`diagrams/README.md`](diagrams/README.md) for the full diagram index.

---

## Ethics & Responsible Use

This repository:
- Does **not** contain exploit weaponization
- Does **not** include phishing kits or malware
- Does **not** provide step-by-step real-world abuse instructions

It exists to **improve security through understanding attacker behavior**.

Read the full ethics statement in [`ethics-and-scope.md`](ethics-and-scope.md).

---

## Why This Repo Exists

Most cloud security resources explain:
> “What Azure features do.”

This repository explains:
> **“What attackers do with them.”**

---

## Author Intent

This project was built to demonstrate:
- Cloud attacker mindset
- Red team operational reasoning
- Mature handling of offensive knowledge
- Readiness beyond certification-level understanding

---

## Roadmap

Planned future additions:
- CI/CD pipeline abuse
- Cross-tenant trust exploitation
- Defender deception techniques
- Cloud red team reporting examples

---

> **Stealth in Azure is not about exploits.**  
> It is about **identity, timing, and restraint**.
