# Scenario 03 — RBAC Privilege Escalation via Role Chaining

## Attacker Objective

Escalate privileges within an Azure subscription by abusing **Role-Based Access Control (RBAC)** relationships rather than exploiting vulnerabilities.

Attackers target RBAC because:
- Misconfigurations are common
- Permissions compound over time
- Escalation paths are often non-obvious
- Actions appear legitimate

---

## Initial Assumptions

The attacker has:

- Authenticated Azure identity access
- At least one assigned role (e.g., Reader, Contributor, or custom role)
- No direct administrative privileges

The environment contains **multiple resource groups or subscriptions**.

---

## Why RBAC Abuse Works

Azure RBAC is:
- Additive (permissions stack)
- Scope-based (resource → resource group → subscription)
- Often poorly reviewed over time

Small permissions granted for convenience can enable **unexpected privilege escalation paths**.

---

## High-Level Attack Flow

1. Enumerate assigned roles and scopes
2. Identify permissions allowing role assignment, resource modification, or identity interaction
3. Abuse role combinations to expand control
4. Pivot to higher-privileged scopes
5. Achieve effective administrative access

---

## Common Role Chaining Paths (Conceptual)

```text
Reader
  │
  ├─ Can read role assignments
  │
  ▼
Contributor
  │
  ├─ Can modify resources
  │
  ▼
Managed Identity Abuse
  │
  ├─ Identity has higher privileges
  │
  ▼
Owner / User Access Administrator
```

Attackers look for **indirect authority**, not direct admin roles.

---

## Abuse Techniques (Conceptual)

- Modifying Automation Accounts linked to privileged identities
- Assigning roles within allowed scopes
- Editing resources that execute under higher privileges
- Abusing custom roles with overlooked permissions

No commands or tooling are provided.

---

## OPSEC Considerations (Attacker Side)

- Role assignment changes are highly logged
- Escalation should minimise scope changes
- Sudden permission spikes are suspicious
- Using existing identities reduces noise

Stealthy escalation favors **existing trust relationships**.

---

## Detection Gaps Observed

RBAC abuse often succeeds because:
- Role reviews are infrequent
- Custom roles are poorly understood
- Permission inheritance is overlooked
- Monitoring focuses on sign-ins, not authorisation changes

---

## Red Team Takeaway

> In Azure, privilege escalation is rarely explosive —  
> it is **incremental, quiet, and contractual**.

---

## Defensive Awareness (Optional)

Defenders should:
- Regularly audit role assignments
- Limit role assignment permissions
- Review custom roles carefully
- Monitor changes to high-impact roles
