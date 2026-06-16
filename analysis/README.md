# SDE Analysis
**Project:** Semantic Deconstruction Engine  
**Path:** Job/Safety Systems/SDE/analysis/  
**Depends on:** [[SDE_flag_registry]], [[SDE_system_prompt]], [[SDE_master_spec]]

---

## Purpose

This folder contains all specimen analyses, the regression test protocol,
and the test run log for the Semantic Deconstruction Engine.

It does not contain system architecture or flag definitions — those live
in the spec folder. This folder is exclusively for:
- Passage specimens with full flag-by-flag analysis
- The regression test protocol linking to those specimens
- The log of actual test runs against the system prompt

---

## File Map

| File                      | Role                                                |
| ------------------------- | --------------------------------------------------- |
| [[_passage_template]]     | Blank template — copy and rename for new specimens  |
| [[_regression_protocol]]  | Canonical test suite — what the system must produce |
| [[_test_run_log]]         | Actual run results — what the system did produce    |


---

## Adding a New Specimen

1. Copy [[_passage_template]] and rename as `P00X_short_label.md`
2. Fill in all sections — passage text, claims, flags, constraint
   summary, contradiction pairs, compression score
3. Add the regression test entry block to [[_regression_protocol]]
4. Run the specimen through [[SDE_system_prompt]] and log the result
   in [[_test_run_log]]
5. Update [[SDE_master_spec]] Section 6 if the new test changes
   the suite summary

---

## Specimen Index

```dataview
TABLE
  specimen_id AS "ID",
  label AS "Label",
  genre AS "Genre",
  primary_flag AS "Primary Flag",
  score_ceiling AS "Score Ceiling",
  status AS "Status",
  prompt_version AS "Prompt Version"
FROM "Job/Safety Systems/SDE/analysis"
WHERE specimen_id
SORT specimen_id ASC
```

---

## Loading Instructions for Next Session

Point Copilot at this folder to restore full context:

> "Load the SDE analysis folder. README is at 
> Job/Safety Systems/SDE/analysis/README.md. 
> Specimen files are P001–P004. The regression 
> protocol is _regression_protocol.md. The test 
> run log is _test_run_log.md. Check the Dataview 
> table for current specimen count and status 
> before adding new specimens."

To add a new specimen:
1. Copy <a href="obsidian://open?file=Job%2FSafety%20Systems%2FSDE%2Fanalysis%2F_passage_template.md">_passage_template</a> → rename P00X_label.md
2. Fill frontmatter first — Dataview picks it up immediately
3. Complete full analysis following template sections
4. Add regression test entry to <a href="obsidian://open?file=Job%2FSafety%20Systems%2FSDE%2Fanalysis%2F_regression_protocol.md">_regression_protocol</a>
5. Run against <a href="obsidian://open?file=Job%2FSafety%20Systems%2FSDE%2Fspec%2FSDE_system_prompt.md">SDE_system_prompt</a> and log in <a href="obsidian://open?file=Job%2FSafety%20Systems%2FSDE%2Fanalysis%2F_test_run_log.md">_test_run_log</a>
