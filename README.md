# Requester minimal-pairs v3 formal study

Browser-based independent annotation study for Prolific participants. The app:

- reads `PROLIFIC_PID`, `STUDY_ID`, and `SESSION_ID` from Prolific URL parameters;
- signs each participant into Firebase anonymously;
- saves consent, each judgment, and completion state to Cloud Firestore;
- keeps a local browser recovery copy for interrupted-session recovery;
- presents 20 judgments balanced across the five actions (four each);
- automatically redirects participants after the 20th Firebase save to Prolific completion code `C1HLTWWJ`;
- keeps only one essential step-by-step practice example;
- requires a perfect six-question, page-by-page comprehension check, including applied purpose and redact-versus-abstain cases;
- blocks internally inconsistent judgment/action combinations until they are revised;
- requires the four judgment fields, action, and confidence;
- stores rerun data under a new study-scoped Firestore path so prior pilot labels remain archived but cannot enter rerun analysis.

## Required Firebase setup

In Firebase project `agentmemory-7e124`:

1. Enable **Authentication → Sign-in method → Anonymous**.
2. Create a **Cloud Firestore** database.
3. Merge this study's rules into the project's active Firestore ruleset. Do **not** deploy this repository's rules file by itself: this Firebase project is shared with another study, and a standalone deploy would overwrite that study's rules.

Formal responses are stored under `studies/requester-minimal-pairs-v3-formal-balanced20-20260720/participants/{anonymousUid}/responses/{caseId}`. The rules let an anonymous account access only its own records and do not allow browser-side deletion. Prior pilot data remains under its legacy path and must not enter the formal analysis.

## Formal protocol

- Give every rater the same 20 judgments: four expose, four redact, four suppress, four refuse, and four abstain.
- Estimate approximately 45 minutes and compensate accordingly.
- Require all six comprehension questions to be answered correctly before annotation.
- Exclude every pilot label from formal agreement calculations.
- Compute exact action agreement, Fleiss' kappa, family-level unresolved/adjudication rates, three-way disagreement, and median confidence only among complete 20-response participants.

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
