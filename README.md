# BRSR → ISSB S2 Data Quality Validator

> An institutional-grade ESG analytics terminal for mapping Indian BRSR disclosures to ISSB S2 climate standards.

**[→ Open Live Tool](https://shashwatr9j.github.io/brsr-validator/)**

---

## What it does

Indian listed companies file sustainability data under SEBI's BRSR framework. Global institutional investors require disclosures aligned with ISSB S2. The gap between the two is where data quality problems and greenwashing risk live. This tool automates the forensic layer of that translation.

---

## Core modules

**Data Ingestion** — Accepts raw BRSR JSON payloads for Steel, Power, and Cement sectors. Field-level inventory against ISSB S2 mandatory requirements.

**ISSB S2 Pillar Mapping** — Cross-references every BRSR field against its ISSB S2 paragraph. Surfaces materiality gaps including Scope 3 Category 11 and Category 15 absences.

**Carbon Quality Radar** — Five-tier durability hierarchy for offset portfolios. Triggers NET_ZERO_INTEGRITY_RISK when avoidance credits exceed 40% of volume.

**Greenwash Detection** — Six heuristics: cherry-picked base years, Scope 3 avoidance, credit opacity, intensity laundering, target creep, offsetting-as-strategy.

**Assurance Readiness Score** — Weighted 0–100 score against institutional ESG integration thresholds.

**Peer Screener** — 12-entity brown-sector universe with live filtering by sector, score, and greenwash risk.

**Report Generator** — PDF memo, JSON pipeline export, and CSV flag register outputs.

---

## Scoring methodology

| Condition | Impact |
|---|---|
| Base score | +75 |
| Scope 3 not disclosed | −20 |
| Net Zero + >40% avoidance credits | −25 |
| FY2020 or earlier base year | −15 |
| Offset registry IDs absent | −10 |
| Reasonable assurance | +15 |
| Limited assurance | +3 |
| SBTi validated | +8 |
| Transition plan disclosed | +7 |

**80+** = ASSURANCE READY · **60–79** = CONDITIONAL · **40–59** = HIGH RISK · **<40** = REJECT

---

## Real-company benchmarks (FY2023-24)

| Company | Score | Verdict | Key factor |
|---|---|---|---|
| Infosys | 90/100 | READY | Reasonable assurance, SBTi, full S3, transition plan |
| Tata Steel | 72/100 | CONDITIONAL | Strong disclosure but FY2020 base year costs −15 pts |
| Adani Power | 30/100 | REJECT | No assurance, no Scope 3, COVID base year |
| Bharat Steel (sample) | 8/100 | REJECT | All four critical deductions triggered |

---

## Sample JSON

```json
{
  "entity": "Company Name",
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
  "sbt_validated": false,
  "transition_plan_disclosed": false
}
```

To test with a real company: pull Scope 1, Scope 2, and assurance details from any SEBI BRSR filing (free on BSE India or company investor relations pages), format as JSON, paste into Data Ingestion, and run validation.

---

## Governance

All analysis is governed by `AGENTS.md` — a machine-readable protocol defining adversarial evaluation posture, the carbon credit durability hierarchy, greenwash detection heuristics, and scoring methodology.

---

## Stack

Single-file HTML/CSS/JS · Chart.js · IBM Plex Mono + Sans · No build step · No dependencies · Deployable anywhere

---

*Personal project demonstrating ESG data pipeline design and ISSB S2 compliance tooling.*
