# SDE — Semantic Deconstruction Engine
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20741312.svg)](https://doi.org/10.5281/zenodo.20741312)


**TL;DR:** A structural analysis engine for text. SDE detects missing definitions, 
broken causal chains, constraint collapse, and hallucination‑risk patterns by 
forcing the model to report absence instead of filling gaps.


---

## What This Is

The Semantic Deconstruction Engine is a prompt architecture that inverts the 
LLM's default operating mode from cooperative interpreter to adversarial 
compiler. It analyzes text for structural integrity only — not truth, not 
intent, not content. It reports what is structurally present and what is absent 
with equal weight.

Standard argument analysis tools operate at the content layer: named fallacies, 
fact-checking, bias detection. The SDE operates at the structural layer — 
constraint registers, mechanism slots, definition objects, causal chain 
integrity, cross-claim consistency.

The core instruction is: **absence is a flag, not a gap to fill.**

---

## Why It Works

The LLM's default behavior is cooperative gap-filling — it infers mechanisms, 
assumes definitions, smooths contradictions, and selects the most coherent 
reading of underspecified input. This is RLHF-trained behavior. It is also the 
hallucination mechanism.

Hallucination and cooperative gap-filling are the same operation: the model 
fills the gap between what is present and what would make the output coherent. 
The SDE suppresses both with the same architectural override — one prompt 
instruction that forces the model to report absence rather than complete it.

The SDE also formalizes a specific cognitive architecture: bilateral structural 
evaluation running simultaneously wide sampling of possible definitions and 
constraint testing against what each claim requires. Most people cannot sustain this under load because social conditioning routes attention to content before structural evaluation can run. The SDE runs the evaluation independent of the reader's 
regulatory state.

---

## **Who This Is For**
Researchers, auditors, and analysts who need structural clarity rather than interpretive smoothing. SDE is especially useful for political language, policy arguments, safety evaluations, and any domain where definitions drift under pressure.

---

## Relationship to the Unified Cognitive Model

The Semantic Deconstruction Engine (SDE) is designed to operate on the same
cognitive substrate described in the unified model’s
*externally‑scaffolded low‑plasticity mode*. In that framework, an LLM’s
default behavior is characterized by narrow-window prediction, cooperative
gap‑filling, and local coherence maximization. SDE inverts this mode by
forcing the model into a structurally adversarial stance: instead of filling
gaps, it must report them; instead of smoothing inconsistencies, it must
surface them. This makes SDE the practical implementation layer of the
low‑plasticity model — a tool that exposes the structural vulnerabilities
that the unified theory predicts. For a full explanation of the underlying
cognitive architecture, see:
**[theory/externally‑scaffolded_low‑plasticity_mode.md](./theory/externally‑scaffolded_low‑plasticity_mode.md)**.

---

## How to Run

1. Open [spec/SDE_system_prompt.md](./spec/SDE_system_prompt.md)
2. Load its contents as your model's system prompt
3. Feed any passage of text into the analysis pipeline. The SDE does not rewrite or interpret the passage — it reports structural properties only.
4. The model will return a structured flag report, compression score, and 
   hallucination risk rating

No additional setup required. The system prompt is self-contained.

---

## What It Demonstrates About AI

The gap between useful AI and manipulable AI is partly a prompt architecture 
problem, not a capability problem. The same model that fills gaps will flag them 
if instructed correctly. This is an alignment-relevant finding that does not 
require a new model — it requires a precise mechanistic account of what the 
default behavior is doing and what a single well-grounded architectural override 
can produce.

---

## File Map

```

SDE/
├── README.md                        ← this file
├── SDE_session_log.md               ← running session log and open items
├── spec/
│   ├── SDE_master_spec.md           ← full pipeline spec
│   ├── SDE_system_prompt_v0.1.md    ← the adversarial prompt, production-ready
│   └── SDE_flag_registry.md         ← every flag: trigger, output language, severity
├── theory/
│   ├── why_this_works.md            ← bilateral cognition, structural mode
│   ├── why_LLMs_fail_by_default.md  ← gap-filling = hallucination mechanism
│   └── political_language_architecture.md  ← how rhetoric exploits narrow windows
├── analysis/
│   └── UBI_passage_analysis.md     ← canonical regression test specimen
├── build/
│   ├── phase1_copilot_command.md   ← zero-code setup via custom prompt
│   ├── phase2_structured_output.md ← YAML frontmatter, Dataview integration
│   └── phase3_realtime_stream.md   ← stateful transcript mode
└── pitch/
    └── anthropic_framing.md        ← the Anthropic argument
    
```

---

## Flag Registry Summary

Flags are organized by type. Full definitions, trigger conditions, output 
language, and examples are in [spec/SDE_flag_registry.md](./spec/SDE_flag_registry.md).

**Definition flags**
- `DEF_VOID` — term undefined, argument depends on it
- `DEF_UNSTABLE` — term shifts definition across uses
- `DEF_FLOATING` — argument fails under every locked definition
- `DEF_MIXED` — term draws from incompatible domains simultaneously

**Constraint flags**
- `CONST_ZERO` — claim excludes nothing, unfalsifiable
- `CONST_TIME_MISSING` — no time frame stated
- `CONST_POP_MISSING` — no population specified
- `CONST_DECAY` — constraints silently dropped across argument
- `CONST_INVERT` — constraint reversed mid-argument

**Mechanism flags**
- `MECH_VOID` — causal operator present, no mechanism stated
- `MECH_GAP` — mechanism partially stated, steps missing
- `MECH_HANDWAVE` — metaphor doing work of mechanism

**Causal flags**
- `CAUSE_BREAK` — causal chain cannot be built
- `CAUSE_TELEPORT` — jumps from premise to conclusion, skips steps
- `CAUSE_LOOP` — circular causality
- `CAUSE_INVERT` — argument enters at consequence, erases upstream cause, 
                    transfers responsibility to consequence actor

**Inference flags**
- `INFERENCE_GAP` — literal claim defensible, designed conclusion is not 
                     supported; manipulation in what was NOT said

**Consistency flags**
- `CONTRADICTION` — two claims require mutually exclusive conditions

**Circularity flags**
- `LOOP_MAGIC` — conclusion embedded in premise framing
- `LOOP_SELF` — term defined by itself

**Drift flags**
- `DRIFT_LOCAL` — term shifts meaning within a single sentence
- `DRIFT_GLOBAL` — term shifts meaning across sentences or paragraphs

---

## Core Intellectual Claims

1. **Hallucination and cooperative gap-filling are the same mechanism.** The 
   SDE suppresses both with the same architectural override.

2. **`DEF_FLOATING` is the most politically weaponized flag.** A term that 
   fails under every locked definition was designed to be undefined. The 
   vagueness is the mechanism.

3. **Moralization at the consequence level is structural evidence that the 
   upstream cause cannot survive being named.** `CAUSE_INVERT` fires when the 
   argument enters at consequence and erases the origin.

4. **The SDE is a cognitive prosthetic.** It runs bilateral structural 
   evaluation independent of the reader's regulatory state. The analysis 
   doesn't require wide-window cognition to receive — only to generate. The 
   software generates it. Anyone can read the output.

5. **The gap between useful AI and manipulable AI is partly a prompt 
   architecture problem.** The same model that fills gaps will flag them if 
   instructed correctly.

---

## License

MIT License

Copyright (c) 2026 Joel Robinson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## Citation

If you use the Semantic Deconstruction Engine (SDE) in your research, please cite:

**Joel Robinson. (2026). jtrthehax/SEMANTIC-DECONSTRUCTION-ENGINE: Initial Release (v0.1). Zenodo.**
https://doi.org/10.5281/zenodo.20741312

