# CHLORA — Documentation Architecture Review
**Scope:** Full audit of the 15-document library (00–14), evaluated as the
permanent source of truth for a multi-year production.
**Reviewer role:** Documentation architecture only. No canon, story, biology,
or gameplay content is evaluated on its creative merits.

This library is a substantial improvement over a flat-bible structure: every
document now carries a Purpose statement, an explicit Scope ("does define" /
"does not define"), a Tier, and a Related Documents footer. That framework is
the correct foundation. The findings below are about where the *content*
hasn't yet caught up to the *rules* the documents themselves already state.

---

## 1. Overall Architecture

**Hierarchy is logical and explicit.** Development Guide (12) states the
precedence order (Constitution → Canon Bible → Reference → Support →
conversation history) and a Foundation/Reference/Support tier grouping that
correctly accounts for all 15 documents with no gaps or duplicates. This is
a genuinely good piece of architecture — most indie projects never write this
rule down at all. **[No action needed — noted as a strength.]**

**Finding A — Scope conflict between Character Bible and Image Bible.**
*Priority: Critical*
Character Bible's own Scope section lists **"Visual identity guidelines"**
as something *it* defines. Image Bible's Purpose claims it defines **"the
visual language of Chlora"** in general, with no carve-out excluding
character-specific visual rules. Both documents therefore believe they own
Chlora's visual identity, and both contain near-identical rules as a result
(bob haircut, hair behavior pre/post-activation, symbiont bioluminescence —
worded almost identically in Character Bible's "Visual Identity" subsection
and Image Bible's "IMG-001" entry). This is not simple duplication (§2) —
it's an unresolved ownership question at the *scope-definition* level, and
trimming the repeated text won't fix it permanently until one document's
scope is narrowed. Recommend Character Bible's scope keep only a
one-line *identity summary* (e.g. "practical, exploration-ready") and defer
all production-level visual rules to Image Bible's IMG-001 entry.

**Would I merge any documents?**
No merges are necessary at the current stage. Character Bible and Culture
Bible were clearly split apart deliberately last revision (Character = *who
people are*, Culture = *how society lives*) and the split mostly works now —
see §2 for the residual overlap that remains.

**Would I split any documents?**
Not yet — but Bestiary (05) and Story Bible (09) are architected as single
files that will not survive the stated long-term scale (500+ organisms, 200+
pages). See §7 for the specific recommendation; flagging here because it's
an architecture decision, not just a content fix.

**Does every concept have one authoritative home?**
Mostly yes in principle (Glossary owns terms, Canon Bible owns facts,
specialized bibles own elaboration). In practice, several facts are still
fully re-explained rather than referenced — see §2.

---

## 2. Ownership — Where the Same Information Still Lives in Multiple Files

| # | Duplicated content | Appears in | Recommended sole owner | Priority |
|---|---|---|---|---|
| 1 | "The Edge is not a physical wall / force field / barrier" | Canon Bible, Glossary, World Bible, Biology Bible (4×) | **Canon Bible** (it's a fact, that's Canon Bible's job). Glossary should drop the justification clause and keep only a neutral definition. World/Biology Bibles should reference Canon Bible instead of restating. | **High** |
| 2 | "Skyhook is entirely mechanical / aerospace-engineered" | Canon Bible, World Bible, Image Bible (IMG-002), Glossary | **Canon Bible** for the fact; **World Bible** for physical characteristics; **Image Bible** should reference both rather than re-assert "entirely mechanical" as its own rule | Medium |
| 3 | "Hair behaves naturally until symbiont activation" (near-verbatim) | Character Bible (Visual Identity), Image Bible (IMG-001) | **Image Bible** — this is a production visual rule, not a character-role fact | High (tied to Finding A above) |
| 4 | Symbiont dormant/active mechanism | Canon Bible, Biology Bible, Glossary, Character Bible, Image Bible (5×) | **Biology Bible** for mechanism, **Canon Bible** for the bare fact, **Glossary** for term only | Medium |
| 5 | "Primarily ecological rather than martial/a weapon" (combat framing) | Canon Bible, Biology Bible, Game Design Document | **Canon Bible** for the fact; **GDD** for the gameplay implication (encounter design). Biology Bible's restatement adds nothing new and should be cut to a cross-reference. | Medium |
| 6 | Custodian duties list (infrastructure, archives, life-support…) | Character Bible (full list), Culture Bible (abbreviated restatement) | **Character Bible** (structural facts); Culture Bible should reference it and speak only to *cultural meaning* | Low |
| 7 | Origin-of-symbiont-via-Pickers | Character Bible, Story Bible | **Story Bible** ("Before the Game") — Character Bible's Pickers entry should link out rather than restate the incident | Low *(this is already much improved vs. the prior draft — only 2 files now, not 3)* |

**General rule to apply going forward:** when two documents assert the same
sentence, the one whose *stated Scope* most specifically owns that fact
should keep it, and the other should replace the sentence with a
cross-reference. Development Guide's own principle — *"When in doubt, move
information rather than copy it"* — already says this; §2 is simply the list
of remaining places that principle hasn't been applied yet.

---

## 3. Cross-References — Where a Link Should Replace an Explanation

- **Add "10 — Glossary" to every Reference-tier document's Related Documents
  list.** *(Priority: High)* Right now, only Canon Bible links to the
  Glossary. World Bible, Biology Bible, Bestiary, Character Bible, Culture
  Bible, Game Design Document, Story Bible, and Image Bible all use
  Glossary-defined terms constantly but none of them link to it. This is a
  one-line fix per file with outsized navigational value.
- Replace Biology Bible's "Primarily an ecological interface rather than a
  weapon" with "*see Canon Bible — The Symbiont*." (Medium)
- Replace World Bible's and Biology Bible's "not a physical wall or force
  field" clauses with "*see Canon Bible — The Edge*." (High, pairs with §2.1)
- Character Bible's Pickers section: replace the origin-story sentence with
  "*see Story Bible — Before the Game*." (Low)
- Design Journal's symbiont-naming entry (the "suit" → "symbiont" decision)
  would benefit from a link to the Glossary's "Symbiont" entry, since that's
  the terminology the decision established. (Low)

---

## 4. Missing Documentation

**Finding B — No top-level index or README exists.**
*Priority: High*
There are 15 numbered documents and no document that tells a new reader what
order to read them in, or gives a 60-second summary of the whole set. (The
Development Guide comes closest, but its purpose is contributor workflow,
not orientation.) Given the explicit "inherited by another developer in five
years" framing, this is the single most impactful cheap addition available:
a short, unnumbered `README.md` — or a `00a` index — listing every document,
one sentence each, and a suggested reading order for new contributors
(likely: Constitution → Canon Bible → Glossary → then the Reference tier).

**Finding C — No unique-ID convention for named entities.**
*Priority: High*
Nowhere in the library is there a rule for giving organisms, characters, or
locations a stable identifier independent of their (mutable) display name.
This matters little today with a handful of named entities, but at 500+
organisms and dozens of characters, renames become expensive and
cross-references (art files, future code, localization keys) become
ambiguous without one. This is far cheaper to define now than to retrofit
later. Natural home: a new short section in the Development Guide, not a
whole new document.

**Finding D — No changelog exists, and it isn't clear whether that's
intentional.**
*Priority: Medium*
The Development Guide's Release Workflow ends with "tag a new project
version in Git" and states "Git records document history," which implies git
history is meant to substitute for a changelog. That's a defensible choice,
but it should be stated as a deliberate decision (ideally in the Development
Guide itself) rather than left implicit — otherwise a future contributor may
reasonably assume a changelog was simply lost.

**Other gaps, lower urgency (flagging only since asked to identify all
materially useful missing documentation):**
- A **Writing/Voice Style Guide** for in-game text (dialogue tone,
  jargon-introduction rules) will eventually be needed once Story Bible's
  planned "Dialogue notes" mature — not needed yet. *(Low)*
- An **Asset naming/pipeline conventions** note (filenames, folder layout for
  sprites/audio) will matter once the Art Backlog in the Production Roadmap
  starts producing files. *(Medium — pairs naturally with Finding C.)*

---

## 5. Internal Consistency

- **Finding E — Glossary entries occasionally state facts, not definitions.**
  *Priority: Medium.* The Glossary's own Purpose section draws a clean line:
  *"The Glossary defines what a term means, while the Canon Bible establishes
  what is true about it."* Its own "The Edge" entry then adds *"It is not a
  physical wall or force field"* — a truth-claim, not a definition — which
  violates the rule the document sets for itself. Worth fixing precisely
  because the Glossary is the document every cross-reference in this report
  points to; it needs to be the most disciplined file in the set.

- **Heading capitalization doesn't match the Glossary's own Naming
  Conventions.** *Priority: Medium.* The Naming Conventions list distinguishes
  terms where "The" is part of the proper noun (**The Edge, The Wilds, The
  Outlier**) from terms where it isn't (**Skyhook, Symbiont, Frozen,
  Custodians, Pickers**). Section headings elsewhere don't respect this:
  Character Bible and Culture Bible both use "# The Frozen" and "# The
  Custodians," and Canon Bible uses "# The Symbiont" — treating all three as
  if "The" belonged to the proper noun, which the Glossary says it doesn't.
  ("# Pickers," by contrast, is used correctly everywhere.) Small, mechanical
  fix; worth doing precisely because it's the kind of drift that compounds
  over years of new contributors copying existing headings.

- **No controlled vocabulary for the `Status` and `Tier` metadata fields.**
  *Priority: Low.* Status values in use: `Authoritative`, `Authoritative
  Reference`, `Living Reference`, `Living Document` — four values with no
  defined distinction between, e.g., "Living Reference" (Bestiary, Story
  Bible) and "Living Document" (Design Journal, Development Guide, Research
  Library, Production Roadmap). Similarly, `Tier` values are more granular
  per-document (Core Canon, Culture, Characters, Biology, Biology Reference,
  Game Design, Narrative…) than the three-bucket Foundation/Reference/Support
  model the Development Guide uses to organize the whole set. Neither is
  wrong, but neither is defined anywhere, which means new documents will
  guess. Recommend the Development Guide gain a short "Status values" and
  "Tier values" legend.

- **Resolved since last pass, worth confirming:** the earlier "suit" vs.
  "symbiont" terminology conflict (Image Bible previously used "Suit" as a
  proper-noun visual term, which contradicted Canon Bible's explicit "not a
  technological power suit" rule) is no longer present — Image Bible's
  current IMG-001 entry uses "Symbiont" throughout, and the Design Journal's
  one use of *"suit"* is clearly historical/rationale framing, not live
  terminology. No further action needed.

---

## 6. Documentation Quality

| Doc | Rating | Why |
|---|---|---|
| 00 Project Constitution | **Excellent** | Stays entirely philosophical, never leaks into fact/story/system territory, gives every other document a clear standard to be evaluated against. |
| 01 Canon Bible | **Good** | Now genuinely terse and fact-only (a major improvement over restating full explanations). Held back only by the residual "not a wall or force field"-style clauses that duplicate Glossary/World Bible language. |
| 02 Image Bible | **Good** | Well organized (Philosophy → Approved References → Future Targets → Checklist), but IMG-001's overlap with Character Bible's Visual Identity section (Finding A) is a real ownership problem, not just a stylistic one. |
| 03 World Bible | **Good** | Clean geography/environment focus, but repeats Edge/Skyhook facts Canon Bible already owns instead of building past them. |
| 04 Biology Bible | **Good** | Strong, tight philosophy section; "Chlora's Symbiont" restates Canon Bible almost verbatim instead of adding biology-specific depth beyond what's already established as fact. |
| 05 Bestiary | **Excellent** *(at current scale — see §7)* | Clear philosophy, well-differentiated lineages vs. ecological roles (this correctly avoids the taxonomy confusion a flatter version of this document could have had), and a genuinely usable Standard Species Template. |
| 06 Character Bible | **Good** | Clean role/philosophy sections; the Visual Identity subsection is the one piece that doesn't belong here (Finding A). |
| 07 Culture Bible | **Good** | Nicely differentiated from Character Bible on *meaning* vs. *role*; minor residual overlap on Custodian duties. |
| 08 Game Design Document | **Good** | Clear pillars and loop; one restated Canon Bible fact ("primary role is ecological rather than martial") that could be a cross-reference instead. |
| 09 Story Bible | **Excellent** | The cleanest document in the set — no restated facts, entirely within its own lane, genuinely unique content (dramatic question, act structure, arc direction). A good model for what the others should look like. |
| 10 Glossary | **Needs Revision** | Not for writing quality — for violating its own stated Purpose by including truth-claims (Finding E). Because every other cross-reference recommendation in this report routes through the Glossary, its internal discipline matters disproportionately. |
| 11 Design Journal | **Excellent** | Does exactly what it claims, chronologically, without drifting into fact or story territory. Another good model document. |
| 12 Development Guide | **Good** | The single most valuable structural addition in the library — but it should own the still-missing controlled vocabularies (Status/Tier) and the explicit git-vs-changelog policy statement (Finding D). |
| 13 Research Library | **Good** | Sensible categories and a usable workflow; currently has no actual sources logged yet, which is expected at this stage rather than a flaw. |
| 14 Production Roadmap | **Good** | Clear workflow and backlog structure; doesn't reference Canon Bible/Constitution in its Related Documents despite being fully downstream of them. |

---

## 7. Long-Term Scalability

Assuming 500+ organisms, 200+ pages of story, dozens of characters, and years
of development, two specific architecture decisions will break, and one
process gap will compound painfully if not addressed early.

**Bestiary (05) — Critical.** A flat single-file bestiary with a 12-field
Standard Species Template cannot hold 500 entries in any usable way: it
becomes unreviewable in pull requests, unsearchable at a glance, and merge
conflicts become constant once more than one person edits it. Recommend
splitting into one file per organism (or per lineage-family) under a
`/bestiary/` directory once entries exceed roughly 20–30, with `05_Bestiary.md`
becoming the index + philosophy + template reference it largely already is.

**Story Bible (09) — High.** The same failure mode applies at 200+ pages:
"chapter breakdowns, scene outlines, emotional beats, dialogue notes" cannot
live in one file at that volume. Recommend the same pattern: Story Bible
stays as the structural overview (what exists today), with a `/story/`
directory holding one file per Act/Chapter as they're written.

**Character Bible (06) — Medium-High.** "Dozens of characters" is
manageable in one file *if* kept to role-summary level, but the document's
own "Future Character Entries" section promises full biographies, dialogue
notes, and concept art references per character — which will bloat the file
the same way. Recommend splitting into per-character files once the named
cast exceeds roughly 10–15 individuals, with Character Bible remaining the
roster/index plus the core institutional entries (Frozen, Custodians,
Pickers, Researchers).

**Process gap — Medium.** None of the above splits will stay consistent
unless the Glossary is updated every time a new organism, character, or
location is named. The Development Guide's Canon Workflow currently lists
"Canon Bible update → Related document updates" but doesn't explicitly
require a Glossary update as its own checklist step. At low volume this is
easy to remember; at 500+ named entities it won't be. Recommend making
"Update Glossary" an explicit, unskippable step in the Canon Workflow.

**Planning note:** none of this needs to be built today — the current
single-file structure is completely appropriate for the project's present
size. The recommendation is to decide the split/ID convention *now*, while
there are only a handful of entries to migrate, rather than after 500 exist.

---

## 8. Professional Comparison

*(Documentation architecture only — not a comparison of the game itself.)*

This library's **process and philosophy layer is already close to
professional-grade**: an explicit precedence hierarchy, a canon-approval
workflow (Proposal → Discussion → Approval → Canon update → related-document
update → journal entry), scope statements on every document, and a
single-source-of-truth principle stated in the Constitution itself. Many
professional teams take years to formalize documentation discipline this
clearly; most indie projects never do.

Where this diverges from typical studio practice is **tooling and scale
infrastructure**, not process:

- Professional studios managing hundreds of bestiary/character entries
  typically move that content into a wiki or lightweight structured database
  (Notion, Confluence, or a custom tool) rather than flat Markdown files —
  specifically for search, backlinks, and per-entry review status. The
  current Markdown-in-Git approach is a very reasonable choice at this stage
  (portable, diffable, tool-agnostic) and doesn't need to change yet, but
  it's the layer most likely to need re-architecting at the stated long-term
  scale (§7).
- Professional teams usually assign a **named owner per document/domain**
  (a lore lead signs off on Canon Bible changes, an art director on the
  Image Bible, etc.). This library has an approval *process* but no
  assigned *roles* — appropriate for a small/solo team today, worth
  revisiting if the team grows.
- Given the project already lives in Git, a lightweight **automated
  consistency check** (a script flagging near-duplicate paragraphs across
  files, or verifying every Related Documents link is bidirectional) is a
  natural, low-effort next step that mirrors what larger teams build once
  manual audits like this one become too slow to run by hand each time.

**Overall:** the documentation *discipline* here is ahead of where most
projects this size are. The gap to close is architectural preparation for
scale (file-splitting conventions, unique IDs, a controlled metadata
vocabulary) rather than anything about how the team thinks about or
organizes their canon.

---

## Priority Summary

| Priority | Findings |
|---|---|
| **Critical** | Character Bible / Image Bible visual-identity scope conflict (§1, §2.3); Bestiary single-file structure won't survive 500+ organisms (§7) |
| **High** | "Edge is not a wall" repeated in 4 files (§2.1); Glossary not cross-referenced by any Reference-tier document (§3); no top-level README/index exists (§4-B); no unique-ID convention for named entities (§4-C); Story Bible single-file structure won't survive 200+ pages (§7) |
| **Medium** | Skyhook facts repeated across 4 files (§2.2); Symbiont dormant/active mechanism repeated across 5 files (§2.4); combat-framing repeated across 3 files (§2.5); Glossary stating facts instead of definitions (§5); heading capitalization contradicts Glossary's own naming conventions (§5); no changelog policy stated explicitly (§4-D); Character Bible split-readiness (§7); Glossary-update step missing from Canon Workflow (§7) |
| **Low** | Custodian duties restated in Culture Bible (§2.6); Pickers origin story in two files instead of one (§2.7); no controlled vocabulary for Status/Tier metadata (§5); Production Roadmap missing Constitution/Canon links (§6); future Style Guide and Asset-naming docs (§4) |

---

*This report evaluates documentation architecture only. No canon, story,
biology, or gameplay content was altered, interpreted, or expanded.*
