# Service Principal Persistence — Attack Flow Diagram

## Diagram Purpose

This diagram visualizes how attackers establish or abuse **service principals** to maintain durable, non-interactive access in Azure.

It is intended to:
- Show why application identities are attractive for persistence
- Highlight the difference between “new identity” and “abused existing identity”
- Emphasize stealth tradeoffs and logging choke points

No tooling or step-by-step creation instructions are included.

---

## Diagram: Service Principal Persistence Flow

---

## Flow Description

```text
Initial Access
(User identity with limited privileges)
        │
        ▼
Discovery
(App registrations / service principals / roles)
        │
        ▼
┌──────────────────────────────────┐
│ Persistence Choice               │
│  A) Abuse existing app identity  │
│  B) Establish new app identity   │
└──────────────────────────────────┘
        │
        ▼
Role / Permission Alignment
(RBAC or API permissions)
        │
        ▼
Non-Interactive Token Access
(Automation-like behavior)
        │
        ▼
Durable Access to Azure Resources
(Survives many user remediations)
```

---

## Key Abuse Concepts

- Application identities are “expected” to run quietly
- Ownership and inventory are often weak
- Permissions can be broad and persistent
- Activity can blend into DevOps automation patterns

Attackers aim to look like normal operations.

---

## Trust Boundaries Crossed

- Human access → Application identity access
- Interactive authentication → Non-interactive operation
- Scoped permissions → Expanded resource control

---

## OPSEC Considerations (Attacker Side)

- New apps/credentials are auditable and can be noisy
- Prefer minimal permission additions at first
- Reuse existing identities when possible
- Schedule activity to mimic expected automation

Stealth favors **existing service principals**.

---

## Optional Diagram Enhancements

Future versions may include:
- Separate “delegated vs application permissions” branches
- Visibility points for app consent and credential addition
- Indicators for high-signal events (tenant-wide consent, role spikes)
- Defender review checkpoints

---

## Usage

Use this diagram:
- Embedded in `01-service-principal-persistence.md`
- In red team reports and debriefs
- For interview walkthroughs and whiteboarding

