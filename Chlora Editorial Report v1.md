# CHLORA — Editorial Report
**Prepared as a documentation audit of v1.0/v1.1 design bible set (docs 00–16)**

This report does not add or alter canon. It identifies structural, referential,
and consistency issues across the existing 17 documents so an editorial pass
can address them deliberately.

---

## 1. Duplicated Information

The same explanatory paragraphs are independently written (not cross-referenced)
in multiple documents. This is the single biggest issue in the set — when one
of these gets updated later, the others will silently drift out of sync.

| Concept | Appears fully re-explained in |
|---|---|
| **The Edge** (not a wall/force field, invisible, advances/retreats) | Canon Bible (01), Biology Bible (04), World Bible (03), Glossary (10) |
| **The Skyhook** (mechanical, aerospace-engineered, orbital elevator) | Canon Bible (01), World Bible (03), Image Bible (02, IMG-002), Culture Bible (07, implicitly) |
| **The Wilds** (microbiology at macro scale, real-science-first) | Canon Bible (01), Biology Bible (04), World Bible (03), Image Bible (02, IMG-003), Bestiary (05) |
| **Symbiont dormant/active states** | Canon Bible (01), Biology Bible (04), Character Bible (06), Image Bible (IMG-001), Glossary (10) |
| **Origin story of the symbiont** (Edge advance → stranded → picker recovers it) | Canon Bible (01, "Origin of the Symbiont"), Character Bible (06, "Pickers"), Story Bible (09, "The Discovery") — told three times, nearly verbatim |
| **The Frozen** (preservation-focused ruling class, ideals list) | Character Bible (06), Culture Bible (07) |
| **The Custodians** (who they are, what they maintain) | Character Bible (06), Culture Bible (07) |
| **The Outlier** (transition zone definition) | Canon Bible (01), World Bible (03), Culture Bible (07), Glossary (10) |
| **Humanity vs. Wilds visual contrast table** | Design Principles (00, "Contrast Creates Identity") and Image Bible (02, "Visual Philosophy") — near-identical bullet lists |
| **"Combat is secondary" framing** | Biology Bible (04), Character Bible (06), Game Design Document (08) — each phrased slightly differently (see §2) |
| **Organism ecological-role taxonomy** | Biology Bible (04, "Organism Families") and Bestiary Foundation (05, "Ecological Roles") — overlapping but non-identical lists (see §3) |

**Recommendation:** Pick one canonical home per concept (see §6), reduce the
others to a sentence + cross-reference.

---

## 2. Contradictions & Risky Inconsistencies

Nothing here is a hard canon contradiction, but several items will confuse an
editor or a new writer joining the project:

- **"Suit" vs. "symbiont" terminology.** The Canon Bible is explicit: *"The
  organism is a living symbiont, not a technological power suit."* Yet the
  Image Bible's IMG-001 visual rules use the word **"Suit"** four times
  ("Dormant symbiont appears fossil-like," but also "**Suit** resembles living
  tissue rather than fabric or armor"). This is the one place where wording
  actively works against a stated canon rule rather than just duplicating it.
  Recommend replacing "suit" with "symbiont" (or "symbiotic form") throughout
  the Image Bible.

- **Authority hierarchy is stated two different ways.** The README says *"The
  Canon Bible is the authoritative source of truth. Conversation history is
  not."* AI Instructions rule 1 says *"Canon **documents** override
  conversation history"* (plural, unscoped). It's unclear whether "canon
  documents" means the Canon Bible alone, or any of the numbered bibles. Worth
  making explicit — especially since World/Biology/Character/Culture Bibles
  all currently contain declarative, canon-sounding statements themselves.

- **Combat-philosophy phrasing drifts across documents:**
  - Biology Bible: *"Combat is not its primary purpose"* (leaves room for secondary combat use)
  - Character Bible: *"rather than combat"* (reads as more exclusionary)
  - Game Design Document: *"Combat abilities remain secondary"* + later lists *"Optional combat systems"* under Future Systems
  
  These aren't contradictory, but three different strengths of the same claim
  exist with no single source. Recommend the GDD (the gameplay-authority doc)
  state this once, precisely, and have the others reference it.

- **Versioning/changelog gap.** Character Bible is tagged **v1.1**, but the
  Changelog (12) only documents an "Initial Documentation Release" and never
  mentions what changed between v1.0 → v1.1, or why. Per AI Instructions rule
  8 ("update existing documentation instead of creating contradictory
  versions"), every version bump should leave a Changelog trace — this one
  didn't.

---

## 3. Near-Duplicate Taxonomies Worth Reconciling

Biology Bible's planned **"Organism Families"** (Grazers, Filter feeders,
Predators, Colonial organisms, Decomposers, Pollinators, Symbionts, Keystone
species) and Bestiary Foundation's **"Ecological Roles"** (Primary producer,
Grazer, Filter feeder, Predator, Parasite, Mutualist, Pollinator, Decomposer,
Scavenger, Keystone species, Ecosystem engineer) are answering two different
questions — *evolutionary lineage* vs. *functional role* — but nothing in
either document says so. As written, a reader could reasonably assume
"Symbionts" (a family) and "Mutualist" (a role) are meant to be the same
thing, or wonder why the lists don't match. Recommend one sentence in each doc
clarifying the family/role distinction, and a cross-reference between them.

---

## 4. Missing Cross-References

- Character Bible's "Pickers" section tells the symbiont-discovery story
  inline instead of pointing to Story Bible §"The Discovery" / Canon Bible
  §"Origin of the Symbiont." Same for Culture Bible's "Pickers" section — a
  third retelling with no pointer to the other two.
- The Glossary defines "Image Bible" but no other document by name (not
  "Canon Bible," "World Bible," "Story Bible," etc.). Either extend the
  Glossary to index all 17 documents, or drop the one that's there — the
  current partial coverage looks accidental.
- Canon Bible entries have no link back to the **Design Journal**, which is
  the document that explains *why* each canon decision was made. A reader
  hitting "The Edge is not a physical wall" in the Canon Bible has no way to
  find the Design Journal entry explaining that reasoning unless they already
  know to look.
- World Bible's "Human Presence" section and Culture Bible's "Society"
  section cover the same ground (Skyhook-centered settlement, Outlier
  specialists) with no reference between them.
- Production Roadmap items have no links to the documents that will absorb
  the completed work (e.g., "Design grazer lineage" doesn't point to Biology
  Bible or Bestiary Foundation as the destination).

---

## 5. Terminology Inconsistencies

- **Symbiont naming drift**: "juvenile symbiotic organism," "juvenile
  symbiont," "the organism," "symbiont," and (per §2) "suit" are all used to
  refer to the same thing across different documents. The Glossary entry for
  "Symbiont" should be treated as the locked term, with the others
  normalized to it.
- **"The Wilds" description drift**: called an "ancient biological
  environment" (Glossary), "ancient biological ecosystem" (World Bible),
  "ancient biological phenomenon" (Story Bible, Culture Bible), and
  "persistent biological environment" (Biology Bible). Minor, but worth
  standardizing to one phrase since it recurs so often.
- **"Orbital skyhook/space elevator"** — this exact slash-construction phrase
  is repeated verbatim in at least three documents. It's consistent (good),
  but since it never varies, it's a good candidate to define once in the
  Glossary and shorten to just "Skyhook" everywhere else.

---

## 6. Suggested Ownership Model (who defines what)

To eliminate most of §1's duplication, each core concept could have exactly
one **defining** document, with all others reduced to a short reference line:

| Concept | Suggested sole owner | Everyone else does |
|---|---|---|
| The Edge, The Outlier, The Skyhook, The Wilds (one-paragraph definitions) | **Glossary** | Link to Glossary; don't redefine |
| Full descriptive/atmospheric detail of the above | **World Bible** | Reference World Bible section |
| Symbiont biology (dormancy, activation, function) | **Biology Bible** | Character Bible references it when discussing Chlora |
| Origin-of-symbiont incident | **Story Bible** ("The Discovery") | Canon Bible keeps a one-line fact; Character Bible's Pickers section links out |
| Frozen / Custodians — identity & structure | **Character Bible** | Culture Bible references, focuses only on *daily-life impact* |
| Combat philosophy | **Game Design Document** | Biology/Character Bibles get one linking sentence |
| Visual contrast philosophy (bullet lists) | **Image Bible** | Design Principles keeps only the *principle* ("Contrast Creates Identity"), not the repeated bullet list |

This turns the Canon Bible back into what its own header says it should be —
a fast, authoritative checklist — rather than a second full narrative
document competing with World/Biology/Story Bibles.

---

## 7. Sections That Should Move

- **Biology Bible → "Organism Families (Planned)"**: this is bestiary
  taxonomy, not biology-of-the-Wilds philosophy. Candidate to merge into
  Bestiary Foundation (05), which already owns ecological-role taxonomy.
- **Character Bible → Pickers' closing line** about the symbiont's discovery:
  trim to "see Story Bible" rather than restating the incident.
- **Design Principles → "Visual Philosophy" section**: nearly identical to
  Image Bible's "Visual Philosophy." Keep the *principle* in Design
  Principles, move the detailed bullet lists to Image Bible only.

---

## 8. Merge / Split Candidates

- **Character Bible (06) + Culture Bible (07)**: strong candidate for either
  a full merge into one "Society Bible," or — if kept separate — a hard scope
  split (Character Bible = *who/what these groups are*; Culture Bible = *how
  people live day-to-day*, with zero re-definition of the groups themselves).
  Right now they're two encyclopedic entries on the same subjects.
- **Canon Bible (01)**: currently mixes short canonical facts with full
  explanatory prose that duplicates World/Biology Bible content. Consider
  splitting it down to bullet-only canonical statements, moving the prose
  explanations to the relevant specialized bible.
- **Image Bible (02)**: general visual philosophy/checklist vs. entity-specific
  IMG-00X entries could be split into two sections/documents as the IMG-00X
  list grows — general philosophy is evergreen, entity entries will multiply.

---

## 9. Structural Recommendations Summary

1. Adopt the ownership model in §6 to kill most duplication at the source.
2. Add lightweight "See Also" lines at the bottom of sections instead of
   restating other documents' content.
3. Expand the Glossary to consistently index all 17 document names, or
   remove the one inconsistent entry that's already there.
4. Close the Character Bible v1.0→v1.1 gap in the Changelog, and treat every
   future version bump the same way going forward.
5. Clarify whether "canon documents" (AI Instructions, plural) means the
   Canon Bible alone or the full bible set — this affects how strictly an
   editor should treat World/Biology/Character/Culture Bible statements.
6. Standardize on "symbiont" terminology project-wide and eliminate "suit"
   from the Image Bible specifically, since it cuts against an explicit
   Canon Bible rule.
7. Distinguish "organism families" (lineage) from "ecological roles"
   (function) explicitly, wherever both taxonomies are discussed.

---

*This report covers structural/editorial issues only. No canon was created,
altered, or interpreted beyond what's already written.*
