# Decision Tree — Token Abuse vs Credential Abuse

## Purpose

This decision tree models how an attacker (or red team) chooses between **token-based access** and **credential-based access** in Azure environments.

It is designed to:
- Communicate attacker tradeoffs clearly
- Support scenario planning and reporting
- Reinforce cloud-specific operational thinking

---

## Core Principle

> In cloud environments, **tokens are often more valuable than passwords**.

Credentials provide access, but tokens provide **momentum** — especially after MFA has been satisfied.

---

## Decision Tree (High-Level)

```text
Do you have valid identity material?
│
├─ No
│   └─ Credential acquisition required (out of scope)
│
└─ Yes
    │
    ├─ You have a refresh token?
    │   ├─ Yes
    │   │   └─ Prefer token-based access (durable, low-friction)
    │   └─ No
    │       │
    │       ├─ You have an access token?
    │       │   ├─ Yes
    │       │   │   └─ Use token for enumeration and scoping
    │       │   └─ No
    │       │
    │       └─ You have credentials?
    │           ├─ MFA enforced?
    │           │   ├─ Yes → token acquisition becomes priority
    │           │   └─ No  → credential abuse may be viable
    │           └─ Conditional Access strict?
    │               ├─ Yes → prefer tokens already issued inside policy
    │               └─ No  → credential reuse may be feasible
```

---

## Attacker Tradeoffs

### Token Abuse (Prefer When)

- Refresh tokens are available
- MFA is strong and enforced
- Conditional Access blocks unfamiliar sign-ins
- The attacker wants low-noise API access
- The attacker wants continuity across password resets

**Strength:** Post-auth durability  
**Weakness:** Token patterns can be correlated if noisy

---

### Credential Abuse (Prefer When)

- MFA is absent or weak
- Legacy auth is allowed
- Access is needed for interactive workflows
- Token acquisition is difficult or blocked
- The attacker needs user-context UI access

**Strength:** Flexible access paths  
**Weakness:** Higher detection and user impact risk

---

## Red Team Note

In professional operations, attackers commonly:

1. Use credentials to authenticate once (if possible)
2. Convert access into tokens
3. Operate using tokens for the remainder of the engagement

This reduces friction and detection opportunities.

---

## Defensive Awareness (Optional)

Defenders reduce both options by:
- Enforcing MFA consistently
- Monitor possible MFA fatigue techniques
- Limiting refresh token lifetimes
- Monitoring token usage anomalies
- Auditing OAuth and app consent
- Restricting legacy authentication
