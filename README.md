# BRSR → ISSB S2 Data Quality Validator

> An institutional-grade ESG analytics terminal for mapping Indian BRSR disclosures to ISSB S2 climate standards — built for brown-sector analysis at scale.

**[→ Open Live Tool](https://shashwatr9j.github.io/brsr-validator/)**

---

## What it does

Indian listed companies file sustainability data under SEBI's Business Responsibility and Sustainability Report (BRSR) framework. Global institutional investors increasingly require disclosures aligned with the ISSB S2 Climate standard. The gap between the two is where data quality problems — and greenwashing risk — live.

This tool automates the forensic layer of that translation.

---

## Core modules

**Data Ingestion**
Accepts raw BRSR JSON payloads for Steel, Power, and Cement sector entities. Supports drag-and-drop upload or direct paste. Runs a field-level inventory against ISSB S2 mandatory disclosure requirements.

**ISSB S2 Pillar Mapping**
Cross-references every populated BRSR field against its corresponding ISSB S2 paragraph. Scores mapping confidence per field and surfaces materiality gaps — including critical absences like Scope 3 Category 11 (Use of Sold Products) and Category 15 (Financed Emissions).

**Carbon Quality Radar**
Applies a five-tier durability hierarchy to offset credit portfolios. Flags portfolios over-reliant on non-permanent avoidance instruments (REDD+, IFM) and under-allocated to high-durability engineered removals (DAC, Subsurface Biomass Storage). Triggers `NET_ZERO_INTEGRITY_RISK` when avoidance credits exceed 40% of total volume.

**Greenwash Detection**
Six pattern-detection heuristics including cherry-picked base years, Scope 3 structural avoidance, credit quality opacity, intensity laundering, target qualification creep, and offsetting-as-primary-strategy.

**Assurance Readiness Score**
Weighted 0–100 score modelled on institutional ESG data integration thresholds. Deductions applied per flag category; additive credit for third-party assurance and SBTi validation.

**Peer Screener**
12-entity brown-sector universe (Steel, Power, Cement) with live filtering by sector, sort by score/coverage/greenwash risk. Includes Tata Steel, JSW, NTPC, UltraTech, and others.

**Report Generator**
Produces structured institutional memos in PDF memo, JSON pipeline export, and CSV flag register formats.

---

## Assurance scoring methodology

| Condition | Impact |
|---|---|
| Base score | +60 |
| Materiality gap (per critical field) | −10 |
| Net Zero integrity risk | −25 |
| Baseline integrity failure | −15 |
| Leakage unquantified (per tranche) | −5 |
| Assurance scope mismatch | −15 |
| Limited assurance present | +5 |
| SBTi validated targets | +8 |

Scores ≥ 80 → `ASSURANCE_READY` · 60–79 → `CONDITIONAL` · 40–59 → `HIGH_RISK` · < 40 → `REJECT`

---

## Sample payload

```json
{
  "entity": "Bharat Steel Ltd.",
  "fiscal_year": "FY2023-24",
  "sector": "steel",
  "scope1_mtco2e": 142850,
  "scope2_market_mtco2e": 89200,
  "scope3_disclosed": false,
  "net_zero_claim": true,
  "offset_credits": {
    "redd_plus_pct": 68,
    "ifm_pct": 22,
    "dac_pct": 10,
    "registry_ids_disclosed": false
  },
  "base_year": 2020,
  "third_party_assurance": "limited",
  "sbt_validated": false
}
```

---

## Governance

All analysis is governed by `AGENTS.md` — a machine-readable protocol file that defines adversarial evaluation posture, the carbon credit durability hierarchy, greenwash detection heuristics, and scoring methodology. Agents operating in this system default to maximum skepticism; disclosure claims are treated as unverified until an audit trail is present.

---

## Stack

Single-file HTML/CSS/JS · Chart.js · IBM Plex Mono + Sans · No build step · No dependencies · Deployable anywhere

---

*Built as a personal project to demonstrate ESG data pipeline design and ISSB S2 compliance tooling.*