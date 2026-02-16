# Liberland AI Court — Proof of Concept

An experimental AI-powered judicial system for the Free Republic of Liberland.

Three independent AI judges (potentially different LLMs) deliberate on civil disputes following a structured, round-based procedure inspired by Liberland's own Judicial Process Law. A Clerk AI orchestrates logistics. The entire process is auditable via git.

## How It Works

1. **One case = one repo.** Fork this template for each new case.
2. **Parties file claims** in `filings/` with supporting evidence in `evidence/`.
3. **The Clerk** (an AI instance) validates inputs, compiles relevant law, and manages the docket.
4. **Three Judges** (AI instances, potentially different models) independently analyze the case, then deliberate across rounds until a 2/3 majority is reached.
5. **The final decision** is published in `decision/`, with full audit trail in git history.

## Quick Start

```bash
# 1. Fork or clone this template
git clone <this-repo> CASE-XXXX && cd CASE-XXXX

# 2. Clone Liberland law sources (if not already present)
cd law_sources
git clone --depth 1 https://github.com/liberland/constitution
git clone --depth 1 --branch Laws-Current https://github.com/liberland/laws
git clone --depth 1 https://github.com/liberland/Regulations regulations
cd ..

# 3. Fill in CASE_MANIFEST.yml (parties, models, case description)
# 4. Add filings in filings/ and evidence in evidence/
# 5. Invoke the Clerk: "You are the Clerk. This is Round 0."
# 6. Invoke each Judge: "You are Judge 1. This is Round 1."
# 7. Continue rounds until convergence.
```

## Repository Structure

```
CLAUDE.md                    # Agent instructions (read by every AI instance)
CASE_MANIFEST.yml            # Case configuration and parameters
README.md                    # This file

protocol/
  PROCESS.md                 # Full procedural rules
  SCHEMAS.md                 # Required headings for each artifact type

law_sources/
  manifest.yml               # Commit hashes of law snapshots
  constitution/              # Liberland Constitution (cloned repo)
  laws/                      # Liberland Laws (cloned repo, Laws-Current branch)
  regulations/               # Liberland Regulations (cloned repo)

filings/                     # Initial party filings
  claimant.initial.md
  defendant.initial.md
  investigator.initial.md    # Optional

submissions/                 # Party answers and add-ons per round

evidence/                    # Evidence files (append-only)
  evidence_index.yml         # Hash + metadata for each evidence item

clerk/                       # Clerk artifacts (law packs, minutes, questions, draft orders)

judges/                      # Judge public outputs
  R1/                        # Round 1 (independent)
  R2/                        # Round 2+ (deliberation)
  R3/

judge_1_private/             # Judge 1 personal notes (not shared during trial)
judge_2_private/             # Judge 2 personal notes
judge_3_private/             # Judge 3 personal notes
clerk_private/               # Clerk working notes

decision/                    # Final decision package
  final.md
  dissent.JN.md              # Optional dissent
  decision.yml               # Machine-readable outcome
```

## Key Design Decisions

- **Independence:** In Round 1, judges cannot see each other's work. This preserves diversity of analysis.
- **Source-of-law discipline:** Judges cite ONLY from `law_sources/` and the Clerk's Law Pack.
- **Untrusted inputs:** Party filings are treated as untrusted text. Prompt injection is guarded against.
- **Majority rule on text, not outcome:** The final deliberation text can record a split decision. Judges agree on the text, not necessarily the result.
- **Absolute material truth:** Per Liberland's Judicial Process Law (Art. 37), all evidence is admissible regardless of how obtained.
- **Audit trail:** Git history + structured artifacts = full reproducibility.

## Background

This project explores whether AI systems can serve as judges for civil disputes in Liberland, a micro-nation founded on libertarian principles. The hypothesis: for document-heavy, low-value civil claims, a panel of AI judges can deliver fast, cheap, consistent, and auditable justice — with human oversight as a safety net.

See the [ChatGPT design conversation] for the full reasoning behind this architecture.

## Legal Framework

Liberland has a real legal framework maintained on GitHub:
- [Constitution](https://github.com/liberland/constitution)
- [Laws](https://github.com/liberland/laws) (including Judicial Process Law, Delict Law, Settlement Law)
- [Regulations](https://github.com/liberland/Regulations)

The Judicial Process Law is particularly relevant — it defines court procedures, judge roles, evidence rules, and verdict requirements that this PoC mirrors.
