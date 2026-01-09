# Scenario 07 — Conditional Access Blind Spots

## Attacker Objective

Operate **inside Conditional Access (CA) policy boundaries** by abusing the fact that CA is primarily evaluated at authentication time, not continuously.

Attackers do not aim to bypass Conditional Access outright —  
they aim to **work within it**.

---

## Initial Assumptions

The attacker has:

- Valid Azure identity context (token, OAuth app, managed identity, or guest)
- Access that was issued under compliant Conditional Access conditions
- No need to trigger new interactive sign-ins

Conditional Access policies are correctly configured but not exhaustive.

---

## Why Conditional Access Has Blind Spots

Conditional Access decisions are typically based on:
- User or app identity
- Device state
- Location
- Risk at sign-in time

Once access is granted:
- Tokens remain valid for their lifetime
- Post-issuance behavior is weakly enforced
- API usage is less scrutinised than logins

---

## High-Level Attack Flow

1. Authenticate under compliant conditions
2. Receive access and/or refresh tokens
3. Shift activity to non-interactive API usage
4. Operate within granted scopes
5. Avoid triggering re-authentication

---

## Common Blind Spot Patterns (Conceptual)

```text
Compliant Sign-In
  │
  ├─ MFA satisfied
  ├─ Trusted device/location
  │
  ▼
Token Issued
  │
  ▼
Non-Interactive API Usage
  │
  ▼
Sustained Access Without Re-Evaluation
```

Attackers aim to **never re-cross the CA evaluation boundary**.

---

## Abuse Techniques (Conceptual)

- Token reuse from compliant sessions
- OAuth and application-based access
- Automation-like access patterns
- Timing activity to avoid risk recalculation

No bypass techniques or tooling are included.

---

## OPSEC Considerations (Attacker Side)

- Avoid triggering new sign-in events
- Maintain behavior consistent with original compliance context
- Prefer API access over portal interaction
- Limit geographic or device changes

Stealth is achieved by **remaining invisible to CA rechecks**.

---

## Detection Gaps Observed

Conditional Access blind spots exist because:
- Enforcement is front-loaded at authentication
- Token usage is loosely correlated to sign-in context
- API behavior is harder to baseline
- Alerts focus on login risk, not session behavior

---

## Red Team Takeaway

> Conditional Access controls *entry* — not *movement*.

---

## Defensive Awareness

Defenders should:
- Enable Continuous Access Evaluation where possible
- Reduce token lifetimes
- Monitor anomalous API usage
- Correlate token activity with sign-in context
