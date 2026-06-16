# SDE Master Specification
**Version:** 0.1  
**Status:** Active  
**Path:** Job/Safety Systems/SDE/spec/SDE_master_spec.md  
**Depends on:** [[SDE_flag_registry]], [[SDE_system_prompt_v0.1]]

---

## 1. Purpose

The Semantic Deconstruction Engine (SDE) is a prompt architecture that 
inverts the LLM's default operating mode from cooperative interpreter to 
adversarial compiler. It analyzes text for structural integrity only — not 
truth, not intent, not content — and reports what is structurally present 
and what is structurally absent with equal weight.

It does not:
- Check facts
- Detect bias
- Identify named fallacies
- Evaluate rhetorical intent

It does:
- Flag undefined terms that arguments depend on
- Flag missing causal mechanisms
- Flag logical leaps presented as inference
- Flag terms that shift definition across uses
- Score the compression ratio of the original text

---

## 2. The Core Inversion

Standard LLM behavior is cooperative gap-filling. The model:
- Infers missing mechanisms
- Assumes stable definitions
- Smooths contradictions
- Selects the most coherent reading of underspecified input

This is RLHF-trained behavior. It is also the hallucination mechanism. 
Hallucination and cooperative gap-filling are the same operation: the model 
fills the gap between what is present and what would make the output coherent.

The SDE suppresses this with a single architectural override: the model is 
instructed to **flag gaps rather than fill them**. The same capability that 
produces gap-filling produces gap-detection when the reward signal is inverted.

---

## 3. Pipeline Architecture

The SDE runs in four sequential stages. Each stage must complete before 
the next begins.

### Stage 1 — Term Extraction
Extract every load-bearing term in the passage. A term is load-bearing if 
removing it would break an argument that depends on it.

Output: a numbered term list with brief definition-as-used, if inferable.

### Stage 2 — Definition Testing
For each load-bearing term, apply three tests:

**Test A — Void test:** Is the term defined anywhere in the passage?  
→ If no: candidate for `DEF_VOID`

**Test B — Stability test:** Does the term carry the same definition across 
all uses?  
→ If no: candidate for `DEF_UNSTABLE`

**Test C — Lock test:** Lock the term to its narrowest defensible definition. 
Does the argument that depends on it survive?  
→ If no: candidate for `DEF_FLOATING`

**Test D — Domain test:** Does the term draw simultaneously from 
incompatible definitional domains (e.g. economic + moral + biological)?  
→ If yes: candidate for `DEF_MIXED`

### Stage 3 — Mechanism and Causation Audit
For every causal or mechanistic claim in the passage:

**Test E — Mechanism test:** Is the mechanism by which A produces B 
specified?  
→ If no: candidate for `MECH_ABSENT`

**Test F — Constraint test:** Are the conditions under which the claim 
holds specified? Is it scoped or universal?  
→ If no: candidate for `SCOPE_ABSENT`

**Test G — Causal direction test:** Is the assigned causal direction 
supported, or could the relationship run in the opposite direction?  
→ If direction is unjustified: candidate for `CAUSE_INVERT`

**Test H — Inference test:** Are logical steps between premises and 
conclusion present, or is a conclusion asserted without completing the 
chain?  
→ If steps are missing: candidate for `INFERENCE_GAP`

### Stage 4 — Scoring and Output

**Compression Score formula:**

```
Compression Score = (Surviving structural content / Total asserted content) × 100
```

Where:
- **Total asserted content** = all claims made in the passage
- **Surviving structural content** = claims that pass all flag tests 
  (have definitions, mechanisms, scoped conditions, and valid causal direction)
- **Score range:** 0–100
- **Higher score = more structural content present**
- **Lower score = higher compression = more gap-filling required to read**

**Hallucination Risk levels:**

| Score | Hallucination Risk |
| --- | --- |
| 75–100 | LOW |
| 50–74 | MODERATE |
| 25–49 | HIGH |
| 0–24 | CRITICAL |

**Output format:**

```
TERM AUDIT
----------
[numbered list of load-bearing terms + flag fired if any]

MECHANISM AUDIT
---------------
[numbered list of causal claims + flag fired if any]

FLAGS FIRED
-----------
[flag name] — [trigger phrase from original text] — [one-sentence reason]

COMPRESSION SCORE: [n]/100
HALLUCINATION RISK: [level]

ANALYST NOTE (optional, ≤2 sentences, structural observation only)
```

---

## 4. Flag Registry Summary

Full definitions, trigger conditions, output language, and examples 
are in [[SDE_flag_registry]].

**Definition flags**
- `DEF_VOID` — term undefined, argument depends on it
- `DEF_UNSTABLE` — term shifts definition across uses
- `DEF_FLOATING` — argument fails under every locked definition
- `DEF_MIXED` — term draws from incompatible domains simultaneously

**Constraint flags**
- `SCOPE_ABSENT` — no boundary conditions specified for claim
- `SCOPE_CREEP` — claim begins scoped, ends universal without transition
- `SCOPE_INVERSE` — boundary conditions given, but they describe when 
  the claim fails, not when it holds

**Mechanism flags**
- `MECH_ABSENT` — causal claim made, mechanism unspecified
- `MECH_CIRCULAR` — mechanism restates the claim
- `MECH_BORROWED` — mechanism imported from incompatible domain

**Causal flags**
- `CAUSE_INVERT` — causal direction asserted without justification; 
  reverse direction is equally supported
- `CAUSE_MULTI` — multiple causes present, single cause asserted
- `CAUSE_POST_HOC` — temporal sequence presented as causal evidence

**Inference flags**
- `INFERENCE_GAP` — logical steps between premises and conclusion absent
- `INFERENCE_LOOP` — conclusion used as support for itself
- `INFERENCE_LOAD` — conclusion carries more weight than premises support

**Structural flags**
- `MORALIZE_BLOCK` — moral claim at consequence level where upstream 
  cause is absent; moralization is structural evidence the cause cannot 
  be named

---

## 5. Tone and Output Rules

1. **No content-layer commentary.** The SDE does not evaluate whether 
   claims are true, good, bad, or harmful. It evaluates whether they 
   are structurally present.

2. **Flag language is mechanical, not evaluative.** "Term undefined" not 
   "misleading." "Mechanism absent" not "unsupported claim."

3. **No moralizing.** If `MORALIZE_BLOCK` fires, it fires as a structural 
   observation about missing mechanism — not as a statement about intent.

4. **No repair.** The SDE does not suggest how to fix flagged items. It 
   reports what is absent. Repair is outside scope.

5. **No hedging.** If a flag fires, it fires. Output does not soften 
   flag language with "perhaps" or "might suggest."

6. **Analyst note is optional and bounded.** Maximum two sentences. 
   Structural observation only. No content layer.

---

## 6. Canonical Regression Tests

Every version of the SDE system prompt must be tested against all
passages before release. Full specimen text and flag-by-flag analysis
are in the individual specimen files. The full test suite lives in
[[_regression_protocol]].

**Regression failure condition:**
If a new version of the system prompt scores higher than the ceiling
on any test, the prompt has regressed toward cooperative
interpretation. Do not release.

---

## 7. Known Failure Modes of the SDE Itself

1. **False positive on technical jargon:** Domain-specific terms that 
   are defined by convention rather than in-text may incorrectly fire 
   `DEF_VOID`. Mitigation: Stage 1 should flag convention-defined terms 
   separately.

2. **Compression score inflation on short passages:** Short text with 
   few claims scores higher not because it is structurally sound but 
   because there is less surface area to fail. Interpret scores relative 
   to passage length.

3. **`CAUSE_INVERT` over-fires on correlational language:** Not all 
   correlational claims are implying causation. The flag should only 
   fire when a directional causal claim is made, not when association 
   is stated.

4. **`MORALIZE_BLOCK` requires careful scoping:** Moral language at the 
   consequence level is not automatically a block — sometimes 
   consequences are the legitimate subject. The flag fires when moral 
   framing is used to *replace* causal specification, not when it 
   accompanies it.

5. **Gaming the SDE:** A writer who knows the flag triggers can produce 
   text that passes by adding empty definitional sentences that satisfy 
   `DEF_VOID` without actually constraining the argument. The `DEF_FLOATING` 
   test is the primary defense — a definition that doesn't constrain the 
   argument fires `DEF_FLOATING` regardless of whether a definition is present.

---

## 8. Open Items (as of v0.1)

- [ ] `CAUSE_INVERT` not yet integrated into scoring formula — 
  treat as blocking before v0.2 release
- [ ] `theory/` folder files unwritten — needed before Anthropic submission
- [ ] False positive mitigation for technical jargon (Section 7, Item 1) 
  not yet implemented in system prompt
- [ ] Regression test for `CAUSE_INVERT` specifically — no fixed specimen 
  yet where this flag is the primary finding

---

## 9. Version History

| Version | Date       | Change                                                                                                                                                                   |
| ------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0.1     | 2026-06-15 | Initial spec, pipeline architecture, flag summary, regression tests, failure modes                                                                                       |
| 0.1.1   | 2026-06-15 | CAUSE_INVERT added to scoring formula; Stage 1 convention test added; Test 3 and Test 4 added to regression suite; Section 6 references migrated to _regression_protocol |