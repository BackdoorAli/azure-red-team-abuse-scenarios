# Scenarios — Index

This directory contains attacker-focused Azure abuse scenarios, organised by phase of operation.

Each scenario includes:
- Attacker objective
- Initial assumptions
- High-level attack flow
- Decision logic
- OPSEC considerations
- Detection gaps (optional defensive awareness)

> **Note:** This repository intentionally avoids step-by-step instructions that could enable unauthorised activity.
> All scenarios assume authorised testing or lab environments.

---

## 02 — Identity Abuse

- **Overview:** `02-identity-abuse/00-identity-abuse-overview.md`
- **Scenario 01:** `02-identity-abuse/01-token-abuse.md`
- **Scenario 02:** `02-identity-abuse/02-oauth-consent-abuse.md`

Related diagrams:
- `../diagrams/identity-abuse/token-abuse-attack-flow.md`

---

## 03 — RBAC Privilege Escalation

- **Scenario 03:** `03-rbac-privilege-escalation/01-role-chaining.md`

Related diagrams:
- `../diagrams/rbac-escalation/role-chaining-attack-flow.md`

---

## 04 — Lateral Movement

- **Scenario 04:** `04-lateral-movement/01-managed-identity-abuse.md`

Related diagrams:
- `../diagrams/lateral-movement/managed-identity-attack-flow.md`

---

## 05 — Persistence

- **Scenario 05:** `05-persistence/01-service-principal-persistence.md`

Related diagrams:
- `../diagrams/persistence/service-principal-persistence-flow.md`

---

## Roadmap (Next Additions)

Planned future scenarios include:
- Guest user pivoting and tenant trust abuse
- Conditional Access blind spots
- Key Vault pivot patterns
- Automation Account abuse patterns
- Subscription boundary hopping
- OPSEC failures and detection gaps

