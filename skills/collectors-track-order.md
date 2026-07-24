---
name: Track a PSA grading order
description: Check the progress and shipping status of a PSA grading order or submission.
api: openapi/collectors-psa-openapi-original.json
operations: [Order_GetProgress, Order_GetSubmissionProgress]
---

# Track a PSA grading order

Monitor where a submission is in PSA's grading pipeline.

## Auth
- Bearer access token in `Authorization: bearer <access token>`.
- Base URL: `https://api.psacard.com/publicapi`.

## Steps
1. If you have an order number, call `Order_GetProgress` with the `orderNumber` path parameter.
2. If you have a submission number, call `Order_GetSubmissionProgress` with the `submissionNumber` path parameter.
3. Both return an `OrderProgress`: read boolean stage flags (`readyForLabelReview`, `gradesReady`, `accountingHold`, `shipped`), the `orderProgressSteps[]` timeline, and shipping (`shipCarrier`, `shipTrackingNumber`).

## Notes
- Read-only; safe to poll. No documented rate limit — poll conservatively.
- See conventions/collectors-conventions.yml for the auth + error-envelope contract.
