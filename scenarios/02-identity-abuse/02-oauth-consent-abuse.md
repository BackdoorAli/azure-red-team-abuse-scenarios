# Scenario 02 — OAuth Application Consent Abuse

## Attacker Objective

Establish **durable, low-noise access** to Azure and Microsoft 365 resources by abusing OAuth application consent rather than user credentials.

From an attacker perspective, OAuth abuse is valuable because:
- Access persists independently of user password changes
- Tokens can be refreshed silently
- Activity appears as legitimate application behavior

---

## Initial Assumptions

The attacker has one of the following:

- Ability to convince a user to grant OAuth consent (authorised testing scenario)
- Access to a compromised user account with app consent privileges
- Existing access to a low-privileged Azure identity

The attacker does **not** initially assume administrative roles.

---

## Why OAuth Abuse Works

OAuth consent mechanisms are designed for usability and integration, not adversarial resistance.

Common weaknesses include:
- Overly broad permission scopes
- Poor visibility into app behavior
- Long-lived refresh tokens
- Limited review of existing app consents

Once consent is granted, the application becomes a **trusted identity**.

---

## High-Level Attack Flow

1. OAuth application is registered (or abused)
2. User or admin grants consent
3. Application receives delegated or application permissions
4. Tokens are issued to the application
5. Application accesses resources autonomously

---

## Attacker Decision Logic

```text
Consent Type?
│
├─ Delegated Permissions
│   ├─ Acts as user
│   ├─ Limited to user context
│   └─ Lower detection risk
│
└─ Application Permissions
    ├─ Acts independently
    ├─ Broader access
    └─ Higher impact, higher scrutiny
```

Attackers often start with **delegated permissions** and escalate if possible.

---

## Abuse Techniques (Conceptual)

- Requesting excessive scopes during consent
- Blending malicious access with legitimate application activity
- Using application identity for non-interactive access
- Pivoting from Microsoft Graph to other services

No implementation or tooling is provided.

---

## OPSEC Considerations (Attacker Side)

- Excessive API calls increase visibility
- Rare or unusual scopes attract attention
- Application permissions are more heavily logged
- Tenant-wide consent increases blast radius

Well-crafted abuse mimics normal SaaS integrations.

---

## Detection Gaps Observed

OAuth abuse often goes unnoticed because:
- Applications are treated as trusted entities
- User focus is on sign-ins, not app behavior
- Consent events are reviewed infrequently
- Token usage is attributed to apps, not users

---

## Red Team Takeaway

> OAuth abuse transforms an application into an insider.

---

## Defensive Awareness (Optional)

Defenders should:
- Audit OAuth app consents regularly
- Limit who can grant tenant-wide consent
- Monitor high-risk permission scopes
- Remove unused or stale applications
