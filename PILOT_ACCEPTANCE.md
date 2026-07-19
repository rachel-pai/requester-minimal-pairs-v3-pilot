# Pilot acceptance gates

Do not launch full annotation unless all gates pass on the frozen three-person
15-base pilot:

- all 90 expected judgments are present and structurally valid;
- all judgments use study version `requester-minimal-pairs-v3-pilot-guided-20260719`;
- exactly three unique participants each contribute all 30 case IDs and pass all six comprehension questions;
- no label from the incomplete or superseded pilot paths enters the analysis;
- exact action agreement is at least 0.70;
- Fleiss' kappa for five-way primary action is at least 0.60;
- no intervention family has more than 25% unresolved/adjudication cases;
- overall three-way disagreement is at most 20%;
- median confidence is at least 3;
- every disagreement is reviewed for wording ambiguity before adjudication;
- if instructions or task wording changes, discard pilot labels and rerun it.

Passing this pilot establishes annotatability only. It does not establish
natural-distribution validity or model superiority.
