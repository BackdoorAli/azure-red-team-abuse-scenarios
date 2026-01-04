# Scenario 09 — Subscription Boundary Hopping

## Attacker Objective

Move laterally **across Azure subscriptions** by abusing identity trust, RBAC scope inheritance, and management group relationships.

Attackers target subscription boundaries because:
- Organisations assume subscriptions are hard security boundaries
- RBAC assignments often span multiple subscriptions
- Visibility is fragmented across management scopes

---

## Initial Assumptions

The attacker has:

- Authenticated Azure identity access
- Privileges scoped to at least one subscription
- No initial access to other subscriptions

The organisation operates **multiple subscriptions** under the same tenant.

---

## Why Subscription Hopping Works

Subscriptions are **management and billing boundaries**, not strict security barriers.

Common weaknesses include:
- Shared identities across subscriptions
- Role assignments inherited from management groups
- Over-permissioned “central” identities
- Poor cross-subscription visibility

Attackers exploit **organisational convenience**.

---

## High-Level Attack Flow

1. Enumerate accessible subscriptions
2. Identify shared identities or inherited roles
3. Discover cross-subscription permissions
4. Pivot into additional subscriptions
5. Repeat to expand tenant-wide access

---

## Common Hopping Patterns (Conceptual)

```text
Subscription A
  │
  ├─ Shared Identity / Role
  │
  ▼
Management Group
  │
  ▼
Subscription B
  │
  ▼
Expanded Control Surface
```

---

## Abuse Techniques (Conceptual)

- Leveraging identities with multi-subscription roles
- Exploiting management group inheritance
- Using automation or app identities scoped broadly
- Pivoting via shared resources or pipelines

No commands or enumeration steps are provided.

---

## OPSEC Considerations (Attacker Side)

- Subscription enumeration is auditable
- Rapid cross-subscription movement is noisy
- Expanding scope gradually reduces detection
- Staying within expected operational roles is quieter

---

## Detection Gaps Observed

Subscription hopping often goes unnoticed because:
- Teams monitor subscriptions independently
- No single view of tenant-wide access
- Role inheritance is poorly understood
- Alerts focus on resource activity, not scope expansion

---

## Red Team Takeaway

> In Azure, subscriptions divide billing — not trust.

---

## Defensive Awareness (Optional)

Defenders should:
- Review management group role assignments
- Limit identities with cross-subscription access
- Centralize logging and monitoring
- Audit subscription access regularly
