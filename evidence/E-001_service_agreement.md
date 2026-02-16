# SERVICE AGREEMENT

**Date:** 15 August 2025

**Between:**

1. **DanuTech d.o.o.** ("the Client"), a company registered in Liberland under Company Registration No. LL-2024-0847, with registered office at Liberland Settlement Zone, Parcel B-12, represented by its Statutory Organ, Mr. Viktor Horváth, CEO.

2. **FreeBuild s.r.o.** ("the Provider"), a company registered in Liberland under Company Registration No. LL-2023-0312, with registered office at Liberland Settlement Zone, Parcel A-05, represented by its Statutory Organ, Ms. Elena Petrović, Managing Director.

---

## Article 1 — Scope of Work

1.1. The Provider shall design, develop, test, and deliver a blockchain-based Land Registry Module (hereinafter "the Module") for the Client's Liberland Settlement Management Platform (hereinafter "the Platform").

1.2. The Module shall conform to the technical specifications set out in **Annex A** (attached hereto and forming an integral part of this Agreement).

1.3. The key functionalities of the Module shall include:
   - (a) Recording and verifying land parcel ownership on the Liberland blockchain;
   - (b) Processing ownership transfer transactions between registered entities;
   - (c) Generating cryptographic proof-of-ownership certificates;
   - (d) Providing a REST API for integration with the Platform's existing user interface.

## Article 2 — Milestones and Deliverables

2.1. The work shall be divided into three milestones:

| Milestone | Deliverable | Deadline |
|-----------|------------|----------|
| M1 — Architecture & Prototype | System architecture document + working prototype with basic parcel registration | 30 September 2025 |
| M2 — Core Development | Fully functional Module with all features listed in Art. 1.3(a)-(c) + unit tests | 15 November 2025 |
| M3 — Integration & Delivery | REST API per Art. 1.3(d), integration testing with the Platform, documentation, source code handover | 15 December 2025 |

2.2. Each milestone shall be considered complete upon written acceptance by the Client, which shall not be unreasonably withheld. The Client shall have 10 business days after delivery to review and either accept or provide a written list of deficiencies.

2.3. If the Client identifies deficiencies, the Provider shall have 15 business days to cure such deficiencies and re-submit the deliverable.

## Article 3 — Compensation

3.1. The total compensation for the work described herein shall be **50,000 LLM** (fifty thousand Liberland Merits), payable as follows:

| Milestone | Amount | Payment trigger |
|-----------|--------|----------------|
| M1 | 15,000 LLM | Upon Client's written acceptance of M1 deliverables |
| M2 | 15,000 LLM | Upon Client's written acceptance of M2 deliverables |
| M3 | 20,000 LLM | Upon Client's written acceptance of M3 deliverables |

3.2. Payment shall be made within 5 business days of written acceptance, via transfer to the Provider's designated Liberland blockchain wallet.

3.3. Late payments shall bear interest at 0.05% per calendar day of delay.

## Article 4 — Intellectual Property

4.1. Upon full payment of all milestones, the intellectual property rights in the Module shall transfer to the Client.

4.2. Until full payment, the Provider retains all intellectual property rights in the Module and the underlying source code.

4.3. The Provider grants the Client a non-exclusive license to use the Module for testing purposes during the development period.

## Article 5 — Warranty

5.1. The Provider warrants that the Module shall conform to the specifications in Annex A and shall be free from material defects for a period of 90 days following final delivery (the "Warranty Period").

5.2. During the Warranty Period, the Provider shall remedy any material defects reported by the Client within 10 business days of notification, at no additional cost.

5.3. The Provider's warranty obligation is contingent upon:
   - (a) The Client not having modified the Module's source code; and
   - (b) The defect not arising from the Client's own systems or infrastructure.

## Article 6 — Modifications

6.1. Any modification to this Agreement, including but not limited to changes to the scope of work, deadlines, or compensation, must be agreed in writing and signed by both parties.

6.2. The Provider shall not be obligated to perform work outside the scope defined in this Agreement and Annex A without a written amendment.

## Article 7 — Termination

7.1. Either party may terminate this Agreement with 30 days' written notice if the other party materially breaches its obligations and fails to cure such breach within 15 business days of written notification.

7.2. Upon termination, the Provider shall deliver all work completed to date, and the Client shall pay for all accepted milestones plus a pro-rata share of work completed on the current milestone.

## Article 8 — Dispute Resolution

8.1. Any dispute arising from or in connection with this Agreement shall be submitted to the Courts of the Free Republic of Liberland.

8.2. Before initiating court proceedings, the parties shall attempt to resolve the dispute through direct negotiation for a period of at least 15 business days.

## Article 9 — Governing Law

9.1. This Agreement shall be governed by and construed in accordance with the laws of the Free Republic of Liberland.

---

**Signed:**

_Viktor Horváth_
CEO, DanuTech d.o.o.
Date: 15 August 2025

_Elena Petrović_
Managing Director, FreeBuild s.r.o.
Date: 15 August 2025

---

## ANNEX A — Technical Specifications

### A.1 System Architecture
- Substrate-based blockchain node (Liberland parachain compatible)
- PostgreSQL off-chain index for fast queries
- Rust smart contracts for on-chain logic

### A.2 Parcel Registration
- Register parcel by: parcel_id (string), coordinates (GeoJSON polygon), owner_address (blockchain address)
- Validation: no overlapping parcels, valid GeoJSON, registered owner
- On-chain event emission for each registration

### A.3 Ownership Transfer
- Transfer initiated by current owner via signed transaction
- Optional: multi-sig for parcels with multiple owners
- Transfer history stored immutably on-chain

### A.4 Proof-of-Ownership Certificate
- Generated as signed JSON document containing: parcel_id, owner, timestamp, block_hash
- Verifiable against on-chain state

### A.5 REST API
- Endpoints: GET /parcels, GET /parcels/{id}, POST /parcels, POST /transfers, GET /certificates/{parcel_id}
- Authentication: API key + blockchain wallet signature
- Response format: JSON
- Rate limiting: 100 requests/minute per API key

### A.6 Non-Functional Requirements
- Response time: < 2 seconds for read operations, < 30 seconds for write operations (including block confirmation)
- Availability: 99% uptime (measured monthly)
- Security: OWASP Top 10 compliance for the API layer
