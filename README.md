# Requester minimal-pairs v3 pilot

Browser-based independent annotation pilot for two remaining Prolific participants. The app:

- reads `PROLIFIC_PID`, `STUDY_ID`, and `SESSION_ID` from Prolific URL parameters;
- signs each participant into Firebase anonymously;
- saves consent, each judgment, and completion state to Cloud Firestore;
- keeps a local browser recovery copy and offers a CSV backup;
- redirects completed participants to Prolific completion code `C1HLTWWJ`.

## Required Firebase setup

In Firebase project `agentmemory-7e124`:

1. Enable **Authentication → Sign-in method → Anonymous**.
2. Create a **Cloud Firestore** database.
3. Deploy the included rules with `firebase deploy --only firestore:rules`.

Responses are stored under `participants/{anonymousUid}/responses/{caseId}`. The rules let an anonymous account access only its own records and do not allow browser-side deletion.

## Prolific study URL

Use the deployed GitHub Pages URL with Prolific's standard parameters:

```text
https://rachel-pai.github.io/requester-minimal-pairs-v3-pilot/?PROLIFIC_PID={{%PROLIFIC_PID%}}&STUDY_ID={{%STUDY_ID%}}&SESSION_ID={{%SESSION_ID%}}
```

Do not publish annotator CSVs or anything under `private_do_not_share`.
