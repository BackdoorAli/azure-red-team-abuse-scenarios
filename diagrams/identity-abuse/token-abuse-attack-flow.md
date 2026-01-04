# Token Abuse — Attack Flow Diagram

## Diagram Purpose

This diagram visualises how an attacker abuses Azure identity tokens **after authentication has already occurred**.

It is designed to:
- Show where control shifts from user to attacker
- Highlight trust boundaries
- Emphasize why token-based access is difficult to detect
- Support interview and presentation explanations

This diagram intentionally avoids tools and commands.

---

## Diagram: Azure Identity Token Abuse Flow

**Suggested filename (SVG/PNG):**
`token-abuse-attack-flow.svg`

---

## Flow Description

```text
User Authentication
        │
        ▼
Azure Entra ID Issues Token
        │
        ▼
┌─────────────────────────┐
│  Access Token Issued    │
│  Refresh Token Issued   │
└─────────────────────────┘
        │
        ▼
Token Obtained by Attacker
        │
        ▼
Non-Interactive API Usage
        │
        ▼
Resource Enumeration
        │
        ▼
Token Refresh / Replay
        │
        ▼
Sustained Azure Access
```

---

## Key Trust Boundaries

- Authentication → Authorisation boundary
- User session → Token lifetime boundary
- Conditional Access → Post-issuance usage boundary

Attackers operate **entirely after these boundaries are crossed**.

---

## Red Team Emphasis

- No credential reuse required
- MFA already satisfied
- Network location often irrelevant
- Abuse occurs through legitimate APIs

This is why token abuse is favored in cloud intrusions.

---

## Optional Diagram Enhancements

For future versions, I'll consider adding:

- Conditional Access evaluation point
- Logging and monitoring gaps
- Blue team visibility markers
- Noise vs stealth indicators

---

## Usage

This diagram is intended to be:
- Embedded in scenario documentation
- Used during interviews
- Referenced during red team planning
- Included in presentations or reports

