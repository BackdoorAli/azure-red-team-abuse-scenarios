# Identity Abuse Scenarios — Overview

## Why Identity Is the Primary Azure Attack Surface

In Azure environments, **identity is the control plane**.

Unlike traditional on-prem networks where attackers must pivot through hosts and network segments, cloud attackers who compromise identity can often:
- Enumerate resources remotely
- Interact directly with management APIs
- Bypass network-based controls entirely

For this reason, **identity abuse is the most common and most damaging class of cloud intrusion**.

---

## Attacker Perspective

From a red team perspective, identity abuse is attractive because it:

- Requires no exploits
- Scales across regions and subscriptions
- Persists independently of endpoints
- Often survives password resets
- Bypasses many traditional security controls

Attackers prioritise **identity access** over host access.

---

## Assumed Initial Conditions

All scenarios in this section assume the attacker has obtained **some form of Azure identity context**, such as:

- A stolen access token
- A stolen refresh token
- OAuth application consent
- Compromised service principal
- Guest user access

The attacker does **not** initially assume high privileges.

---

## Identity ≠ Privilege

A critical concept throughout these scenarios:

> **Authentication does not equal authorisation.**

Attackers must:
1. Discover what the identity can access
2. Enumerate effective permissions
3. Identify escalation paths through trust relationships

Most Azure breaches occur **after** this discovery phase.

---

## Scenario Categories in This Section

This identity abuse section covers:

- Token abuse and replay
- OAuth application consent abuse
- Guest-to-internal tenant pivoting
- Conditional Access blind spots
- Identity-based lateral movement

Each scenario is written from an **attacker decision-making perspective**.

---

## How to Read These Scenarios

Each scenario includes:

- Attacker objective
- Initial assumptions
- High-level attack flow
- Decision logic
- OPSEC considerations
- Detection gaps

Commands and tooling are intentionally minimised.

---

## Red Team Takeaway

> In Azure, the fastest path to impact is not exploitation —  
> it is **identity abuse combined with patience**.
