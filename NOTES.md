# Saved-up questions

Notes appended by automated entity-rewrite runs when something needs a human decision.
(Path chosen because `~/.claude/skills/jayms-post-build/references/JAYMS-entity-explorer-todo.md`
did not exist in this environment as of 2026-09-18.)

- 2026-09-18: ISBE (internationalstandardbible.com) is blocked by this environment's
  egress/org policy (proxy returns `connect_rejected` / 403 on CONNECT), so place/group
  entries this run had to fall back to general knowledge instead of the real ISBE text.
  Worth re-checking in a future run in case the network policy changes.
- 2026-09-18: entity named "Azorigin" (strong G107, canonical Matthew 1:13-14) appears to
  be a data artifact, the actual biblical name is "Azor" (an ancestor of Jesus in
  Matthew's genealogy). The dictNote was written describing Azor correctly, but the
  `name` field itself looks wrong and probably needs a source-data fix, not a content fix.
