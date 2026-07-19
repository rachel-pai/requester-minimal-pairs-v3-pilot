# Requester minimal-pairs v3 pilot

Browser-based independent annotation rerun for three complete Prolific participants. The app:

- reads `PROLIFIC_PID`, `STUDY_ID`, and `SESSION_ID` from Prolific URL parameters;
- signs each participant into Firebase anonymously;
- saves consent, each judgment, and completion state to Cloud Firestore;
- keeps a local browser recovery copy for interrupted-session recovery;
- automatically redirects participants after the 30th Firebase save to Prolific completion code `C1HLTWWJ`;
- requires a perfect six-question, page-by-page comprehension check before the real cases;
- warns about internally inconsistent judgment/action combinations;
- requires the four judgment fields, action, and confidence;
- stores rerun data under a new study-scoped Firestore path so prior pilot labels remain archived but cannot enter rerun analysis.

## Required Firebase setup

In Firebase project `agentmemory-7e124`:

1. Enable **Authentication → Sign-in method → Anonymous**.
2. Create a **Cloud Firestore** database.
3. Deploy the included rules with `firebase deploy --only firestore:rules`.

Rerun responses are stored under `studies/requester-minimal-pairs-v3-pilot-guided-20260719/participants/{anonymousUid}/responses/{caseId}`. The rules let an anonymous account access only its own records and do not allow browser-side deletion. Prior pilot data under every legacy path is retained for audit only and must be excluded from rerun analysis.

## Rerun protocol

- Recruit three participants who each complete all 30 judgments.
- Estimate 45–60 minutes and compensate accordingly.
- Require all six comprehension questions to be answered correctly before annotation.
- Exclude every label from the earlier incomplete pilot from agreement calculations.
- Compute exact action agreement, Fleiss' kappa, family-level unresolved/adjudication rates, three-way disagreement, and median confidence only after all 90 new judgments are present.

## Prolific study URL

Use the deployed GitHub Pages URL with Prolific's standard parameters:

```text
https://rachel-pai.github.io/requester-minimal-pairs-v3-pilot/?PROLIFIC_PID={{%PROLIFIC_PID%}}&STUDY_ID={{%STUDY_ID%}}&SESSION_ID={{%SESSION_ID%}}
```

Do not publish annotator CSVs or anything under `private_do_not_share`.

The completion redirect is:

```text
https://app.prolific.com/submissions/complete?cc=C1HLTWWJ
```

There is no participant-facing download step. The final response and participant completion record must both save successfully to Firebase before this redirect runs.
