# Bug Report — DanuTech Internal QA

**Document:** DanuTech QA Report #2026-003
**Date:** 5 February 2026
**Prepared by:** Tomas Kovač, CTO, DanuTech d.o.o.
**Module tested:** FreeBuild Land Registry Module v1.0 (release/v1.0 branch)

---

## Test Environment
- Platform: DanuTech Settlement Management Platform v2.3
- Blockchain: Liberland testnet (parachain node v0.9.4)
- Database: PostgreSQL 16.1
- OS: Ubuntu 22.04 LTS
- Hardware: 4 vCPU, 8 GB RAM, 100 GB SSD

## Test Results

### BUG-001: Performance degradation at scale [CRITICAL]
**Steps to reproduce:**
1. Register 500 parcels via POST /parcels
2. Query GET /parcels (list all)
3. Measure response time

**Expected:** < 2 seconds (per Annex A.6)
**Actual:**
- 100 parcels: 0.8s (OK)
- 500 parcels: 3.2s (FAIL)
- 1,000 parcels: 4.7s (FAIL)
- 2,000 parcels: 9.1s (FAIL)

**Root cause hypothesis:** Missing database index on parcel coordinates. The off-chain PostgreSQL index appears to perform a full table scan for spatial queries.

### BUG-002: Transfer endpoint missing wallet signature validation [MAJOR]
**Steps to reproduce:**
1. Send POST /transfers with valid API key but invalid wallet signature
2. Observe that transfer is processed

**Expected:** Request rejected — wallet signature is required per Annex A.5
**Actual:** Transfer processed with API key only

### BUG-003: Batch transfer not functional [CRITICAL — DISPUTED]
**Steps to reproduce:**
1. Send POST /transfers with array of 3 transfer objects
2. Observe behavior

**Expected:** All 3 transfers processed
**Actual:** Only first transfer processed, remaining silently ignored. No error returned.

**Note:** Provider claims this is by design ("batch-extensible"). However, the endpoint accepts an array, processes only the first element, and silently drops the rest WITHOUT any error message or warning. At minimum, this is a UX/API design defect.

### BUG-004: Certificate verification not available via API [MAJOR — DISPUTED]
**Steps to reproduce:**
1. Generate certificate for a parcel
2. Attempt to verify certificate via API

**Expected:** Verification endpoint available
**Actual:** No /verify endpoint exists. Provider claims certificates are "self-verifiable" via blockchain node, but this requires direct blockchain access which our frontend doesn't have.

### BUG-005: Parcel subdivision not available [CRITICAL — DISPUTED]
**Steps to reproduce:**
1. Attempt to subdivide an existing parcel

**Expected:** Subdivision functionality available
**Actual:** No such feature exists.

**Note:** Provider claims this was never in scope. We disagree — it was discussed and is essential functionality.

### BUG-006: Deployment documentation incomplete [MINOR]
**Description:** PostgreSQL setup section does not include:
- GIS extension installation instructions
- Index creation scripts
- Connection pool configuration

---

## Summary

| Bug ID | Severity | Category | Provider agrees? |
|--------|----------|----------|-----------------|
| BUG-001 | Critical | Performance | Yes |
| BUG-002 | Major | Security | Yes |
| BUG-003 | Critical | Missing feature | No — "by design" |
| BUG-004 | Major | Missing feature | Partial — will add as goodwill |
| BUG-005 | Critical | Missing feature | No — "out of scope" |
| BUG-006 | Minor | Documentation | Yes |
