# M3 Delivery and Rejection Correspondence

## M3 Delivery Notice

**From:** elena.petrovic@freebuild.ll
**To:** viktor.horvath@danutech.ll, tomas.kovac@danutech.ll
**Date:** 28 January 2026, 11:00 UTC
**Subject:** M3 Delivery — Land Registry Module Complete

Viktor, Tomas,

I'm pleased to confirm the delivery of M3 — the final milestone of the Land Registry Module project.

**Deliverables included:**
1. REST API — all 5 endpoints per Annex A.5, fully functional
2. Integration testing suite — 47 integration tests, all passing against the Platform test environment
3. Technical documentation — API reference, deployment guide, architecture overview
4. Source code — full repository access granted via Git (branch: release/v1.0)

**Notes:**
- The API meets all non-functional requirements (response time, availability targets)
- Security review completed — no OWASP Top 10 vulnerabilities found
- PDF certificate generation (added as goodwill) is included
- The transfer endpoint is batch-extensible as discussed but processes single transfers

**NOT included (as per our prior correspondence):**
- Parcel subdivision feature — no change order was signed
- Batch transfer processing — design is extensible but not implemented

Delivery is 6 weeks past the original M3 deadline of December 15, 2025. The delay was primarily caused by:
- Time spent on PDF certificate integration (approximately 5 days)
- Architecture modifications to make the system batch-extensible (approximately 8 days)
- Additional integration testing complexity arising from the Platform's November infrastructure update (approximately 10 days — DanuTech changed the staging environment configuration mid-project without notice)

I request written acceptance or a deficiency list within 10 business days per Article 2.2.

Best regards,
Elena Petrović
Managing Director, FreeBuild s.r.o.

---

## M3 Rejection

**From:** tomas.kovac@danutech.ll
**To:** elena.petrovic@freebuild.ll
**CC:** viktor.horvath@danutech.ll
**Date:** 7 February 2026, 09:15 UTC
**Subject:** M3 Rejection — Critical Deficiencies

Elena,

After thorough testing, we cannot accept M3. The following critical deficiencies have been identified:

### Critical Issues

1. **No batch transfer support** — The transfer endpoint only processes one transfer at a time. For our investor demo and production use, batch processing is essential. Your email of October 21 confirmed the architecture would support this.

2. **No parcel subdivision** — This was discussed as a necessary feature. Without it, the Module is incomplete for real-world settlement management.

3. **Performance degradation under load** — When we tested with 500+ parcels in the registry, read operations exceeded the 2-second response time requirement. At 1,000 parcels, average response time was 4.7 seconds.

### Major Issues

4. **Certificate verification endpoint missing** — Annex A.4 states certificates should be "verifiable against on-chain state" but there is no verification endpoint in the API.

5. **API authentication inconsistency** — The POST /transfers endpoint does not require wallet signature, only API key. This contradicts Annex A.5.

### Minor Issues

6. **Documentation gaps** — The deployment guide does not cover the PostgreSQL index setup in sufficient detail.

M3 is **rejected**. Please address ALL issues, including items 1 and 2, within the 15-business-day cure period.

Regards,
Tomas Kovač
CTO, DanuTech d.o.o.

---

## FreeBuild Response to Rejection

**From:** elena.petrovic@freebuild.ll
**To:** tomas.kovac@danutech.ll
**CC:** viktor.horvath@danutech.ll
**Date:** 10 February 2026, 14:30 UTC
**Subject:** Re: M3 Rejection — Response

Tomas,

I've reviewed your deficiency list. My responses:

### Items I accept and will fix:

- **Item 3 (Performance):** Valid concern. The PostgreSQL index configuration needs optimization for large datasets. I can fix this within 5 business days.
- **Item 5 (API auth):** You're right — the wallet signature validation was inadvertently disabled in the integration branch. Fix: 1 day.
- **Item 6 (Documentation):** Will update. Fix: 2 days.

### Items I dispute:

- **Item 1 (Batch transfers):** This was never agreed. I explicitly stated in my email of October 20 that batch transfers require a change order. My email of October 21 confirmed only that the architecture would be "batch-extensible" — meaning designed for easy future addition, NOT that batch processing would be implemented. This is NOT a deficiency in the delivered Module.

- **Item 2 (Parcel subdivision):** This was never part of the contract. I explicitly declined to add this feature without a signed change order (email of November 10). No change order was ever produced. This is NOT a deficiency.

- **Item 4 (Certificate verification endpoint):** Annex A.4 specifies that certificates should be "verifiable against on-chain state." The certificates contain the block_hash and can be verified by any blockchain node — this is the standard verification mechanism. A separate REST endpoint for verification was not specified in Annex A.5's endpoint list. However, I'm willing to add a GET /verify/{certificate_hash} endpoint as a goodwill gesture.

### Proposed resolution:

I will fix items 3, 4 (as goodwill), 5, and 6 within the cure period. Items 1 and 2 are out of scope and require separate agreements.

I expect payment of the 20,000 LLM M3 balance upon acceptance of the fixed deliverables.

Elena Petrović

---

*[No written response from DanuTech to this email.]*
