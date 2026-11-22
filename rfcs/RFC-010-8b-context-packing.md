# RFC-010: Evaluating `8b-is` Utilities for Wave/Ternary Compression, Token-Budgeted Context Packing, and Quantization Governance

**Document ID:** `RFC-010`  
**Status:** Informational / Architectural Evaluation & Edge Integration Specification  
**Target Environment:** Constrained `ARM64` Edge Nodes (`Android Termux`, `< 80 MB` Pure-Python Footprint) & Multi-Tier Local Workstations  
**Evaluated Ecosystem:** [`Borealiscodes/8b-is`](https://github.com/Borealiscodes/8b-is) (forked from [`8b-is`](https://github.com/8b-is), including [`8b-is/smart-tree`](https://github.com/8b-is/smart-tree) and `MEM|8` / `UltraDreamState` primitives)  
**Companion Specifications:** `RFC-006` (*The Geometry of Institutional Enclosure*), `RFC-007` (*Decoupling Attribution from Inference*), `RFC-008` (*Edge-Sovereign Deterministic Verification Toolkit*), `RFC-009` (*Deterministic Hardware-Bounded Inference Admission via `llmfit`*)

---

## Author & Human Context Disclaimer
> **Pacing, Sovereignty, and Self-Kindness Note:** As a neurodivergent human rights defender facing institutional duress, transnational repression, academic exclusion, and the denial of grants to explore this technology, **I owe myself the kindness of returning to this work strictly on my own terms.** Even with the roadmap, mathematics, and cross-repository analysis mapped out here, this specification is a calm reference point—never a deadline, obligation, or demand to build or maintain a system. Step away, rest, and return only when nervous-system capacity, safety, and curiosity align.

---

## 1. Executive Assessment: What `8b-is` Actually Is vs. How It Fits Your Stack

[`Borealiscodes/8b-is`](https://github.com/Borealiscodes/8b-is) is a fork of the **[`8b.is`](https://github.com/8b-is) Open-Source Systems Research** index—a Rust/Zig/DSP systems group exploring wave-based memory (`MEM|8`), 9-state complex ternary $\Sigma\Delta$ modulation (`UltraDreamState`), ephemeral cryptographic handshakes (`zeno`), and high-speed AST/directory compression ([`smart-tree`](https://github.com/8b-is/smart-tree)).

### 1.1 Crucial Architectural Clarification (Quantization vs. Compression)
Before integrating `8b-is` utilities, distinguish **three different meanings of "compression/quantization"**:

| Mechanism | What `8b-is` Provides | What Your `RFC-007`–`RFC-009` Stack Needs | Verdict |
| :--- | :--- | :--- | :--- |
| **1. LLM Weight Quantization (`GGUF` / `INT4` / `Q4_K_M`)** | **Does NOT provide** a general-purpose `llama.cpp` / `GGUF` weight quantizer. Its $\Sigma\Delta$ quantizers (`packRowSigmaDelta()`) target signal/phase bitplanes (`5.22 ENOB`, `1.04° RMS`), not transformer `safetensors` weight matrices. | Handled upstream by [`Borealiscodes/llmfit`](https://github.com) (`RFC-009` Layer 0) + pre-quantized `GGUF` weights (`Q4_K_M` / `IQ4_XS`). | **Do not use `8b-is` for LLM weight quantization.** |
| **2. Context & Corpus Compression (`MEM|8` / `smart-tree`)** | **[`smart-tree`](https://github.com/8b-is/smart-tree)** compresses directory trees, ASTs, and text corpora into ultra-dense, token-budgeted representations (`Marqant` / quantum-mode layouts) with `MEM|8` wave-anchored memory. | Directly reduces prompt token counts before sending evidentiary dossiers into a small local model (`1.5B–3B`) on constrained hardware. | **High Utility (Pre-Proposal Context Packing).** |
| **3. Supply-Chain & Ephemeral Boundary Security** | `smart-tree` includes a **Supply-Chain Security Scanner** (flagging rogue `npm`/`pip` patterns) and `zeno` defines single-use `32B` `0x62`-gate frame seals. | Reinforces `RFC-007` tamper-evident ingestion and Termux air-gap hygiene. | **Moderate-to-High Utility (Audit Hygiene).** |

---

## 2. Actionable Utilities in `8b-is` & Where They Plug In

### Utility A: `smart-tree` (`st`) Deterministic Context & Corpus Packing
* **What it does:** Written in Rust (`10–24x` faster than GNU `tree`), `smart-tree` supports **token-budgeted compression modes** (`--mode quantum`, `--mode marqant`, `--mode summary-ai`) that strip syntactic noise while preserving structural hierarchy.
* **How it fits `RFC-007` / `RFC-008`:**
  * **Strict Rule (`Lossless Manifest First`):** Never hash a *compressed* file as your primary evidentiary record. Under `RFC-007` Layer 1, you **must** first seal the raw unmodified bytes ($h_D = \text{SHA-256}(B)$) into `SourceManifest` (`RFC-008`).
  * **Where `smart-tree` helps:** Once `SourceManifest` is sealed, use `smart-tree` to compress large multi-file case directories into a compact index (`< 4,000` tokens) so a small workstation LLM (`RFC-009`) can locate *which* chunk IDs to inspect—without blowing out KV-cache RAM.
  * **Termux Constraint:** Do **not** compile `smart-tree` via `cargo` on your Android tablet (compiling Rust crates consumes `> 1.5 GB` in `~/.cargo` and `target/`). Use a pre-built `aarch64` release binary if available, or use the pure-Python `RFC-010` lossless/budgeted packer below on Termux.

### Utility B: Quiescence Gate ($\Gamma(t)$) & Dead-Zone Clamping (`MEM|8`)
* **What it does:** In the `8b-is` Rosetta Stone, the **Quiescence Gate $\Gamma(t)$** with dead-zone clamp ($\Delta = \gamma / 2$) halts runaway/idle compute loops when signal change falls below an entropy threshold.
* **How it fits `RFC-008` / `RFC-009`:** Prevents infinite retry loops in agentic LangGraph pipelines (`Borealiscodes/synapse`) when a small quantized model repeatedly fails `verify_proposal_gate()` (`QUOTE_MISMATCH`). After $k$ consecutive rejections on the same chunk, the Quiescence Gate clamps retries to zero and routes the chunk to human review—saving battery, thermal headroom, and CPU cycles on `ARM64`.

### Utility C: Supply-Chain Security Scanner
* **What it does:** Scans project dependency trees (`pyproject.toml`, `requirements.txt`, `package.json`) for anomalous or malicious package patterns.
* **How it fits `Termux Edge SOP`:** Run before installing any new Python dependency into `.venv` on your edge workstation.

---

## 3. Mathematical & Computational Formalization

### 3.1 Two-Stage Provenance-Preserving Context Compression
Let $D = \{d_1, d_2, \dots, d_m\}$ be a multi-document evidentiary dossier.

1. **Lossless Cryptographic Seal (`RFC-007` Invariant):**
   $$\mathcal{M}_D = \text{Seal}\big(D\big), \quad h_{\mathcal{M}} = H\left(\parallel_{j=1}^m H(B_j)\right)$$
2. **Token-Budgeted Structural Projection ($\Pi_B$):**
   Let $\Pi_B : D \to \tilde{D}$ denote a compression operator (such as `smart-tree --mode marqant` or deterministic extractive reduction) constrained by a hard token budget $B_{\text{tok}}$ determined by `llmfit` (`RFC-009`):
   $$|\text{Tokens}(\Pi_B(D))| \le B_{\text{tok}} \ll |\text{Tokens}(D)|$$
3. **Attribution Recovery Invariant:**
   Even when an LLM generates a candidate proposal $p$ over the compressed view $\Pi_B(D)$, the deterministic CPU gate $\mathcal{G}(p, \mathcal{M}_D)$ (`RFC-008`) evaluates $p$'s `exact_verbatim_quote` ($q$) against the **uncompressed, sealed source chunk** $t_i \in \mathcal{M}_D$:
   $$\mathcal{G}\big(p(\Pi_B(D)),\; \mathcal{M}_D\big) = 1 \iff q \subseteq t_i \;\land\; H(\text{UTF8}(t_i)) = h_{c_i}$$
   Thus, lossy context compression can **never** corrupt evidentiary attribution: if compression distorts a quote, $\mathcal{G}$ deterministically rejects it.

---

### 3.2 Quiescence Retry Clamp ($\Gamma_{\text{retry}}$)
Borrowed from `8b-is`'s Quiescence Gate $\Gamma(t)$, define the retry gate for chunk $c_i$ after $r$ failed LLM extraction attempts with cumulative gate error $E_r$:

$$\Gamma_{\text{retry}}(c_i, r) = \begin{cases} 1 & \text{if } r < R_{\max} \;\land\; \Delta_{\text{novelty}}(p_r, p_{r-1}) > \frac{\gamma}{2} \\ 0 & \text{otherwise (Clamp to Human Quarantine)} \end{cases}$$

If a quantized model emits identical or near-identical hallucinated quotes ($\Delta_{\text{novelty}} \le \gamma/2$), $\Gamma_{\text{retry}}$ immediately halts inference on chunk $c_i$, eliminating wasted compute.

---

### 3.3 Quantization Bit-Budget Selection (`RFC-009` + `RFC-010`)
When preparing an LLM for a workstation node (`allow_local_llm == True` in `RFC-009`), model weight footprint $W(P, b)$ for $P$ billion parameters at $b$ bits per weight (plus KV-cache overhead $\kappa$) is bounded by:

$$W(P, b) \approx \frac{P \cdot b}{8} \cdot (1 + \kappa) \le \min\Big(0.70 \cdot M_{\text{avail}},\; S_{\text{free}} - S_{\text{reserve}}\Big)$$

* **Actionable Quantization Path (Workstation Only):** Use `llama.cpp` (`llama-quantize`) or `optimum-quanto` on a desktop/workstation host—**never on Termux**—to quantize schema-adherent base models (`Qwen2.5-3B-Instruct` or `Llama-3.2-3B-Instruct`) to `Q4_K_M` ($b \approx 4.8\text{ bits/weight}$, $\approx 2.1\text{ GiB}$), then validate fit via `llmfit recommend --json`.

---

## 4. Pure-Python Edge Bridge (`rfc010_context_packer.py`)
For your `ARM64` Termux workstation (`0` Rust compilation overhead, `< 1 MB` footprint), this module implements **token-budgeted dossier packing** and the **Quiescence Retry Clamp ($\Gamma_{\text{retry}}$)** directly atop `rfc008_toolkit.py`:

```python
"""
rfc010_context_packer.py
RFC-010 Token-Budgeted Context Compression & Quiescence Retry Clamp.
Adapts 8b-is structural packing & quiescence invariants for pure-Python ARM64 Termux.
"""

from __future__ import annotations

import difflib
import re
from dataclasses import dataclass
from typing import List, Sequence

from rfc008_toolkit import SourceManifest, TextChunk


@dataclass(frozen=True)
class PackedContextIndex:
    manifest_sha256: str
    token_budget: int
    estimated_tokens_used: int
    packed_prompt: str


def estimate_tokens(text: str) -> int:
    """Fast deterministic token estimator (~4 chars/token for English/legal prose)."""
    return max(1, (len(text) + 3) // 4)


Use code with caution.
def compress_chunk_preview(chunk: TextChunk, max_chars: int = 240) -> str:
"""
Create a whitespace-normalized structural preview of a sealed chunk
for LLM routing while preserving its exact chunk_id anchor.
"""
collapsed = re.sub(r"\s+", " ", chunk.text).strip()
if len(collapsed) <= max_chars:
snippet = collapsed
else:
half = max_chars // 2
snippet = f"{collapsed[:half]} ... {collapsed[-half:]}"
return f"[CHUNK {chunk.chunk_id} | sha256:{chunk.chunk_sha256[:12]}] {snippet}"
def pack_manifest_within_budget(
manifest: SourceManifest,
token_budget: int = 1500,
) -> PackedContextIndex:
"""
Deterministically pack chunk routing previews within a strict token budget
so small quantized models never overflow KV-cache RAM.
"""
lines: List[str] = [
f"SOURCE: {manifest.source_filename} (manifest={manifest.manifest_sha256[:16]})",
"INSTRUCTION: Select chunk_id(s) below and extract exact_verbatim_quote from full chunk text.",
]
used = estimate_tokens("\n".join(lines))
for chunk in manifest.chunks:
entry = compress_chunk_preview(chunk)
cost = estimate_tokens(entry)
if used + cost > token_budget:
lines.append(f"[TRUNCATED AT CHUNK {chunk.chunk_id} DUE TO TOKEN BUDGET {token_budget}]")
break
lines.append(entry)
used += cost
return PackedContextIndex(
manifest_sha256=manifest.manifest_sha256,
token_budget=token_budget,
estimated_tokens_used=used,
packed_prompt="\n".join(lines),
)
def quiescence_retry_gate(
prior_quotes: Sequence[str],
latest_quote: str,
max_retries: int = 2,
dead_zone_gamma: float = 0.20,
) -> bool:
"""
8b-is Quiescence Gate adaptation:
Returns True if retry is permitted; returns False (clamps loop) if retry count
is exhausted or quote novelty falls inside the dead-zone clamp (delta <= gamma / 2).
"""
if len(prior_quotes) >= max_retries:
return False
dead_zone = dead_zone_gamma / 2.0
for prev in prior_quotes:
similarity = difflib.SequenceMatcher(None, prev, latest_quote).ratio()
novelty = 1.0 - similarity
if novelty <= dead_zone:
return False
return True
```

## 5. Summary Decision Matrix for Your Archive


Task	Tool to Use	Where to Run It
Verify whether your device can safely host an LLM	llmfit (RFC-009)	Workstation or Termux (EDGE_CPU_AUDIT_ONLY auto-lock)
Quantize an open-weights model (FP16 -> Q4_K_M)	llama.cpp (llama-quantize)	Desktop / Workstation only (never on Termux)
Compress large case directories into token-bounded maps	smart-tree (8b-is) or rfc010_context_packer.py	Workstation (smart-tree Rust binary) or Termux (rfc010_context_packer.py)
Halt repetitive LLM hallucinations & save compute	quiescence_retry_gate() (8b-is $\Gamma(t)$ concept)	Both Workstation & Termux
Verify quotes, timestamps & enclosure geometry	rfc008_toolkit.py (RFC-006 / RFC-007)	Both Workstation & Termux (0 MB AI weights)

---

## 6. References (APA 7th Edition)

* 8b.is Research Group. (2026). 8b.is: Open-source systems research & MEM|8 architecture [Computer software]. GitHub. https://github.com/8b-is
* 8b.is Research Group. (2026). smart-tree: Context-aware directory visualization engine with MEM8 compression [Computer software]. GitHub. https://github.com/8b-is/smart-tree
* Borealiscodes. (2026). RFC-006: The geometry of institutional enclosure [Preprint / Technical specification]. Zenodo. doi.org
* Borealiscodes. (2026). RFC-007: Decoupling attribution from inference [Preprint / Technical specification]. Zenodo. doi.org
* Borealiscodes. (2026). 8b-is: Research fork of 8b.is open-source systems repository [Computer software]. GitHub. https://github.com/Borealiscodes/8b-is
* Borealiscodes. (2026). llmfit: Research fork for hardware-bounded LLM sizing [Computer software]. GitHub. github.com
* Friston, K. (2010). The free-energy principle: A unified brain theory? Nature Reviews Neuroscience, 11(2), 127–138. doi.org
* Gerganov, G. (2024). llama.cpp: LLM inference in C/C++ and GGUF quantization [Computer software]. GitHub. github.com
* National Institute of Standards and Technology. (2015). Secure Hash Standard (SHS) (FIPS PUB 180-4). U.S. Department of Commerce. doi.org


