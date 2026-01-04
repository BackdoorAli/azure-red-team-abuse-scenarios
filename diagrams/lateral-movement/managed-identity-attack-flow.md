# Managed Identity Abuse — Lateral Movement Diagram

## Diagram Purpose

This diagram visualises how attackers move laterally in Azure by leveraging **Managed Identities** and service-to-service trust relationships.

It is intended to:
- Demonstrate cloud-native lateral movement (often without endpoints)
- Highlight where identity and permission boundaries are crossed
- Show why “resource influence” matters more than “host access”

No tooling or commands are included.

---

## Diagram: Managed Identity Lateral Movement Flow

**Suggested filename (SVG/PNG):**
`managed-identity-lateral-movement-flow.svg`

---

## Flow Description

```text
Compromised User Identity
(Limited RBAC)
        │
        ▼
Resource Enumeration
(Find identity-bearing resources)
        │
        ▼
Resource Influence Achieved
(App Service / Automation / VM Extension / Function)
        │
        ▼
Resource Requests Token
(as Managed Identity)
        │
        ▼
Token Used Against Azure APIs
(ARM / Graph / Key Vault)
        │
        ▼
Access to New Scope / New Resources
        │
        ▼
Repeat (Identity Movement)
```

---

## Key Abuse Concepts

- **Identity-bearing resources** are lateral movement vehicles
- **Influence** over a workload can be more valuable than direct privileges
- **Tokens** enable control-plane actions remotely
- Lateral movement is often **API-driven**

---

## Trust Boundaries Crossed

- Human identity → Non-human identity
- Resource scope → Broader scope (RG / Subscription)
- Workload control → Identity authority

Each boundary increases attacker reach.

---

## OPSEC Considerations (Attacker Side)

- Prefer modifying workflows over role assignments
- Avoid sudden spikes in sensitive API calls
- Limit pivot depth to maintain stealth
- Blend actions into expected automation behavior

---

## Optional Diagram Enhancements

Future versions may include:
- Identity types (system vs user-assigned)
- Noise indicators per pivot method
- Defender visibility points (logs/alerts)
- “High value” targets (Key Vault, Storage, Graph)

---

## Usage

Use this diagram:
- Embedded in `01-managed-identity-abuse.md`
- In engagement debriefs and reports
- For interview walkthroughs and whiteboarding

