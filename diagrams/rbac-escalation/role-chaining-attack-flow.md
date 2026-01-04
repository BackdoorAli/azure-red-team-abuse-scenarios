# RBAC Privilege Escalation — Role Chaining Attack Flow

## Diagram Purpose

This diagram illustrates how attackers escalate privileges in Azure by **chaining RBAC permissions** rather than exploiting vulnerabilities.

It is intended to:
- Visualise non-obvious escalation paths
- Highlight scope inheritance abuse
- Show how small permissions compound
- Support red team explanations and reporting

No tooling or commands are represented.

---

## Diagram: Azure RBAC Role Chaining Flow

**Suggested filename (SVG/PNG):**
`rbac-role-chaining-attack-flow.svg`

---

## Flow Description

```text
Initial Azure Identity
(Role: Reader / Limited Custom Role)
        │
        ▼
Permission Enumeration
(Scopes, Role Assignments)
        │
        ▼
Resource Modification Capability
(Contributor / Partial Write Access)
        │
        ▼
Indirect Identity Control
(Automation Account / Managed Identity)
        │
        ▼
Higher-Privilege Identity Context
(Owner / User Access Administrator)
        │
        ▼
Effective Subscription Control
```

---

## Key Abuse Concepts

- **Additive permissions** enable unexpected authority
- **Scope inheritance** expands impact silently
- **Indirect control** is preferred over direct assignment
- **Identity-linked resources** are prime escalation targets

Attackers rarely seek immediate admin access — they **build towards it**.

---

## Trust Boundaries Crossed

- Resource-level → Subscription-level authority
- Human identity → Non-human identity
- Operational permissions → Administrative control

Each boundary crossed increases attacker leverage.

---

## OPSEC Considerations (Attacker Side)

- Role assignment events are heavily logged
- Resource modifications are less scrutinised
- Escalation should remain within existing scopes
- Avoid tenant-wide changes when possible

Quiet escalation favors **existing identities and workflows**.

---

## Optional Diagram Enhancements

Future versions may include:
- Logging and alert visibility points
- Noise indicators per action
- Defender review checkpoints
- Custom role misconfiguration highlights

---

## Usage

This diagram can be used:
- Alongside RBAC escalation scenarios
- During pentest debriefs
- In red team reporting
- For interview walkthroughs

