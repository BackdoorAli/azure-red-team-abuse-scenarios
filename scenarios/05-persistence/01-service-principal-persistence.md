# Scenario 05 — Persistence via Service Principal Abuse

## Attacker Objective

Maintain durable access to Azure resources by establishing or abusing a **Service Principal** (application identity) that can operate non-interactively.

From an attacker perspective, service principals are valuable because:
- They are non-human identities (often less scrutinized)
- They support long-lived access patterns
- They can be granted precise or broad permissions
- They persist beyond user password resets

---

## Initial Assumptions

The attacker has:

- Authenticated access to Azure with limited privileges
- A path to influence identity configuration (directly or indirectly)
- No tenant-wide administrative control initially

The environment includes applications, automation, or integrations using service principals.

---

## Why Service Principal Persistence Works

Service principals are designed for automation and integration.

Common weaknesses include:
- Over-privileged application roles
- Long-lived credentials and weak rotation
- Poor inventory and ownership tracking
- Infrequent review of app permissions and role assignments

Attackers exploit the fact that application identities are treated as **operational necessities**.

---

## High-Level Attack Flow

1. Identify existing service principals and app registrations
2. Discover which have meaningful RBAC roles or API permissions
3. Establish persistence by creating or abusing an application identity
4. Operate using non-interactive tokens
5. Blend activity into normal automation patterns

---

## Persistence Patterns (Conceptual)

```text
Initial Access
  │
  ├─ Find over-privileged app identity
  │        OR
  ├─ Create/abuse app identity via indirect control
  │
  ▼
Assign RBAC Role / API Permission
  │
  ▼
Non-Interactive Token Access
  │
  ▼
Durable Control of Azure Resources
```

Attackers prefer persistence that survives user remediation actions.

---

## Abuse Techniques (Conceptual)

- Leveraging existing service principals with excessive privileges
- Abusing app registrations to obtain durable identity context
- Using role assignments that appear legitimate (“automation”)
- Operating with low-noise, scheduled activity patterns

No commands, tooling, or step-by-step creation instructions are provided.

---

## OPSEC Considerations (Attacker Side)

- New app registrations can be high-signal
- New credentials added to apps are auditable
- Permission grants may trigger alerts (especially tenant-wide)
- Persistence should be scoped narrowly at first

Stealthy persistence favors **existing identities** and minimal privilege changes.

---

## Detection Gaps Observed

Service principal persistence can evade detection because:
- App identities are expected to run without humans
- Ownership is unclear or outdated
- Activity blends into normal DevOps patterns
- Alerts focus on user logins rather than application actions

---

## Red Team Takeaway

> In Azure, the quietest persistence often looks like “automation.”

---

## Defensive Awareness (Optional)

Defenders should:
- Inventory all service principals and app registrations
- Remove stale apps and unused credentials
- Enforce credential rotation and short lifetimes
- Monitor permission grants and role assignment changes
- Apply least privilege to application identities
