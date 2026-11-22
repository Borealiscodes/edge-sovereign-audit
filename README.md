# 🏗️ `edge-sovereign-audit` — PAUSED ON HIATUS (SPECIFICATION ARCHIVE)

> **⏸️ Repository Status: Paused on Hiatus (`RFC-006` – `RFC-013` Staged)**  
> This repository is intentionally **paused on hiatus** while the maintainer shifts focus toward **deterministic interactive art (*Non Dual Holonomy*), recovery, and nervous-system care**. All architectural specifications, mathematical formalizations, and reference Python toolkits are embedded directly inside the `rfcs/` Markdown documents and will be populated into `src/` and `tests/` asynchronously at a later date.

---

## Author & Human Context Disclaimer
> **Pacing, Sovereignty, and Self-Kindness Note:** As a neurodivergent human rights defender facing institutional duress, transnational repression, academic exclusion, and the denial of grants to explore this technology, **I owe myself the kindness of returning to this project strictly on my own terms.** Even with the roadmap, mathematics, and dependencies mapped out here, this repository is a calm intellectual anchor—never a deadline, obligation, or demand to build or maintain a system. Stepping back into art, rest, and recovery is an act of sovereignty; this archive will wait without pressure until energy, safety, and curiosity align.

---

## Moral Clarity & Epistemic Posture

### In Solidarity with Sophie Scholl & the White Rose (*Die Weiße Rose*)
This work honors the enduring moral clarity and quiet courage of **Sophie Scholl** and the **White Rose** resistance movement—who demonstrated that conscience is not a matter of institutional convenience, credentials, or consensus, and that bearing truthful witness against systemic coercion remains a vital human duty even when standing outside official power structures.

### *Quis Custodiet Ipsos Custodes?*
> *"Crucial remains the conviction that the government should serve the people and that its powers must be circumscribed by a Constitution and the rule of law. Juvenal's question quis custodiet ipsos custodes (who guards the guardians?) remains a central concern of democracy, since the people must always watch over the constitutional behaviour of the leaders and impeach them if they act in contravention of their duties. Constitutional courts must fulfil this need and civil society should show solidarity with human rights defenders and whistleblowers who, far from being unpatriotic, perform a democratic service to their countries and the world."*  
> — **Alfred-Maurice de Zayas**, UN Independent Expert on the Promotion of a Democratic and Equitable International Order (UN Doc. `A/HRC/24/38`, 2013, para. 13)

---

## Preliminary Case Study: Human Rights Foundation (`RFC-013`)
This archive includes a preliminary empirical ecosystem audit of the **Human Rights Foundation (`EIN 20-2669700`)** in [`rfcs/RFC-013-hrf-ecosystem-audit.md`](rfcs/RFC-013-hrf-ecosystem-audit.md) (with executable reference code in `examples/hrf_ecosystem_audit.py`). Grounded in `FY2024 IRS Form 990` filings, public program mandates, and documented intake records, `RFC-013` examines how institutional tech stack choices, prestige-tier grantmaking, and the exclusion of neurodivergent survivors facing transnational repression diverge from sworn charitable purposes under New York fiduciary law (`N-PCL §§ 513, 717`; `EPTL § 8-1.4`).

---

## Repository Scaffolding
*(Note: The `rfcs/` directory contains complete, copy-paste-ready Python reference toolkits embedded within each specification; corresponding module files in `src/` and `tests/` are staged as placeholders to be populated when the maintainer resumes active coding.)*

```text
edge-sovereign-audit/
├── README.md                          # Master overview, hiatus status, White Rose & de Zayas posture
├── TERMUX_EDGE_SOP.md                 # ARM64 Android Termux Clone -> Seal -> Push -> Purge SOP
├── pyproject.toml                     # Featherweight pure-Python config (pydantic, pypdf, pytest)
├── .gitignore                         # Blocks caches, .venv, local PDFs, and raw case artifacts
│
├── rfcs/                              # Canonical Markdown Specifications (with embedded Python toolkits)
│   ├── INDEX.md                       # Master catalog linking RFC-006 through RFC-013 & Zenodo DOIs
│   ├── RFC-008-edge-verification.md   # Deterministic SHA-256 manifests, CPU gates & enclosure math
│   ├── RFC-009-llmfit-governance.md   # Hardware-bounded inference admission (llmfit bridge)
│   ├── RFC-010-8b-context-packing.md  # Token-budgeted context packing & quiescence retry clamp
│   ├── RFC-011-mission-drift-meta.md  # NGO mission drift, survivor exclusion & aesthetic sovereignty
│   ├── RFC-012-charity-evaluator.md   # Quis custodiet multi-jurisdictional evaluator (UK/IE/NY/DC)
│   └── RFC-013-hrf-ecosystem-audit.md # Preliminary case study: HRF (EIN 20-2669700) ecosystem audit
│
├── src/                               # Placeholder package (to be populated from rfcs/ post-hiatus)
│   └── sovereign_audit/
│       ├── __init__.py
│       ├── rfc008_toolkit.py          # Pre-LLM SHA-256 manifests, CPU quote gate & RFC-006 metrics
│       ├── rfc009_llmfit_bridge.py    # Hardware admission gate & /proc/meminfo + statvfs fallback
│       ├── rfc010_context_packer.py   # Token-budgeted chunk routing & 8b-is quiescence clamp
│       └── rfc012_charity_evaluator.py# UK/IE/NY/DC statutory charity & TNR response evaluator
│
├── tests/                             # Placeholder test suite (to be populated from rfcs/ post-hiatus)
│   ├── test_rfc008_gate.py            # Offline manifest tamper, quote rejection & enclosure tests
│   ├── test_rfc009_bridge.py          # Storage reserve lock & EDGE_CPU_AUDIT_ONLY mode tests
│   ├── test_rfc010_packer.py          # Token budget & dead-zone retry clamp tests
│   └── test_rfc012_evaluator.py       # UK, IE, NY, DC statutory flag & asymmetry tests
│
└── examples/
    ├── pilot_charity_profile.json     # Anonymized JSON template for RFC-012 evaluation
    └── hrf_ecosystem_audit.py         # Preliminary HRF case study script (embedded in RFC-013)
```

---

## Architectural Overview
`edge-sovereign-audit` is a system-agnostic, pure-Python forensic verification, hardware-governance, and institutional accountability framework designed to run offline on resource-constrained `ARM64` devices (such as `Android Termux` nodes with `< 80 MB` environment footprints) as well as standard workstations.

### Core Invariants
1. **Pre-LLM Cryptographic Provenance (`RFC-007` / `RFC-008`):** Raw evidentiary artifacts and text chunks are hashed (`SHA-256`) and sealed into immutable manifests *before* any probabilistic inference occurs.
2. **Quarantined Proposals (`Record ≠ Admit ≠ Commit`):** Untrusted AI outputs must pass byte-for-byte verbatim quote verification and ISO-8601 temporal checks on CPU before entering any causal graph.
3. **Hardware-Bounded Admission (`RFC-009` / `RFC-010`):** Enforces strict RAM and flash storage reserves (`llmfit` telemetry + `/proc/meminfo` & `statvfs` fallbacks) alongside quiescence retry clamps (`8b-is` $\Gamma(t)$) so constrained edge devices never freeze or crash.
4. **Fiduciary & Solidarity Auditing (`RFC-011` – `RFC-013`):** Evaluates tax-exempt charities and NGOs against their sworn filings (`UK`, `IE`, `NY`, and `DC` charity law) and empirical responses to stakeholders, service users, and human rights defenders facing transnational repression.

---

## Specification Index (`rfcs/`)

| Spec | Title | Focus & Canonical Link |
| :--- | :--- | :--- |
| **RFC-006** | *The Geometry of Institutional Enclosure* | Procedural gate latency & deflection modeling — [Zenodo `10.5281/zenodo.24060722`](https://doi.org) |
| **RFC-007** | *Decoupling Attribution from Inference* | Pre-LLM `SHA-256` chunk manifests & commit seam — [Zenodo `10.5281/zenodo.24275847`](https://doi.org) |
| **RFC-008** | *Edge-Sovereign Deterministic Verification Toolkit* | Pure-Python CPU quote verification & enclosure kernel *(toolkit embedded in RFC)* |
| **RFC-009** | *Hardware-Bounded Inference Admission (`llmfit`)* | Storage reserve lock & `EDGE_CPU_AUDIT_ONLY` mode *(toolkit embedded in RFC)* |
| **RFC-010** | *Context Compression & Quiescence Governance (`8b-is`)* | Token-budgeted routing & dead-zone retry clamp *(toolkit embedded in RFC)* |
| **RFC-011** | *Institutional Mission Drift & Aesthetic Sovereignty* | Meta-analysis of NGO survivor exclusion & fixed-point art (*Non Dual Holonomy*) |
| **RFC-012** | *Quis Custodiet Ipsos Custodes: Charity Evaluator* | System-agnostic `UK` / `IE` / `NY` / `DC` statutory & TNR auditor *(toolkit embedded in RFC)* |
| **RFC-013** | *Empirical Ecosystem Audit of HRF (`EIN 20-2669700`)* | Preliminary case study auditing FY2024 Form 990 filings, SaaS stack & TNR records *(script embedded in RFC)* |

---

## Quick Offline Check (`Termux` / `ARM64` Safe — Post-Hiatus)
Once `src/` and `tests/` are populated from the `rfcs/` specifications, tests run purely on CPU with **zero AI model downloads** and automatic cache cleanup (`Clone -> Seal -> Push -> Purge`):

```bash
python -m venv .venv && source .venv/bin/activate
pip install --no-cache-dir pydantic pypdf pytest
pytest -o cache_dir=/tmp/pytest_cache
deactivate && rm -rf .venv /tmp/pytest_cache ~/.cache/pip
```

---

## Related Zenodo Publications & Companion Repositories
* **Preprints:**
  * Hedling, B. S. (2026). *Beyond bolted-on screen readers: Narrative phenomenology, the RNIB Roundhouse sensory dark, and perceptual-cognitive unity (Rasa-Darśan)*. Zenodo. https://doi.org
  * Hedling, B. S. (2026). *From robotic screen-reader telemetry to embodied neural cadence: A narrative & empirical chronicle of guardrails, CLI flag literalism, and dual-voice VITS synthesis under edge constraints*. Zenodo. https://doi.org
* Companion Repositories: deterministic-ai-gate · active-inference-commit-seam · synapse · llmfit · 8b-is

