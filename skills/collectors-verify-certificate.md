---
name: Verify a PSA certificate
description: Look up a graded PSA card or PSA/DNA certificate by its cert number and retrieve its images.
api: openapi/collectors-psa-openapi-original.json
operations: [Cert_GetByCertNumber, Cert_GetImagesByCertNumber]
---

# Verify a PSA certificate

Use the PSA Public API to confirm a certificate is genuine and read its grade, subject, and population data.

## Auth
- All requests require a Bearer access token. Register at https://www.psacard.com/publicapi.
- Send header: `Authorization: bearer <access token>`.
- Base URL: `https://api.psacard.com/publicapi`.

## Steps
1. Call `Cert_GetByCertNumber` with the `certNumber` path parameter. It returns a `PublicCertificationModel` wrapping a `PSACert` (card) and/or `DNACert` (autograph/memorabilia).
2. Check the envelope: `IsValidRequest` must be true; `ServerMessage` of "No data found" means the cert number is unknown.
3. Read grade fields (`CardGrade`, `GradeDescription`), identity (`Year`, `Brand`, `Subject`), and population (`TotalPopulation`, `PopulationHigher`).
4. Optionally call `Cert_GetImagesByCertNumber` with the same `certNumber` to fetch label/item images.

## Notes
- Read-only; no idempotency key needed (safe to retry).
- Errors: HTTP 204 = missing cert number; 4xx = bad path; 500/IsValidRequest=false = invalid credentials. See errors/collectors-problem-types.yml.
