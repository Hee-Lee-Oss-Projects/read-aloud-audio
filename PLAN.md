# PLAN — read-aloud-audio

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

Hundreds of thousands of openly-licensed and public-domain texts — Project Gutenberg classics,
Standard Ebooks editions, Wikisource transcriptions, OpenStax and other open textbooks, CC-licensed
children's stories and decodable readers — exist as text only. A learner who is still acquiring
reading fluency, a print-disabled reader, a dyslexic reader, an emergent or adult-literacy learner,
or an English-language learner cannot *hear* most of them, and cannot follow along word-by-word as
the audio plays. The single most evidence-backed support for early and struggling readers —
**simultaneous listening-while-reading with the spoken word highlighted in the text** — is almost
entirely missing from the open commons.

`read-aloud-audio` turns each openly-licensed work (or chapter) into an **open, text-aligned
read-along**: clear narration plus machine-readable timing data that highlights each word/sentence
as it is spoken. The deliverable is a triple — **(1) the audio** in open formats, **(2) the
text↔audio alignment** (EPUB 3 Media Overlays / SMIL + WebVTT + a JSON sidecar), and **(3) a
packaged read-along** (EPUB 3 with Media Overlays) — published **upstream** under an open license,
with **speaker consent and full provenance** recorded for every voice. Success is not "files
rendered" — it is **read-alongs published, live, and confirmed usable by real literacy learners**.

This project is **low risk** overall, but it has three real hazards that are designed for, not
hand-waved: (1) **voice consent & provenance** — a human voice is personal data and is impersonable;
synthetic narration can be a deepfake vector. We never record, clone, or synthesize a voice without
explicit, recorded, revocable consent, we never imitate an identifiable real person, and every
output is labeled human-narrated or AI-synthesized. (2) **pronunciation accuracy** — for a literacy
learner a mispronounced word is actively miseducating; names, foreign words, and technical terms get
a pronunciation-review gate. (3) **source license & provenance** — only public-domain or
open-licensed source texts are ever used, and public-domain status is verified *per jurisdiction*
(the classic "PD in the US, still in copyright elsewhere" trap).

This document is honest about what is not yet in place: **no distribution partner or beneficiary
organisation is secured.** No open-audiobook host (LibriVox-style), open-publisher (Standard
Ebooks-style), archive, or literacy organisation has yet agreed to host our read-alongs or to
validate them with learners. **Partner / distribution channel: TO BE SECURED.** Until at least one
channel is confirmed, delivery-dependent tasks carry `verifiedNeed = false`, and M0 makes securing a
channel a hard exit gate. We do not produce audio with nowhere to ship it.

## Problem & beneficiaries

**Who is helped (primary beneficiaries):**

- **Emergent and developing readers (children).** Listening-while-reading with synchronized
  word/sentence highlighting builds decoding, fluency, prosody, and vocabulary — one of the
  best-evidenced literacy supports. Most open texts have no such audio.
- **Adult literacy and English-language learners.** Hearing accurate, well-paced narration aligned
  to text supports independent practice without a tutor present.
- **Print-disabled readers** — blind, low-vision, and dyslexic readers who rely on audio and on
  read-along highlighting. Open audio that is *aligned* to text (not just a bare recording) is rare.
- **Educators, tutors, and families** who adopt open texts and need accessible, read-along versions
  but lack capacity to record and align them.

**Secondary beneficiaries:**

- The **open-knowledge commons** itself — Project Gutenberg, Standard Ebooks, Wikisource, OpenStax,
  open children's-book and decodable-reader projects — whose texts become more usable as accessible,
  aligned read-alongs for everyone.

**The verified need (the literacy evidence).** That listening-while-reading with synchronized text
improves fluency and comprehension for developing and struggling readers is well established in the
reading-research literature, and the accessibility need for aligned audio (EPUB 3 Media Overlays,
DAISY) is codified in accessible-publishing standards. The *underlying need* is not in dispute, so
the proposal marks the literacy need as real. **However**, a documented need is not a secured
delivery channel or a validated fit with a specific learner population.

**The partner gap (honest).** No distribution host and no literacy/education partner has yet agreed
to (a) publish our read-alongs where learners will find them, or (b) validate that a produced
read-along actually helps the intended learners. **Partner / distribution channel: TO BE SECURED.**
Because impact and even output format depend on the channel, delivery-dependent tasks set
`verifiedNeed = false` until a channel is confirmed; channel-securing is an M0 exit criterion and a
hard gate on production.

## Goals and non-goals

**Goals**

- Produce **accurate, clearly-narrated, text-aligned read-alongs** of openly-licensed / public-domain
  texts, with word- or sentence-level synchronization suitable for literacy practice.
- Capture and store **explicit, revocable speaker consent and full voice provenance** for every
  narration — human or synthetic — and **label** each output accordingly.
- Verify **source-text license and public-domain status per jurisdiction**, and record provenance,
  edition, and attribution for every work.
- Publish every finished read-along **upstream** under an open license, in **open, standards-based
  formats** (EPUB 3 Media Overlays, FLAC/Opus/MP3, WebVTT) — no proprietary lock-in.
- Make the work safely parallelizable: a published narration & pronunciation style guide, a
  self-contained per-work/per-chapter task unit, and human QA gates that scale.
- Measurably help real learners — validated with literacy educators and, where possible, learners.

**Non-goals**

- **Not** using any source text whose license/PD status is unverified or non-open (hard exclusion).
- **Not** cloning, imitating, or synthesizing the voice of any **identifiable real person** without
  explicit recorded consent; **not** producing voice deepfakes or impersonations, ever.
- **Not** using synthetic narration unless the voice model is clearly licensed for this use **and**
  the underlying voice talent's consent to synthesis & redistribution is documented; synthetic output
  is always labeled as such (see Scope for the gated synthetic path).
- **Not** a hosted SaaS, public "narrate any text/upload your voice" service, or a general TTS API.
- **Not** building or training voice-cloning models, and **not** using narrators' recordings to train
  any voice model (consent explicitly excludes this).
- **Not** abridging, editorializing, translating, or "modernizing" source texts — we narrate the text
  as published (translation/abridgement are separate projects).
- **Not** narrating high-stakes instructional content (medical, legal, safety procedures) as
  authoritative read-aloud; such texts are out of the default flow and gated (see Quality & risk).
- **Not** dramatized/multi-voice productions with sound design in the default flow (a future option).

## Success metrics (outcomes)

Outcome-based and learner-centric. "Hours of audio rendered" is explicitly **not** the headline
metric; **published-live-and-usable** is.

| Metric | Baseline | Target (first 2 quarters post-M0) |
|---|---|---|
| Read-alongs (works/chapters) **published upstream and live** | 0 | ≥ 50 chapters across ≥ 2 works/collections |
| **Speaker-consent & provenance completeness** (signed consent + provenance per voice) | n/a | **100%** — hard gate; 0 publications without it |
| **License/PD-verification completeness** (per-jurisdiction PD or open license recorded) | n/a | **100%** — hard gate; 0 publications without it |
| **Alignment accuracy** (median word/sentence onset error vs. human-checked reference) | n/a | ≤ 150 ms median sentence onset; ≤ 5% of segments needing manual correction |
| **Pronunciation error rate** (errors per 1,000 words at QA, esp. names/foreign/technical) | n/a | ≤ 2 / 1,000; **0** uncorrected errors merged |
| **Audio-quality conformance** (loudness target, peak ceiling, noise floor met) | n/a | ≥ 95% of files pass automated loudness/peak/noise checks first time |
| **Text-audio fidelity** (no skipped/added/substituted words vs. source) | n/a | **0** fidelity defects merged (hard QA gate) |
| **Synthetic-output labeling** (every AI-narrated item clearly labeled) | n/a | **100%** |
| **Acceptance rate** at the distribution channel (published ÷ submitted) | n/a | ≥ 85% (signals quality, not volume) |
| **Beneficiary validation** (literacy educator and/or learner confirms a read-along is usable) | none | ≥ 1 qualitative validation per work/collection |

**Audio-quality bar (objective, not "sounds fine").** Loudness normalized to an integrated target
(EBU R128 / ITU-R BS.1770, e.g. −16 LUFS for spoken-word distribution; −18 to −23 LUFS where the
host requires), **true-peak ≤ −1 dBTP**, measured **noise floor** below a stated threshold, no
clipping, consistent levels across a work. These are checked automatically before human QA.

**Alignment-accuracy bar (reproducible).** A held-out human-aligned reference set (a fixed sample of
chapters with hand-checked segment boundaries) is the ground truth; the aligner's onset/offset error
is measured against it per release of the pipeline, so accuracy is comparable over time.

Note: per-collection coverage and learner-outcome targets are deferred until M0 secures a channel
and a partner, and measures a real baseline — inventing them now would be dishonest.

## Scope

**In scope**

- Narration + text-aligned read-alongs for **openly-licensed / public-domain still text** (prose,
  poetry, children's books, decodable readers, open-textbook prose passages).
- Two narration sources, both consent- and provenance-gated:
  - **Human narration (primary path)** — volunteer/contributed narrators, LibriVox-style, with signed
    speaker consent and provenance; the AI pipeline does preparation, alignment, QA, and packaging.
  - **Synthetic narration (gated, opt-in path)** — only with a clearly-licensed TTS voice whose
    underlying talent consented to synthesis & redistribution; **always labeled synthetic**; never an
    imitation of an identifiable real person.
- **Forced alignment** producing word/sentence timing (EPUB 3 Media Overlays / SMIL, WebVTT, JSON).
- **Packaging** as EPUB 3 with Media Overlays (read-along), plus standalone audio (FLAC/WAV master →
  Opus + MP3) and a plain transcript.
- Per-work **license/PD verification, attribution, provenance, and consent records.**
- A published, versioned **narration & pronunciation style guide** and **audio-quality spec**.
- Upstream **distribution adapters** for the secured channel(s).

**Out of scope**

- Any text with unverified, non-open, or jurisdiction-ambiguous rights (hard exclusion).
- **Voice cloning / impersonation of identifiable real people; deepfake voice of any kind.**
- Training voice/TTS models, or using narrator recordings to train models.
- Hosting/streaming infrastructure, user accounts, or a public upload service.
- Abridgement, translation, modernization, or editorial alteration of source text.
- Dramatized multi-voice productions, sound effects, music beds (default flow).
- Narrating high-stakes instructional content as authoritative (medical/legal/safety) — gated/escalated.
- Pronunciation *teaching* or phonetics datasets (overlaps `open-pronunciation-audio`; not this project).

## Solution approach & architecture

This is a **content/data + media-pipeline** project with supporting **adapter code**, run in the
**donated lane**: a human runs their own agent interactively to do text prep, alignment QA, and
packaging, and (for human narration) records or coordinates the voice; Elyos prepares the per-work
task workspace and opens the upstream submission/PR. **The CLI never invokes or authenticates an
agent and never runs headless** (per CLAUDE.md). Audio-tool invocation (ffmpeg, forced aligner, TTS)
is the human operator's local action, wrapped by `adapters/`.

**Pipeline (per work / chapter)**

1. **Select & verify source text.** Pull a text from an approved open/PD source. **Verify rights per
   jurisdiction** (PD-US vs. life+70 elsewhere; or a specific CC license), capture canonical source,
   edition/version, author, translator (if any — separately rights-checked), license id, and
   attribution. *Unverified or jurisdiction-ambiguous → drop, do not use.*
2. **Prepare & segment text.** Normalize, segment into paragraphs/sentences (and words for
   word-level highlighting), preserve structure (headings, chapters, verse lines). Build a
   **pronunciation lexicon** for proper nouns, foreign words, archaic spellings, and technical terms,
   with IPA and/or respelling, flagged for pronunciation review.
3. **Narrate.**
   - *Human path:* a narrator records per chapter. Before any recording is accepted, capture a
     **signed speaker-consent & provenance record** — speaker name or chosen pseudonym, consent to
     record + redistribute under the named open license, explicit consent that AI tools process the
     audio **for alignment/QA only and not for model training/cloning**, confirmation the speaker is
     of age (or guardian consent), and the right to withdraw.
   - *Synthetic path (gated):* render with a clearly-licensed TTS voice; record **voice provenance**
     (model, version, voice id, license, talent-consent attestation). Output is labeled synthetic.
4. **Master audio.** Clean (de-noise lightly, trim), normalize loudness to the target, enforce
   true-peak ceiling and noise-floor threshold; keep a lossless master (FLAC/WAV), derive Opus + MP3.
5. **Forced alignment.** Align audio to the prepared text producing segment timings; emit EPUB 3
   Media Overlays (SMIL), WebVTT, and a JSON sidecar. Measure alignment error vs. the reference set.
6. **Human QA (mandatory).** A reviewer listens through and checks, against a rubric: **text-audio
   fidelity** (every word present, none added/substituted/skipped), **pronunciation** (esp. flagged
   lexicon items — specialist/native-speaker for foreign-language items), **audio quality**
   (levels/noise/artifacts), and **alignment accuracy** (highlight tracks the voice; no drift).
   Defects are tagged by an error taxonomy.
7. **Package.** Assemble the read-along: EPUB 3 + Media Overlays, plus standalone audio + WebVTT +
   transcript + a metadata/credits page carrying license, attribution, **speaker credit/consent
   reference**, and the **human-narrated / AI-synthesized label**.
8. **Publish upstream (additive).** An adapter submits to the secured channel (open-audiobook host,
   open-publisher PR, archive deposit). Never overwrite an existing better version; contributions are
   additive. Attribution, provenance, and consent reference travel with the contribution.
9. **Track to live.** Record publication status; a deed is "done" only when **published, live, and
   playable** for learners.

**Components**

- `style-guide/` — narration & pronunciation style guide (diction, pacing for literacy, prosody,
  how to handle dialogue/verse, pronunciation-lexicon conventions, what *not* to dramatize) and the
  **audio-quality spec** (loudness/peak/noise targets, file formats, sample rate).
- `consent/` — the **speaker-consent & voice-provenance record** schema and signed-record store
  (references only; see Security & privacy for handling), plus the synthetic-voice provenance schema.
- `pipeline/` — source selection, **per-jurisdiction rights verification**, text segmentation,
  pronunciation-lexicon tooling, alignment runner, audio-mastering runner, and the per-work record
  schema.
- `adapters/` (Elyos-conformant — all tool/host-specific logic lives here):
  - `adapters/align/` — wrap the forced aligner (e.g. aeneas / Montreal Forced Aligner / WhisperX)
    behind a neutral interface; emit SMIL/WebVTT/JSON.
  - `adapters/audio/` — wrap ffmpeg / loudness tooling for mastering and format derivation.
  - `adapters/tts/` — *optional, gated* wrapper for a clearly-licensed synthetic voice.
  - `adapters/publish-*/` — one per secured distribution channel (host API / repo PR / archive deposit).
- `records/` — per-work provenance/QA records (audit artifact; not a re-publication of the audio).

**Tech stack & conventions.** TypeScript, ESM, pnpm workspaces for tooling/adapters; ffmpeg and a
forced aligner as external tools invoked locally and wrapped in `adapters/`. Output formats: EPUB 3
with Media Overlays (SMIL), WebVTT, FLAC/WAV master, Opus + MP3 derivatives, plain-text transcript.
Loudness per EBU R128 / ITU-R BS.1770. Adapter/pipeline **code is MIT**; **audio + alignment +
read-along** are licensed to match the source/host (PD/CC0/CC-BY/CC-BY-SA — see next section). DCO
sign-off (`git commit -s`) on all code and PRs.

**Per-work narration record (data model, draft)**

```
workId             stable id within source collection
chapterId          chapter/section id (nullable for single-unit works)
sourceUrl          canonical URL of the source text/edition
sourceCollection   e.g. "project-gutenberg" | "standard-ebooks" | "wikisource" | "openstax"
edition            edition/version identifier of the text used
author             author (+ translator if any, separately rights-checked)
rights             { status: "PD" | "CC-*", license, jurisdictionsVerified[], evidenceUrl }
attribution        required attribution string (source + author/translator)
narrationType      human | synthetic
speakerRef         reference to signed consent/provenance record (human) — NOT raw PII inline
voiceProvenance    synthetic only: { model, version, voiceId, license, talentConsentRef }
audio              { masterPath, opusPath, mp3Path, durationSec, lufs, truePeakDb, noiseFloorDb }
pronunciationLexicon list of {term, ipa|respelling, reviewedBy} for flagged items
alignment          { smilPath, vttPath, jsonPath, medianOnsetErrMs, segmentsCorrected }
qaStatus           drafted | needs-pronunciation-review | reviewed | rejected
qaScores           { fidelity, pronunciation, audioQuality, alignment } + taxonomy tags
upstreamRef        channel submission/PR/deposit id once submitted
publishStatus      submitted | published | declined
label              "human-narrated" | "AI-synthesized" (always present on output)
provenance         tools, models, versions, dates, reviewer, consent reference
```

**Key decisions**

- *Upstream-first, open-formats-only.* We publish into open hosts in open standards (EPUB 3 Media
  Overlays, WebVTT, FLAC/Opus/MP3); `records/` is an audit/provenance log, not a competing library.
- *Human narration is the primary path; synthetic is gated and labeled.* The headline literacy value
  (clear, natural prosody) is best served by human voices; synthetic narration is an explicitly
  consented, clearly-licensed, always-labeled fallback — never an impersonation.
- *Consent and per-jurisdiction rights are hard gates.* No audio is published without a signed
  speaker-consent/provenance record and verified source rights for the target jurisdiction(s).
- *Human-in-the-loop QA is non-optional.* No read-along publishes without human fidelity,
  pronunciation, audio-quality, and alignment review — the difference between "helps a learner" and
  "teaches a child the wrong word."

## Data, licensing & compliance

**This is the critical, conservative section. Two licensing surfaces: the source *text* and the
narrator's *voice*.**

**Allowed source texts (only these classes).**

- **Public-domain texts** — Project Gutenberg, Wikisource, Standard Ebooks (PD editions), and
  similar, **with PD status verified for the target jurisdiction(s)**, not assumed.
- **Open-licensed texts** — CC0, CC-BY, CC-BY-SA (and CC-BY-NC *only* where it does not conflict with
  the host and our non-commercial public-good use; flagged for review) from OpenStax, open
  children's-book / decodable-reader projects, and similar.

**Hard source-rights gate.** Before *any* narration:

1. The text's rights are verified: **public-domain status confirmed for each jurisdiction we
   publish to** (e.g. PD-US vs. life-of-author+70 elsewhere — a US-PD text may still be in copyright
   in other countries), **or** a clear CC license. **Unknown / "PD in US only" without scoping /
   ambiguous / all-rights-reserved → excluded.** Translations and introductions have *their own*
   rights and are checked separately.
2. License id, edition, source URL, evidence of PD/license, retrieval date, and required
   **attribution** are recorded in the work record.

**Voice / speaker rights & consent gate (equally hard).**

- **Human narration:** no recording is accepted, processed, or published without a **signed speaker
  consent & provenance record** that grants: recording, redistribution under the named open license,
  AI processing **for alignment/QA only (not training/cloning)**, age confirmation (or guardian
  consent for minors — default is to **avoid minor narrators** unless a partner has a proper consent
  process), and a documented **right to withdraw**. Consent records are stored securely and
  referenced — not inlined as raw PII in public records.
- **Synthetic narration:** only with a TTS voice model **clearly licensed for redistribution of
  generated audio**, where the underlying voice talent's **consent to synthesis & redistribution is
  documented**. Output is **labeled AI-synthesized**. **Never** an imitation/clone of an identifiable
  real person. No use of a model whose voice provenance/consent cannot be evidenced.

**Output licensing.** The read-along (audio + alignment + EPUB) is licensed **compatibly with the
source and host**: PD source → CC0 / Public Domain dedication for the new recording where the
narrator consents, or CC-BY with speaker attribution; CC-BY / CC-BY-SA source → matching CC license.
The *new recording* carries its own copyright that the narrator licenses openly via the consent
record. Adapter/pipeline **code is MIT**. We never impose an Elyos license on upstream content or
strip a source's required attribution/share-alike terms.

**Privacy / PII stance.** A human voice is personal (biometric-adjacent) data. We: collect the
minimum identity needed for credit/consent; let narrators use a **pseudonym**; store signed consent
securely and reference it (no raw PII in public `records/` or logs); honor **withdrawal** (take down
on request and record disposition); and **never** use recordings to train/clone models. Source texts
may contain references to private living individuals only as already published in the open text — we
add no new claims.

**Content suitability.** Some PD texts contain dated, offensive, or culturally harmful content. For
literacy/children contexts we (a) prefer curated, age-appropriate, openly-licensed works, (b) add a
neutral provenance/context note where a classic text carries historical bias rather than silently
editing it, and (c) keep the project **non-partisan** for any civic/political text. We narrate texts
faithfully; we do not editorialize, and we do not select texts to push a viewpoint.

**Robots / automation policy.** Source retrieval and upstream submission honor each host's API
terms, rate limits, and bot/contribution policies. We do not scrape around access controls.

## Quality, review & risk gates

**Risk tier: low** overall, with explicit **medium** escalations and a **high** out-of-flow gate.

- **low** — straightforward PD/CC prose in a well-supported language, human-narrated, non-sensitive;
  standard QA.
- **medium** — (a) **pronunciation-critical content** (foreign-language passages, heavy proper-noun
  or technical vocabulary) → reviewer with the relevant language/subject skill; (b) **any synthetic
  narration** → extra consent/provenance + labeling review; (c) **children's content** → age-fit and
  pronunciation review (a mispronunciation miseducates a new reader).
- **high (escalation, out of default flow)** — narrating **high-stakes instructional text**
  (medical, legal, safety) as authoritative read-aloud requires credentialed expert sign-off and a
  "not advice" framing, **or the text is declined**. The default flow does not narrate such content.

**Required review before a deed is "done":**

1. **Source-rights check passed** — per-jurisdiction PD or open license, with attribution +
   provenance recorded.
2. **Speaker-consent / voice-provenance check passed** — signed human consent on file, or documented
   synthetic-voice license + talent consent; output correctly labeled.
3. **Text-audio fidelity review** — every word of the source is present; nothing added, substituted,
   or skipped (hard gate; 0 defects merged).
4. **Pronunciation review** — flagged lexicon items correct; foreign-language items cleared by a
   reviewer with the relevant skill (medium).
5. **Audio-quality check** — loudness/true-peak/noise-floor targets met; no clipping/artifacts.
6. **Alignment review** — highlighting tracks the voice within tolerance; no cumulative drift.

**Definition of Shipped (project-level).** A reviewed read-along is **published upstream, live, and
playable** for learners (open-audiobook host / open-publisher / archive), in open formats, with
license + attribution + speaker-consent reference + provenance recorded and the human/synthetic label
present. Rendered-but-not-published ≠ shipped.

## Roadmap & milestones

Phased; each milestone has measurable exit criteria. M0 is a deliberately thin, manual, end-to-end
slice — it must prove one chapter can travel from an openly-licensed source to a **published, live,
text-aligned read-along** before anything scales.

**Sequencing — securing a distribution channel is a hard gate.** The channel-securing research task
is a **blocking prerequisite**: no narration, alignment, or publish task starts until ≥ 1 channel is
confirmed. **Kill/pivot criteria:** if, after the time-boxed channel-securing effort, no candidate
channel will accept human-reviewed, openly-licensed, consent-backed read-alongs, the project
**pivots** (next candidate channel per the decision tree) or **stops** — it does not produce audio
with nowhere to ship.

**Candidate upstream channels (priority order, with acceptance posture).** The metric is decoupled
from any single host:
1. **Open-publisher / open-repo (Standard Ebooks-style or an open-textbook repo)** — PR/deposit-based,
   clearest path where the repo invites contributions; posture: *generally welcoming to additive
   accessibility contributions; per-repo confirmation required.*
2. **Open-audiobook host (LibriVox-style) / Internet Archive deposit** — large audience for PD audio;
   posture: *welcoming to PD recordings under their process; confirm their stance on text-aligned
   EPUB Media Overlays and on AI-assisted alignment/AI-synthesized narration before scaling.*
3. **Wikisource / Wikimedia Commons (audio + aligned text)** — high volume; posture: *community- and
   policy-sensitive; needs pre-engagement on AI-assisted/synthetic audio before any volume.*
4. **A named literacy/education partner** — highest-value for *validation*, but **TO BE SECURED.**

**Decision tree (which channel first):** confirmed PR/deposit-accepting open publisher/repo? → start
there. Else an open-audiobook host/archive that accepts our format after confirmation? → start there.
Else a Wikisource community willing after pre-engagement? → start there. Else → kill/pivot criteria.

**M0 — Foundation & cold-start (prove one end-to-end read-along).**
Goal: publish the narration/pronunciation style guide + audio-quality spec, define the consent &
rights record formats, secure ≥ 1 distribution channel, and publish one small hand-produced
read-along end-to-end.

**M0 work-selection criteria (the cold-start unit must exercise the hard paths, not the easy one).**
Choose **one short PD work or 1–3 chapters** that include: at least one passage with **proper
nouns / foreign or archaic words** (exercises the pronunciation lexicon + review), structure beyond
flat prose (a heading and either dialogue or verse), and — if the synthetic path is in M0 scope — one
short segment produced via the **gated synthetic path** to exercise labeling/provenance. A single
trivially-easy paragraph is explicitly disallowed; it would not prove the pipeline.

Exit criteria:
- Narration & pronunciation style guide v1 **and** audio-quality spec v1 published (CC-BY-4.0).
- Speaker-consent/voice-provenance record format and per-jurisdiction rights-verification format
  finalized and applied to the cold-start unit.
- ≥ 1 distribution channel **confirmed** (a host/repo that will accept our read-alongs) — closes the
  partner gap for one channel; **gates** all narrate/align/publish work.
- ≥ 1 read-along (1–3 chapters) **published upstream, live, and playable**, with EPUB 3 Media
  Overlays + WebVTT + open audio, full source-rights + consent + provenance, and the human/synthetic
  label present.
- Alignment-accuracy reference set established and the cold-start unit's alignment error measured.
- Baseline for the chosen channel/collection recorded (what exists vs. what's missing).

**M1 — Pipeline & adapters (make it repeatable).**
Goal: turn the manual slice into a repeatable, policy-compliant pipeline.
Exit criteria:
- Alignment adapter + audio-mastering adapter working; ≥ 1 publish adapter live and policy-compliant.
- Per-jurisdiction rights gate + consent-record gate + text segmentation + pronunciation-lexicon
  tooling operational, routing flagged items to the right reviewer.
- Reviewer workflow + QA rubric (fidelity, pronunciation, audio, alignment) + error taxonomy
  documented; ≥ 2 reviewers (incl. ≥ 1 with pronunciation/language skill) onboarded.
- ≥ 10 chapters published upstream; acceptance rate and alignment accuracy measured.

**M2 — Controlled scale (one work/collection, deep).**
Goal: complete meaningful, learner-usable read-alongs in 1–2 works/collections, quality held.
Exit criteria:
- ≥ 50 chapters published upstream and live across ≥ 2 works/collections.
- Acceptance rate ≥ 85%; pronunciation error rate ≤ 2/1,000; 0 fidelity defects; audio-quality
  conformance ≥ 95%; alignment within tolerance.
- ≥ 1 beneficiary validation (literacy educator and/or learner) per work/collection.
- 100% consent + 100% rights completeness; 0 license/consent violations.

**M3 — Broaden & sustain (more works, durable ops).**
Goal: add works/collections, optionally extend (e.g. additional languages), and stand up maintenance.
Exit criteria:
- ≥ 2 additional works/collections onboarded with confirmed channels.
- Outcome-tracking dashboard (published/live counts, accuracy, consent/rights completeness) maintained.
- Documented maintainer + reviewer + narration-coordinator rotation; sustainability plan in effect.

## Work breakdown

The itemized, schema-mapped backlog lives in **`TASKS.md`** (same directory), organised by the
milestones above, with one task per work unit, stable IDs (`read-aloud-audio-<area>-NNN`), a
size/risk/reviewer table per milestone, acceptance criteria for the key tasks, an example Task JSON
for the first M0 task, and `verifiedNeed = false` on delivery-dependent tasks until a channel is
secured. The production backlog fans out: at scale, **one work (or chapter) = one task**, drawn from
a milestone-scoped, channel-confirmed batch.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the style guide, audio-quality spec, pipeline, adapters, and the
  overall quality/consent bar.
- **Narration coordinator:** recruits and manages narrators, **owns the consent & provenance
  process**, ensures every voice has a signed, current consent record and honors withdrawals.
- **Reviewers / rotation:** an audio-QA pool (fidelity, audio quality, alignment) with **≥ 1
  reviewer per relevant language** for pronunciation; rotation documented in M1.
- **Steward (last-mile owner):** owns each distribution-channel relationship and shepherds
  contributions to *published/live* — accountable for "delivered, not merged."
- **Partner / requestor:** TO BE SECURED — distribution host(s) and a literacy/education partner who
  validates with learners and prioritises works.
- **Expert reviewers (risk tiers):** language/pronunciation specialist for medium; credentialed
  expert for any high-risk escalation (high-stakes instructional text) before publish, or decline.
- **Beneficiary validators:** literacy educators and, where possible, learners who confirm read-alongs
  are actually usable.

## Dependencies & integrations

- **Source-text repositories** — Project Gutenberg, Standard Ebooks, Wikisource, OpenStax, open
  children's-book/decodable-reader projects (texts + rights metadata; honor terms & rate limits).
- **Forced aligner** — e.g. aeneas / Montreal Forced Aligner / WhisperX (chosen and wrapped in
  `adapters/align/`); produces SMIL/WebVTT/JSON timings.
- **Audio tooling** — ffmpeg + loudness/measurement tools (EBU R128 / ITU-R BS.1770), wrapped in
  `adapters/audio/`.
- **Synthetic voice (optional, gated)** — a clearly-licensed TTS voice with documented talent
  consent, wrapped in `adapters/tts/`; only if the synthetic path is enabled.
- **Distribution channels** — open-publisher repo / open-audiobook host / Internet Archive /
  Wikisource; **pre-engagement is a required exit artifact** of the channel-securing task: a
  documented statement of intent, confirmation that human-reviewed, openly-licensed, consent-backed
  read-alongs (and the host's stance on AI-assisted alignment / any AI-synthesized narration) are
  welcome, and an agreed volume ramp.
- **Standards** — EPUB 3 Media Overlays (SMIL), WebVTT, EBU R128, ITU-R BS.1770, WCAG / accessible
  publishing (DAISY) guidance for read-along.
- **Elyos platform pieces** — `packages/cli` (task workspace + PR/submission prep, donated lane), the
  Task schema (`packages/schema`), and `adapters/` for all tool/host-specific code. The CLI never
  runs an agent headless and never authenticates a coding agent.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Voice used without consent / impersonation / deepfake | Low | High | Hard consent gate (signed, revocable record per voice); no clone/imitation of identifiable real people; synthetic only from clearly-licensed, talent-consented voices; every output labeled human/synthetic; recordings never used for training | Narration coordinator |
| Source text not actually PD in a target jurisdiction | Medium | High | Per-jurisdiction rights verification; "PD-US only" without scoping = excluded; translations/intros rights-checked separately; evidence recorded; stop-the-line on any violation | Steward |
| Mispronunciation miseducates a literacy learner | Medium | High | Pronunciation lexicon for flagged terms; mandatory pronunciation review; native/skilled reviewer for foreign-language items (medium); 0 uncorrected errors merged | Reviewers |
| Alignment drift makes highlighting wrong (worse than none for learners) | Medium | Medium | Alignment-accuracy reference set + per-release measurement; human alignment review per chapter; tolerance thresholds; manual correction of failing segments | Maintainer / Reviewers |
| Text-audio mismatch (skipped/added/substituted words) | Medium | High | Mandatory fidelity review against source; 0 defects merged; error taxonomy tracks failure classes | Reviewers |
| Poor audio quality (noise, clipping, inconsistent levels) | Medium | Medium | Objective audio-quality spec (LUFS/true-peak/noise floor) checked automatically before human QA; lossless master retained | Maintainer |
| No distribution partner/channel secured → nothing ships | Medium | High | Channel-securing is an M0 exit gate and blocks production; `verifiedNeed=false` until secured; decision tree across candidate channels; do not over-produce | Maintainer / Steward |
| Host rejects AI-assisted/AI-synthesized audio | Medium | Medium | Pre-engagement exit artifact incl. host's stance on AI alignment / synthetic narration; lead with human narration; label everything; metric decoupled from a single host | Steward |
| Narrator withdraws consent after publication | Low | Medium | Right-to-withdraw in consent record; documented takedown + disposition process; provenance log records final state | Narration coordinator |
| Synthetic voice misused to imitate a real person | Low | High | Synthetic path gated and labeled; explicit ban on identifiable-person imitation; voice provenance + talent-consent attestation required | Maintainer |
| Reviewer/narrator capacity becomes the bottleneck | High | Medium | Narrator recruitment + reviewer rotation; chapter-sized units; flag easy vs. hard; scale fan-out only to review capacity | Maintainer |
| Dated/offensive content in PD texts harms learners | Medium | Medium | Prefer curated age-appropriate works; neutral provenance/context note (not silent editing); non-partisan stance; partner-guided selection | Maintainer / Partner |
| Duplicate/redundant production across sessions | Medium | Low | Per-work claim/lock (TTL + owner) keyed on source-id/chapter; milestone-scoped, channel-confirmed batches; check existing host versions before producing | Maintainer |

## Security & privacy

- **Threat surface.** Mostly content-integrity, consent, and licensing rather than classic security:
  unconsented or impersonated voice, mislabeled synthetic audio, unverified source rights, and
  mispronunciation/fidelity defects. Adapters also touch external write APIs (host submission, repo
  PRs, archive deposits).
- **Secrets handling.** Any host/API tokens are supplied via the human operator's own environment,
  never written into logs, receipts, records, or committed files (per CLAUDE.md). Donated lane: the
  human authenticates with their own account; Elyos stores no agent credentials.
- **PII / consent.** Speaker identity is collected minimally; pseudonyms allowed; signed consent
  stored securely and **referenced, never inlined** in public `records/` or logs; recordings are
  **never** used to train/clone models; withdrawal is honored with a documented takedown path.
- **Abuse / misuse prevention.** No voice cloning or impersonation; synthetic output always labeled;
  no narration of non-open texts; honor host rate limits and policies; every publish is
  human-reviewed. Refuse and flag (per Elyos guardrails) any request to clone/imitate a real voice,
  to narrate non-open text, to produce deceptive/impersonated audio, or to narrate high-stakes
  instructional content as authoritative without expert review.

## Sustainability & maintenance

- **Post-delivery ownership.** Read-alongs live upstream in the host collections — once published
  they are durable and not Elyos-dependent. Lossless masters + alignment sources are retained so a
  work can be re-derived to new formats/standards later.
- **Additive contributions only.** We add missing read-alongs; we do not overwrite better existing
  versions. Conflicts are resolved by re-fetch-and-re-evaluate, never clobbering host content.
- **Project maintenance.** The maintainer keeps the style guide, audio-quality spec, aligner, and
  adapters current with host APIs/policies and standard updates; the narration coordinator keeps
  consent records current and processes withdrawals; reviewer rotation keeps QA capacity alive.
- **Outcome tracking.** A lightweight dashboard tracks published/live counts, alignment accuracy,
  pronunciation-error rate, and consent/rights completeness per work/collection over time.
- **Wind-down.** If a channel closes or a consent is withdrawn, in-flight items are completed,
  cleanly withdrawn, or taken down; the provenance log records final disposition.

## Open questions

- Which distribution channel is secured first — an open publisher/repo, an open-audiobook host /
  Internet Archive, or Wikisource? (Blocks M0 exit.) And what is each host's stance on **AI-assisted
  alignment** and on **AI-synthesized narration**?
- Is the **synthetic-narration path in scope for M0**, or human-narration only until later? (Affects
  the cold-start unit and the consent/provenance tooling sequencing.)
- What exact **output license** does each chosen channel require for new recordings (CC0 vs. CC-BY
  with speaker attribution) — confirm before publishing at volume.
- What is the right **alignment granularity** for the literacy goal — word-level, sentence-level, or
  both — and which forced aligner best hits the accuracy bar per language?
- What is the **credential bar** for a pronunciation reviewer per language (native speaker? linguist?),
  and how is foreign-language QA staffed?
- How are **minor narrators** handled — excluded by default, or admitted only via a partner with a
  vetted guardian-consent process?
- What **loudness target** does each host expect (−16 vs. −18/−23 LUFS), and what noise-floor
  threshold is acceptable across donated home-recording environments?
- For **content suitability**, who decides a PD text is appropriate for a literacy/children context —
  the maintainer, the partner, or a published selection rubric?
- Should **multilingual** read-alongs be this project or a sibling (overlaps `open-pronunciation-audio`,
  `decodable-readers`, `public-domain-translations`)?

## References

- `C:\code\elyos\CLAUDE.md` — Elyos work rules, lanes, quality bar, refusal guardrails.
- `C:\code\elyos\docs\good-deed-definition.md` — good-deed criteria and risk tiers.
- `C:\code\elyos\packages\schema\src\schemas.ts` — Task JSON schema.
- `C:\code\elyos\planning\ROADMAP.md` — portfolio roadmap (read-aloud-audio is a Track 3 candidate).
- `C:\code\elyos\governance\proposals\read-aloud-audio.md` — originating proposal (TO BE WRITTEN).
- EPUB 3 Media Overlays (SMIL) specification — synchronized text & audio read-along.
- W3C WebVTT — Web Video Text Tracks (timed text / cue timing).
- EBU R128 / ITU-R BS.1770 — loudness normalization for spoken-word audio.
- DAISY / accessible-publishing guidance — read-along and print-disability access.
- Creative Commons license suite (CC0, CC-BY, CC-BY-SA) and Public Domain.
- Forced-alignment tools: aeneas, Montreal Forced Aligner, WhisperX (candidate, to be evaluated).

---

## Appendix A — Improvements applied

Twenty-five specific improvements identified against the first draft and **applied** above
(not merely listed). Each is concrete and reflected in the document.

1. **Split the licensing section into two surfaces — text *and* voice.** Added an explicit
   voice/speaker rights-and-consent gate alongside source-text rights, because a narration project
   has two independent legal surfaces.
2. **Per-jurisdiction PD verification.** Replaced naive "public domain" with verification *per
   target jurisdiction* (the "PD-US but not elsewhere" trap), and required translations/introductions
   to be rights-checked separately.
3. **Explicit deepfake / impersonation ban.** Added a hard non-goal and refusal: never clone or
   imitate an identifiable real person's voice; this is the project's sharpest abuse vector.
4. **Synthetic narration gated, not banned outright.** Defined a consented, clearly-licensed,
   always-labeled synthetic path (with talent-consent attestation) instead of an unrealistic blanket
   ban — useful for scale while staying safe.
5. **Mandatory human/synthetic labeling.** Made labeling a first-class output field and a success
   metric (100%), so listeners always know what they're hearing.
6. **Objective audio-quality spec.** Replaced "good audio" with measurable EBU R128 / ITU-R BS.1770
   targets (integrated LUFS, true-peak ≤ −1 dBTP, noise-floor threshold) checked automatically before
   human QA.
7. **Reproducible alignment-accuracy bar.** Added a held-out human-aligned reference set and a
   median-onset-error metric measured per pipeline release, so "aligned well" is testable.
8. **Pronunciation lexicon + review gate.** Added a flagged-term lexicon (IPA/respelling) and a
   pronunciation-review step, because a mispronunciation actively miseducates a literacy learner.
9. **Text-audio fidelity as a hard gate.** Added an explicit fidelity check (no skipped/added/
   substituted words) with 0 defects merged — distinct from pronunciation and alignment.
10. **Right-to-withdraw + takedown path.** Added revocable consent, a documented takedown process,
    and disposition logging — narrators can change their minds.
11. **No-training/cloning clause in consent.** Consent explicitly permits alignment/QA only and
    forbids using recordings to train or clone voice models.
12. **Minor-narrator handling.** Added a default to avoid minor narrators absent a partner with a
    vetted guardian-consent process, and surfaced it as an open question.
13. **Channel decision tree + kill/pivot.** Borrowed and adapted the exemplar's decision tree so
    production is gated on a confirmed channel and the project stops rather than over-produces.
14. **`verifiedNeed=false` until a channel is secured.** Made the honesty stance explicit and tied
    it to delivery-dependent tasks, matching Elyos house practice.
15. **Open-formats-only key decision.** Pinned EPUB 3 Media Overlays + WebVTT + FLAC/Opus/MP3 to
    avoid proprietary lock-in and ensure durability.
16. **Lossless master retention for re-derivation.** Added FLAC/WAV master retention so works can be
    re-packaged to future formats/standards without re-recording.
17. **Content-suitability stance for PD texts.** Added handling of dated/offensive classic content
    (curated selection + neutral context note, not silent editing) and a non-partisan rule for civic
    texts.
18. **Per-work claim/lock for fan-out.** Added TTL'd locking keyed on source/chapter id so parallel
    donated sessions don't double-produce the same work.
19. **Narration coordinator role.** Added a dedicated role owning the consent/provenance process and
    withdrawals — distinct from maintainer/steward/reviewer.
20. **Pronunciation reviewer per language.** Required ≥ 1 reviewer with the relevant language skill in
    the reviewer pool, and made it a medium-risk gate.
21. **High-stakes instructional content gated/declined.** Added a high-risk escalation (or decline)
    for narrating medical/legal/safety text authoritatively, with "not advice" framing.
22. **PII-minimization in records.** Consent stored securely and *referenced*, never inlined as raw
    PII in public `records/` or logs; pseudonyms allowed.
23. **Cold-start unit must exercise hard paths.** Required the M0 unit to include proper nouns/foreign
    words, real structure, and (if in scope) a synthetic segment — not a trivial paragraph.
24. **Beneficiary validation with literacy experts/learners.** Made learner/educator validation a
    success metric and an M2 exit criterion, since the whole point is helping real readers.
25. **Distinct error taxonomy across four QA axes.** Defined fidelity, pronunciation, audio-quality,
    and alignment as separate scored dimensions with tagged failure classes, so we learn *how* the
    pipeline fails and tune the style guide.

## Review sign-off

**Reviewer:** Senior staff engineer + TPM (drafting author self-review) · **Date:** 2026-06-28 ·
**Scope:** PLAN.md (17 required sections + Appendix A) and TASKS.md (schema mapping, milestone
tables, acceptance criteria, DoD, example Task JSON).

**Completeness check.**
- All 17 required H2 sections present and in order. ✔
- Outcome-based, beneficiary-centric metrics with baselines + targets (and honest deferrals). ✔
- License/provenance treated as the critical section, covering **both** source-text and voice
  surfaces, conservatively. ✔
- Risk tier (low, with medium escalations + high out-of-flow gate) and Definition of Shipped
  ("published, live, playable") stated. ✔
- Roadmap M0..M3 each have measurable exit criteria; M0 is a thin cold-start with a hard channel
  gate. ✔
- TASKS.md maps every field of `taskSchema`; example Task JSON validated field-by-field against
  `packages/schema/src/schemas.ts`. ✔
- `verifiedNeed=false` on delivery-dependent tasks; `true` only on self-evidently-useful,
  channel-independent artifacts (style guide, specs). ✔

**Correctness fixes applied during review.**
- Confirmed Elyos donated-lane rule: clarified that the CLI never runs an agent headless and that
  ffmpeg/aligner/TTS invocation is the human operator's local action wrapped by `adapters/`.
- Ensured no funded tasks appear (so `fundedBudgetUsd` is correctly omitted); noted where the schema
  would require it if a funded task were added.
- Verified the example Task JSON uses only enum-legal values for `type`, `lane`, `priority`,
  `riskTier`, `deliverable`, `tokenEstimate`, `status`, and includes all `required` fields with a
  non-empty `output` and a real `outputLicense`.
- Aligned PLAN milestone names/IDs with TASKS milestone sections.

**Outstanding (human decisions, see Open questions).** Distribution channel + host stance on
AI-assisted/synthetic audio; whether the synthetic path is in M0 scope; per-channel output license;
alignment granularity + aligner choice; pronunciation-reviewer credential bar; minor-narrator policy.
These are explicitly flagged and do not block M0 *planning*, but the channel decision blocks M0
*exit*.

**Verdict:** Approved as a Draft (v0.1.0) for maintainer review. No invented partners or metrics; all
gaps marked TO BE SECURED.
