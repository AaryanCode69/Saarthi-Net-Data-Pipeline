# Aadhaar Pulse

> A synthetic, explainable data intelligence platform for simulating aggregated Aadhaar-like update behavior.

---

## 🎯 Project Overview

Aadhaar Pulse is a data intelligence platform that uses **synthetic, anonymized, aggregated data** to:

- **Track internal migration flows** — Detect population movement patterns across districts
- **Detect peri-urban growth zones** — Identify areas transitioning from rural to urban
- **Identify digital exclusion risk** — Highlight regions with low digital adoption

### ⚠️ Important Disclaimer

> **This project does NOT use real Aadhaar data.**
> 
> All data is synthetic, anonymized, and aggregated at the district level.
> No personal, biometric, demographic, or UID fields are used.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        AADHAAR PULSE                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐        │
│   │  Synthetic  │───▶│     ML      │───▶│   Backend   │        │
│   │    Data     │    │  Pipeline   │    │    APIs     │        │
│   └─────────────┘    └─────────────┘    └──────┬──────┘        │
│                                                 │               │
│                                                 ▼               │
│                                          ┌─────────────┐       │
│                                          │  Frontend   │       │
│                                          │  Dashboard  │       │
│                                          └─────────────┘       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Design Principles

| Principle | Description |
|-----------|-------------|
| **Monolith-first** | Backend is monolith-first, microservice-ready |
| **Read-only APIs** | Backend does NOT compute ML logic; reads precomputed outputs |
| **Explainable ML** | Rule-based intelligence, no black-box models |
| **Strict contracts** | Minimal schemas, no field creep |

---

## 📊 Data Granularity

| Dimension | Granularity |
|-----------|-------------|
| **Spatial** | District level only |
| **Temporal** | Monthly (`YYYY-MM`) |
| **Identifiers** | Stable `district_id` (e.g., `RJ_JPR`) |

**NOT supported:**
- Daily data
- Individual records
- Sub-district aggregation

---

## 🧠 ML / Data Intelligence Scope

The ML layer is a **rule-based, explainable intelligence system** — not predictive AI.

### Key Signals

| Signal | Interpretation |
|--------|----------------|
| Address update velocity | Migration indicator |
| Youth ratio patterns | Workforce mobility |
| Address vs mobile updates | Digital exclusion risk |
| Sustained growth patterns | Peri-urbanization |

### Output Schema

All ML outputs conform to this **final payload shape**:

```json
{
  "district_id": "RJ_JPR",
  "month": "2024-07",
  "migration_score": 0.72,
  "migration_category": "high",
  "peri_urban_label": "rapid_growth",
  "digital_exclusion_score": 34
}
```

| Field | Type | Description |
|-------|------|-------------|
| `district_id` | string | Stable district identifier |
| `month` | string | Temporal period (`YYYY-MM`) |
| `migration_score` | float | Normalized score (0.0–1.0) |
| `migration_category` | enum | `low` \| `moderate` \| `high` \| `very_high` |
| `peri_urban_label` | enum | `stable` \| `emerging` \| `rapid_growth` \| `saturated` |
| `digital_exclusion_score` | integer | Risk index (0–100) |

---

## 📁 Project Structure

```
Saarthi-Net-Data-Pipeline/
├── .github/
│   └── instructions/
│       └── rules.instructions.md    # Global project rules (READ FIRST)
├── data/
│   └── contracts/
│       ├── district_master.csv      # District ID master list
│       └── api_payload_schema.json  # Final API payload schema
└── README.md
```

### Data Contracts

| File | Purpose |
|------|---------|
| `district_master.csv` | Single source of truth for district identifiers |
| `api_payload_schema.json` | JSON Schema for ML output / API payload |

---

## 🔌 API Endpoints (Planned)

| Endpoint | Description |
|----------|-------------|
| `/migration` | Migration scores and categories |
| `/peri-urban` | Peri-urbanization labels |
| `/digital-risk` | Digital exclusion scores |
| `/dashboard` | Aggregated dashboard payload |

All endpoints are **read-only** and serve precomputed data.

---

## 🎨 Frontend Expectations

- Consumes district × month level data
- Map-based visualizations (choropleth + overlays)
- No client-side computation
- Color scales derived from categories/scores

---

## 🚫 Ethical & Legal Constraints

These constraints are **absolute and non-negotiable**:

| ❌ NOT Allowed | ✅ Required |
|----------------|-------------|
| Real Aadhaar data | Synthetic data only |
| UIDAI API references | Custom synthetic schemas |
| Personal/individual records | District-level aggregation |
| Biometric/demographic fields | Anonymized signals only |
| Black-box ML models | Explainable rule-based logic |

---

## 🛠️ Development Guidelines

### Naming Conventions

| Context | Convention |
|---------|------------|
| CSV headers | `snake_case` |
| JSON keys | `camelCase` |
| District IDs | `UPPER_CASE` (e.g., `RJ_JPR`) |

### Code Rules

- No redundant fields
- No inferred fields without documentation
- No magic constants without comments
- No schema changes without approval

---

## 📜 Source of Truth

The file `.github/instructions/rules.instructions.md` is the **global source of truth** for all project constraints.

> If there is any conflict, the rules file overrides all other assumptions.

---

## 📋 Phase Roadmap

| Phase | Objective | Status |
|-------|-----------|--------|
| **Phase 0** | Data contracts & identifiers | ✅ Complete |
| **Phase 1** | Synthetic data generation | 🔲 Planned |
| **Phase 2** | ML pipeline implementation | 🔲 Planned |
| **Phase 3** | Backend API development | 🔲 Planned |
| **Phase 4** | Frontend dashboard | 🔲 Planned |


