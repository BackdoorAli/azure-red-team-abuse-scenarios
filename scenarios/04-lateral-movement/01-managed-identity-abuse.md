# Scenario 04 — Lateral Movement via Managed Identity Abuse

## Attacker Objective

Pivot across Azure resources by abusing **Managed Identities** and service-to-service trust relationships.

In Azure, lateral movement often occurs **without touching endpoints**:
- The control plane is accessible remotely
- Services authenticate to other services automatically
- Identity is embedded into resource workflows

---

## Initial Assumptions

The attacker has:

- Authenticated access to Azure with limited privileges (e.g., Contributor on a resource group)
- Visibility into deployed resources and their identities
- No direct access to sensitive resources initially

The environment includes services using managed identities (system-assigned or user-assigned).

---

## Why Managed Identity Abuse Works

Managed identities are designed to:
- Remove the need to store secrets
- Authenticate resources automatically
- Enable clean service-to-service access

Attackers exploit this because:
- Privileged identities are often attached to automation or compute
- Permissions are granted broadly for convenience
- Identity use is assumed to be legitimate service behavior

---

## High-Level Attack Flow

1. Enumerate resources with managed identities
2. Identify which identities have meaningful permissions
3. Gain influence over a resource that can request tokens as that identity
4. Use the identity context to access new resources
5. Repeat to expand reach

---

## Common Pivot Patterns (Conceptual)

```text
Low-Privilege User
  │
  ├─ Can modify a resource (e.g., automation / app service / VM extension)
  │
  ▼
Resource Requests Token
(as Managed Identity)
  │
  ▼
Token Used Against Azure APIs
(ARM / Graph / Key Vault)
  │
  ▼
Access to Higher-Value Resources
```

Attackers hunt for **identity-bearing resources** they can influence.

---

## Abuse Techniques (Conceptual)

- Modifying a workload that runs under a managed identity
- Abusing automation to execute service-to-service actions
- Pivoting from a compute identity into Key Vault, Storage, or other control-plane targets
- Using identity context for subscription/resource group traversal

No commands or deployment steps are provided.

---

## OPSEC Considerations (Attacker Side)

- Direct token requests may be detectable if abnormal
- Sudden access to Key Vault is high-signal
- Persistence is easier once an identity pivot succeeds
- Subtle resource changes are quieter than role changes

Attackers prefer modifying **workflows** over changing **roles**.

---

## Detection Gaps Observed

Managed identity abuse is difficult to spot because:
- Requests appear as valid service behavior
- Logs often attribute actions to the resource identity
- Normal baselines for service-to-service calls are poorly defined
- Organisations over-trust “non-human” identities

---

## Red Team Takeaway

> In Azure, lateral movement is often **identity movement**.

---

## Defensive Awareness (Optional)

Defenders should:
- Minimise managed identity privileges
- Monitor token requests and sensitive API access
- Restrict who can modify identity-bearing resources
- Review automation and CI/CD permissions regularly
