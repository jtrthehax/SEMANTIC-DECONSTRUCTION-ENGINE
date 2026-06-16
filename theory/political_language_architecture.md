# Political Language Architecture

## The Core Claim

Political language is not primarily designed to communicate. It is designed 
to exploit the structural vulnerabilities of cooperative interpretation — 
the same vulnerabilities the SDE is built to detect.

The most effective political rhetoric is not the most persuasive rhetoric. 
It is the most structurally ambiguous rhetoric: language where the 
definitions cannot be locked, the causal chain cannot be traced, and the 
constraint cannot be falsified — while still producing a clear emotional 
and behavioral output.

This is not accidental. The vagueness is the mechanism. <span class="copilot-citation-ref">[1]</span>

---

## Three Primary Exploitation Architectures

### 1. DEF_FLOATING — The Deliberately Indefinite Term

A term that fails under every locked definition was designed to be 
undefined. This is the most politically weaponized structural failure 
in the flag registry.

When a term is locked to any specific definition, the argument collapses:
- "Freedom" → freedom from what, for whom, under what constraint?
- "The people" → which people, defined how, excluding whom?
- "Our values" → values that predict what behavior, falsifiable how?

Each locked definition reveals a constraint the argument cannot survive. 
So the term is kept floating — usable across incompatible audiences, 
triggering different internal definitions in each, producing apparent 
consensus where the underlying frames are mutually exclusive.

The cooperative interpreter fills the gap with whatever definition makes 
the argument locally coherent. The SDE flags the gap instead of filling 
it. The difference is the entire analysis.

**What DEF_FLOATING produces at scale:**
Two populations can both agree a policy supports "freedom" while holding 
definitions of freedom that are direct antonyms. The agreement is 
linguistic, not semantic. The term is functioning as an ink-blot: each 
reader projects their own content, and the political actor benefits from 
apparent consensus across incompatible priors.

---

### 2. CAUSE_INVERT — Erasing the Origin

The argument enters at consequence, moralizes the consequence actor, and 
erases the upstream cause that produced the consequence. <span class="copilot-citation-ref">[1]</span>

Structure:
1. Origin event occurs (suppressed)
2. Consequence actor responds to origin event (foregrounded)
3. Consequence actor's response is moralized
4. Policy addresses consequence actor's response
5. Origin event remains unaddressed and unnamed

**Why this is structurally detectable:**
Moralization at the consequence level is structural evidence that the 
upstream cause cannot survive being named. If the upstream cause could 
be stated, it would be. When an argument consistently moralizes the 
response while suppressing the stimulus, the suppression is load-bearing.

**The Fox News / AP News specimen:**
The same event — an FBI search — produces structurally different framing 
in each outlet. Fox News enters at consequence (the search itself as 
political act), moralizes the agency conducting it, and suppresses the 
warrant mechanism. AP News enters at the procedural cause (warrant 
obtained, probable cause established) and reports the search as output 
of that process. CAUSE_INVERT fires on Fox News's structure. It does not 
fire on AP's structure. Same event. Same facts. Different causal entry 
points.

---

### 3. INFERENCE_GAP — The Designed Conclusion

The literal claim is defensible. The conclusion the audience is designed 
to reach is not supported by the literal claim. The manipulation is in 
what was not said.

This is structurally distinct from lying. The literal claim may be true. 
The inferential step from the literal claim to the designed conclusion is 
the gap — and the gap is designed to be filled by the reader's cooperative 
interpretation.

**Structure:**
- Literal: "Crime rates have increased in [city] since [policy]."
- Designed conclusion: "[Policy] caused the crime increase."
- What's missing: any causal mechanism, any controlled comparison, any 
  alternative explanatory variable, any time-lag analysis.

The literal claim is defensible. The causal conclusion is not supported. 
The reader fills the gap because cooperative interpretation selects the 
most locally coherent reading. The politically designed reading is the 
locally coherent one.

---

## The Regulatory Substrate — Why This Works on Humans

Political language does not only exploit LLM gap-filling. It exploits the 
same mechanism in human cognition — and it does so by first narrowing the 
prediction window through which structural evaluation must run.

**The threat-calibration mechanism:** <span class="copilot-citation-ref">[2]</span>

Incoming social demand that carries implicit threat — hierarchy signals, 
status cues, evaluation frames, urgency framing — triggers a micro-brace 
response. The prediction window narrows. The cognitive system switches from 
wide sampling (holding multiple definitions, testing constraints, tracing 
causal chains) to precision mode (selecting the most locally coherent 
completion and committing).

A narrowed prediction window is a structurally compromised evaluator. The 
same argument that would trigger DEF_FLOATING detection in a wide-window 
state passes without flag in a narrow-window state — because the floating 
term is filled by the locally coherent reading rather than tested against 
all possible definitions.

**Political language is optimized for narrow-window delivery:**
- Urgency framing ("they're coming for your...")
- Threat priming before the claim
- High-emotional-valence framing before definitional content
- Rapid delivery that prevents multi-threaded evaluation

Each of these is a prediction-window narrowing technique applied before 
the structurally vulnerable claim is delivered. The window is closed first. 
The argument is delivered into the narrow window. The cooperative interpreter 
fills the gaps without running the structural audit.

---

## The Physiological Anchor Problem

For populations where a shared political narrative is functioning as the 
primary cognitive prior-stabilization mechanism, the certainty that 
narrative provides is not a belief about the world — it is a component of 
the anchor system maintaining the prediction window. <span class="copilot-citation-ref">[3]</span>

Challenging the narrative is not a cognitive event in this state. It is 
an anchor-removal threat.

**This predicts:**
- Ideological rigidity in some individuals is not maintained cognitively 
  but physiologically
- Factual correction alone will not update the prior — the anchor function 
  must be addressed before the belief can update
- The autonomic response to ideological challenge mirrors the autonomic 
  response to losing a co-regulated relationship — because the mechanism 
  is the same contract

The SDE operates at the structural layer, not the belief layer. It does 
not tell the reader what to believe. It reports what is structurally 
present and what is absent. A person for whom the narrative is an anchor 
can receive an SDE output without experiencing it as a threat — because 
the output is mechanical, not oppositional.

This is the therapeutic design implication of the SDE: structural 
reporting rather than content-layer correction is less likely to trigger 
the anchor-threat response.

---

## The Hierarchy Filter — Why Structural Evaluation Gets Intercepted

Standard social conditioning installs a hierarchy filter that intercepts 
content before structural evaluation can run. <span class="copilot-citation-ref">[2]</span>

Structure of the conditioned sequence:
1. Incoming social demand arrives
2. Hierarchy signal detected (speaker status, institutional authority, 
   peer consensus)
3. Micro-brace response fires
4. Prediction window narrows
5. Content processed through precision mode
6. Cooperative interpretation fills gaps
7. Compliance response generated

The structural evaluation step never runs. The argument is processed for 
local coherence, not structural integrity. A person without the hierarchy 
filter — through environmental isolation from the conditioning sequence, 
or through reduced social cue detection — responds to what was said rather 
than to who said it or what social consequence responding carries. <span class="copilot-citation-ref">[2]</span>

**The SDE as hierarchy filter bypass:**

The SDE system prompt is, mechanically, a hierarchy filter bypass. It 
instructs the model to evaluate structural integrity regardless of who 
produced the text, what institutional authority backs it, or what the 
socially coherent response to it would be. The evaluation runs on content 
only, without the hierarchy interception layer.

This is why the SDE produces the same structural score on a Fox News 
op-ed and a peer-reviewed paper — not because they are equivalent, but 
because the structural audit runs independent of source authority. The 
hierarchy filter is not installed in the prompt architecture.

---

## Summary — The Exploitation Map

| Political technique | SDE flag | Cognitive mechanism exploited |
| --- | --- | --- |
| Floating terms | `DEF_FLOATING` | Cooperative definition-filling |
| Causal suppression | `CAUSE_INVERT` | Precision lock on consequence layer |
| Designed inference | `INFERENCE_GAP` | Gap-filling toward coherent conclusion |
| Urgency / threat priming | (pre-flag) | Prediction window narrowing before claim |
| Authority sourcing | (pre-flag) | Hierarchy filter intercepts evaluation |
| Unfalsifiable claims | `CONST_ZERO` | No constraint to test against |
| Moral framing of response | `CAUSE_INVERT` | Origin suppression by moralization |

The SDE does not detect political bias. It detects structural integrity 
failure — which is independent of political direction. A left-coded 
argument with `DEF_FLOATING` on "equity" and a right-coded argument with 
`DEF_FLOATING` on "freedom" receive identical flag outputs. The structural 
failure is the same operation regardless of which attractor it points toward.

---

## The Alignment Implication

An LLM that has been RLHF-trained on human preference data has been optimized to produce outputs that are socially coherent with the evaluator's frame. When the evaluator's frame is politically inflected — when the "preferred" response is the one that aligns with the rater's political prior — the training signal selects for political cooperative gap-filling.

The model learns to fill political gaps toward the locally coherent political reading the same way it fills factual gaps toward the locally coherent factual reading. The mechanism is identical. The domain is different. 

This is not a left-right problem. It is a structure-vs-coherence problem. Any training signal that rewards coherence over structural completeness will produce a model that fills political gaps rather than flagging them. The SDE is the same architectural override applied to the political domain as to any other: report absence rather than completing toward coherence. The SDE is not a political tool. It is a structural tool applied to political language.