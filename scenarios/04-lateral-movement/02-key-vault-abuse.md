# Scenario 08 — Key Vault Abuse Chains

## Attacker Objective

Leverage access to **Azure Key Vault** to expand control over cloud resources by abusing secrets, keys, and certificates tied to identities and services.

Key Vault is a prime target because it often:
- Stores credentials for automation and services
- Bridges identity and infrastructure
- Provides access that cascades into other systems

---

## Initial Assumptions

The attacker has:

- An authenticated Azure identity (user, app, or managed identity)
- Read or limited access to a Key Vault
- No direct administrative control initially

The Key Vault is used by applications, automation, or CI/CD workflows.

---

## Why Key Vault Abuse Works

Key Vault is trusted as a secure storage mechanism, but:

- Permissions are frequently over-scoped
- Secrets are reused across services
- Rotation is inconsistent
- Access is granted to “make things work”

Attackers exploit **indirect trust** in stored secrets.

---

## High-Level Attack Flow

1. Discover accessible Key Vaults
2. Enumerate secrets, keys, or certificates
3. Identify where those secrets are used
4. Use recovered material to access new services
5. Chain access to escalate privileges or move laterally

---

## Common Abuse Chains (Conceptual)

```text
Identity Access
  │
  ├─ Can read Key Vault secrets
  │
  ▼
Retrieve Secret / Certificate
  │
  ▼
Authenticate to Service
(App / Automation / API)
  │
  ▼
Expanded Access
(New identity or higher scope)
```

---

## Abuse Techniques (Conceptual)

- Using stored credentials to access automation accounts
- Leveraging certificates for app authentication
- Pivoting from Key Vault to storage, compute, or APIs
- Combining Key Vault access with managed identity abuse

No tooling or extraction steps are provided.

---

## OPSEC Considerations (Attacker Side)

- Secret access events may be logged
- Bulk secret access is high signal
- Certificates provide quieter authentication paths
- Timing access to match automation schedules reduces noise

---

## Detection Gaps Observed

Key Vault abuse often succeeds because:
- Secret access is assumed legitimate
- Logs are not centrally monitored
- Secret usage is not correlated with downstream access
- Ownership and rotation practices are weak

---

## Red Team Takeaway

> Key Vault is not just storage — it is a **trust amplifier**.

---

## Defensive Awareness (Optional)

Defenders should:
- Apply least privilege to Key Vault access
- Monitor secret access patterns
- Enforce regular rotation
- Separate secrets by environment and function
