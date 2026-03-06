# OASIS
## Observational Alignment & Semantic Intelligence Substrate
### v0.1

---

## Definition

OASIS is a non-intrusive semantic alignment substrate that lets independently governed systems expose representations, declare correspondence, and derive observable alignment state. It does not move data, mutate systems, reconcile records, or execute workflows.

---

## 1. Core Principles

| Principle | Description |
|-----------|-------------|
| **Declarative** | OASIS stores definitions, not operational data copies. |
| **Deterministic** | Same registrations + same rules + same source state → same surfaces. |
| **Non-intrusive** | No write-back, no orchestration, no enforcement. |
| **Epistemic** | Absence and mismatch are valid states, not silent failures. |

---

## 2. Required Artifacts

### A. Registration

Describes what a system exposes.

| Field | Required | Description |
|-------|----------|-------------|
| `system_id` | ✅ | Identifier for the system |
| `anchor_name` | ✅ | Shared semantic anchor |
| `ees_type` | ✅ | `ENTITY` \| `EVENT` \| `STATE` |
| `representation_name` | ✅ | Name of the exposed representation |
| `primary_key_field` | ✅ | Primary key field name |
| `natural_key_fields` | ➖ | Optional array of natural key fields |
| `access_type` | ✅ | `VIEW` \| `API` \| `QUERY` \| `FILE` |
| `access_descriptor` | ✅ | Endpoint or connection reference |
| `version` | ✅ | Version identifier |
| `registered_at` | ✅ | Registration timestamp |

---

### B. Alignment

Declares how two registrations correspond.

| Field | Required | Description |
|-------|----------|-------------|
| `alignment_id` | ✅ | Unique alignment identifier |
| `anchor_name` | ✅ | Shared semantic anchor |
| `left_registration_id` | ✅ | Reference to left registration |
| `right_registration_id` | ✅ | Reference to right registration |
| `alignment_rule_type` | ✅ | `KEY_MATCH` \| `COMPOSITE` \| `EXPRESSION` |
| `alignment_expression` | ✅ | Rule expression |
| `version` | ✅ | Version identifier |
| `effective_date` | ✅ | Date the alignment takes effect |

---

### C. Surfaces

Derived, read-only outputs.

#### Alignment Surface

| Field | Description |
|-------|-------------|
| `anchor_name` | Shared semantic anchor |
| `left_key` | Key from the left registration |
| `right_key` | Key from the right registration |
| `alignment_status` | Derived alignment status (see below) |
| `derived_at` | Derivation timestamp |

**Status Values:**

| Status | Meaning |
|--------|---------|
| `ALIGNED` | Both sides match |
| `LEFT_ONLY` | Record exists only on the left |
| `RIGHT_ONLY` | Record exists only on the right |
| `PARTIAL` | Partial correspondence |
| `RULE_FAILURE` | Alignment rule could not be evaluated |

---

#### Status Surface

| Field | Description |
|-------|-------------|
| `anchor_name` | Shared semantic anchor |
| `system_name` | Name of the system |
| `presence_status` | Whether the system has a registration |
| `availability_status` | Whether the system is reachable |
| `alignment_status` | Derived alignment state |
| `derived_at` | Derivation timestamp |

---

#### Exposure Surface

| Field | Description |
|-------|-------------|
| `anchor_name` | Shared semantic anchor |
| `system_name` | Name of the system |
| `exposed_to` | Consuming system or scope |
| `access_descriptor` | Endpoint or connection reference |
| `exposure_tier` | Tier classification |
| `effective_date` | Date the exposure takes effect |

---

## 3. Invariants

- OASIS stores **no canonical entity copies**.
- OASIS executes **no side effects**.
- All surfaces are **derivable** from registrations and alignment rules.
- **EES typing is mandatory**.
- Alignment rules are **versioned**.
- **Absence is explicitly modeled**.

---

*OASIS v0.1 — Observational Alignment & Semantic Intelligence Substrate*
