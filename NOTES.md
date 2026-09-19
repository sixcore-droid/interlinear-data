# Saved-up questions

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
