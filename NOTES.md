# Saved-up questions

- 2026-09-21: another instance of the recurring detached-HEAD false-alarm pattern.
  Session started detached at 053ddf4 with a stale cached `origin/main` briefly
  showing 17d81f6 (44 commits behind) before an explicit `git fetch origin main`
  updated it to 053ddf4, exactly matching HEAD, i.e. no push was actually lost this
  time, just the same pre-fetch-cache illusion the 2026-09-20 note already
  diagnosed. Ran `git checkout -B main HEAD` to attach `main` (fast-forward, already
  up to date with origin). Re-confirmed person/place/group rewrite is still complete
  (0 not-yet-rewritten in all three; kind=="unknown" still has 10 out-of-scope
  stragglers, unchanged). No content batch this run per the task's own instructions
  for the fully-complete case.

- 2026-09-20 (later run): started detached again at ffd3f70 with local `main` showing
  17d81f6, which looked at first like the same recurring bug. This time `git fetch
  origin main` before touching anything showed origin/main was actually already at
  ffd3f70, i.e. the previous run's push had landed fine; the "stale" local `main` was
  just this fresh container's cached ref from before that push, not a missed push. Ran
  `git checkout -B main HEAD` to attach main to the current tip (fast-forward, no new
  push needed since origin already matched). Lesson for future runs: always `git fetch
  origin main` first and compare against the freshly-fetched origin/main, not the
  container's pre-fetch local ref, before concluding a push was lost. Also
  re-confirmed the full rewrite (person/place/group) is still complete; no content
  batch was done this run.

- 2026-09-20: the detached-HEAD bug documented just below recurred on the very commit
  that documented it. This session started detached again at 4fcd5b5 (one commit ahead
  of local/origin main at 17d81f6), confirming the root cause is environmental: every
  fresh session/container starts on a detached HEAD regardless of what branch state the
  prior session left behind, not a one-off mistake in a single run. Recovered by
  `git checkout -B main HEAD` (fast-forward, main was a clean ancestor) and pushed;
  `git ls-remote origin main` confirmed origin/main landed on 4fcd5b5. This means
  jayms.com had been serving the pre-2026-09-18 dataset (missing the entire place-tier
  and group-tier rewrite, 42 commits) for roughly 30-54 hours longer than the previous
  run's fix note assumed, since that fix's own commit never actually reached origin.
  Every future run MUST do this exact sequence before any other git command: check
  `git symbolic-ref -q HEAD` (if it fails/prints nothing, HEAD is detached), run
  `git checkout -B main HEAD` regardless to guarantee a real branch pointed at the
  current tip, and after `git push origin main` verify with
  `git ls-remote origin main` (or `git rev-parse HEAD origin/main`) that the remote SHA
  actually matches, not just that push exited 0. Do this check-and-fix at the very start
  of the run, before reading entities.json, since a stale push means nothing else in the
  run matters.

- 2026-09-20: at the start of this run, confirmed (after the recovery above) that the
  full rewrite is complete: kind=="person" (2007 non-curated), kind=="place" (759
  non-curated), and kind=="group" (192 non-curated) all have dictSource starting with
  "study-bible", "Tyndale", or "International Standard Bible Encyclopedia" already, zero
  not-yet-rewritten records left in any of the three tiers. Per the run instructions, no
  new content batch was done this run. Note: kind=="unknown" (18 non-curated, 10 not yet
  rewritten) was never in scope for this project and is untouched; the run instructions
  only ever named person/place/group, so leaving it as-is.

- 2026-09-19 (later, ~19:30 run): found that every run since 2026-09-18 06:21 (15
  scheduled firings, 41 commits, the full place-tier and group-tier rewrite) had been
  committing successfully in this working directory but landing on a DETACHED HEAD
  rather than the `main` branch, so `git push origin main` was pushing the unmoved local
  `main` ref (a no-op that still exits 0 and prints success) instead of the new commits.
  origin/main was still sitting at 17d81f6 (2026-09-18 00:56) while local history had
  raced 30+ hours ahead; production (jayms.com) had not received any place- or
  group-tier rewrite the whole time. Recovered by branching the detached tip
  (`recovered-work` at 1a73640), fast-forwarding local `main` onto it, confirming HEAD
  was attached to `refs/heads/main` afterward, and pushing for real; origin/main now
  matches local at 1a73640 and entities.json is confirmed valid JSON with 3026 records.
  Root cause of how HEAD got detached in the first place is still unknown (possibly a
  `git checkout <sha>` in an earlier run, e.g. to inspect a specific commit, that was
  never followed by `git checkout main`); future runs should verify `git symbolic-ref -q
  HEAD` succeeds (prints `refs/heads/main`) before committing, and should not trust a
  clean `git push` exit code alone as proof the push actually moved origin/main, check
  `git rev-parse HEAD origin/main` match afterward instead.

- 2026-09-19: third and final group-tier batch (all 77 remaining not-yet-rewritten group
  records, all single-canonical-ref); the group tier is now fully complete, 0
  not-yet-rewritten records left in kind=="person", kind=="place", or kind=="group". Only
  kind=="unknown" (10 remaining, not part of this task's scope) still has un-rewritten
  records; a future run may want clarification on whether that tier should be included.
  ISBE (internationalstandardbible.com) was checked again at the start of this run via
  curl and is still blocked (connection reset through the proxy), consistent with every
  prior run's note, so this batch used general knowledge throughout; dictSource is
  "study-bible (ACAI + Tyndale)" for all 77. Almost the entire remaining pool was
  wilderness-census clan names from Numbers 26 (patronymic families named for a son or
  grandson of one of the twelve tribal patriarchs) plus a handful of "resident of X"
  epithets for David's mighty men and a few nation/ethnonym terms (Samaritans, Sabeans,
  Dedanites, Parthians, etc.), so most entries are short, 1-2 sentences. Two records
  worth flagging: "Baharumite" (H978, 1 Chr. 11:33) and "Barhumite" (H1273, 2 Sam.
  23:31) are two separate site records for the very same man (Azmaveth of Bahurim) under
  variant spellings from the parallel mighty-men lists, both now rewritten to note the
  connection; and "Jezerite" (H373, Num. 26:30) turned out to be Gideon's own clan, the
  Abiezrites of Gilead within Manasseh, distinct from the unrelated "Jezerites" (H3340,
  1 Chr. 25:11), which actually names a division of Asaph's Levitical singers, not a
  genealogical clan at all; both were kept as separate, distinctly worded records. Also
  caught one mistagged entry: "Ophni" (H6078, Josh. 18:24) is tagged kind=="group" but is
  actually a town of Benjamin, not a clan or people group; the dictNote was written to
  say so honestly rather than inventing a fake gentilic sense. Real archaeology folded in
  where genuine: the Code of Hammurabi stele found at Susa (Susanchites), the excavated
  Dedanite/Lihyanite inscriptions at al-Ula in Arabia (Dedanim), and the 2010s Philistine
  cemetery excavation at Ashkelon (Eshkalonites). Path note for future runs: no
  jayms-post-build skill directory exists in this environment, so these notes go in
  NOTES.md at the repo root, as prior runs have done.

- 2026-09-19: second group-tier batch (55 more not-yet-rewritten group/gentilic records,
  sorted by canonical-ref count descending); 77 not-yet-rewritten group records remain
  after this run. ISBE (internationalstandardbible.com) is still blocked in this
  environment; this run's WebFetch attempt returned an explicit EGRESS_BLOCKED error from
  the network proxy for that domain (not just a curl timeout), confirming it is a
  deliberate proxy policy block rather than a flaky connection, consistent with every
  prior run's note. WebSearch was used once to verify the Kurkh Monolith / battle of
  Qarqar fact (Hamath's king Irhuleni in the anti-Assyrian coalition with Ahab) before
  writing it into the Hamathite entry; dictSource is "study-bible (ACAI + Tyndale)"
  throughout this batch, not an ISBE citation. Most of this batch is minor gentilic
  epithets (David's mighty men, wilderness-census clan names, "resident of X" tags
  applied to a single named individual), so entries are short, 1-3 sentences. One
  multi-sense catch this run: "Hezronites" (H2697, Num. 26:6 and 26:21) is not one clan
  but two distinct clans that happen to share the same demonym, descended from two
  different men named Hezron (a son of Reuben, and a separate grandson of Judah through
  Perez who is also an ancestor in David's own genealogical line); the record was
  rewritten to cover both. No source-data misspellings (the Azorigin/Onespiphorus/
  Dinhaban/Adronicus/Nakbi/Asharoth pattern from earlier runs) turned up in this batch.
  Path note for future runs: no jayms-post-build skill directory exists in this
  environment, so these notes go in NOTES.md at the repo root, as prior runs have done.

- 2026-09-19: thirteenth and final place-tier batch (all 64 remaining not-yet-rewritten
  place records, all single-canonical-ref); the place tier is now fully complete, 0
  not-yet-rewritten place records left, so the pool moves entirely to kind=="group"
  next run (187 remaining), with kind=="unknown" (10 remaining) after that. ISBE
  (internationalstandardbible.com) is still blocked via curl and WebFetch in this
  environment (agent-proxy status confirms a 403 policy denial on the CONNECT to that
  host), consistent with every prior run, so this batch again used general knowledge,
  dictSource "study-bible (ACAI + Tyndale)" throughout; WebSearch was not blocked and
  was used to verify several facts before writing them rather than assume them (the
  Migdal Stone and the 2009/2016 first-century synagogue excavations at Magdala, James
  Pritchard's 1970s excavation of Zarephath/Sarepta confirming the site by an inscribed
  seal and uncovering over twenty pottery kilns, the Mesha Stele's own claim to have
  rebuilt Kiriathaim, the still-unlocated site of Akkad despite over a century of
  search, the Tel Dan Stele found at the site of Laish/Leshem/Dan, Tiglath-pileser
  III's annals recording the annexation of Abel-beth-maachah near Beth-maachah,
  Sennacherib's own annals naming Mahalliba (matching Ahlab) among the Phoenician
  towns that submitted in his 701 BC campaign, and the Lydian-Aramaic "Sparda"
  inscription from Sardis relevant to Sepharad). One data-quality issue handled in the
  dictNote text rather than corrected in the data: "Gibeah" (strong H1388) carries
  kind=="place" but its only canonical reference, 1 Chronicles 2:49, is a Judahite
  Calebite genealogical entry naming a clan/settlement called Gibea, not the far
  better-known Gibeah of Benjamin (Saul's hometown); the new dictNote explains this
  distinction rather than writing a biography of the wrong Gibeah, same pattern as the
  recurring genealogical place-name notes in earlier batches. This file lives at the
  repo root because no jayms-post-build skill path exists in this container.

- 2026-09-19: twelfth place-tier batch (50 entities, pool entirely single-canonical-ref
  since the tenth batch; 64 not-yet-rewritten place records remain). ISBE
  (internationalstandardbible.com) is still blocked via curl and WebFetch in this
  environment (agent-proxy status confirms a 403 policy denial / EGRESS_BLOCKED on
  that host), consistent with every prior run, so this batch again used general
  knowledge, dictSource "study-bible (ACAI + Tyndale)" throughout; WebSearch was not
  blocked and was used to spot-check the least-certain facts before writing them
  (the Great Isaiah Scroll's "Syene" reading for Sinim at Isa. 49:12, Strabo's
  testimony that the Persian kings favored Chalybon/Helbon wine, the 2011 discovery
  of a probable martyrium over the apostle Philip's tomb at Hierapolis, and the
  three-year siege of Sharuhen recorded in the tomb autobiography of Ahmose son of
  Ebana), all confirmed rather than assumed. Two data-quality issues found and
  handled in the dictNote text itself rather than corrected in the data: "Allon"
  (H438, 1 Chr. 4:37) carries kind=="place" but its own canonical reference is
  actually a Simeonite genealogical entry, not a location (Easton's headword covers
  both an oak-tree landmark and this person under one entry); and "Helbah" (H2463,
  Ezek. 27:18) has a canonical reference that describes Helbon, a wine-trading town
  near Damascus, not Helbah of Asher (the place its duplicate-name sibling H2462,
  Judg. 1:31, correctly refers to) - the dictNote for H2463 was written about
  Helbon and flags the mismatch inline. Several other entries in this batch are
  genealogical place-as-person names from 1 Chronicles 2 (Beth-gader, Machbenah,
  Jorkeam), written to explain that Chronicles convention rather than invent
  biographies for them.
- 2026-09-19: eleventh place-tier batch (55 entities, all single-canonical-ref; 114
  not-yet-rewritten place records remain). ISBE (internationalstandardbible.com) is
  still blocked (agent-proxy status confirms a 403 policy denial on the CONNECT to
  that host), consistent with every prior run, so this batch again used general
  knowledge, dictSource "study-bible (ACAI + Tyndale)" throughout, with real
  corroboration folded in where genuinely established: the Amarna letters naming
  Hinnatuna/Hannathon as a contested Galilee garrison town centuries before Joshua,
  Tiglath-pileser III's own annals recording the Assyrian conquest of Abel-maim
  (Abel-beth-maachah), the excavated Iron Age royal compound and lmlk-stamped jar
  handles at Ramat Rahel proposed as Beth-haccerem, the Naville excavation of
  store-chamber ruins at Tell el-Maskhuta long identified with Pithom (noting the
  competing Tell er-Retabeh identification rather than overclaiming), and the
  scholarly identification of Koa with the well-attested Mesopotamian region of
  Gutium. One duplicate-record fix: "Addar" (H146, 1 Chr. 8:3, kind=="place") is
  not a place at all but the same person already covered under "Ard" (H714, Bela's
  son); rewritten to say so plainly rather than invent a fake location, the mirror
  image of the recurring place/deity-tagged-as-person pattern flagged in earlier
  batches. One textual crux flagged rather than silently resolved: "Ummah" (Josh.
  19:30, Asher) is widely read as "Acco" by scholars following the LXX, since Acco
  is otherwise absent from Asher's town list despite Judg. 1:31 placing it in
  Asher's territory; noted in the dictNote itself rather than picked as fact.
  This file lives at the repo root because no jayms-post-build skill path exists
  in this container; a future run should check both locations.
- 2026-09-19: tenth place-tier batch (55 entities, pool now entirely single-canonical-ref,
  so no further ref-count sort was meaningful; 169 not-yet-rewritten place records remain).
  ISBE still blocked via curl in this environment (TLS connect failure, exit 56), consistent
  with every prior run, so this batch used general knowledge, dictSource
  "study-bible (ACAI + Tyndale)" throughout, with real corroboration folded in for Gaza
  (Amarna letters), Erech/Uruk (excavated temple precincts, origin of cuneiform), and Hara
  (Tiglath-pileser III's annals recording the Transjordan deportations). One content-error
  correction, not just a flag: "Iron" (H3375, Josh. 19:38) had a dictNote entirely about the
  metal iron rather than the Naphtali town of that name; rewritten to describe the actual
  place. Two textually uncertain entries flagged rather than resolved: "Dan also" (H2051,
  Ezek. 27:19), where the Masoretic text is difficult and some scholars read "Vedan" (an
  Arabian place) instead of the tribe/territory of Dan, a genuine textual-critical question a
  human editor may want to weigh in on rather than have silently picked one reading; and
  "Bamah" (H1117, Ezek. 20:29), which is a prophetic wordplay on the generic term "high
  place" rather than a normal toponym, kept as a place entry since the verse itself treats it
  as a name but worth a second look if the kind taxonomy ever gets more granular.
- 2026-09-19: ninth place-tier batch (50 entities, all tied at a single canonical
  reference each, since the place pool is now entirely down to single-verse
  entries); 224 not-yet-rewritten place records remain. ISBE
  (internationalstandardbible.com) is still blocked via curl in this environment
  (gateway answers 403 to CONNECT), consistent with every prior run, so this batch
  again used general knowledge, dictSource "study-bible (ACAI + Tyndale)"
  throughout, with real archaeology/extrabiblical corroboration folded in where
  genuinely established (the Lysanias-the-tetrarch inscription near Abila
  confirming Luke 3:1, the Ahiram sarcophagus and Amarna letters for Gebal/Byblos,
  the Deir Alla "Balaam son of Beor" plaster inscription and the Assyrian
  attestation of Pitru for Pethor, the Tiglath-pileser III conquest record for
  Kullani/Canneh, Tel Aphek's excavated strata for Antipatris, and the excavated
  Roman lighthouse for Patara). Two canonical-reference mismatches found, not
  corrected here, only flagged: "Mearah" (strong H4632) carries the canonical ref
  Isaiah 32:14, but that verse only uses the same Hebrew word as a common noun
  ("den"/"cave"); the actual place Mearah is named at Joshua 13:4, near Sidon, and
  the new dictNote describes that place while the canonical field is probably
  wrong. Similarly "Avim" (strong H5761) carries the canonical ref Joshua 18:23,
  a Benjamite town, but Easton's old dictNote text described the unrelated
  coastal Avvite people of Deut. 2:23; the new dictNote covers the actual town at
  Josh. 18:23 and notes the two are different, but the underlying strong-number
  tagging may deserve a look. Same pattern as the Japha/Mesha/Urbanus notes
  below, where a name or kind tag didn't match its own cited verse.
- 2026-09-19: eighth place-tier batch (55 entities, sorted by canonical-ref count
  descending); the pool is now entirely down to entries with a single canonical
  reference each (274 not-yet-rewritten place records remain after this run). ISBE
  (internationalstandardbible.com) is still blocked via curl in this environment
  (connect_rejected through the egress proxy), consistent with every prior run, so
  this batch used general knowledge plus a few genuine archaeology/extrabiblical
  corroborations already well established (the Moabite Stone's mention of
  Baal-meon for Beon, the Ahmose-era Egyptian siege of Sharuhen, the Tel Moza
  Iron Age temple excavation for Mozah, the Kiriath-jearim/Tell Deir el-Azhar
  platform for Baale of Judah, Carthage's tophet precincts for Tophet), dictSource
  "study-bible (ACAI + Tyndale)" throughout. Two mistagged-kind findings: "Mesha"
  (strong H4331, 1 Chr. 8:9) is actually a Benjamite man, son of Shaharaim, not a
  place, distinct from the Arabian place Mesha (H4852, Gen. 10:30, also in this
  batch) and the Moabite king Mesha (H4338, already rewritten as a person); and
  "Urbanus" (strong G3773, Rom. 16:9) is actually a person, Paul's fellow worker
  greeted alongside Stachys, not a place, despite both carrying kind=="place" in
  this dataset. Both were rewritten to describe what they actually are rather than
  invented as fake locations, per the established pattern for this kind of error.
  Two likely name-spelling data issues, not corrected here, only flagged: "En-hakhore"
  (strong H5875, Judg. 15:19) is spelled "Enhakkore" in the KJV; "Bene-barak"
  (strong H1139, Josh. 19:45) is spelled "Beneberak" in the KJV. Neither looks like
  a transliteration choice so much as a possible transcription slip in the source
  data, same pattern as the Gath-rimmon/Japha/Azorigin notes below.
- 2026-09-19: fifth place-tier batch (50 entities, sorted by canonical-ref count
  descending, now down to entries with 3-4 canonical refs); 487 not-yet-rewritten
  place records remain. ISBE (internationalstandardbible.com) is still blocked via
  curl in this environment (gateway answers 403 to CONNECT), consistent with every
  prior run, but WebSearch was not blocked and did surface real ISBE-derived facts
  and other real archaeology/extrabiblical corroboration indirectly (Amarna-letters
  gate-of-Joppa mention, the Mesha/Moabite Stone's own claim to have rebuilt
  Baal-meon, Tiglath-pileser III's summary inscriptions listing the conquest of
  Ijon and Abel-beth-maacah matching 2 Kings 15:29, Thutmose III's Karnak
  topographical list naming Achshaph, the 1956 Kerti Höyük inscription that fixed
  Derbe's location, Sargon II's Khorsabad inscription on the Samaria deportation
  underlying Halah, and the Sabaean-inscription identification of Raamah with
  Ragmatum in Yemen), so dictSource is still "study-bible (ACAI + Tyndale)"
  rather than a real ISBE-text citation. Two data-integrity findings from this
  batch: the entity named "Japha" (strong H3305, refs Josh. 19:46, 2 Chr. 2:16,
  Ezra 3:7, Jonah 1:3) is really Japho, the Hebrew name for Joppa; its `name`
  field looks like a corrupted/misspelled transliteration and probably needs a
  source-data fix to "Japho" (or "Joppa"), same pattern as the Azorigin/
  Onesiphorus/Dinhaban/Adronicus/Nakbi/Gath-rimmon/Daniel notes above. Separately,
  "Phenice" strong G5403 (refs Acts 11:19, 15:3, 21:2, all KJV "Phenice" =
  Phoenicia the coastal region) had carried Easton's text about a *different*
  place, the harbor called Phoenix on Crete's south coast (Acts 27:12), which is
  a distinct entity in this dataset under strong G5405 and still not rewritten;
  this run's new dictNote for G5403 correctly describes Phoenicia and flags the
  distinction so a future run isolates G5405 as its own short Phoenix-harbor entry.

Notes appended by automated entity-rewrite runs when something needs a human decision.
(Path chosen because `~/.claude/skills/jayms-post-build/references/JAYMS-entity-explorer-todo.md`
did not exist in this environment as of 2026-09-18.)

- 2026-09-19: fourth place-tier batch (50 entities, sorted by canonical-ref count
  descending); 537 not-yet-rewritten place records remain. ISBE
  (internationalstandardbible.com) is still blocked via curl in this environment
  (connect_rejected through the egress proxy), so this run again used general
  knowledge, dictSource "study-bible (ACAI + Tyndale)" throughout. Two data-artifact
  findings worth flagging: the entity literally named "Gath-rimmon. d" (strong
  H1667) has a corrupted `name` field with a stray ". d" suffix, same pattern as the
  Azorigin/Onespiphorus/Dinhaban/Adronicus/Nakbi notes above, it should just be
  "Gath-rimmon"; and several entities tagged kind=="place" turned out on inspection
  to have zero canonical refs actually describing a place at all, only people who
  share the headword (Shema H8087, Mikloth H4732, Zophai H6689 all rewritten this
  run as person entries despite their place tag, since every one of their canonical
  refs points to a person, not a location). Shema H8090 (Josh. 15:26, the actual
  town) is a separate untouched record for a future run.
- 2026-09-19: first place-tier batch (55 entities, sorted by canonical-ref count
  descending) is rewritten; person tier is fully done (0 not-yet-rewritten records
  left) so the pool has moved to kind=="place" (692 remaining after this run).
  ISBE (internationalstandardbible.com) was still blocked via curl and WebFetch this
  run (egress proxy returns connect_rejected/EGRESS_BLOCKED), consistent with every
  prior run's note above, so these place entries are general-knowledge (dictSource
  "study-bible (ACAI + Tyndale)"), not real ISBE text; WebSearch could still surface
  short real ISBE snippets indirectly (the search API isn't blocked even though the
  domain fetch is), which is worth trying more deliberately in a future run.
- 2026-09-19: found a real data-integrity bug, not just an obscure name: the record
  named "Daniel" with strong H1835 (kind="place", 32 canonical refs from Genesis
  through 1 Kings) is mislabeled. H1835 is the Hebrew word for "Dan" (Jacob's son /
  his tribe / the city of Dan, "from Dan to Beersheba"), not Daniel the prophet
  (whose correct records are H1840 and H1841/G1158, both already curated separately).
  Its canonical refs (Gen. 30:6, 49:16-17, Judg. 18:29, etc.) confirm this is really
  about Dan. The dictNote was rewritten to correctly describe Dan and flags the
  mismatch inline, but the `name` field itself needs a source-data fix from "Daniel"
  to "Dan", same pattern as the Azorigin/Onespiphorus/Dinhaban/Adronicus/Nakbi notes
  above.
- 2026-09-19: two duplicate-headword pairs noticed this run, left for a future run
  since they weren't in this batch's top-55 slice (each has few canonical refs):
  "Hebron" strong H5683 (1 ref, Josh. 19:28) still carries the old duplicated Easton
  text for the whole Hebron headword; it should be rewritten as just the minor town
  on Asher's border, not the city of Hebron (already correctly rewritten under
  H2275 this run). Likewise "Jeshua" strong H3443 (kind="unknown", 1 ref) still
  carries the same duplicated Easton text as H3442 (rewritten this run); it should
  get its own short, non-duplicate entry once its specific canonical ref is checked.

- 2026-09-18: ISBE (internationalstandardbible.com) is blocked by this environment's
  egress/org policy (proxy returns `connect_rejected` / 403 on CONNECT), so place/group
  entries this run had to fall back to general knowledge instead of the real ISBE text.
  Worth re-checking in a future run in case the network policy changes.
- 2026-09-18: entity named "Azorigin" (strong G107, canonical Matthew 1:13-14) appears to
  be a data artifact, the actual biblical name is "Azor" (an ancestor of Jesus in
  Matthew's genealogy). The dictNote was written describing Azor correctly, but the
  `name` field itself looks wrong and probably needs a source-data fix, not a content fix.
- 2026-09-18: entity named "Onespiphorus" (strong G3683, canonical 2 Timothy 1:16, 4:19)
  looks like the same kind of data artifact as Azorigin above, the actual biblical name
  is "Onesiphorus". The dictNote was written describing Onesiphorus correctly, but the
  `name` field itself likely needs a source-data fix.
- 2026-09-18: entity named "Dinhaban" (strong H1838, canonical Genesis 36:32,
  1 Chronicles 1:43) is very likely a misspelling of "Dinhabah" in the source data (the
  capital city of Bela son of Beor, Edom's first king). Content was written to describe
  Dinhabah correctly; the `name` field may need a source-data fix.
- 2026-09-18: the name "Mesha" has FOUR separate records in entities.json, all sharing
  Easton's one 3-sense headword text before this run: H4852 (Genesis 10:30, a place in
  Arabia), H4337 (1 Chronicles 2:42, Caleb's eldest son) and H4338 (2 Kings 3:4, the king
  of Moab of the Moabite Stone) match Easton's three senses and were rewritten correctly
  this run. But H4331 (1 Chronicles 8:9) is a FOURTH, distinct Mesha not covered by
  Easton's headword at all, a son of Shaharaim in Benjamin's genealogy, born in Moab from
  his wife Hodesh. A future run rewriting H4852 and H4331 needs to write H4852 as the
  Arabian place and H4331 as this separate Benjamite, not reuse the Caleb/Moab-king text.
- 2026-09-18: ISBE (internationalstandardbible.com) is still blocked in this environment
  (proxy `recentRelayFailures` shows `connect_rejected`, gateway 403 on CONNECT), same as
  the prior run's note above; place/group-flavored entries this run again fell back to
  general knowledge instead of the real ISBE text.
- 2026-09-18: entity named "Adronicus" (strong G408, canonical Romans 16:7) is very likely
  a misspelling of "Andronicus" in the source data (the Jewish Christian Paul greets in
  Rom. 16:7 alongside Junia). The dictNote was written describing Andronicus correctly,
  but the `name` field itself probably needs a source-data fix, same pattern as
  Azorigin/Onespiphorus/Dinhaban noted above.
- 2026-09-18: entity named "Nakbi" (strong H5147, canonical Numbers 13:14) is very likely
  a misspelling of "Nahbi" in the source data (the Naphtalite spy, son of Vophsi, sent by
  Moses to scout Canaan). The dictNote was written describing Nahbi correctly, but the
  `name` field itself probably needs a source-data fix, same pattern as
  Azorigin/Onespiphorus/Dinhaban/Adronicus noted above.
- 2026-09-18: ISBE (internationalstandardbible.com) is still blocked in this environment
  (curl to internationalstandardbible.com times out / connection reset through the proxy),
  same as prior runs' notes above; this run stayed in the person tier so it didn't need
  ISBE, but worth re-checking connectivity before a future place/group-tier run.
- 2026-09-19: rewrote the last 30 person-tier entities (all single-canonical-ref names),
  which brings kind=="person" curated==false to zero not-yet-rewritten records; the
  rewrite pool now moves to kind=="place" (747 remaining) next run. Caught several more
  misclassified entries tagged as person that are actually a gentilic/clan name (Isri,
  the Jezerite family of Naphtali, Num. 26:49), a gate name (Sur, 2 Kings 11:6), a trade
  commodity (Pannag, Ezek. 27:17), a tribal group (Nodab, 1 Chr. 5:19; Leummim, Gen. 25:3),
  and a symbolic place name (Hamonah, Ezek. 39:16). Also isolated the Antipas record
  (G493, Rev. 2:13 only) to the martyr of Pergamum, not Herod Antipas, since the "Herod"
  entity (G2264) already covers Herod Antipas under its own canonical refs.
  ISBE (internationalstandardbible.com) was still blocked in this environment when
  checked at the start of this run (proxy connect_rejected), consistent with every prior
  run's note above; worth re-checking again before the place-tier work begins.
- 2026-09-19: third place-tier batch (55 more entities, sorted by canonical-ref count
  descending); 587 not-yet-rewritten place records remain. ISBE direct fetch (curl and
  WebFetch) was still blocked this run, but WebSearch could still surface real facts
  about ISBE-indexed pages indirectly, so this run used WebSearch to verify several
  genuine archaeology/history facts (Lachish ostraca and Azekah, the Erastus and Lystra
  Zeus/Hermes inscriptions, Woolley's royal cemetery at Ur, the Bethsaida et-Tell/el-Araj
  debate, Laodicea's lukewarm aqueduct system, Tel Dor's Phoenician sequence) even though
  it never got real ISBE article text itself, so dictSource is still "study-bible (ACAI +
  Tyndale)" for all 55, not the ISBE citation. Two content-level findings worth flagging:
  "Lasharon" (H8289, Joshua 12:18) turned out to share its Strong's number with six other
  references that are actually the well-known Sharon coastal plain (1 Chr. 5:16, 27:29;
  Song 2:1; Isa. 33:9, 35:2, 65:10), not a separate obscure Canaanite town, so the record
  was rewritten to describe Sharon itself, with Lasharon noted as its Joshua 12:18 form;
  a future run could consider whether the `name` field should really be "Sharon."
  "Asharoth" (H6252) had a null dictNote and looks like a source-data misspelling of
  "Ashtaroth" (Og of Bashan's capital); content was written describing Ashtaroth
  correctly, but the `name` field may need a source-data fix, same pattern as
  Azorigin/Onespiphorus/Dinhaban/Adronicus/Nakbi noted above. Also caught two records
  whose canonical refs mix a place with an unrelated same-headword person genealogy
  that a plain read of the old dictNote would have missed: "Gedor" (H1446) also names a
  man in Benjamin's genealogy tied to Saul's family (1 Chr. 8:31, 9:37), not just the two
  Judah-area towns Easton's headword covered; "Shimron" (H8110) is both a Canaanite city
  in Zebulun (Josh. 11:1-2, 19:15) and, unrelated in origin, a son of Issachar who named
  the Shimronite clan (Gen. 46:13; Num. 26:24; 1 Chr. 7:1). Both were rewritten to cover
  both senses.
