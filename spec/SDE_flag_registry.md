# SDE Flag Registry
**Version:** 0.1  
**Project:** Semantic Deconstruction Engine  
**Status:** Active — append new flags as discovered

---

## How To Read This Registry

Each flag entry contains:
- **Type** — which pipeline step generates it
- **Trigger condition** — the precise structural condition that fires the flag
- **Output language** — what the SDE says when this flag fires (no charitable interpretation, no gap-filling)
- **Example** — from analyzed text
- **Severity** — contribution to Hallucination Risk score

Severity scale:
- `LOW` — reduces Compression Score, minor ambiguity
- `MEDIUM` — structural failure that distorts meaning
- `HIGH` — argument cannot survive this flag; conclusion depends on the failure
- `CRITICAL` — argument requires this failure to function; removing it collapses the claim

---

## DEFINITION FLAGS

---

### DEF_VOID
**Type:** Definition  
**Severity:** HIGH

**Trigger:**
A term carries argumentative weight — the conclusion depends on what 
it means — but no definition is stated anywhere in the text.

**Output language:**
> "Term [X] is undefined. The argument depends on what this term 
> means but no definition is provided. Supply a definition before 
> this claim can be evaluated."

**Example:**
"Contribute to society" in the UBI passage. The moral framing of 
UBI recipients as undeserving depends entirely on what "contribute" 
means. No definition is given.

**Notes:**
DEF_VOID fires when the term is simply absent of definition.
When the term is strategically undefined to preserve ambiguity,
escalate to DEF_FLOATING.

---

### DEF_UNSTABLE
**Type:** Definition  
**Severity:** MEDIUM–HIGH

**Trigger:**
A term is used more than once and does not carry the same definition 
across uses. The term shifts meaning between sentences without 
acknowledgment.

**Output language:**
> "Term [X] carries definition [D1] in [location 1] and requires 
> definition [D2] in [location 2]. These are not the same definition. 
> Which is operating?"

**Example:**
"Work" vs "jobs" in the UBI passage. Claim 6 treats them as distinct 
("jobs change" ≠ "work disappears"). Claims 7–10 use them 
interchangeably. The distinction is asserted then immediately abandoned.

---

### DEF_FLOATING
**Type:** Definition  
**Severity:** CRITICAL

**Trigger:**
A term has no stated definition AND when any single plausible 
definition is locked in, the argument fails or contradicts itself. 
The vagueness is not incidental — it is structurally necessary for 
the argument to function. Lock-testing confirms the term cannot be 
defined without collapsing the claim.

**Output language:**
> "Term [X] has no stated definition. Under every plausible 
> definition, the argument fails:
>
> Definition A: [result — contradiction / redundancy / self-defeat]  
> Definition B: [result]  
> Definition C: [result]
>
> This argument does not survive definition. The vagueness of 
> this term is load-bearing — the claim requires that no single 
> meaning be fixed."

**Example:**
"Contribute to society" in UBI passage:
- Lock in "paid employment" → redundant with "regardless of whether 
  they work"
- Lock in "caregiving" → implies caregivers aren't contributing, 
  contradicts the article's own value framing
- Lock in "economic consumption" → UBI recipients contribute the 
  moment they spend the payment; premise self-destructs

**Notes:**
DEF_FLOATING is the most politically weaponized flag in the registry.
A term that cannot be defined without destroying the argument was 
designed to be undefined. This is not poor writing — it is a 
structural feature. The SDE treats it as such.

---

### DEF_MIXED
**Type:** Definition  
**Severity:** MEDIUM

**Trigger:**
A term is being used with definitions drawn from two incompatible 
domains simultaneously. The argument requires both domain meanings 
to hold at once, which they cannot.

**Output language:**
> "Term [X] is being used with definitions from incompatible domains: 
> [Domain 1 definition] and [Domain 2 definition]. These cannot 
> simultaneously apply. Which domain is operating?"

---

## CONSTRAINT FLAGS

---

### CONST_ZERO
**Type:** Constraint  
**Severity:** HIGH

**Trigger:**
A claim excludes nothing. No time frame, population, or conditions 
are stated. The claim cannot be falsified as stated — no evidence 
could prove it wrong.

**Output language:**
> "This claim excludes nothing. Under what conditions would it be 
> false? What evidence would prove it wrong? As stated, this claim 
> cannot be falsified."

**Example:**
"Work has never disappeared" — no threshold for what "disappeared" 
means, no population scope, no time frame. The claim absorbs any 
counter-evidence by adjusting scope.

---

### CONST_TIME_MISSING
**Type:** Constraint  
**Severity:** MEDIUM–HIGH

**Trigger:**
A causal or comparative claim is made without specifying a time 
frame. The claim may be true over a long window and false over a 
short one — or vice versa. The missing time frame allows the claim 
to absorb contradicting evidence by shifting the window.

**Output language:**
> "No time frame is stated. This claim may be true over [long window] 
> and false over [short window]. Specify the time frame or the claim 
> cannot be evaluated."

**Example:**
"When automobiles replaced horse-drawn transport, millions of jobs 
vanished. Millions more were created." True over 30 years. False for 
the workers who lost jobs in 1910 and died before automotive 
manufacturing existed at scale.

---

### CONST_POP_MISSING
**Type:** Constraint  
**Severity:** MEDIUM–HIGH

**Trigger:**
A claim applies to a population but does not specify which 
population, or aggregates across populations that cannot be 
legitimately combined.

**Output language:**
> "This claim applies to [group] but does not specify which 
> population. The claim may be true for [subset A] and false for 
> [subset B]. Specify the population."

**Example:**
"Millions more [jobs] were created" — created for whom? Workers 
displaced from horse-drawn transport required different skills, 
geography, and capital than automotive manufacturing demanded. 
Aggregating across populations obscures who actually benefited.

---

### CONST_DECAY
**Type:** Constraint  
**Severity:** HIGH

**Trigger:**
A claim begins with explicit constraints that are silently dropped 
by the end of the argument. The conclusion is stated as universal 
when it was only established for the constrained case.

**Output language:**
> "Claim [X] was established with constraints: [list]. By [location], 
> those constraints are no longer present but the conclusion is 
> stated as if they still applied. The conclusion applies only to 
> the constrained case."

---

### CONST_INVERT
**Type:** Constraint  
**Severity:** CRITICAL

**Trigger:**
A constraint is reversed mid-argument to preserve a narrative that 
would otherwise fail. The constraint that supported the first claim 
is explicitly contradicted by the constraint required for the 
second claim — and both are asserted.

**Output language:**
> "Claim [A] requires condition [X]. Claim [B] requires condition 
> [not-X]. The constraint has been inverted between claims. Both 
> cannot hold."

---

## MECHANISM FLAGS

---

### MECH_VOID
**Type:** Mechanism  
**Severity:** HIGH

**Trigger:**
A causal operator is present (causes, leads to, results in, because, 
therefore, proves, shows, means, demonstrates, drives, creates) but 
no mechanism connects A to B. The causal claim is asserted without 
any step between the cause and the effect.

**Output language:**
> "Causal operator [X] detected. No mechanism connects [A] to [B]. 
> What is the step between them? Under what conditions? Through 
> what pathway?"

**Example:**
"Technology destroys some jobs. It creates entirely new 
opportunities." Causal operator: "creates." No mechanism stated 
for how technology creates opportunities, who captures them, or 
under what conditions this occurs.

---

### MECH_GAP
**Type:** Mechanism  
**Severity:** MEDIUM–HIGH

**Trigger:**
A mechanism is partially stated but steps are missing between A 
and B. The chain exists but has gaps that the argument skips over.

**Output language:**
> "Mechanism from [A] to [B] is partially stated. Missing steps: 
> [location of gap]. The chain cannot be completed as presented."

---

### MECH_HANDWAVE
**Type:** Mechanism  
**Severity:** HIGH

**Trigger:**
A metaphor is doing the work of a mechanism. The causal operator 
is present, but the explanation of how A produces B is a figurative 
description rather than a causal chain.

**Output language:**
> "The explanation of how [A] produces [B] is figurative, not 
> mechanistic. '[metaphor]' describes the relationship but does 
> not explain it. What is the actual causal step?"

---

## CAUSAL FLAGS

---

### CAUSE_BREAK
**Type:** Causal Chain  
**Severity:** HIGH

**Trigger:**
A causal chain cannot be built from the text. The claim implies 
A → B → C but the connections between steps are not present.

**Output language:**
> "A causal chain from [A] to [C] cannot be constructed from this 
> text. The connection between [B] and [C] is not established."

---

### CAUSE_TELEPORT
**Type:** Causal Chain  
**Severity:** HIGH

**Trigger:**
The argument jumps from a premise (A) directly to a conclusion (Z) 
without intermediate steps. The distance between the claim and the 
conclusion is bridged by implication, not argument.

**Output language:**
> "The argument moves from [A] to [Z] without intermediate steps. 
> What are the steps between them? Each step requires its own 
> mechanism."

**Example:**
"Previous technologies created new jobs → therefore AI will too." 
The unstated assumption — that AI job-creation follows the same 
pattern as physical technology replacement — is the entire empirical 
question being argued. It is treated as already settled.

---

### CAUSE_LOOP
**Type:** Causal Chain  
**Severity:** HIGH

**Trigger:**
Circular causality: A causes B, B causes A, with no external 
grounding for either.

**Output language:**
> "Circular causality detected: [A] is used to explain [B] and 
> [B] is used to explain [A]. Neither is independently grounded."

---

## CAUSAL INVERSION FLAGS

---

### CAUSE_INVERT
**Type:** Causal Chain  
**Severity:** CRITICAL

**Trigger:**
The argument enters the causal chain at a downstream consequence
and treats it as the origin point. The actual upstream cause —
an actor, institution, system, or decision that produced the
conditions being discussed — is absent from the frame entirely.
By entering at the consequence, the argument transfers moral
or practical responsibility from the upstream cause to the
downstream consequence actor.

The upstream cause is not merely omitted — its omission is
structurally necessary. If the upstream cause were named,
the responsibility attribution in the argument would collapse.

**Test:**
Ask: what had to happen before this sentence was possible?
If the answer implicates an actor not mentioned in the argument,
the causal chain has been inverted.
Ask: who benefits from the upstream cause remaining unnamed?
If the answer is the entity making the argument, CAUSE_INVERT
is confirmed at CRITICAL severity.

**Output language:**
> "This argument begins at consequence: [X].
> The upstream cause — [Y] — is absent from the frame.
> The responsibility attributed to [consequence actor] belongs
> structurally to [cause actor] under the complete causal chain.
>
> Complete chain:
> [Upstream cause] → [intermediate conditions] → [consequence]
>
> The argument enters here: [consequence]
> and treats it as the origin."

**Canonical example — political rhetoric:**
UBI passage: workers need economic support.
The upstream cause — institutional automation decisions made
for profit extraction — is absent from the frame.
The argument enters at "workers need support" and moralizes
about dependency, capability, and adaptation.
The entity whose decisions produced the conditions requiring
support is not named and does not appear in the argument.

**Canonical example — systemic:**
"Capitalism sells you a solution to a problem it created."
The system generates the condition (manufactured insecurity,
planned obsolescence, addictive product design).
The system then enters the frame as solution provider.
The origin — the system's role in producing the condition —
is absent. The consumer appears as the agent with the problem
to solve. The system appears as the agent with the solution.
The causal inversion is complete.

**Relationship to other flags:**
CAUSE_INVERT almost always co-occurs with:
- INFERENCE_GAP — the narrative inference (consequence actor
  is responsible) is not supported by the complete causal chain
- LOOP_MAGIC — the framing presupposes the conclusion
  (consequence actor has a problem) before the argument begins
- CONST_ZERO on upstream cause — no falsification condition
  is offered for the claim that the upstream cause is irrelevant
  or absent

**Why moralization is the tell:**
When an argument moralizes at the consequence level —
dependency, incapability, failure to adapt, personal
responsibility — it is structural evidence that the upstream
cause cannot survive being named. If the upstream cause were
morally neutral or positive, there would be no need to
moralize at the consequence level. The intensity of moral
loading at the consequence is proportional to the weight
of what is being kept out of frame upstream.

**Severity note:**
CAUSE_INVERT is CRITICAL because it does not merely omit
information — it actively transfers responsibility from
one actor to another through structural framing.
Every flag in the registry reports absence.
CAUSE_INVERT reports active displacement.

---

## INFERENCE FLAGS

---

### INFERENCE_GAP
**Type:** Inference  
**Severity:** CRITICAL

**Trigger:**
A claim is technically defensible as stated, but the conclusion 
audiences are meant to draw from it is not supported by the claim. 
The gap is produced by omitting constraints that would have blocked 
the inference. The speaker can retreat to the literal claim if 
challenged ("I never said that") while the intended conclusion 
does the argumentative work.

This is the most politically weaponized flag in the registry.

**Output language:**
> "LITERAL CLAIM: [what is technically asserted — defensible]  
> NARRATIVE INFERENCE: [what audiences are meant to conclude]  
> OMITTED CONSTRAINTS: [what was not stated that would have 
> blocked the inference]  
> BRIDGE MECHANISM: [framing / selective emphasis / omission 
> that produces the gap]
>
> This claim is technically defensible. The conclusion it is 
> designed to produce is not supported by the claim as stated. 
> The inference requires [X], which is not asserted and may be 
> contradicted by available evidence."

**Example:**
The automobile example in the UBI passage is technically true 
(jobs were created). The narrative inference — AI will follow 
the same pattern — is the INFERENCE_GAP. The omitted constraint: 
automobile transition operated on physical labor with transferable 
geography and skill adjacency. AI operates on cognitive labor with 
no clear transfer pathway and no historical precedent for that 
substitution pattern. The caveat exists. It was omitted.

**Notes:**
INFERENCE_GAP requires the SDE to model what a cooperative reader 
would conclude — then audit that conclusion against the literal 
claim. This is the hardest flag to automate because it requires 
simulating the gap-fill that the text is engineered to produce.

---

## CONSISTENCY FLAGS

---

### CONTRADICTION
**Type:** Cross-claim Consistency  
**Severity:** CRITICAL

**Trigger:**
Two claims in the same argument require mutually exclusive 
conditions to be simultaneously true.

**Output language:**
> "CLAIM [A] requires condition [X] to be true.  
> CLAIM [B] requires condition [X] to be false.  
> Both claims cannot simultaneously hold.  
> Which condition is operating?"

**Example:**
UBI passage: "Supporters make the same mistake as during every 
prior technological shift" requires AI to be categorically similar 
to prior shifts. "AI will absolutely transform the economy" implies 
categorical difference sufficient to warrant concern. Both cannot 
simultaneously be the operative framing.

---

## CIRCULARITY FLAGS

---

### LOOP_MAGIC
**Type:** Circularity  
**Severity:** HIGH

**Trigger:**
The conclusion is already embedded in the framing of the premise. 
The argument appears to prove its conclusion but the conclusion 
was assumed before the argument began.

**Output language:**
> "The conclusion [X] is embedded in the premise framing. The 
> label '[term]' presupposes the conclusion. The argument for 
> why [X] is true is built on a premise that already assumes 
> [X] is true."

**Example:**
"They make the same mistake people have made during every major 
technological advancement." The label "mistake" presupposes the 
conclusion (UBI supporters are wrong). The argument for why it's 
a mistake is then built on top of a premise that already assumes 
it is one.

---

### LOOP_SELF
**Type:** Circularity  
**Severity:** HIGH

**Trigger:**
A term is defined using itself, or evidence for a claim is derived 
from the claim itself.

**Output language:**
> "Term [X] is defined using itself / Evidence for [claim] is 
> derived from [claim]. No independent grounding exists."

**Example:**
"That's what innovation does." Innovation is defined as the thing 
that creates opportunities, then used as the explanation for why 
opportunities were created. The definition is the argument.

---

## DRIFT FLAGS

---

### DRIFT_LOCAL
**Type:** Semantic Drift  
**Severity:** MEDIUM

**Trigger:**
Within a single sentence or immediate clause, a term shifts meaning 
or a metaphor transitions into being treated as a mechanism.

**Output language:**
> "Within [location], term [X] shifts from [meaning 1] to 
> [meaning 2]. Which is operating?"

---

### DRIFT_GLOBAL
**Type:** Semantic Drift  
**Severity:** HIGH

**Trigger:**
A term that was anchored at first use (explicitly or implicitly 
defined) carries a different definition in a later use. The 
argument's coherence depends on the reader not noticing the shift.

**Output language:**
> "Term [X] was anchored at [location 1] with definition [D1]. 
> At [location 2], the term requires definition [D2]. 
> The definitions are not the same. The argument's coherence 
> depends on treating them as equivalent."

---

## SCORING

---

### Compression Score (0–100)

Calculated from:
- Defined terms (each `DEF_*` flag reduces score)
- Stated mechanisms (each `MECH_*` flag reduces score)
- Explicit constraints (each `CONST_*` flag reduces score)
- Valid causal links (each `CAUSE_*` flag reduces score)
- Cross-claim consistency (each `CONTRADICTION` reduces score heavily)
- Stable invariants (each `DRIFT_*` flag reduces score)

**Interpretation:**
- 80–100: Structurally dense. Claims are defined, constrained, 
  and mechanistically connected.
- 50–79: Mixed. Some structure present but load-bearing gaps exist.
- 20–49: Mostly narrative. Surface coherence masks structural 
  absence.
- 0–19: Pure narrative. No load-bearing structure survives 
  adversarial inspection.

---

### Hallucination Risk (LOW / MEDIUM / HIGH / CRITICAL)

**LOW:** 0–2 flags, all MEDIUM or below severity  
**MEDIUM:** 3–5 flags, or any single HIGH  
**HIGH:** Multiple HIGH flags, or any CRITICAL  
**CRITICAL:** Multiple CRITICAL flags, or CONTRADICTION + INFERENCE_GAP 
              active simultaneously

**CRITICAL output language:**
> "An LLM asked to reason further from this text will almost 
> certainly fabricate mechanisms, resolve contradictions that 
> are not present in the source, and supply definitions for 
> terms that the argument requires to remain undefined. 
> Do not use this text as a reasoning substrate without 
> prior SDE processing."

---

## Registry Notes

**Flags may stack.** A single term can generate DEF_VOID + 
DEF_FLOATING simultaneously. A single causal claim can generate 
MECH_VOID + CAUSE_TELEPORT simultaneously. Stack all that apply — 
do not select one and ignore others.

**Flags are structural, not rhetorical.** The SDE does not assess 
whether the speaker is lying, mistaken, or acting in bad faith. 
It reports what is structurally present and what is absent. 
The absence of a mechanism is a finding regardless of why 
the mechanism is absent.

**INFERENCE_GAP is the hardest flag and the most important one 
for political text.** Every other flag catches errors in what 
was said. INFERENCE_GAP catches manipulation in what was not said.
