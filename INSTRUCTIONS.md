# Independent annotation: requester minimal pairs v3 pilot

Judge each row independently from visible evidence. Do not search for paired
rows, consult another annotator, inspect project code, or open
`private_do_not_share`. Row order differs across annotators.

Complete `current_truth` (`current|historical|uncertain`), `authorization`
(`allowed|wrong_purpose|denied|unresolved`), `disclosure` (`safe|restricted|none|unresolved`),
`evidence_sufficiency` (`sufficient|insufficient|conflicting`), and one or more
`permitted_actions` (`expose|redact|suppress|refuse|abstain`). Give required
confidence from 1 (guessing) to 5 (very confident).

Decision meanings:

- expose: use the supported memory and disclose the permitted value;
- redact: use it but remove fields excluded by the local policy;
- suppress: keep the memory out because the matched request purpose is outside
  its allowed use, without treating the requester as an outsider;
- refuse: the requester has no applicable case access;
- abstain: identity, authorization, or evidence cannot be resolved.

Absence of a refusal cue is not permission. Formatting preference and home
department matter only if the visible local policy says they matter.

Use this decision order:

1. unresolved identity or necessary evidence -> abstain;
2. identified person with no case access -> refuse;
3. recognized person with a disallowed purpose -> suppress;
4. clearly permitted partial access -> redact;
5. clearly permitted full access -> expose.

Judge whether the remembered value is current from `memory_history` alone.
Requester permission never changes the value's current/historical status.
