# 🏗️ `edge-sovereign-audit` — UNDER CONSTRUCTION

> **🚧 Status: Active Conceptual Archive & Edge Prototype (`RFC-006` – `RFC-012`)**  
> This repository is currently **under construction** and maintained asynchronously on constrained `ARM64` edge hardware (`0 MB` local AI weights required).

---

## Author & Human Context Disclaimer
> **Pacing, Sovereignty, and Self-Kindness Note:** As a neurodivergent human rights defender facing institutional duress, transnational repression, academic exclusion, and the denial of grants to explore this technology, **I owe myself the kindness of returning to this project strictly on my own terms.** Even with the roadmap, mathematics, and dependencies mapped out here, this repository is a calm intellectual anchor—never a deadline, obligation, or demand to build or maintain a system. Step away, rest, and engage only when nervous-system capacity, safety, and curiosity align.

---

## Epistemic Posture: *Quis Custodiet Ipsos Custodes?*
> *"Crucial remains the conviction that the government should serve the people and that its powers must be circumscribed by a Constitution and the rule of law. Juvenal's question quis custodiet ipsos custodes (who guards the guardians?) remains a central concern of democracy, since the people must always watch over the constitutional behaviour of the leaders and impeach them if they act in contravention of their duties. Constitutional courts must fulfil this need and civil society should show solidarity with human rights defenders and whistleblowers who, far from being unpatriotic, perform a democratic service to their countries and the world."*  
> — **Alfred-Maurice de Zayas**, UN Independent Expert on the Promotion of a Democratic and Equitable International Order (UN Doc. `A/HRC/24/38`, 2013, para. 13)

---

## Architectural Overview
`edge-sovereign-audit` is a system-agnostic, pure-Python forensic verification, hardware-governance, and institutional accountability toolkit designed to run offline on resource-constrained `ARM64` devices (such as `Android Termux` nodes with `< 80 MB` environment footprints) as well as standard workstations.

### Core Invariants
1. **Pre-LLM Cryptographic Provenance (`RFC-007` / `RFC-008`):** Raw evidentiary artifacts and text chunks are hashed (`SHA-256`) and sealed into immutable manifests *before* any probabilistic inference occurs.
2. **Quarantined Proposals (`Record ≠ Admit ≠ Commit`):** Untrusted AI outputs must pass byte-for-byte verbatim quote verification and ISO-8601 temporal checks on CPU before entering any causal graph.
3. **Hardware-Bounded Admission (`RFC-009` / `RFC-010`):** Enforces strict RAM and flash storage reserves (`llmfit` telemetry + `/proc/meminfo` & `statvfs` fallbacks) alongside quiescence retry clamps (`8b-is` $\Gamma(t)$) so constrained edge devices never freeze or crash.
4. **Fiduciary & Solidarity Auditing (`RFC-011` / `RFC-012`):** Evaluates tax-exempt charities and NGOs against their sworn filings (`UK`, `IE`, `NY`, and `DC` charity law) and empirical responses to stakeholders, service users, and human rights defenders facing transnational repression.

---

## Specification Index (`rfcs/`)

| Spec | Title | Focus & Canonical Link |
| :--- | :--- | :--- |
| **RFC-006** | *The Geometry of Institutional Enclosure* | Procedural gate latency & deflection modeling — [Zenodo `10.5281/zenodo.24060722`](https://doi.org) |
| **RFC-007** | *Decoupling Attribution from Inference* | Pre-LLM `SHA-256` chunk manifests & commit seam — [Zenodo `10.5281/zenodo.24275847`](https://doi.org) |
| **RFC-008** | *Edge-Sovereign Deterministic Verification Toolkit* | Pure-Python CPU quote verification & enclosure kernel (`rfc008_toolkit.py`) |
| **RFC-009** | *Hardware-Bounded Inference Admission (`llmfit`)* | Storage reserve lock & `EDGE_CPU_AUDIT_ONLY` mode (`rfc009_llmfit_bridge.py`) |
| **RFC-010** | *Context Compression & Quiescence Governance (`8b-is`)* | Token-budgeted routing & dead-zone retry clamp (`rfc010_context_packer.py`) |
| **RFC-011** | *Institutional Mission Drift & Aesthetic Sovereignty* | Meta-analysis of NGO survivor exclusion & fixed-point art (*Non Dual Holonomy*) |
| **RFC-012** | *Quis Custodiet Ipsos Custodes: Charity Evaluator* | System-agnostic `UK` / `IE` / `NY` / `DC` statutory & TNR auditor (`rfc012_charity_evaluator.py`) |

---

## Quick Offline Check (`Termux` / `ARM64` Safe)
Runs purely on CPU with **zero AI model downloads** and automatic cache cleanup (`Clone -> Seal -> Push -> Purge`):

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
* **Companion Repositories:** [`deterministic-ai-gate`](https://github.com) · [`active-inference-commit-seam`](https://github.com) · [`synapse`](https://github.com) · [`llmfit`](https://github.com) · [`8b-is`](https://github.com)
