# interlinear-data

Word-level Greek/Hebrew interlinear data and a Strong's/BDB/Abbott-Smith
lexicon, hosted for the interactive Bible tools on [jayms.com](https://jayms.com).
Fetched live by the page's own JavaScript at `raw.githubusercontent.com` —
nothing here is a database or a service, just static JSON.

## Files

- **One JSON file per book, the whole Bible** — all 27 New Testament books
  (`matthew.json` through `revelation.json`) and all 39 Old Testament
  books (`genesis.json` through `malachi.json`) — word-by-word: original-
  language text, lemma, gloss, full morphology, Strong's number, and (NT
  only) Louw-Nida domain, plus the NET Bible translation of each verse
  (`netFallback`, used if the live NET fetch fails at render time). A
  handful of individual verses differ from Textus Receptus/KJV numbering
  because of real versification differences between traditions (e.g. Mark
  16:9-20 is bracketed out of the SBLGNT critical NT text; Hebrew Psalm
  superscriptions are frequently verse 1 in the Hebrew numbering but
  unnumbered in English) — not gaps in the data.
  - NT source: [Clear-Bible/macula-greek](https://github.com/Clear-Bible/macula-greek) (SBLGNT), **CC BY 4.0**.
  - OT source: [Clear-Bible/macula-hebrew](https://github.com/Clear-Bible/macula-hebrew) (WLC), **CC BY 4.0**.

- **`lexicon.json`** — every Strong's number used across every book above
  plus the site's own tools — the full NT Greek vocabulary (5,440 entries)
  and full OT Hebrew vocabulary (8,418 entries), 13,858 total — each with
  a Strong's Concordance definition and, where one exists, the matching
  classical lexicon entry in full: Brown-Driver-Briggs (Hebrew) or
  Abbott-Smith (Greek). Sources:
  - Strong's definitions: [openscriptures/strongs](https://github.com/openscriptures/strongs), **CC BY-SA**.
  - BDB text + the Strong's-to-BDB bridge: [openscriptures/HebrewLexicon](https://github.com/openscriptures/HebrewLexicon), public domain (1906 print edition). Where a Strong's number has more than one BDB homograph root, the lowest-lettered ("aug") cross-reference is used as the primary sense.
  - Abbott-Smith text: [translatable-exegetical-tools/Abbott-Smith](https://github.com/translatable-exegetical-tools/Abbott-Smith), public domain (1922 print edition). Abbott-Smith's XML tags each entry with its own Strong's number(s) directly. A "SYN.:" cross-reference note some print entries carry couldn't be reliably reconstructed from the XML alone and is omitted from a small number of entries.

- **`word-index.json`** — a concordance index over every NT book: every
  content word (verb / noun / adjective / adverb — function words
  filtered out), keyed by Strong's number, with every occurrence as a
  `{chapter, verse, wordIndex, book}` reference back into that book's own
  JSON file.

- **`word-index-hebrew.json`** — the same concordance shape, over every OT
  book (kept as a separate file/tool tab from the Greek one — different
  language, different Word Study screen).

## License

This repo's own compiled/merged JSON is released **CC BY 4.0**, matching its
primary source (Macula). Attribution for the underlying works belongs to the
sources listed above, not to this repo.

## Used by

The interlinear popup, Word Study, and Entity Explorer tools at
[jayms.com](https://jayms.com).
