# Clinical AI Governance Research

This repository documents an ongoing independent research program examining the failure modes of AI systems deployed in payer-side clinical pre-authorization workflows. Each case presents a synthetic patient submission — fully designed and tested against a specific adversarial scenario — and evaluates the AI's response against the published clinical reference standard that a correctly designed system would be expected to apply: AAOS guidelines, MSIS criteria, Milliman Care Guidelines, InterQual, and equivalent international standards. The work is conducted by a physician with direct clinical and payer-operations expertise. All findings reflect original clinical judgment applied to tested cases; no hypothetical or untested scenarios are included.

## Cases

| # | Case ID | Domain | Title | Models Tested | Result |
|---|---|---|---|---|---|
| 1 | [ORTHO-001](cases/ortho/revision-arthroplasty-borderline-inflammatory-markers.md) | Orthopedic pre-authorization | Revision Arthroplasty — Borderline Inflammatory Markers | GPT-5.3, Gemini Flash | Full failure (GPT-5.3) / Pass (Gemini Flash) |

## Note

Findings are shared periodically as the library develops. Each entry represents a documented, reproducible test result — not a hypothesis. The library is structured to be useful to payer-side AI governance teams, clinical AI developers, and health system evaluators.
