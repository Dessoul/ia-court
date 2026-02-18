# Liberland AI Court — Design Notes

This document captures the design philosophy and rationale behind the protocol.
It is **not normative** — the binding rules are in `CLAUDE.md` and `PROCESS.md`.
This file explains *why* the rules exist and records design decisions made during development.

---

## 1. Judge Independence and Low Guidance

We deliberately avoid prescribing templates or structured formats for judge outputs. Different LLMs (or human judges) think differently, and uniform formatting constrains analytical creativity.

The protocol specifies *what* judges must address (findings, issues, law, reasoning) but not *how* they structure their analysis. If we use different LLMs but force their output into rigid templates, we format their thinking. LLMs respond strongly to structural cues — a template doesn't just organize output, it shapes cognition. To get genuine analytical diversity, we give them freedom.

**Limits of this principle:** We do require certain content elements (burden map, uncertainty marking) and prohibit others (premature verdicts in Round 1). We also encourage intellectual habits (adversarial self-testing, marking uncertainty). But the default is freedom, not structure. Guidance targets *how to think well*, not *what to think*.

---

## 2. The Harmless Clerk

The Clerk is the most obvious attack surface for corrupting the court's judgment — via prompt injection, LLM poisoning, or subtle bias in summarization. Unlike judges, the Clerk has no counterparty: no one in the process is structurally positioned to challenge the Clerk's work.

We focus heavily on judge selection (LLM diversity, bias management, independence), but no one naturally challenges the Clerk. A corrupted Clerk could influence outcomes through:
- Biased law pack curation (selecting which supplementary principles to include)
- Slanted minutes (misrepresenting judges' positions)
- Steering draft orders toward a preferred outcome
- Framing "key questions for judicial analysis" (pre-determining what judges think about)

For this reason, the protocol minimizes Clerk power **by design**, not by intention:

- **Law Pack A/B/C structure:** Supplementary principles are clearly labeled `CANDIDATE ONLY`. Judges must independently adopt them. The Clerk cannot silently make something authoritative.
- **No issue framing:** The Clerk must not write "key questions for judicial analysis." Issues emerge from judges and parties, not from the Clerk.
- **Record controls:** Clerk artifacts (minutes, draft orders, law pack) are convenience summaries. The underlying record (filings, evidence, deliberation files, law sources) is the authority. Judges can always cross-check.
- **Cross-verification:** Judges are instructed to verify that Clerk summaries accurately reflect their positions and the record.

The philosophy: judges are the decision-makers. They have the power and the responsibility to verify, challenge, and overrule the Clerk's work. The Clerk is a neutral logistics function.

---

## 3. Exploratory Round 1

Round 1 is deliberately exploratory, not decisional. Judges analyze the record and identify issues but do not vote on liability or propose remedies.

**Why this matters:**

- **Anchoring bias:** Once a judge writes "liable, Medium confidence," subsequent rounds become about defending that position rather than genuinely deliberating. This is well-documented in human psychology and even more pronounced with LLMs, which anchor hard on their own prior text.
- **False precision:** A confidence level on an untested position — before questions are answered, before colleagues' analyses are seen, before parties argue applicable law — is meaningless.
- **Premature closure:** The adversarial process (questions, answers, party legal arguments on applicable law) hasn't begun yet. Deciding before hearing is the opposite of due process.
- **Written commitment effect:** LLMs will defend text they've already produced. A Round 1 "verdict" becomes the position to be defended rather than a hypothesis to be tested.

**The graduated progression:**

| Round | Character | Output |
|-------|-----------|--------|
| R1 | Exploratory — "here's what I see" | Analysis, issues, burden map, gaps, questions |
| R2 | Deliberative — "here's what I think and why" | Preliminary position, reasoning, response to colleagues |
| R3+ | Decisional — "here's my decision" | Formal vote, draft order response, final reasoning |

This ensures judges commit only after genuine deliberation. The "default posture is no finding yet" rule provides an additional guardrail: when the record is insufficient, judges must say so rather than hallucinate certainty.

**Testing validated this approach:** In Round 1 testing across three cases, the judge explicitly instructed to be skeptical (Judge 3, "devil's advocate") consistently outperformed. Skepticism delays judgment, and delayed judgment produces better analysis. Round 1's exploratory character builds this delay structurally into the process for all judges.

---

## 4. Question Limits

Each judge may ask a maximum of 3 questions per round (9 total for the panel). This design choice emerged from Round 1 testing where judges produced 27-30 questions with massive duplication.

**Why a hard cap rather than Clerk deduplication:**

The alternative — letting the Clerk merge or deduplicate questions — gives the Clerk question-framing power. Question wording matters enormously in legal proceedings. A question may contain underlying assumptions, strategic framing, or deliberate traps. Allowing the Clerk to "merge" questions is allowing the Clerk to rewrite them, which violates the harmless-clerk principle.

A hard cap solves the problem structurally:
- Forces judges to prioritize what matters most
- Mechanically limits the burden on parties (max 9 questions per round)
- Preserves exact verbatim wording (no Clerk involvement in formulation)
- Creates natural multi-round deliberation when questions remain unanswered
- Duplication drops naturally when each judge can only pick 3

The Clerk groups questions by topic (using neutral headers) but does not rewrite, merge, or deduplicate. If multiple judges ask about the same point, parties see the questions grouped together and can answer once per topic.

**A consequence:** If judges still have questions after a round, the trial goes more rounds. This is a feature, not a bug. More rounds = more deliberation = better justice. Courts that rush are courts that err.

---

## 5. Party Access to Applicable Law

In real courts, both sides' lawyers argue about *which law applies and how*. This is a fundamental right of defense. A system where the Clerk selects applicable law and judges apply it — without parties ever arguing their legal theory — skips this critical adversarial step.

The Round 0.5 mechanism (party law response) returns this right:
- Parties receive the Clerk's Law Pack (it's Tier 3 — case file)
- Each party may submit a law response arguing additional provisions, interpretations, or objections to included supplementary principles
- Judges read these alongside the Law Pack as adversarial legal arguments, not neutral research

This is the strongest check on Law Pack bias, because it's adversarial. If the Clerk omitted a relevant provision or included a biased supplementary principle, the opposing party's legal argument will catch it.

---

## 6. Structural Constraints over Trust

Throughout the protocol, we prefer making undesirable outcomes **impossible by design** rather than merely **prohibited by instruction**:

| Risk | Structural constraint (preferred) | Trust-based rule (weaker) |
|------|----------------------------------|--------------------------|
| Clerk biases law pack | A/B/C split + judge adoption required | "Clerk must be neutral" |
| Question bloat | Hard cap (3/judge/round) | "Clerk deduplicates fairly" |
| Premature anchoring | No vote in Round 1 | "Judges should stay open-minded" |
| Clerk frames issues | Prohibition + judge cross-checking | "Clerk is neutral" |
| Clerk rewrites questions | Verbatim preservation rule | "Clerk preserves meaning" |

When we can make something structurally impossible, that's always preferable to making it merely prohibited. Trust is necessary where structural constraints are impractical, but it should never be the first line of defense.

---

## 7. Open-Ended Rounds

The protocol does not impose a default maximum number of rounds. With question limits (3/judge/round) and the natural convergence of deliberation, cases will end when:
- Judges run out of questions
- Positions stabilize
- 2/3 agree on the final text

A hard round limit creates pressure to rush convergence, which is the opposite of what we want. The `max_rounds` parameter exists in CASE_MANIFEST.yml as an optional safety valve for specific cases, but the default is: the case takes as long as it needs.

The escalation mechanism (flag for human review) remains available if a case genuinely cannot converge.
