# Scenario 06 — Guest User to Internal Tenant Pivot

## Attacker Objective

Leverage **guest user access** (B2B collaboration) to pivot into an Azure tenant and gain broader visibility or privileges than originally intended.

Attackers favor guest access because:
- It is often treated as low risk
- Monitoring is weaker than for internal users
- Permissions tend to sprawl over time
- Trust assumptions are frequently incorrect

---

## Initial Assumptions

The attacker has:

- Access to a guest (B2B) account in the target tenant
- No administrative privileges
- Limited but legitimate access to shared resources

Guest access was intentionally granted by the organisation.

---

## Why Guest Abuse Works

Azure B2B is designed for collaboration, not adversarial environments.

Common weaknesses include:
- Over-permissioned guest users
- Guests added to groups with inherited privileges
- Lack of lifecycle management for guest accounts
- Poor visibility into guest activity

Attackers exploit **implicit trust** created by collaboration.

---

## High-Level Attack Flow

1. Authenticate as guest user
2. Enumerate accessible resources and groups
3. Identify inherited permissions and group memberships
4. Abuse trust relationships to expand access
5. Pivot deeper into tenant resources

---

## Common Pivot Patterns (Conceptual)

```text
Guest User
  │
  ├─ Member of shared group
  │
  ▼
Group Has RBAC Permissions
  │
  ▼
Access to Azure Resources
  │
  ▼
Indirect Privilege Expansion
```

---

## Abuse Techniques (Conceptual)

- Leveraging group-based RBAC assignments
- Exploiting misclassified guest vs member roles
- Using shared collaboration resources as footholds
- Combining guest access with identity abuse techniques

No tooling or procedural steps are provided.

---

## OPSEC Considerations (Attacker Side)

- Guest logins are sometimes monitored separately
- Over-enumeration increases visibility
- Slow, targeted access expansion is quieter
- Pivoting via groups is less noisy than direct role changes

---

## Detection Gaps Observed

Guest abuse often succeeds because:
- Guest activity is deprioritised
- Ownership of shared resources is unclear
- Group permissions are not reviewed regularly
- Guest lifecycle management is weak

---

## Red Team Takeaway

> In Azure, “external” does not always mean “low impact.”

---

## Defensive Awareness

Defenders should:
- Audit guest user permissions regularly
- Enforce guest access reviews
- Restrict guest membership in privileged groups
- Monitor guest activity for anomalies
