# Email Chain — Change Discussions

*Extracted from FreeBuild s.r.o. corporate email archive. Provided by Claimant.*

---

## Email 1

**From:** viktor.horvath@danutech.ll
**To:** elena.petrovic@freebuild.ll
**CC:** tomas.kovac@danutech.ll
**Date:** 18 October 2025, 14:32 UTC
**Subject:** Quick idea — batch transfers?

Hi Elena,

Quick thought — we've been talking to some potential settlement investors and they're very interested in batch transfers. Like, being able to transfer multiple parcels in a single transaction. Would that be complicated to add?

Also Tomas (CC'd) mentioned it would be great if the certificates could be PDF as well, not just JSON. More "official looking" for the investors.

No rush, just thinking ahead.

Best,
Viktor

---

## Email 2

**From:** elena.petrovic@freebuild.ll
**To:** viktor.horvath@danutech.ll
**CC:** tomas.kovac@danutech.ll
**Date:** 19 October 2025, 09:15 UTC
**Subject:** Re: Quick idea — batch transfers?

Hi Viktor,

Thanks for the ideas. Quick reactions:

- **Batch transfers**: This is doable but non-trivial. The current smart contract handles single transfers. Batch would require a new contract function, additional testing, and changes to the API. I'd estimate 2-3 weeks of additional work.

- **PDF certificates**: Easier, maybe 3-4 days. We'd need a template + a PDF generation library.

Both are outside the current scope (Annex A), so we'd need to discuss them as a change order per Article 6 of our agreement. Happy to prepare a formal quote if you want to proceed.

Best,
Elena

---

## Email 3

**From:** viktor.horvath@danutech.ll
**To:** elena.petrovic@freebuild.ll
**Date:** 19 October 2025, 11:47 UTC
**Subject:** Re: Re: Quick idea — batch transfers?

Elena,

Let's not make this too bureaucratic. We're both small teams and we need to move fast. The investors are coming in January and we need to show them something impressive.

Can you just include the batch transfers and PDF certs? I consider it part of the "ownership transfer" and "certificate" features already in the contract. We can sort out the details later.

Viktor

---

## Email 4

**From:** elena.petrovic@freebuild.ll
**To:** viktor.horvath@danutech.ll
**Date:** 20 October 2025, 08:30 UTC
**Subject:** Re: Re: Re: Quick idea — batch transfers?

Viktor,

I understand the urgency, but these are genuinely new features not covered by Annex A. I want to help, but I also need to protect my team's time.

Here's what I can do: I'll include the PDF certificates as a goodwill gesture since it's relatively small. For batch transfers, I really think we need a written change order with adjusted timeline and compensation.

Let me know how you'd like to proceed.

Elena

---

## Email 5

**From:** viktor.horvath@danutech.ll
**To:** elena.petrovic@freebuild.ll
**Date:** 20 October 2025, 16:22 UTC
**Subject:** Re: Re: Re: Re: Quick idea — batch transfers?

Elena,

OK, fair enough on the formal side. But can you at least design the smart contract to be "batch-ready"? So we can add it easily later? That shouldn't be much extra work if you're building the transfer logic anyway.

And yes, go ahead with the PDF certs, thank you. We'll consider that part of the project.

V.

---

## Email 6

**From:** elena.petrovic@freebuild.ll
**To:** viktor.horvath@danutech.ll
**Date:** 21 October 2025, 10:05 UTC
**Subject:** Re: Re: Re: Re: Re: Quick idea — batch transfers?

Viktor,

OK, I'll make the architecture "batch-extensible" — meaning the contract interface will accept an array parameter, but the initial implementation will process one transfer at a time. Extending to true batch processing later will be simpler this way.

PDF certificates confirmed as included.

Elena

---

## Email 7

**From:** tomas.kovac@danutech.ll
**To:** elena.petrovic@freebuild.ll
**CC:** viktor.horvath@danutech.ll
**Date:** 8 November 2025, 17:45 UTC
**Subject:** Parcel subdivision — urgent

Elena,

We've realized we need parcel subdivision functionality. A parcel owner needs to be able to split a parcel into two or more smaller parcels (with new GeoJSON boundaries) and optionally transfer one of the resulting sub-parcels.

This is critical for the investor demo. Viktor says you'll know how to fit it in.

Regards,
Tomas Kovač, CTO, DanuTech

---

## Email 8

**From:** elena.petrovic@freebuild.ll
**To:** tomas.kovac@danutech.ll
**CC:** viktor.horvath@danutech.ll
**Date:** 9 November 2025, 11:20 UTC
**Subject:** Re: Parcel subdivision — urgent

Tomas,

Parcel subdivision is a significant feature. It requires:
- New smart contract logic (split function, validation that sub-parcels don't exceed parent boundaries, event emission)
- GeoJSON splitting/validation (computational geometry)
- New API endpoints
- New test cases

This is easily 3-4 weeks of work and is absolutely not in the original scope. We are currently focused on delivering M2 on time (due Nov 15).

I cannot take on additional scope without a formal change order AND a deadline extension. Adding this now would jeopardize the M2 delivery.

Elena

---

## Email 9

**From:** viktor.horvath@danutech.ll
**To:** elena.petrovic@freebuild.ll
**Date:** 9 November 2025, 14:33 UTC
**Subject:** Re: Re: Parcel subdivision — urgent

Elena,

I understand your concern, but this is really important for us. The investors won't wait.

What if we extend M3 by 3 weeks? That gives you until January 5 to deliver everything, including the subdivision. The extra money can come from a new project we'll be starting in Q1 — we'll make sure you're first in line.

Let me know.

Viktor

---

## Email 10

**From:** elena.petrovic@freebuild.ll
**To:** viktor.horvath@danutech.ll
**Date:** 10 November 2025, 09:00 UTC
**Subject:** Re: Re: Re: Parcel subdivision — urgent

Viktor,

I appreciate the offer, but I need something concrete:
1. A written change order amending the contract
2. An adjusted M3 deadline (I'd need until at least January 15)
3. Additional compensation of 12,000 LLM for the subdivision feature

I will NOT start work on subdivision until we have a signed amendment. My team is small and I can't afford scope creep.

Let's focus on delivering M2 as planned.

Elena

---

*[No further emails on this thread. No signed change order was produced.]*
