# Scenario 01 — Azure Identity Token Abuse

## Attacker Objective

Maintain authenticated access to Azure resources **without repeated authentication** by abusing issued identity tokens.

From an attacker perspective, tokens are preferred over credentials because they:
- Bypass MFA after issuance
- Are often long-lived
- Generate fewer interactive login events
- Are harder to attribute to a user

---

## Initial Assumptions

The attacker has obtained **a valid Azure identity token**, such as:

- An access token
- A refresh token
- An OAuth-issued token tied to a user or application

The attacker does **not** initially assume elevated privileges.

---

## Why Token Abuse Works in Azure

Azure identity tokens are:
- Decoupled from the original authentication context
- Valid across multiple Microsoft APIs
- Often insufficiently monitored after issuance

Conditional Access policies are evaluated **at token issuance**, not continuously.

---

## High-Level Attack Flow

1. Token acquisition (out of scope)
2. Token validation against Azure APIs
3. Scope and permission discovery
4. Token reuse or refresh
5. Pivoting to additional services

---

## Attacker Decision Logic

```text
Token Type?
│
├─ Access Token
│   ├─ Short-lived
│   ├─ Used for enumeration
│   └─ Limited persistence value
│
└─ Refresh Token
    ├─ Long-lived
    ├─ Enables silent re-authentication
    └─ High persistence value
```

Attackers prioritise **refresh tokens** when available.

---

## Abuse Techniques (Conceptual)

- Reusing tokens from non-interactive contexts
- Enumerating resources within granted scopes
- Pivoting between Microsoft Graph and Azure Resource Manager
- Refreshing tokens to extend access duration

No command-level instructions are provided.

---

## OPSEC Considerations (Attacker Side)

- Excessive API enumeration increases detection risk
- Token reuse from unusual geolocations is noisy
- Refresh token abuse creates identifiable patterns
- Guest identities often trigger higher scrutiny

A disciplined attacker limits scope and frequency.

---

## Detection Gaps Observed

Token abuse frequently evades detection because:

- Token usage does not equal interactive login
- Session correlation across services is limited
- Token refresh events receive less scrutiny
- Alerts focus on credential misuse, not token misuse

---

## Red Team Takeaway

> In Azure environments, compromise often begins **after authentication**.  
> Token abuse turns valid identity into durable access.

---

## Defensive Awareness (Optional)

While this repository is attacker-focused, defenders should:
- Reduce refresh token lifetimes
- Monitor token usage anomalies
- Enforce Continuous Access Evaluation
- Limit token scope wherever possible
