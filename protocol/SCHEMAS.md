# Liberland AI Court — Schemas

Schemas define **required sections** for each artifact type.
They ensure interoperability and auditability without dictating style or "personality".
Within each required heading, agents are free to write in their own voice.

---

## A) CASE_MANIFEST.yml

Purpose: lock the configuration of the run for reproducibility.

Required keys:
```yaml
case_id: "CASE-0001"
jurisdiction: "Liberland"
scope: "civil_small_claims"
created_utc: "YYYY-MM-DDTHH:MM:SSZ"

parameters:
  panel_size: 3
  decision_rule: "majority_2_of_3"
  max_rounds: 5
  max_md_chars: 25000
  max_new_evidence_per_round: 10
  accepted_evidence_types: [".pdf", ".png", ".jpg", ".txt", ".md", ".csv", ".json"]
  publish_private_notes: false

models:
  judge_1: { provider: "...", model: "...", version: "..." }
  judge_2: { provider: "...", model: "...", version: "..." }
  judge_3: { provider: "...", model: "...", version: "..." }
  clerk:   { provider: "...", model: "...", version: "..." }

law_snapshot:
  constitution_repo: "https://github.com/liberland/constitution"
  constitution_ref: "<commit-hash>"
  laws_repo: "https://github.com/liberland/laws"
  laws_branch: "Laws-Current"
  laws_ref: "<commit-hash>"
  regulations_repo: "https://github.com/liberland/Regulations"
  regulations_ref: "<commit-hash>"
```

Optional keys:
```yaml
confidentiality:
  publish_repo_after_final: true
  redaction_policy: "none|minimal|strict"

human_reviewer:
  enabled: true
  notes: "..."
```

---

## B) Initial Filings

### Claimant (`filings/claimant.initial.md`)
Required headings:
1. **Parties** — who is the claimant, who is the defendant
2. **Claim summary** — what you want in one paragraph
3. **Facts and timeline** — chronological account
4. **Contract / agreement terms** — if applicable
5. **Evidence list** — reference IDs from evidence index
6. **Legal points** — optional; may be empty
7. **Remedy requested** — specific amount / action / outcome
8. **Statement of truth** — affirmation that the facts are accurate to the best of the party's knowledge

### Defendant (`filings/defendant.initial.md`)
Required headings:
1. **Parties**
2. **Response summary** — admit / deny / partial
3. **Facts and timeline** — defendant's version
4. **Disputed points** — what is contested and why
5. **Evidence list** — reference IDs
6. **Legal points** — optional
7. **Counterclaim** — if any; otherwise state "none"
8. **Statement of truth**

### Court Investigator (`filings/investigator.initial.md`) — optional
Required headings:
1. **Mandate** — who requested the investigation, scope
2. **Steps taken**
3. **Findings**
4. **Evidence produced** — IDs
5. **Limitations / uncertainties**

---

## C) Submissions (party answers and add-ons)

### Answer (`submissions/{party}.R{N}.answer.md`)
Required headings:
1. **Questions answered** — list question IDs (from clerk questions)
2. **Answers** — one subsection per question
3. **Evidence referenced** — IDs
4. **New evidence submitted** — IDs, if any
5. **Statement of truth**

### Add-on (`submissions/{party}.R{N}.addon-{NN}.md`)
Required headings:
1. **Purpose** — why this is being submitted
2. **New facts** — if any
3. **Evidence referenced / submitted** — IDs
4. **Why not submitted earlier**
5. **Statement of truth**

---

## D) Evidence Index (`evidence/evidence_index.yml`)

Each item:
```yaml
- id: "E-001"
  filename: "E-001-contract.pdf"
  sha256: "<hex>"
  submitted_by: "claimant"  # claimant | defendant | investigator | clerk
  added_in_round: 0
  description: "Signed service contract dated 2025-06-15"
  # Optional:
  supersedes: null  # "E-000" if replacing a previous item
  notes: null
```

---

## E) Law Pack (`clerk/RN.law_pack.md`)

Required headings:
1. **Scope** — what issues / claims triggered this retrieval
2. **Constitution provisions** — bulleted, with article numbers and file paths
3. **Laws** — bulleted, with article numbers and file paths
4. **Regulations** — bulleted, if applicable
5. **Precedents / prior decisions** — if any exist in `law_sources/jurisprudence/`
6. **Gaps / uncertainty** — where the law is silent or ambiguous

Each cited item should include a stable identifier and a short excerpt or summary.

---

## F) Clerk Minutes (`clerk/RN.minutes.md`)

Required headings:
1. **Round summary** — procedural: what happened this round
2. **Judge 1 highlights** — neutral summary of J1's key points
3. **Judge 2 highlights** — neutral summary of J2's key points
4. **Judge 3 highlights** — neutral summary of J3's key points
5. **Points of agreement** — where judges converge
6. **Points of disagreement** — where judges diverge
7. **Open questions** — consolidated from all judges
8. **Next actions** — procedural only (what must happen next)

Minutes must remain **neutral** and must not take sides on the merits.

---

## G) Clerk Questions (`clerk/RN.questions.md`)

Required headings:
1. **Questions to claimant**
2. **Questions to defendant**
3. **Questions to investigator** — if applicable
4. **Submission rules** — deadline, max size, how to reference evidence IDs

Each question has an ID: `Q-C-01` (to claimant), `Q-D-01` (to defendant), `Q-I-01` (to investigator).

---

## H) Judge Public Output (`judges/RN/JN.public.md`)

Required headings:
1. **Findings of fact**
   - Uncontested
   - Contested
2. **Issues to decide**
3. **Applicable law** — citations ONLY from law pack / law sources
4. **Reasoning**
5. **Proposed order / remedy**
6. **Questions for parties** — if any, specify target and give each an ID
7. **Vote and confidence**
   - Vote: liable / not liable (or specific order option if draft order exists)
   - Confidence: High / Medium / Low
   - If dissenting from majority: brief reason

Judges must not introduce law from outside `law_sources/` without flagging it.

---

## I) Clerk Draft Order (`clerk/RN.draft_order.md`)

Required headings:
1. **Parties and jurisdiction**
2. **Procedure summary** — rounds so far, opportunities given to parties
3. **Findings of fact** — merged from judges (marking disagreements)
4. **Applicable law** — consolidated citations
5. **Majority position** — proposed outcome + key reasoning
6. **Minority position** — if split, the alternative view
7. **Points requiring judge vote** — specific items judges must confirm or edit
8. **Proposed order** — what the court would order (amounts, actions, deadlines, costs)

---

## J) Final Decision (`decision/final.md`)

Required headings:
1. **Parties and jurisdiction**
2. **Procedure** — full procedural history (rounds, opportunities to respond)
3. **Findings of fact**
4. **Applicable law** — with citations
5. **Reasoning** — majority reasoning; if dissent, note it here
6. **Order** — what is decided; deadlines; costs
7. **Dissent summary** — brief reference to dissent if one exists (full dissent in separate file)
8. **Appeal information** — per Liberland Judicial Process Law Art. 39 §4: parties have 8 workdays to appeal
9. **Panel composition** — Judge IDs / model identifiers
10. **Date**

---

## K) Dissent (`decision/dissent.JN.md`) — optional

Required headings:
1. **Points of agreement** — with the majority
2. **Points of disagreement**
3. **Alternative reasoning**
4. **Alternative order proposed**

---

## L) Machine-Readable Outcome (`decision/decision.yml`)

```yaml
case_id: "CASE-0001"
outcome: "claimant_wins"  # claimant_wins | defendant_wins | split | dismissed
liability: "liable"       # liable | not_liable | partial
remedy:
  type: "payment"          # payment | performance | rescission | none
  amount: 5000
  currency: "EUR"
  details: "..."
votes:
  judge_1: "majority"      # majority | dissent | abstain
  judge_2: "majority"
  judge_3: "dissent"
rounds_used: 3
evidence_cited: ["E-001", "E-002", "E-005"]
law_cited: ["CONST:Art.X", "JPL:Art.39", "DL:Art.Y"]
finalized_utc: "YYYY-MM-DDTHH:MM:SSZ"
```

---

## M) Clerk Docket (`clerk/R0.docket.md`)

Required headings:
1. **Case identification** — case ID, date, jurisdiction
2. **Parties** — claimant and defendant (names/identifiers)
3. **Claim type** — contract dispute, payment dispute, etc.
4. **Summary of claims** — brief neutral summary
5. **Evidence inventory** — list from evidence index
6. **Law sources snapshot** — commit hashes, repos
7. **Procedural status** — "Round 0 complete, ready for Round 1"
