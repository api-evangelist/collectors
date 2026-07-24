---
name: Read a PSA population report
description: Retrieve the PSA population report (grade distribution) for a spec by SpecID.
api: openapi/collectors-psa-openapi-original.json
operations: [Pop_GetPSASpecPopulation]
---

# Read a PSA population report

Get how many examples of a given card/spec PSA has graded, by grade.

## Auth
- Bearer access token in `Authorization: bearer <access token>`.
- Base URL: `https://api.psacard.com/publicapi`.

## Steps
1. Obtain a `SpecID` (present on a cert record from `Cert_GetByCertNumber`).
2. Call `Pop_GetPSASpecPopulation` with the `specID` path parameter.
3. It returns a `PSASpecPopulationModel` with `PSAPop` and `PSADNAPop` summaries — per-grade counts (`Grade1`..`Grade10`, `Auth`, `Total`).

## Notes
- Read-only. Combine with the Verify-a-certificate skill: a cert's `SpecID` feeds this call.
- See data-model/collectors-data-model.yml for the entity relationships.
