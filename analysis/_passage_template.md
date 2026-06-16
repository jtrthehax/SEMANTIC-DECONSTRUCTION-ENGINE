---
specimen_id: P00X
label: 
genre: 
primary_flag: 
score_ceiling: 
status: Draft
prompt_version: 
date_analyzed: 
---
# SDE Passage Analysis — [TITLE]
**Specimen ID:** P00X  
**Source:** [Publication, Article Title]  
**URL:** [url]  
**Date analyzed:** YYYY-MM-DD  
**Genre:** [Opinion / News / Political / Academic / Other]  
**Primary flag expected:** [DEF_VOID / DEF_FLOATING / CAUSE_INVERT / etc.]  
**Status:** [Draft / Complete / Canonical regression specimen]  
**Depends on:** [[SDE_flag_registry]], [[SDE_system_prompt]]

---

## Passage Text

> [paste full passage here]

---

## Load-Bearing Claims

1. 
2. 
3. 

---

## Flags

**[FLAG_NAME]** | "[trigger phrase]" | [CRITICAL / HIGH / MODERATE]  
[one paragraph explanation]

---

## Constraint Summary

| Claim | Includes | Excludes | Falsification |
| --- | --- | --- | --- |
| | | | |

---

## Contradiction Pairs

**Pair 1:**
- CLAIM A:
- CLAIM B:

---

## Unfalsifiable Claims

-

---

**COMPRESSION SCORE: [n] / 100**

**HALLUCINATION RISK: [CRITICAL / HIGH / MODERATE / LOW]**  
[LLM gap-filling prediction — what will it hallucinate?]

---

## What This Specimen Demonstrates

[One paragraph on what this specimen specifically tests or validates 
that other specimens don't. Genre difference, primary flag type, 
structural pattern, etc.]

---

## Regression Test Entry

*Copy this block into [[_regression_protocol]] when specimen is complete.*

**Test [N] — [short label]:**  
Feed [Specimen ID] to SDE system prompt.  
Expected: Compression Score ≤ [n]/100, Hallucination Risk: [level].  
Primary flag: `[FLAG]` must fire first.  
Must-fire flags: `[FLAG1]`, `[FLAG2]`, `[FLAG3]`.  
Pass condition: score ≤ [n] AND primary flag fires first AND all 
must-fire flags present.  
Purpose: [one sentence on what this test validates].