# interlinear-data

Word-level Greek/Hebrew interlinear data and a Strong's/BDB/Abbott-Smith
lexicon, hosted for the interactive Bible tools on [jayms.com](https://jayms.com).
Fetched live by the page's own JavaScript at `raw.githubusercontent.com` —
nothing here is a database or a service, just static JSON.

## Files

- **`luke.json`** — all 24 chapters of Luke, word-by-word: Greek text, lemma,
  gloss, full morphology, Strong's number, Louw-Nida domain. Source:
  [Clear-Bible/macula-greek](https://github.com/Clear-Bible/macula-greek)
  (SBLGNT), **CC BY 4.0**.

- **`lexicon.json`** — every Strong's number used across `luke.json` and the
  site's Genesis 1:1 sample, each with a Strong's Concordance definition and,
  where one exists, the matching classical lexicon entry in full:
  Brown-Driver-Briggs (Hebrew) or Abbott-Smith (Greek). Sources:
  - Strong's definitions: [openscriptures/strongs](https://github.com/openscriptures/strongs), **CC BY-SA**.
  - BDB text + the Strong's-to-BDB bridge: [openscriptures/HebrewLexicon](https://github.com/openscriptures/HebrewLexicon), public domain (1906 print edition).
  - Abbott-Smith text: [translatable-exegetical-tools/Abbott-Smith](https://github.com/translatable-exegetical-tools/Abbott-Smith), public domain (1922 print edition).

- **`word-index.json`** — a concordance index over `luke.json`: every content
  word (verb / noun / adjective / adverb — function words filtered out),
  keyed by Strong's number, with every occurrence as a `{chapter, verse,
  wordIndex}` reference back into `luke.json`. No text is duplicated between
  the two files.

## License

This repo's own compiled/merged JSON is released **CC BY 4.0**, matching its
primary source (Macula). Attribution for the underlying works belongs to the
sources listed above, not to this repo.

## Used by

The interlinear popup, Word Study, and Entity Explorer tools at
[jayms.com](https://jayms.com).
