# Platform Infrastructure Change Notice

## Internal DanuTech Communication (disclosed during pre-filing negotiation)

**From:** tomas.kovac@danutech.ll
**To:** dev-team@danutech.ll
**Date:** 12 November 2025, 15:30 UTC
**Subject:** Platform v2.3 migration — staging environment update

Team,

We're upgrading the Platform staging environment this weekend (Nov 14-15) to v2.3. Key changes:

- New authentication service (JWT-based, replacing API-key-only)
- Updated blockchain node (parachain v0.9.4, was v0.9.2)
- Database migration to PostgreSQL 16.1 (from 15.4)

**Important:** External integrators (including FreeBuild) have NOT been notified yet. I'll send them the updated API docs on Monday. If their integration breaks over the weekend, we'll help them fix it next week.

Tomas

---

## Notification to FreeBuild

**From:** tomas.kovac@danutech.ll
**To:** elena.petrovic@freebuild.ll
**Date:** 19 November 2025, 11:00 UTC
**Subject:** Platform staging update — heads up

Elena,

FYI, we updated our staging environment last week. Some changes:
- Auth service now uses JWT tokens alongside API keys
- Blockchain node updated to v0.9.4
- DB is now PostgreSQL 16.1

Let me know if anything breaks on your integration side. We can jump on a call if needed.

Regards,
Tomas

---

*Note: The notification was sent 5 days after the migration, and 1 day after FreeBuild submitted M2 deliverables. FreeBuild's M3 integration testing was conducted against the new environment.*
