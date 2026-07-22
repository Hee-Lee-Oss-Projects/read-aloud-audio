# TASKS — read-aloud-audio

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Backlog for the `read-aloud-audio` good-deed project. Read alongside `PLAN.md` (same directory).

## How these tasks map to Hee-Lee Oss

Every task here becomes a **Task JSON** validated by `packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable, e.g. `read-aloud-audio-style-001` (the table's ID column).
- `title` — the task title.
- `project` — `"read-aloud-audio"` for all tasks.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (see each task).
- `lane` — `"donated"` for all tasks (the human runs their own agent / records their own voice; the
  CLI preps the workspace + submission and never runs headless). No `funded` tasks in this backlog,
  so `fundedBudgetUsd` is not required; were a funded task added, the schema's `if/then` would
  require `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["literacy","accessibility","open-culture","audio"]`.
- `riskTier` — `low | medium | high`. Low by default; **medium** for pronunciation-critical /
  foreign-language / synthetic-narration / children's content; **high** only for the gated
  high-stakes-instructional-text escalation (out of default flow).
- `urgent` — boolean (default `false`; nothing here is time-critical).
- `deliverable` — `pr | dataset | document | translation`. Published read-alongs / upstream
  submissions → `pr`; per-work records, lexicons, alignment sets → `dataset`; style guide / specs /
  checklists → `document`. (No item produces a `translation` deliverable — translation is out of scope.)
- `tokenEstimate` — `small | medium | large` (the table's Size column).
- `status` — `open | in-progress | review | delivered | done` (all start `open`).
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — task body fields.
- `requestor` — proposer/maintainer; `verifiedNeed` — **`false`** for delivery-dependent tasks until
  a distribution channel is secured (see PLAN "partner gap"); `true` only where the artifact is
  self-evidently useful and channel-independent (e.g. style guide, specs, record formats).
- `outputLicense` — MIT for code; `CC-BY-4.0` / `CC0-1.0` for docs & datasets; for read-alongs, the
  license compatible with the source text and host (PD/CC0/CC-BY/CC-BY-SA) per the consent record.

At production scale this project fans out: **one work (or chapter) = one task**, drawn from a
milestone-scoped, **channel-confirmed** batch (the `*-narrate-*` / `*-batch-*` tasks are the
templates for that fan-out).

---

## Milestone M0 — Foundation & cold-start

Prove one chapter can travel from an openly-licensed source to a **published, live, text-aligned
read-along**, with verified rights and recorded speaker consent.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| read-aloud-audio-style-001 | Author narration & pronunciation style guide v1 | writing | medium | low | document | — | Maintainer |
| read-aloud-audio-spec-001 | Author audio-quality spec v1 (LUFS / true-peak / noise floor / formats) | writing | small | low | document | — | Maintainer |
| read-aloud-audio-data-001 | Define per-work record + per-jurisdiction rights-verification format | data | small | low | dataset | — | Maintainer |
| read-aloud-audio-data-002 | Define speaker-consent & voice-provenance record format (human + synthetic) | design-spec | small | medium | document | — | Maintainer + Narration coordinator |
| read-aloud-audio-research-001 | Secure ≥1 distribution channel + host stance on AI-assisted/synthetic audio | research | medium | low | document | — | Maintainer + Steward |
| read-aloud-audio-research-002 | Validate per-jurisdiction PD/license rules for target sources | research | small | medium | document | — | Steward |
| read-aloud-audio-narrate-001 | Hand-produce cold-start read-along (1–3 chapters, hard paths covered) | data | large | medium | dataset | research-001 (channel gate), style-001, spec-001, data-001, data-002, research-002 | Pronunciation + audio QA |
| read-aloud-audio-pr-001 | Publish cold-start read-along upstream + measure alignment baseline | maintenance | medium | medium | pr | research-001, narrate-001 | Steward |

**Sequencing — channel-securing is a hard gate.** `research-001` blocks `narrate-001` and `pr-001`:
no narration, alignment, or publishing begins until ≥ 1 distribution channel is confirmed. If the
time-boxed effort confirms no channel, the project hits its **kill/pivot criteria** (next candidate
channel per PLAN's decision tree, or stop) rather than producing audio with nowhere to ship.

**Key task acceptance criteria**

- **read-aloud-audio-style-001** (narration & pronunciation style guide v1)
  - [ ] Defines diction, pacing, and prosody tuned for **literacy practice** (clear, unhurried,
        natural — not dramatized), and how to handle dialogue, verse/line breaks, and headings.
  - [ ] Specifies the **pronunciation-lexicon convention** (IPA and/or respelling) and which item
        classes must be flagged for review (proper nouns, foreign/archaic words, technical terms).
  - [ ] States the text-audio **fidelity rule** (read the text as published; no skipping, adding,
        substituting, abridging, or modernizing).
  - [ ] Includes a **content-suitability** section (curated age-appropriateness, neutral context note
        for dated content, non-partisan stance for civic texts).
  - [ ] Published, versioned, licensed CC-BY-4.0.

- **read-aloud-audio-data-002** (consent & voice-provenance record format)
  - [ ] Human-narration record captures: speaker name or pseudonym, consent to record + redistribute
        under the named open license, **AI-processing-for-alignment/QA-only (no training/cloning)**
        clause, age confirmation (or guardian consent), and a documented **right to withdraw**.
  - [ ] Synthetic-narration record captures: model, version, voice id, **voice license**, and a
        **talent-consent-to-synthesis attestation**; output is marked `AI-synthesized`.
  - [ ] Forbids any record describing a clone/imitation of an identifiable real person.
  - [ ] Specifies **secure storage + reference-only** (no raw PII inlined in public records/logs) and
        a takedown/disposition procedure for withdrawals.
  - [ ] Published as a versioned spec (CC-BY-4.0); riskTier `medium` (consent/PII sensitivity).

- **read-aloud-audio-research-001** (secure distribution channel)
  - [ ] Evaluates candidate channels in priority order (open publisher/repo → open-audiobook
        host/Internet Archive → Wikisource → named literacy partner) with each one's acceptance
        posture, and applies PLAN's decision tree to pick the first to pursue.
  - [ ] Identifies ≥ 1 concrete channel confirmed to accept human-reviewed, openly-licensed,
        consent-backed read-alongs (EPUB 3 Media Overlays + open audio).
  - [ ] Documents the host's stance on **AI-assisted alignment** and on **AI-synthesized narration**.
  - [ ] Produces a **pre-engagement exit artifact**: statement of intent, confirmation the format +
        cadence are welcome, and an agreed volume ramp.
  - [ ] Records the channel's required **output license** and attribution/credit format.
  - [ ] States the time-box and the kill/pivot criteria if no channel is secured.
  - [ ] On success, flips `verifiedNeed=true` for tasks targeting that channel.

- **read-aloud-audio-narrate-001** (cold-start read-along)
  - [ ] Source text rights verified **per target jurisdiction** (PD or CC), with edition,
        attribution, evidence, and retrieval date recorded before any narration.
  - [ ] A signed **speaker-consent/provenance record** exists for the voice (or synthetic
        provenance + talent consent for any synthetic segment); output **labeled** human/synthetic.
  - [ ] The unit exercises the hard paths: ≥ 1 passage with proper nouns/foreign or archaic words
        (lexicon + pronunciation review), structure beyond flat prose, and — if synthetic is in M0
        scope — one synthetic segment exercising labeling/provenance.
  - [ ] Audio meets the audio-quality spec (loudness/true-peak/noise floor; no clipping); lossless
        master retained; Opus + MP3 derived.
  - [ ] Forced alignment produces EPUB 3 Media Overlays (SMIL) + WebVTT + JSON; **0 text-audio
        fidelity defects**; flagged pronunciation items cleared by a skilled reviewer; alignment
        within tolerance after review.

- **read-aloud-audio-pr-001** (publish + baseline)
  - [ ] The read-along is **published upstream, live, and playable** (additive; not overwriting a
        better existing version), with license + attribution + consent reference + provenance + label.
  - [ ] Alignment-accuracy **reference set** established and the unit's median onset error recorded.
  - [ ] Baseline for the chosen channel/collection recorded (what exists vs. missing) for later deltas.

**M0 Definition of Done:** style guide v1 + audio-quality spec v1 + consent/rights record formats
published; ≥ 1 distribution channel confirmed; ≥ 1 read-along (1–3 chapters) published, live, and
playable with full rights + consent + provenance and human/synthetic label; alignment reference set
established and baseline error measured; zero rights/consent violations.

---

## Milestone M1 — Pipeline & adapters

Turn the manual slice into a repeatable, policy-compliant pipeline.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| read-aloud-audio-adapter-001 | Forced-alignment adapter (audio↔text → SMIL/WebVTT/JSON) | code | large | medium | pr | data-001, narrate-001 | Maintainer |
| read-aloud-audio-adapter-002 | Audio-mastering adapter (loudness/peak/noise; FLAC→Opus/MP3) | code | medium | low | pr | spec-001 | Maintainer |
| read-aloud-audio-pipeline-001 | Per-jurisdiction rights-verification + consent-record gate | code | medium | medium | pr | data-001, data-002, research-002 | Steward |
| read-aloud-audio-pipeline-002 | Text segmentation + pronunciation-lexicon tooling | code | large | medium | pr | style-001, data-001 | Maintainer |
| read-aloud-audio-adapter-003 | Publish adapter for the secured channel (submission/PR/deposit) | code | large | medium | pr | research-001, data-001 | Steward |
| read-aloud-audio-doc-001 | Reviewer workflow + 4-axis QA rubric (fidelity/pronunciation/audio/alignment) + error taxonomy | writing | small | low | document | style-001, spec-001 | Maintainer |
| read-aloud-audio-batch-001 | Produce + publish ~10 chapters (first repeatable run) | data | large | medium | pr | adapter-001, adapter-002, adapter-003, pipeline-001, pipeline-002, doc-001 | Reviewer rotation |

**Key task acceptance criteria**

- **read-aloud-audio-pipeline-001** (rights + consent gate)
  - [ ] Rejects any source text whose rights are not verifiably PD (per target jurisdiction) or a
        clear open license ("unknown / PD-US-only without scoping = excluded").
  - [ ] Blocks narration unless a valid signed consent / synthetic-provenance record is linked.
  - [ ] Records rights + attribution + source + retrieval date and the consent reference per work;
        emits an auditable decision log with **no secrets and no raw PII**.

- **read-aloud-audio-adapter-001** (alignment adapter)
  - [ ] Wraps the chosen forced aligner behind a neutral interface; emits EPUB 3 Media Overlays
        (SMIL), WebVTT, and JSON at the configured granularity (word/sentence).
  - [ ] Measures onset/offset error against the alignment reference set and reports it.
  - [ ] Flags low-confidence segments for human alignment review rather than silently shipping drift.

- **read-aloud-audio-adapter-002** (audio-mastering adapter)
  - [ ] Normalizes to the spec's integrated-loudness target, enforces true-peak ≤ −1 dBTP, checks
        noise floor, and rejects clipped audio; retains the lossless master and derives Opus + MP3.
  - [ ] Emits a per-file quality report (LUFS, true-peak, noise floor, duration).

- **read-aloud-audio-batch-001** (first ~10-chapter run)
  - [ ] ≥ 10 chapters published upstream; acceptance rate and median alignment error measured.
  - [ ] Every item passed rights gate → consent gate → fidelity/pronunciation/audio/alignment review →
        publish adapter, with the human/synthetic label present.

**M1 Definition of Done:** alignment + mastering adapters and ≥ 1 publish adapter live and
policy-compliant; rights+consent gate, segmentation, and lexicon tooling operational; reviewer
workflow + 4-axis rubric documented with ≥ 2 reviewers (incl. ≥ 1 with pronunciation/language skill)
onboarded; ≥ 10 chapters published with measured acceptance + alignment accuracy; zero
rights/consent violations.

---

## Milestone M2 — Controlled scale

Complete meaningful, learner-usable read-alongs in 1–2 works/collections, quality held.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| read-aloud-audio-batch-002 | Scale to ≥50 chapters published across ≥2 works/collections | data | large | medium | pr | batch-001 | Reviewer rotation |
| read-aloud-audio-doc-002 | Pronunciation specialist guide (foreign-language / names / archaic terms) | writing | medium | medium | document | style-001 | Language specialist |
| read-aloud-audio-research-003 | Beneficiary validation with literacy educators / learners | research | small | low | document | batch-001 | Maintainer + Partner |
| read-aloud-audio-data-003 | Quality metrics dataset (acceptance, alignment error, pronunciation rate, consent/rights completeness) | data | small | low | dataset | batch-001 | Maintainer |

**Key task acceptance criteria**

- **read-aloud-audio-batch-002** (scale run)
  - [ ] ≥ 50 chapters published upstream and live across ≥ 2 works/collections.
  - [ ] Acceptance rate ≥ 85%; pronunciation error rate ≤ 2/1,000; **0** fidelity defects;
        audio-quality conformance ≥ 95%; alignment within tolerance.
  - [ ] 100% consent + 100% per-jurisdiction rights completeness; zero violations; 100% labeled.

- **read-aloud-audio-research-003** (beneficiary validation)
  - [ ] ≥ 1 literacy educator and/or learner reviews a read-along per work/collection and confirms
        usability (clarity, pacing, highlight tracking).
  - [ ] Findings feed back into the style guide / reviewer rubric.

**M2 Definition of Done:** ≥ 50 chapters across ≥ 2 works/collections at ≥ 85% acceptance with the
quality bars met; ≥ 1 beneficiary validation per work/collection; quality metrics dashboarded; zero
rights/consent violations.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| read-aloud-audio-adapter-004 | Additional distribution-channel adapter (2nd host) | code | large | medium | pr | New channel; needs secured partner |
| read-aloud-audio-tts-001 | Gated synthetic-voice adapter (clearly-licensed, talent-consented, labeled) | code | medium | medium | pr | Only if synthetic path enabled; labeling + provenance mandatory |
| read-aloud-audio-pipeline-003 | Outcome-tracking dashboard (published/live, accuracy, completeness) | code | medium | low | pr | Sustainability metric |
| read-aloud-audio-i18n-001 | Multilingual read-alongs (sibling-project assessment) | research | medium | medium | document | Overlaps open-pronunciation-audio / decodable-readers |
| read-aloud-audio-research-004 | High-stakes-instructional-text escalation path (expert sign-off / "not advice") | research | small | high | document | Defines credentialed-expert gate or decline rule |
| read-aloud-audio-maint-001 | Adapter/aligner maintenance vs host API + standards changes | maintenance | medium | low | pr | Ongoing post-delivery |
| read-aloud-audio-doc-003 | Narrator onboarding + consent-process handbook | writing | small | medium | document | Supports narration coordinator at scale |

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task. `verifiedNeed` is `true` here: a published,
openly-licensed narration & pronunciation style guide is a self-evidently useful artifact and does
not depend on a distribution channel being secured (unlike the `narrate`/`pr` tasks, which are
`false` until M0's channel is confirmed).

```json
{
  "id": "read-aloud-audio-style-001",
  "title": "Author narration & pronunciation style guide v1",
  "project": "read-aloud-audio",
  "type": "writing",
  "lane": "donated",
  "priority": "high",
  "domain": ["literacy", "accessibility", "open-culture", "audio"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "Openly-licensed and public-domain texts (Project Gutenberg, Standard Ebooks, Wikisource, OpenStax, open children's books) mostly exist as text only, with no clear, text-aligned narration. Listening-while-reading with synchronized word/sentence highlighting is one of the best-evidenced supports for emergent, struggling, print-disabled, and language-learning readers. Before any work is narrated at scale across many parallel donated sessions, the project needs a single versioned style guide so narration is consistent, clear, faithful to the source, and tuned for literacy practice rather than dramatized performance.",
  "objective": "Write and publish version 1 of the narration & pronunciation style guide that all narrate/batch tasks will follow.",
  "acceptanceCriteria": [
    "Defines diction, pacing, and prosody tuned for literacy practice (clear, unhurried, natural; not dramatized) and how to handle dialogue, verse/line breaks, and headings.",
    "Specifies the pronunciation-lexicon convention (IPA and/or respelling) and which item classes must be flagged for pronunciation review (proper nouns, foreign/archaic words, technical terms).",
    "States the text-audio fidelity rule: read the text as published with no skipping, adding, substituting, abridging, or modernizing.",
    "Includes a content-suitability section: curated age-appropriateness, a neutral provenance/context note for dated content (not silent editing), and a non-partisan stance for civic texts.",
    "Is published, versioned, and licensed CC-BY-4.0."
  ],
  "resources": [
    "C:\\code\\hee-lee-oss\\planning\\projects\\read-aloud-audio\\PLAN.md",
    "C:\\code\\hee-lee-oss\\governance\\proposals\\read-aloud-audio.md",
    "EPUB 3 Media Overlays (SMIL) specification",
    "W3C WebVTT specification",
    "DAISY / accessible-publishing read-along guidance"
  ],
  "output": "A versioned style-guide document (style-guide/narration-pronunciation-style-guide.md), CC-BY-4.0, covering diction/pacing/prosody for literacy, dialogue/verse/heading handling, the pronunciation-lexicon convention and flagging rules, the text-audio fidelity rule, and content-suitability guidance.",
  "requestor": "jdev1977",
  "verifiedNeed": true,
  "outputLicense": "CC-BY-4.0"
}
```

---

## Generated task index

> Generated by Hee-Lee Oss task-decomposition agent · 2026-06-29 · Branch: hee-lee-oss/task-decomposition
> Seed file kept as-is. 25 new task files generated. 26 total (including seed).
> Fan-out: none — no explicitly enumerated dimensions in the backlog (channel not yet secured; narrate/batch tasks are templates only).

| File | Title | Milestone | Type | Priority | verifiedNeed |
|---|---|---|---|---|---|
| [read-aloud-audio-style-001.json](tasks/read-aloud-audio-style-001.json) | Author narration & pronunciation style guide v1 | M0 | writing | high | true |
| [read-aloud-audio-spec-001.json](tasks/read-aloud-audio-spec-001.json) | Author audio-quality spec v1 | M0 | writing | high | true |
| [read-aloud-audio-data-001.json](tasks/read-aloud-audio-data-001.json) | Define per-work record + per-jurisdiction rights-verification format | M0 | data | high | true |
| [read-aloud-audio-data-002.json](tasks/read-aloud-audio-data-002.json) | Define speaker-consent & voice-provenance record format | M0 | design-spec | high | true |
| [read-aloud-audio-research-001.json](tasks/read-aloud-audio-research-001.json) | Secure ≥1 distribution channel + host stance on AI-assisted/synthetic audio | M0 | research | high | true |
| [read-aloud-audio-research-002.json](tasks/read-aloud-audio-research-002.json) | Validate per-jurisdiction PD/license rules for target sources | M0 | research | high | true |
| [read-aloud-audio-narrate-001.json](tasks/read-aloud-audio-narrate-001.json) | Hand-produce cold-start read-along (1-3 chapters) | M0 | data | high | false |
| [read-aloud-audio-pr-001.json](tasks/read-aloud-audio-pr-001.json) | Publish cold-start read-along upstream + measure alignment baseline | M0 | maintenance | high | false |
| [read-aloud-audio-adapter-001.json](tasks/read-aloud-audio-adapter-001.json) | Forced-alignment adapter (audio-text → SMIL/WebVTT/JSON) | M1 | code | high | false |
| [read-aloud-audio-adapter-002.json](tasks/read-aloud-audio-adapter-002.json) | Audio-mastering adapter (loudness/peak/noise; FLAC→Opus/MP3) | M1 | code | high | false |
| [read-aloud-audio-pipeline-001.json](tasks/read-aloud-audio-pipeline-001.json) | Per-jurisdiction rights-verification + consent-record gate | M1 | code | high | false |
| [read-aloud-audio-pipeline-002.json](tasks/read-aloud-audio-pipeline-002.json) | Text segmentation + pronunciation-lexicon tooling | M1 | code | high | false |
| [read-aloud-audio-adapter-003.json](tasks/read-aloud-audio-adapter-003.json) | Publish adapter for the secured channel | M1 | code | high | false |
| [read-aloud-audio-doc-001.json](tasks/read-aloud-audio-doc-001.json) | Reviewer workflow + 4-axis QA rubric + error taxonomy | M1 | writing | high | true |
| [read-aloud-audio-batch-001.json](tasks/read-aloud-audio-batch-001.json) | Produce + publish ~10 chapters (first repeatable run) | M1 | data | high | false |
| [read-aloud-audio-batch-002.json](tasks/read-aloud-audio-batch-002.json) | Scale to ≥50 chapters published across ≥2 works/collections | M2 | data | medium | false |
| [read-aloud-audio-doc-002.json](tasks/read-aloud-audio-doc-002.json) | Pronunciation specialist guide (foreign-language / names / archaic terms) | M2 | writing | medium | true |
| [read-aloud-audio-research-003.json](tasks/read-aloud-audio-research-003.json) | Beneficiary validation with literacy educators / learners | M2 | research | medium | false |
| [read-aloud-audio-data-003.json](tasks/read-aloud-audio-data-003.json) | Quality metrics dataset | M2 | data | medium | false |
| [read-aloud-audio-adapter-004.json](tasks/read-aloud-audio-adapter-004.json) | Additional distribution-channel adapter (2nd host) | Backlog | code | low | false |
| [read-aloud-audio-tts-001.json](tasks/read-aloud-audio-tts-001.json) | Gated synthetic-voice adapter (clearly-licensed, talent-consented, labeled) | Backlog | code | low | false |
| [read-aloud-audio-pipeline-003.json](tasks/read-aloud-audio-pipeline-003.json) | Outcome-tracking dashboard (published/live, accuracy, completeness) | Backlog | code | low | false |
| [read-aloud-audio-i18n-001.json](tasks/read-aloud-audio-i18n-001.json) | Multilingual read-alongs (sibling-project assessment) | Backlog | research | low | true |
| [read-aloud-audio-research-004.json](tasks/read-aloud-audio-research-004.json) | High-stakes-instructional-text escalation path (expert sign-off / "not advice") | Backlog | research | low | true |
| [read-aloud-audio-maint-001.json](tasks/read-aloud-audio-maint-001.json) | Adapter/aligner maintenance vs host API + standards changes | Backlog | maintenance | low | false |
| [read-aloud-audio-doc-003.json](tasks/read-aloud-audio-doc-003.json) | Narrator onboarding + consent-process handbook | Backlog | writing | low | true |
