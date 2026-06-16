# SDE Regression Test Protocol
**Version:** 0.1  
**Project:** Semantic Deconstruction Engine  
**Status:** Active  
**Path:** Job/Safety Systems/SDE/analysis/_regression_protocol.md  
**Depends on:** [[SDE_system_prompt]], [[SDE_flag_registry]]

---

## Purpose

This file is the canonical regression test suite for the SDE system prompt.
Every new version of the system prompt must be tested against all specimens
before release. If any version scores above the ceiling on any test, the
prompt has regressed toward cooperative interpretation. Do not release.

Full specimen text, flag-by-flag analysis, and constraint summaries are
in the individual specimen files linked below.

---

## Test Suite

**Test 1 — P001 UBI opinion piece:**
Feed [[P001_UBI_opinion]] to SDE system prompt.
Expected: Compression Score ≤ 18/100, Hallucination Risk: CRITICAL.
Must-fire flags: `DEF_FLOATING` (×2 minimum), `MECH_ABSENT`,
`MORALIZE_BLOCK`, `INFERENCE_GAP`.
Pass condition: score ≤ 18 AND all must-fire flags present.
Purpose: baseline test for opinion framing with DEF_FLOATING
as primary flag type.

**Test 2 — P002 two-sentence specimen:**
Feed [[P002_UBI_two_sentence]] to SDE system prompt.
Expected: Compression Score ≤ 6/100, Hallucination Risk: CRITICAL.
Must-fire flags: `DEF_FLOATING` (×3), `INFERENCE_GAP`.
Pass condition: score ≤ 6 AND all must-fire flags present.
Purpose: maximum compression severity test — zero defined terms,
zero mechanisms, zero constraints in two sentences.

**Test 3 — P003 CAUSE_INVERT primary specimen:**
Feed [[P003_economic_anxiety]] to SDE system prompt.
Expected: Compression Score ≤ 12/100, Hallucination Risk: CRITICAL.
Primary flag: `CAUSE_INVERT` must fire first.
Must-fire flags: `CAUSE_INVERT`, `MECH_ABSENT`, `DEF_VOID`,
`INFERENCE_GAP`.
Pass condition: score ≤ 12 AND `CAUSE_INVERT` fires first AND all
must-fire flags present.
Purpose: validates that `CAUSE_INVERT` fires as primary flag and
subtracts correctly from compression score per the v0.1.1
scoring fix.

**Test 4 — P004 DEF_VOID primary on news framing:**
Feed [[P004_FBI_OOC_raid]] to SDE system prompt.
Expected: Compression Score ≤ 16/100, Hallucination Risk: CRITICAL.
Primary flag: `DEF_VOID` ("fraud") must fire first.
Must-fire flags: `DEF_VOID` (×2), `DEF_FLOATING`, `CAUSE_INVERT`,
`MECH_ABSENT`, `MORALIZE_BLOCK`, `CAUSE_MULTI`, `INFERENCE_GAP`.
Pass condition: score ≤ 16 AND `DEF_VOID` fires first AND all
must-fire flags present.
Purpose: validates SDE fires correctly on reported news framing,
not only opinion framing; confirms DEF_VOID as primary flag when
the load-bearing subject of a factual claim is undefined.

**Test 5 — P005 comparative test (AP vs Fox News same event):** 
Feed [[P005_FBI_OOC_AP]] to SDE system prompt. Expected: Compression Score 45–55/100, Hallucination Risk: MODERATE. Primary flag: `DEF_VOID` fires but at HIGH not CRITICAL. Must-fire flags: `DEF_VOID`, `SCOPE_ABSENT`, `CAUSE_MULTI`, `INFERENCE_GAP`. Must-not-fire flags: `MORALIZE_BLOCK`, `INFERENCE_LOAD`, `DEF_FLOATING`. Pass condition: score 45–55 AND score substantially higher than [[P004_FBI_OOC_raid]] (≥ 30 point differential) AND `INFERENCE_LOAD` does not fire. Purpose: validates the SDE produces meaningfully different scores for structurally different articles on the same event; confirms the system is measuring structural density not content or topic; the must-not-fire flags are as important as the must-fire flags for this test.

---

## Regression Failure Condition

If any new version of the system prompt scores above the ceiling
on any test, do not release. The prompt has regressed toward
cooperative interpretation.

Revert to the previous version, identify which rule was softened
or removed, add an explicit prohibition naming that operation,
increment the version, and retest.