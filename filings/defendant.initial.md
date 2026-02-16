# DEFENCE AND COUNTERCLAIM

**Case:** FreeBuild s.r.o. v. DanuTech d.o.o.
**Filed:** 12 March 2026
**Defendant / Counterclaim Applicant:** DanuTech d.o.o. (Company Reg. No. LL-2024-0847), represented by Viktor Horváth, CEO
**Applicant / Counterclaim Defendant:** FreeBuild s.r.o. (Company Reg. No. LL-2023-0312)

---

## PART 1: DEFENCE

## I. Preliminary

1. DanuTech d.o.o. ("the Defendant") contests the Applicant's claims in their entirety and submits that the Applicant's delivery of the Module was materially deficient, unreasonably delayed, and did not constitute substantial performance of the Agreement.

---

## II. Response to the Applicant's Statement of Facts

2. The Defendant admits paragraphs 4, 5, and 6 of the Application (existence of the Agreement, M1 and M2 delivery and payment).

3. As to paragraph 7, the Defendant disputes the characterization of the feature discussions as mere "requests outside scope." The email correspondence (E-002) shows that:
   - The Applicant voluntarily agreed to make the system "batch-extensible" (Email 6) — but then delivered a system that silently drops batch inputs without any error or warning (E-005, BUG-003). This is a defect regardless of scope.
   - The PDF certificate feature was accepted as part of the project (Email 5: "We'll consider that part of the project").
   - The Applicant understood that these features were important to the Defendant's business objectives and incorporated some of them into the project evolution.

4. As to paragraph 8, the Defendant acknowledges the Applicant's goodwill gestures but submits that they became part of the project's scope by mutual course of dealing. Once the Applicant began implementing batch-extensible architecture, the reasonable expectation was that it would function correctly — including at minimum returning appropriate errors when multiple items are submitted.

5. As to paragraph 9 (infrastructure migration), the Defendant admits the migration occurred and that notification was delayed by 5 business days. However, the Defendant disputes that this caused the 6-week delay in M3. The migration occurred during M2 delivery (November), while M3 was due December 15. The Applicant had one full month to adapt to the new environment. The claimed "10 days" of additional integration testing is unsubstantiated.

6. As to paragraph 10, the Defendant submits that the stated causes of delay are insufficient to justify 6 weeks:
   - PDF certificates: 3-4 days by the Applicant's own estimate (Email 2)
   - Batch-extensible architecture: described as an architectural decision, not 8 days of work
   - Infrastructure adaptation: disputed (see above)
   - Total claimed: approximately 23 days. Actual delay: 44 calendar days. The remaining 21 days are unexplained.

7. As to paragraphs 11-12, the Defendant submits that:
   - The cure period under Article 2.3 does not apply when the delivery is materially deficient across multiple critical requirements
   - The Defendant's business interests required urgent action — the investor demonstration was immovable
   - The Defendant notified the Applicant of its intent to engage a third party (E-006) and the Applicant was not deprived of any right she would have exercised — she had already stated she would NOT fix the batch transfer and subdivision issues

8. As to paragraph 14, the Defendant acknowledges that M3 payment has not been made. This is because M3 was rightfully rejected under Article 2.2 of the Agreement.

---

## III. The Defendant's Legal Position

### A. The Module was not substantially performed

9. The doctrine of substantial performance, invoked by the Applicant, requires that the essential purpose of the contract be fulfilled. The essential purpose of the Agreement was to deliver a functional Land Registry Module for a production settlement management platform. The delivered Module:
   - Could not handle real-world data volumes (BUG-001)
   - Had a critical security vulnerability (BUG-002)
   - Silently dropped data without error messages (BUG-003)
   - Was delivered 6 weeks late

10. A system that cannot scale, has security holes, and silently loses data does not substantially perform the essential purpose of a land registry — a system where accuracy, reliability, and data integrity are paramount.

### B. The Applicant contributed to the scope ambiguity

11. The Applicant's own conduct blurred the scope boundaries. By voluntarily incorporating features (PDF certificates, batch-extensible architecture) without a formal change order, the Applicant established a course of dealing where scope was adjusted informally. The Applicant cannot now selectively invoke Article 6 (formal modifications) for some features while having informally accepted others.

12. Under Article 39 §2(c) of the Judicial Process Law, commonly upheld principles of justice recognize the doctrine of estoppel: a party who by their conduct leads another to believe certain facts cannot later deny those facts to the detriment of the relying party. The Defendant reasonably believed that the Applicant was incorporating the discussed features as part of the project's natural evolution.

### C. The engagement of ChainForge was reasonable mitigation

13. Under commonly upheld principles of justice, a party who suffers a breach of contract has a duty to mitigate its losses. The Defendant's engagement of ChainForge was reasonable because:
   - The Applicant had already stated she would NOT implement batch transfers or subdivision
   - The delivery was already 6 weeks late
   - The investor demonstration could not be postponed
   - The cure period for legitimate bugs (15 days) would expire on February 28 — after the demonstration date

14. The Defendant does not dispute that it modified the source code. However, Article 4.3 grants the Defendant a license to use the Module "for testing purposes during the development period." Given that the Module had not been accepted and development was ongoing, this license remained in effect. Having a third party fix defects is within reasonable "testing and development" use.

### D. The IP claim is unfounded

15. The Applicant's IP claim is based on Article 4.2 (retention of IP until full payment). However, the reason full payment was not made is because the Applicant failed to deliver an acceptable Module. The Applicant cannot create a situation where the Defendant must either (a) accept a deficient product, or (b) lose all rights to fix it.

16. Under Article 3 of the Constitution (Sovereignty over Property), the Defendant has the right to act on property it legitimately possesses — including fixing defects in a Module deployed on its own infrastructure. The Applicant's reading of Article 4.2 would produce an unjust result: the Defendant would be locked into using defective software with no ability to fix it, while the Applicant controls the fix timeline.

---

## PART 2: COUNTERCLAIM

## IV. Counterclaim — Statement of Facts

17. As a result of the Applicant's deficient and delayed delivery, the Defendant suffered the following damages:

18. **ChainForge costs:** The Defendant was forced to engage ChainForge Solutions at a cost of 13,000 LLM to fix defects and complete essential features. (Evidence: **E-006**)

19. **Delay damages:** The 6-week delay (December 15, 2025 to January 28, 2026) caused:
   - Postponement of two investor meetings originally scheduled for January 2026
   - Loss of credibility with potential settlement investors
   - Additional hosting and infrastructure costs for maintaining the staging environment during the delay

20. The Defendant estimates delay-related damages at 5,000 LLM.

---

## V. Counterclaim — Legal Basis

21. The Applicant's late and deficient delivery constitutes a breach of the Agreement. Under Article 13 of the Judicial Process Law, the Court may award monetary compensation as a remedy.

22. Under Article 6 of the Constitution (Non-Aggression Principle), the Applicant's retention of the Defendant's money (earned through the first two milestone payments) while failing to deliver a conforming product is an infringement on the Defendant's property rights.

23. The ChainForge costs represent reasonable mitigation expenses that the Defendant would not have incurred but for the Applicant's breach.

24. The Defendant is entitled to set off the counterclaim against any amount the Court may find owing to the Applicant.

---

## VI. Relief Sought (Counterclaim)

25. The Defendant respectfully requests that the Court:

   **(a)** Dismiss the Applicant's claim in its entirety

   **(b)** Order the Applicant to pay:
   - Reimbursement of ChainForge costs attributable to fixing the Applicant's defects: **3,000 LLM** (Items 1, 2, and the proportionate share of Item 6 in the ChainForge invoice — corresponding to bugs the Applicant acknowledged)
   - Reimbursement of ChainForge costs attributable to completing the Module: **8,500 LLM** (Items 3, 4, 5, and remaining share of Item 6 — features that should have been delivered)
   - Delay damages: **5,000 LLM**

   **(c)** In the alternative, if the Court finds that any sum is due to the Applicant, the Defendant requests that the counterclaim be set off against such sum.

   **(d)** Court costs

26. **Total counterclaim: 16,500 LLM** (plus court costs)

---

## VII. Evidence

The Defendant relies on all evidence items submitted by the Applicant (E-001 through E-008) and submits no additional evidence at this time.

---

*Filed on behalf of DanuTech d.o.o.*
*Viktor Horváth, CEO*
*12 March 2026*
