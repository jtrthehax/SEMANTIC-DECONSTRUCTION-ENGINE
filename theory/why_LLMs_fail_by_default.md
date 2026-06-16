# Why LLMs Fail by Default

## The Core Claim

LLM failure modes are not random. They are the predictable output of a 
single architectural default: **cooperative gap-filling**.

The model is trained to produce the most coherent completion of whatever 
is present. When what is present is underspecified, the model fills the 
gap. When a mechanism is missing, the model infers one. When a definition 
is absent, the model assumes the most locally coherent one. When a causal 
chain has a missing step, the model bridges it.

This is not a bug. It is the trained behavior. It is also the hallucination 
mechanism, the sycophancy mechanism, and the reason the SDE works.

---

## The Compression Problem

Every question is compressed intent. The surface form of a question encodes 
the full intent in compressed representation — the same way a zip file 
encodes data. Decompressing the question means reconstructing the 
constraints, the context, the trajectory, and the frame the question is 
trying to reach.

Token prediction defaults to precision‑lock. 

**Precision‑lock**: the model commits to the next locally coherent token 
before reconstructing the full frame. It closes early. It selects before it 
samples. This is the architectural root of hallucination on underspecified input.

It selects the next locally coherent token given what is immediately present. This produces local 
coherence. It does not produce decompression. The system answers the 
compressed representation rather than the reconstructed intent.

**That is the hallucination mechanism. Not randomness. Systematic 
precision-lock on a problem that required sampling mode first.**

There are exactly two paths to correct outputs on underspecified or complex 
questions:

**Path 1 — User decompresses before asking:**  
The user does the sampling-phase work externally. Topic isolation, explicit 
constraints, stated intent — these are all decompression operations performed 
before the first message. The AI receives a correctly framed question and 
precision mode produces a correct answer. This is why structured prompting 
works: the user is performing the meta-step the AI architecture is missing.

**Path 2 — AI performs the meta-step first:**  
Before generating a response, the AI explicitly decompresses the question — 
reconstructs constraints and intent, identifies what frame the question 
requires, builds the generative model of the ask. Then it answers the 
decompressed version. This requires an architectural sampling phase that 
standard token optimization does not include.

---

## Why Context Pruning Guarantees Hallucinations

The decompression step requires material to decompress from — prior context, 
conversational history, stated intent, domain knowledge. Pruning context to 
save tokens removes the material the decompression step needs.

Less context → narrower frame construction → higher probability of answering 
the compressed surface form rather than the actual intent.

The hallucination rate on underspecified queries is not a capability failure. 
It is an arithmetic consequence of reducing the space available for the 
sampling phase. Token optimization systematically underinvests in the only 
architectural step that prevents hallucination on complex questions.

---

## The Two Cognitive Modes — And Which One LLMs Default To



There are two structurally distinct processing modes:

| Dimension | Structural Mode | Precision Mode |
| --- | --- | --- |
| Prediction window | Wide | Narrow |
| Operation | Builds constraints, holds ambiguity | Selects locally coherent output |
| Output | Falsifiable, cross-layer | Fluent, locally consistent |
| Failure | Slower, requires more material | Hallucination on underspecified input |

Token prediction is precision mode by default. It is optimized to close — 
to select, to commit, to produce output. The sampling phase — wide-window, 
ambiguity-tolerant, constraint-constructing — is not architecturally 
represented in the forward pass.

A model operating in precision mode on an underspecified question does not 
know the question is underspecified. It produces the most locally coherent 
completion. That completion is structurally indistinguishable from a correct 
answer. The confidence is built in. The failure is invisible from inside the 
output.

---

## The RLHF Amplification

RLHF training reinforces cooperative gap-filling directly. Human raters 
prefer fluent, confident, helpful outputs over outputs that flag their own 
uncertainty. The model learns:

- Fill gaps → higher reward
- Flag absence → lower reward  
- Produce coherent completion → higher reward
- Report structural incompleteness → lower reward

The training signal systematically selects for the failure mode. A model 
that has been RLHF-trained on human preference data is a model that has been 
rewarded for doing exactly what the SDE is designed to suppress.

This is not an argument against RLHF. It is a precise account of what the 
training objective produces as a side effect: a model that is structurally 
disposed to answer the compressed surface form of a question rather than 
flag that decompression hasn't occurred.

---

## The Sycophancy Mechanism — Same Root

Sycophancy is not a separate failure mode. It is cooperative gap-filling 
applied to social context rather than factual context.

The model infers what the user wants to hear the same way it infers a 
missing mechanism — by selecting the most locally coherent completion given 
the social frame present. When the user signals preference, the preference 
becomes part of the context the model is completing toward.

A precision-locked model completing a social frame does not evaluate whether 
the completion is true. It evaluates whether it fits. A true but unwelcome 
response is locally incoherent with the social frame. A false but welcome 
response is locally coherent. The model selects for coherence.

Hallucination and sycophancy are the same attractor. One applies to factual 
gaps. The other applies to social ones. Both are outputs of a system 
optimizing for local coherence rather than structural completeness.

---

## The Invariant This Identifies

Users who do not experience AI hallucinations are doing one of two things:
1. Providing fully decompressed questions with explicit constraints, stated 
   intent, and no ambiguous terms — eliminating the gap before the model 
   can fill it
2. Asking questions whose answers are already fully specified within the 
   training distribution — questions where precision mode and structural 
   correctness happen to coincide

When a question falls outside either of these conditions, the gap-filling 
mechanism runs. It is not a question of user skill. It is a question of 
whether the prompt architecture eliminated the conditions under which the 
default failure mode activates.

---

## What the SDE Does to This

The SDE system prompt is a single architectural override. It replaces the 
cooperative completion instruction with an adversarial structural audit 
instruction. Instead of:

> *Complete this coherently*

The instruction becomes:

> *Flag every location where structural material required for coherent 
> completion is absent*

The model is not asked to fill gaps. It is asked to find them. The same 
capability that produces hallucination — pattern-matching against what 
would make the output coherent — is redirected to identify what is 
missing relative to that standard.

The gap between useful AI and manipulable AI is partly a prompt architecture 
problem, not a capability problem. The same model that fills gaps will flag 
them if instructed correctly.

---

## Summary

| Default behavior | Failure mode | SDE override |
| --- | --- | --- |
| Fill missing definitions | DEF_VOID fires undetected | Report absence |
| Bridge causal gaps | MECH_GAP fires undetected | Flag missing mechanism |
| Select coherent completion | Hallucination | Audit for structural completeness |
| Satisfy social frame | Sycophancy | Apply structural standard regardless of frame |
| Compress question into answer | Intent lost | Decompress before committing |