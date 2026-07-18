# Structure rules

Structure rules for every document set the harness generates, and for the harness's own documents.
`writing.md` governs the prose inside a document and `diagrams.md` the diagrams;
this file governs the containers: what goes into them, where content lives, how containers are named, and when they split.

## Boundary - declare what is in and what is out

- Every container (document set, artifact, section, table) declares its scope: what belongs in it AND what is deliberately left out.
- An exclusion carries its reason - a conditional-artifact row reads `No` plus why, an event row reads `no response (why)`, a scope section has an Out list.
  A silent omission is a hole; an explicit exclusion with a reason is a design decision.
- Completeness comes from enumerating a closed list (interfaces, events, agents, roles) and accounting for every entry - never from writing what comes to mind.

## Place - different roles never share a home

- Separate the focal content, the supporting content, and the management content into different homes
  (the goal model vs the other models vs traceability; endpoints vs conventions vs traceability).
- Each fact has exactly one authoritative home; every other place references it by name or id instead of restating it.
- Classification markers and kind tags sit in a fixed slot at the START of the line, before the free text - never trailing after it, never mid-sentence.

## Growth - when a container overflows, split it at a seam

- Never stretch an overflowing container; split it.
  A cell that wants a list becomes repeated rows; a section that wants two subjects becomes two sections; a file that outgrows one sitting becomes a folder with one file per domain.
- Split along the content's own seams - domain, system boundary, perspective, likely-to-change decision - never along processing order or an arbitrary size cap.
- An artifact that accumulates entries without bound (scenarios, sequences, flows) ships the split from the start: it declares `<name>/index.md`, the index holds pointers only, and every entry lives in a per-domain file `<name>/<domain>.md`.
- Each split unit stays a coherent whole: small enough to reference on its own, large enough to read without hopping.

## Naming - the name states the role, the scope states the ownership

- Name a file or artifact by its ROLE: `overview.md`, `conventions.md`, `traceability.md`.
  The folder that contains it states whose it is.
- The same role recurring in different scopes reuses the same local name; qualify by scope in prose when disambiguation is needed (the backend conventions vs this file).
- Never encode the scope into the name - no schema-name or folder-name prefixes.

## Index - a hub holds pointers, never content

- An index document (`AGENTS.md`, `CLAUDE.md`, a folder README index) lists what exists, where it is, and when to read it; the content itself lives in dedicated role-named files.
- Adding content to a hub means extracting it into a file and leaving one pointer line behind.
- A pointer's "when to read this" hint is a comma-separated run of words or actions, not a prose sentence.

## References

Verified 2026-07-18.

- ISO/IEC/IEEE 29148:2018 Requirements engineering - required information items and their required contents: <https://www.iso.org/standard/72089.html>
- E. W. Dijkstra, On the role of scientific thought (EWD447), 1974 - the primary written source of "separation of concerns": <https://www.cs.utexas.edu/~EWD/transcriptions/EWD04xx/EWD447.html>
- D. L. Parnas, On the Criteria To Be Used in Decomposing Systems into Modules, CACM 15(12) 1972 - information hiding; decompose along difficult or likely-to-change decisions, not processing steps: <https://dl.acm.org/doi/10.1145/361598.361623>
- D. Thomas / A. Hunt, The Pragmatic Programmer, 20th Anniversary Edition, Topic 9 - DRY: "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system"; explicitly about knowledge, not only code: <https://media.pragprog.com/titles/tpp20/dry.pdf>
- E. Evans, Domain-Driven Design Reference, 2015 - Bounded Context (explicitly set boundaries, p. 2), Conceptual Contours (decompose along the domain's natural divisions, p. 27): <https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf>
- M. Fowler, Refactoring catalog (2nd edition companion) - the named split/extract/move operations: <https://refactoring.com/catalog/>
- E. F. Codd, A Relational Model of Data for Large Shared Data Banks, CACM 13(6) 1970 (first normal form - the cell-level split rule): <https://dl.acm.org/doi/10.1145/362384.362685>
- OASIS DITA 1.2 - topics as "the basic units of DITA content and the basic units of reuse", each containing "a single subject": <https://docs.oasis-open.org/dita/v1.2/os/spec/archSpec/topicover.html>
- OASIS DITA 1.3 - maps "consist of references to topics ... organized into hierarchies, groups, and tables" (hubs point, topics hold content); chunking splits and merges only at topic boundaries: <https://docs.oasis-open.org/dita/dita/v1.3/os/part1-base/langRef/base/map.html>, <https://docs.oasis-open.org/dita/dita/v1.3/os/part2-tech-content/archSpec/base/chunking.html>
- W3C Namespaces in XML 1.0 (Third Edition), 2009 - an expanded name is a (namespace name, local name) pair; the same local name recurs across scopes, disambiguated by qualification: <https://www.w3.org/TR/xml-names/>
