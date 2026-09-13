# interlinear-data

Word-level Greek/Hebrew interlinear data and a Strong's/BDB/Abbott-Smith
lexicon, hosted for the interactive Bible tools on [jayms.com](https://jayms.com).
Fetched live by the page's own JavaScript at `raw.githubusercontent.com` —
nothing here is a database or a service, just static JSON.

## Files

- **One JSON file per New Testament book** (`matthew.json`, `mark.json`,
  `luke.json`, `john.json`, `acts.json`, `romans.json`, `1corinthians.json`,
  `2corinthians.json`, `galatians.json`, `ephesians.json`,
  `philippians.json`, `colossians.json`, `1thessalonians.json`,
  `2thessalonians.json`, `1timothy.json`, `2timothy.json`, `titus.json`,
  `philemon.json`, `hebrews.json`, `james.json`, `1peter.json`,
  `2peter.json`, `1john.json`, `2john.json`, `3john.json`, `jude.json`,
  `revelation.json`) — the entire New Testament, word-by-word: Greek text,
  lemma, gloss, full morphology, Strong's number, Louw-Nida domain, and the
  NET Bible translation of each verse (`netFallback`, used if the live NET
  fetch fails at render time). A handful of individual verses present in
  the Textus Receptus/KJV numbering are bracketed out of the SBLGNT
  critical text and so don't appear (e.g. Mark 16:9-20 is absent as whole
  verses; Romans 16:24, 3 John 15, and Revelation 12:18 are
  versification-numbering differences between traditions, not gaps).
  Source: [Clear-Bible/macula-greek](https://github.com/Clear-Bible/macula-greek)
  (SBLGNT), **CC BY 4.0**.

- **`lexicon.json`** — every Strong's number used across every book above
  plus the site's Genesis 1:1 sample — effectively the full NT Greek
  vocabulary (5,440 entries) — each with a Strong's Concordance definition
  and, where one exists, the matching classical lexicon entry in full:
  Brown-Driver-Briggs (Hebrew) or Abbott-Smith (Greek). Sources:
  - Strong's definitions: [openscriptures/strongs](https://github.com/openscriptures/strongs), **CC BY-SA**.
  - BDB text + the Strong's-to-BDB bridge: [openscriptures/HebrewLexicon](https://github.com/openscriptures/HebrewLexicon), public domain (1906 print edition).
  - Abbott-Smith text: [translatable-exegetical-tools/Abbott-Smith](https://github.com/translatable-exegetical-tools/Abbott-Smith), public domain (1922 print edition). Abbott-Smith's XML tags each entry with its own Strong's number(s) directly, so entries are looked up by that, not by a separate lemma-spelling bridge; a "SYN.:" cross-reference note that some print entries carry couldn't be reliably reconstructed from the XML alone and is omitted from a small number of entries.

- **`word-index.json`** — a concordance index spanning every NT book above:
  every content word (verb / noun / adjective / adverb — function words
  filtered out), keyed by Strong's number, with every occurrence as a
  `{chapter, verse, wordIndex, book}` reference back into that book's own
  JSON file. No text is duplicated between these files.

## License

This repo's own compiled/merged JSON is released **CC BY 4.0**, matching its
primary source (Macula). Attribution for the underlying works belongs to the
sources listed above, not to this repo.

## Used by

The interlinear popup, Word Study, and Entity Explorer tools at
[jayms.com](https://jayms.com).
