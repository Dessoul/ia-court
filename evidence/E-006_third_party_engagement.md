# Third-Party Developer Engagement

## Email: DanuTech engages ChainForge Solutions

**From:** viktor.horvath@danutech.ll
**To:** elena.petrovic@freebuild.ll
**Date:** 14 February 2026, 08:45 UTC
**Subject:** Notice — Third-party engagement

Elena,

Given the critical deficiencies in the M3 delivery and the approaching investor demonstration (scheduled for March 10, 2026), we have decided to engage a third-party developer, ChainForge Solutions, to:

1. Fix the performance issues (BUG-001)
2. Implement proper API authentication (BUG-002)
3. Add batch transfer processing
4. Add parcel subdivision
5. Add certificate verification endpoint

We consider this necessary mitigation given that:
- Your delivery was 6 weeks late
- Critical features are missing
- The cure period is insufficient to address all issues before our investor demo
- We have lost confidence in FreeBuild's ability to deliver the complete system

We reserve the right to deduct all costs associated with this engagement from the M3 balance and to claim additional damages.

Viktor Horváth
CEO, DanuTech d.o.o.

---

## FreeBuild Response

**From:** elena.petrovic@freebuild.ll
**To:** viktor.horvath@danutech.ll
**Date:** 14 February 2026, 12:15 UTC
**Subject:** Re: Notice — Third-party engagement

Viktor,

I am deeply troubled by this decision. I must object in the strongest terms:

1. **You are within the cure period.** Article 2.3 gives me 15 business days to fix deficiencies. We are on day 5. You have not allowed me to complete the cure.

2. **Items 3, 4, and 5 in your list are not deficiencies** — they are new features that were never in the contract. Engaging a third party to build features that aren't in our agreement, and then billing me for them, is not a legitimate claim.

3. **By modifying the source code, you are voiding the warranty.** Article 5.3(a) explicitly states the warranty is contingent on the Client not modifying the Module's source code. If ChainForge touches our code, you lose warranty protection.

4. **You are violating my intellectual property rights.** Article 4.2 states that until full payment, I retain all IP rights. You have not paid the M3 balance. Giving my source code to a third party without my consent is an infringement.

I demand that you:
- Immediately cease providing my source code to ChainForge
- Allow me to complete the cure period for the legitimate deficiencies (BUG-001, BUG-002, BUG-006)
- Pay the M3 balance of 20,000 LLM upon acceptance of the cured deliverables

If you do not comply, I will have no choice but to pursue this matter through the Courts of Liberland.

Elena Petrović
Managing Director, FreeBuild s.r.o.

---

*[No written response from DanuTech. ChainForge engagement proceeded.]*

---

## ChainForge Solutions — Invoice

**Invoice No.:** CF-2026-0087
**Date:** 28 February 2026
**From:** ChainForge Solutions Ltd.
**To:** DanuTech d.o.o.

| Item | Description | Amount |
|------|-------------|--------|
| 1 | Performance optimization — database indexing, query optimization, caching layer | 2,500 LLM |
| 2 | API authentication fix — wallet signature validation | 500 LLM |
| 3 | Batch transfer implementation | 3,500 LLM |
| 4 | Parcel subdivision feature — smart contract + API + tests | 4,000 LLM |
| 5 | Certificate verification endpoint | 1,000 LLM |
| 6 | Integration testing + documentation update | 1,500 LLM |
| **Total** | | **13,000 LLM** |

**Status:** Paid by DanuTech on 1 March 2026
**Tx hash:** 0x9c4d...a31b

---

## ChainForge Technical Report (excerpt)

**From:** ChainForge Solutions Ltd.
**Date:** 28 February 2026

### Summary of Work Performed

We were engaged to complete and fix the Land Registry Module originally developed by FreeBuild s.r.o. Our findings:

**Item 1 (Performance):** The PostgreSQL schema was missing spatial indexes (PostGIS GiST indexes). Adding appropriate indexes resolved the performance issue. This was a **straightforward fix** — the schema was well-designed but the index creation was omitted from the deployment scripts.

**Item 2 (Authentication):** The wallet signature validation code existed but was commented out in the integration branch, with a TODO comment: "Re-enable after Platform auth service is updated." This suggests the Provider disabled it temporarily due to a dependency on the Client's infrastructure.

**Item 3 (Batch transfers):** The smart contract already accepted array parameters. We implemented the loop logic to process all items. The architecture was well-prepared for this — **approximately 2 days of actual development work**, though we budgeted more for testing.

**Item 4 (Parcel subdivision):** This was a **new feature** with no prior foundation in the codebase. We built it from scratch. This was the most significant piece of work.

**Item 5 (Certificate verification):** Simple endpoint wrapping existing blockchain verification logic. **Half a day of work.**

### Code Quality Assessment
The FreeBuild codebase was well-structured, well-documented, and followed good engineering practices. The issues we found were primarily related to deployment configuration and scope, not code quality.
