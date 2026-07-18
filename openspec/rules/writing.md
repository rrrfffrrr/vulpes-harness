# Writing style

Prose rules for every artifact the harness generates, written for two readers:
a human scanning for an answer, and anyone (or any tool) searching the document.
These rules govern prose; diagram rules live in `diagrams.md`.

## Line breaks (semantic line breaks)

- Start each sentence on its own line.
  Break long sentences after clause boundaries (`,` `;` `:`).

  ```markdown
  The gateway rejects an expired token with `401 Unauthorized`.
  If the client then retries with a refreshed token,
  the gateway accepts the request and renews the session.
  ```

- A line break MUST NOT change the rendered output ([SemBr](https://sembr.org/)).
- Multi-sentence list items break into continuation lines (indented under the item); blockquotes continue with a `>` line.
- Where a literal line break is impossible - table cells, headings, inside a link or code span - keep to one short sentence or fragment instead.
  A cell that needs several sentences is prose in the wrong place: move it out of the table.
  Never fake a break with `<br>`.
- Why: sources stay readable, a grep hit returns a whole sentence, and document-version diffs stay sentence-scoped.

## Plain language

- One idea per sentence; keep sentences short.
- Active voice - name the actor ("the server rejects...", never "it is rejected").
- Present tense for current truth.
- Concrete values over vague ranges (`250 ms`, exact copy text - not "fast", "short").

## Scannable structure

- Lead with the conclusion: the first sentence of a document or section carries its main point (inverted pyramid).
- Front-load keywords: the first two words of a heading, list item, or table cell carry the meaning.
- Lists for parallel facts, tables for enumerable facts; prose only where reasoning is needed.
- Headings are sentence case, descriptive, and unique within the document.
  A heading names its subject; never a teaser.
- Keep paragraphs short; more than ~5 sentences is usually two paragraphs.

## Tables

- A table is a relation: one column per kind of fact, one value per cell (first normal form).
- Never pack a second fact into a cell with brackets or separators - `POST /orders`, not `POST /orders [paginated]`;
  a second fact gets its own column.
- A cell that wants a list marks a one-to-many link: repeat the row per value, as a database table would.
- A plural column heading (`Component(s)`) signals a packed cell: name the column singular and repeat rows.
- Keep cell text brief (ideally one line) and entries within a column parallel (all nouns, or all verb-first).

## Terminology

- One term per concept, one concept per term - same spelling and capitalization everywhere.
- Never rotate synonyms for the same thing; synonyms break search.
- Expand an acronym at first use - "long form (ACRONYM)" - and don't introduce an acronym used only once.
- Define a term once (glossary or first use) and use that exact form afterwards.

## Findability

- Write the noun, not the pronoun: "the session token", not "it" or "this value" - a search for the noun must find every statement about it.
- Quote literals verbatim in backticks (error copy, header names, `METHOD /path`, event names) so exact-match search works.
- Anchor with stable identifiers (G1.2, ADR-NNN, `POST /orders`) and repeat them; never "the above endpoint".
- Headings carry the words a reader would search for.

## Numbers, dates, units

- Dates and times in ISO 8601 (`YYYY-MM-DD`, `YYYY-MM-DDThh:mm:ssZ`).
- Every number carries its unit (`250 ms`, `64 px`, `10 MiB`); no bare numbers.

## Document language

- Declare the artifact language once per change (in its overview) and write every artifact in it.
- Do not mix languages mid-document, except verbatim quotes, code, and identifiers.

## References

Verified 2026-07-15; Tables entries verified 2026-07-18.

- Semantic Line Breaks: <https://sembr.org/>
- ISO 24495-1:2023 Plain language - governing principles: <https://www.iso.org/standard/78907.html>
- Google developer documentation style guide (CC BY 4.0): <https://developers.google.com/style>
- Microsoft Writing Style Guide (scannable content; one word per concept): <https://learn.microsoft.com/en-us/style-guide/welcome/>
- NN/g reading research: [How Users Read on the Web, 1997](https://www.nngroup.com/articles/how-users-read-on-the-web/) - [F-shaped pattern, 2017 update](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/) - [Inverted Pyramid, 2018](https://www.nngroup.com/articles/inverted-pyramid/) - [First 2 Words, 2009](https://www.nngroup.com/articles/first-2-words-a-signal-for-scanning/)
- GOV.UK clear titles (search-term-first): <https://guidance.publishing.service.gov.uk/writing-to-gov-uk-standards/writing-guidelines/clear-titles/>
- ISO 8601-1:2019 date/time format: <https://www.iso.org/standard/70907.html>
- E. F. Codd, A Relational Model of Data for Large Shared Data Banks, CACM 13(6) 1970 (first normal form): <https://dl.acm.org/doi/10.1145/362384.362685>
- Microsoft Writing Style Guide - Tables (brief, parallel cell entries): <https://learn.microsoft.com/en-us/style-guide/scannable-content/tables>
