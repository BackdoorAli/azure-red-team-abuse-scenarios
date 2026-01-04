# Scenario 10 — Common Cloud OPSEC Failures & Detection Gaps

## Purpose

This scenario documents **common operational security (OPSEC) failures** made by attackers during Azure intrusions and how these failures lead to detection.

Understanding how attackers get caught is critical for:
- Improving red team tradecraft
- Designing stealthier operations
- Helping defenders prioritize detections

This section aggregates lessons from prior scenarios.

---

## Core OPSEC Principle

> In cloud environments, **noise accumulates across APIs, not hosts**.

Attackers are often detected not by a single action, but by **patterns over time**.

---

## Common OPSEC Failures

### 1. Over-Enumeration

- Enumerating entire tenants or subscriptions quickly
- Excessive API calls across services
- Treating cloud like a flat on-prem network

**Detection risk:** High  
**Why it fails:** API usage is logged and correlatable

---

### 2. Scope Expansion Too Quickly

- Jumping from low privilege to broad scopes rapidly
- Adding high-impact roles early
- Crossing subscription boundaries without staging

**Detection risk:** High  
**Why it fails:** Sudden permission spikes are anomalous

---

### 3. Token Abuse Without Context Preservation

- Reusing tokens from unusual locations
- Switching devices or IPs mid-session
- Ignoring original Conditional Access context

**Detection risk:** Medium–High  
**Why it fails:** Context drift stands out

---

### 4. Misuse of Automation and App Identities

- Running actions outside normal schedules
- Using app identities interactively
- Breaking expected service behavior patterns

**Detection risk:** Medium  
**Why it fails:** Baselines for automation exist

---

### 5. Poor Persistence Choices

- Creating new identities unnecessarily
- Granting overly broad permissions
- Leaving obvious artifacts (unused apps, roles)

**Detection risk:** Medium–High  
**Why it fails:** Persistence stands out during reviews

---

## Detection Gaps That Enable Attackers

Attackers succeed when organisations:
- Focus on sign-ins, not API behavior
- Monitor subscriptions independently
- Lack identity-to-resource correlation
- Treat service identities as implicitly trusted

These gaps appear repeatedly across cloud breaches.

---

## Red Team Takeaway

> Stealth in Azure is about **restraint, timing, and context preservation**.

The best operations look boring!

---

## Defensive Awareness (Optional)

Defenders improve detection by:
- Correlating API activity across services
- Monitoring scope and role changes
- Establishing baselines for automation identities
- Reviewing identity and permission changes regularly

---

## Closing Note

This repository intentionally emphasizes **how attackers fail**, not just how they succeed.

Understanding both sides leads to better security.
