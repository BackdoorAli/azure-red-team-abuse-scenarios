# Diagrams — Index

This directory contains visual representations of Azure red team abuse paths.

Each diagram is paired with a written scenario and focuses on:
- Attacker decision flow
- Trust boundary crossings
- Identity and permission abuse
- Stealth vs noise tradeoffs

Diagrams are provided as **narrative markdown files** with references to SVG/PNG assets.
This allows the project to remain readable even without rendered images.

---

## Identity Abuse Diagrams

- **Token Abuse Attack Flow**  
  `identity-abuse/token-abuse-attack-flow.md`

---

## RBAC Privilege Escalation Diagrams

- **RBAC Role Chaining Attack Flow**  
  `rbac-escalation/role-chaining-attack-flow.md`

---

## Lateral Movement Diagrams

- **Managed Identity Lateral Movement Flow**  
  `lateral-movement/managed-identity-attack-flow.md`

---

## Persistence Diagrams

- **Service Principal Persistence Flow**  
  `persistence/service-principal-persistence-flow.md`

---

## Diagram Conventions

Across all diagrams:
- Arrows indicate trust or control flow
- Boxes represent identities, resources, or control boundaries
- Dashed lines indicate indirect influence
- Labels emphasize attacker-relevant decisions

---

## Roadmap

Planned future diagrams:
- Guest user tenant pivoting
- Conditional Access evaluation blind spots
- Key Vault abuse chains
- Subscription boundary hopping
- OPSEC failure points

