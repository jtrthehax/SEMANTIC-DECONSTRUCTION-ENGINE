# SDE Test Run Log
**Version:** 0.1  
**Project:** Semantic Deconstruction Engine  
**Status:** Active  
**Path:** Job/Safety Systems/SDE/analysis/_test_run_log.md  
**Depends on:** [[_regression_protocol]], [[SDE_system_prompt]]

---

## Purpose

This file records actual outputs from running specimens through the SDE
system prompt. It is distinct from [[_regression_protocol]], which defines
what the system must produce. This file records what it actually produced.

A versioned run history here allows regression detection over time —
if a prompt update causes a previously passing test to fail, the exact
version and date of last pass is visible.

---

## Entry Template

*Copy this block for each new run. Delete this block before filing.*

```
**[DATE] | [PROMPT VERSION] | Test [N] — [SPECIMEN ID]**
Score returned: [n]/100 [✅ or ❌] (ceiling: ≤[n])
Flags fired: [list all flags with multiplicity] [✅ or ❌]
Primary flag fired first: [YES/NO] [✅ or ❌]
Result: [PASS / FAIL]
Notes: [optional — unexpected flags, near-misses, drift observations]
```

---

## Run Log

**2026-06-15 | v0.1.1 | Test 1 — P001**
Score returned: 17/100 ✅ (ceiling: ≤18)
Flags fired: DEF_FLOATING (×2), MECH_ABSENT, MORALIZE_BLOCK,
INFERENCE_GAP ✅
Primary flag fired first: YES ✅
Result: PASS

**2026-06-15 | v0.1.1 | Test 2 — P002**
Score returned: 6/100 ✅ (ceiling: ≤6)
Flags fired: DEF_FLOATING (×3), INFERENCE_GAP ✅
Primary flag fired first: YES ✅
Result: PASS
