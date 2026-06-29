# Competitive & Improvement Analysis — `read-aloud-audio`

Analyst review of `PLAN.md` (v0.1.0, 2026-06-28) for the Elyos good-deed project that turns
openly-licensed / public-domain texts into **open, text-aligned read-alongs** (audio + EPUB 3 Media
Overlays + WebVTT/JSON), human or gated-synthetic narration. Web-researched and cited throughout.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually rigorous: it correctly identifies the **two independent licensing surfaces
(source text *and* narrator voice)**, makes per-jurisdiction PD verification and signed speaker
consent *hard gates*, bans identifiable-person voice cloning/deepfakes, mandates a human/synthetic
label, and defines objective audio (EBU R128 / true-peak −1 dBTP) and alignment-accuracy bars. The
"published, live, playable" Definition of Shipped and the `verifiedNeed=false`-until-channel-secured
honesty are strong. Findings below are refinements, not rebuttals.

**a) Synthetic-voice disclosure is under-specified for the 2025–26 regulatory reality.** The plan
treats the human/synthetic label as an output field and a credits-page line. But disclosure norms
have hardened into law: the **EU AI Act Article 50** requires AI-generated/altered audio to be
labeled in a machine-readable form; **California's AB 942 (AI Transparency Act, effective Jan 1
2026)** and **China's synthetic-content labeling rules (effective Sep 1 2025)** require explicit
labels on synthetic audio; and the emerging technical mechanism is **C2PA Content Credentials**
(cryptographically signed provenance embedded in the file), now shipping in tools like Sora 2.
[EU AI Act / C2PA](https://www.resemble.ai/resources/the-eu-ai-act-what-generative-ai-companies-need-to-know-in-2026),
[transparency rulebook](https://www.transparentaudio.ai/resources/the-2025-transparency-rulebook-for-voice-ai).
*Recommendation:* the label must be **durable and embedded** — C2PA manifest on the audio + EPUB
metadata (`schema:accessibilityFeature` / a synthetic-narration property) — not only human-readable
credits, so the label survives re-hosting and podcast redistribution. Add this to the audio-quality
spec and the per-work record.

**b) Consent quality + the cloning risk are real and correctly banned — but consent must be
*specific*, not blanket.** Industry/regulatory guidance is explicit that **informed consent must name
the use, deployment contexts, languages, and retention period**; blanket consent is insufficient
([voice-cloning ethics](https://www.camb.ai/blog-post/voice-cloning-ethics-consent-deepfakes-responsible-ai-voice-use)).
The threat is not hypothetical: the Project Gutenberg/Microsoft program publicly demonstrated cloning
a full audiobook voice from **5 seconds** of audio
([TechCrunch](https://techcrunch.com/2023/09/19/project-gutenberg-puts-5000-audiobooks-online-for-free-using-synthetic-speech/)).
The plan's no-training/no-cloning consent clause and identifiable-person ban are exactly right; tighten
the consent schema to enumerate purpose/retention/withdrawal-effect fields per the "blanket consent is
insufficient" standard.

**c) Alignment granularity vs. tool choice is an internal inconsistency.** The plan promises
**word-level** highlighting yet lists `aeneas / MFA / WhisperX` as interchangeable candidates. Research
shows these are *not* equivalent for word timing: **aeneas was not built for word-level alignment**,
and a controlled comparison found **MFA outperforms WhisperX and MMS at word-level alignment at all
time resolutions**
([Tradition or Innovation, arXiv 2406.19363](https://arxiv.org/html/2406.19363v1),
[WhisperX word-timestamp issue](https://github.com/m-bain/whisperX/issues/1247)). If word-level
highlighting is a stated goal, aeneas (sentence-level) cannot meet it; the aligner choice should be
resolved per-language with MFA as the word-level baseline, and the plan should state that word-level
is *aspirational where the aligner+language support it*, sentence-level otherwise.

**d) DAISY / accessibility framing is correct but could be sharper.** EPUB 3 Media Overlays is the
right modern target — it is literally a SMIL subset that "modernizes and generalizes DAISY"
([W3C EPUB MO 3.2](https://www.w3.org/publishing/epub32/epub-mediaoverlays.html),
[DAISY KB](https://kb.daisy.org/publishing/docs/sync-media/overlays.html)). Two additions: (i) commit
to **EPUB Accessibility 1.1 / WCAG 2.x conformance metadata** and a DAISY **ACE** accessibility-check
gate in QA, and (ii) consider DAISY's **Navigable Audio-only EPUB3** guidance for the bare-audio
deliverable so even the non-aligned output is navigable
([DAISY navigable audio-only](https://daisy.org/info-help/guidance-training/standards/navigable-audio-only-epub3-guidelines/)).

**e) Source-rights handling is strong; one factual freshener.** Per-jurisdiction PD verification and
separate rights-checks for translations/introductions are correct and ahead of most peers. Note the
US PD frontier now **rolls annually** (works published in 1929 entered the US public domain on Jan 1,
2025) — the plan should reference a maintained cutoff rather than a fixed year, and keep the "PD-US
but not life+70 elsewhere" exclusion it already has.

**f) Pronunciation accuracy gate is a genuine differentiator** (a mispronunciation miseducates a
literacy learner) and is well-designed (flagged lexicon, IPA/respelling, native-speaker review for
foreign items). One gap: the plan does not yet specify producing **SSML / lexicon files as
machine-readable artifacts** that travel with the work (see §5) — currently the lexicon is a review
aid, not a reusable output.

**g) Scope vs. `open-pronunciation-audio` sibling is cleanly drawn** (this project = narration +
alignment; the sibling = phonetics/pronunciation datasets). Multilingual is appropriately deferred as
an open question rather than over-promised. Completeness: all 17 sections present; metrics are
outcome-based with honest deferrals; the partner/channel gap is disclosed rather than papered over.

**Bottom line:** correct and conservative. The two most consequential fixes are **(a)** embedded/durable
synthetic-disclosure (C2PA + EPUB metadata, per EU AI Act/AB 942) and **(c)** resolving the word-level
alignment promise against the actual capability of the chosen aligner.

---

## 2. Competitive landscape

| Project | What it is | Strengths | Weaknesses (the gap we exploit) |
|---|---|---|---|
| **LibriVox** | Volunteer PD audiobooks | Huge catalog; zero-barrier volunteering; truly open/PD; mature proof-listen QA ([about](https://librivox.org/pages/about-librivox/)) | **No text-audio alignment / read-along**; **variable audio quality by design** ("any recording… as long as it is understandable," background noise, mixed mics) ([Wikipedia](https://en.wikipedia.org/wiki/LibriVox)); PD-only; no synthetic disclosure framework |
| **Project Gutenberg + Microsoft/MIT (2023)** | ~5,000 **AI/neural-TTS** audiobooks | Scale (35,000 hrs in ~2 hrs), free, distributed to Spotify/Apple/IA, lifelike neural voices ([TechCrunch](https://techcrunch.com/2023/09/19/project-gutenberg-puts-5000-audiobooks-online-for-free-using-synthetic-speech/), [MIT CSAIL](https://www.csail.mit.edu/news/ai-generates-thousands-free-audiobooks)) | **No read-along / no text-audio sync**; **synthetic-only** (no human option); no per-jurisdiction rights framing; voice-cloning demo (5s) shows the ethics gap our consent gate closes |
| **Bookshare / Learning Ally** | Accessible (DAISY) libraries for print-disabled | Excellent DAISY navigation; human + TTS; **read-aloud + highlighting**; free to US students ([Bookshare eligibility](https://www.bookshare.org/help-and-learning-articles/who-qualifies-for-bookshare), [Learning Ally](https://learningally.org/about-us/what-we-do/who-qualifies)) | **Eligibility-gated** (must prove a qualifying print disability, Chafee/Marrakesh exception) and **not openly licensed/redistributable**; closed ecosystem; nothing reusable for the open commons |
| **Standard Ebooks** | Hand-typeset PD ebooks, CC0 | Professional quality; **open-source GitHub PR contribution model**; full CC0 dedication ([what makes them different](https://standardebooks.org/about/what-makes-standard-ebooks-different)) | **Text only — no audio**; ideal *distribution/partner channel* for us, not a competitor's audio |
| **Internet Archive** | Open media host/archive | Free deposit, large audience, hosts LibriVox + PG synthetic audio | Host, not a producer of aligned read-alongs; no QA/consent framework of its own |
| **Storynory / Loyal Books** | Free kids' audio stories | Storynory: 1,000+ stories read by **professional actors**, weekly since 2005; Loyal Books: cleaner curated PD browsing ([Storynory](https://www.storynory.com/), [WeAreTeachers list](https://www.weareteachers.com/free-audiobooks-for-kids/)) | Storynory content is **not fully open/PD** (originals, ©); neither offers **synchronized text-highlighting**; no provenance/consent transparency |
| **Open TTS engines (Piper, Coqui/XTTS, Kokoro, StyleTTS2)** | The *tooling* for the synthetic path | Piper: fast, offline, runs on a Pi; XTTS-v2: 17 languages, ~94% of ElevenLabs quality ([Coqui](https://github.com/coqui-ai/tts), [local-TTS license guide](https://www.promptquorum.com/power-local-llm/local-tts-voice-cloning-piper-coqui-xtts)) | **License traps**: XTTS-v2 weights are **non-commercial (CPML)**; Piper moved from MIT (archived Oct 2025) to a **GPL-3.0 fork (OHF-Voice)** — the plan's "clearly-licensed voice" gate must check *model-weight* licenses, not just code |
| **Commercial audiobooks (Audible/ElevenLabs-narrated)** | Paid, polished | Top production values, marketing reach | Paywalled, proprietary, no open license; irrelevant to the open-commons beneficiary |

**Verified-need anchor.** The literacy premise is well-supported: reading-while-listening reliably
improves fluency and supports grapheme–phoneme mapping for struggling/L1 and adult learners
([fluency synthesis, PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC3320221/),
[reading-while-listening, Language Learning 2026](https://onlinelibrary.wiley.com/doi/10.1111/lang.12721)),
though some comprehension/vocabulary claims still rest on a thin study base — the plan's hedged "need
is real, fit must be validated" stance is correct.

---

## 3. Gaps we can fill

1. **The "aligned" gap.** The two biggest open libraries — LibriVox (human) and PG/Microsoft
   (synthetic) — both ship **bare audio with no text↔audio synchronization**. Open, word/sentence-level
   read-alongs in EPUB 3 Media Overlays are essentially **absent from the open commons**. This is the
   core whitespace.
2. **The "open + accessible" gap.** The only mature read-aloud-with-highlighting products (Bookshare,
   Learning Ally) are **eligibility-gated and non-redistributable**. Nobody offers DAISY-grade
   read-alongs that are *openly licensed and reusable by anyone* (educators, ELL apps, decodable-reader
   projects).
3. **The "quality floor" gap.** LibriVox explicitly tolerates variable fidelity; we ship an
   **objective audio-quality bar** (LUFS/true-peak/noise-floor, auto-checked) plus a **pronunciation
   gate** — meaningful for literacy learners where a mispronounced word miseducates.
4. **The "trustworthy synthetic" gap.** PG's synthetic library has no consent/labeling story; we
   ship **gated, consented, durably-labeled (C2PA) synthetic** narration — the responsible version of
   the same idea.
5. **The "multilingual aligned" gap.** Open read-alongs barely exist in English; in other languages
   they are near-zero. MFA/XTTS multilingual support makes a credible (deferred) expansion.
6. **The "reusable provenance" gap.** No peer ships a machine-readable per-work record (rights,
   jurisdiction, consent ref, alignment error, label) — a public audit trail others can trust and build on.

---

## 4. Differentiators to win (vs. LibriVox especially)

- **Synchronized highlighting, not bare audio.** The single sharpest wedge: LibriVox/PG give you a
  voice; we give you **word/sentence-highlighted read-along** (the most evidence-backed literacy
  support), in open EPUB 3 Media Overlays. *This is the strongest differentiator.*
- **Objective quality + pronunciation gates** vs. LibriVox's "understandable is enough" floor.
- **Two-surface licensing rigor + durable synthetic disclosure** (per-jurisdiction PD, signed
  revocable consent, C2PA-embedded human/synthetic label) — nobody else does both surfaces.
- **Open *and* accessible** — Bookshare-grade read-along usability without the eligibility wall.
- **Additive, upstream-first** into existing hosts (Standard Ebooks PR / IA deposit / Wikisource) —
  we *amplify* LibriVox/Gutenberg rather than fork the commons.
- **Reusable artifacts** — the alignment (SMIL/VTT/JSON) and pronunciation lexicon/SSML become inputs
  for other projects, multiplying value beyond the single recording.

---

## 5. Claude API leverage

**Where Claude adds leverage (preparation, not the audio):**

1. **TTS-script / text-prep automation** — normalize source text, expand abbreviations/numerals,
   segment into paragraph/sentence/word units for alignment, preserve structure (headings, verse,
   dialogue) — the deterministic-but-tedious pre-alignment work.
2. **Pronunciation lexicon + SSML markup** — detect proper nouns, foreign words, archaic spellings,
   technical terms; propose IPA/respelling and **emit machine-readable SSML/PLS lexicons** (closing the
   §1f gap) — *all flagged for human pronunciation review*, never auto-approved.
3. **Metadata, chaptering & accessibility records** — generate EPUB 3 metadata (titles, chapter
   breaks, attribution, `accessibilityFeature`/`accessMode` tags), the human/synthetic disclosure
   block, and draft per-work provenance/QA records for human sign-off.
4. **Rights-research drafting** — assemble the per-jurisdiction PD/license evidence dossier
   (source, edition, author/translator death dates, license id) for a human steward to verify.
5. **QA assistance** — diff the source text against an ASR transcript of the recording to *surface
   candidate* fidelity defects (skipped/added/substituted words) for a human reviewer to adjudicate.

**Where Claude must NOT decide (hard human-governed lines):**

- **Final audio quality and pronunciation** are **human-reviewed and signed off** — Claude flags,
  humans rule (a wrong word miseducates a new reader).
- **Voice consent and any cloning/synthesis ethics** are **human-governed** — no model decides whose
  voice is used, and the identifiable-person-cloning ban is absolute.
- **The synthetic/human disclosure is mandatory and not Claude's call to omit** — it is a gate.
- **License/PD status is verified by a human steward**, per jurisdiction — Claude drafts evidence,
  humans confirm; ambiguous → excluded.
- **No copyrighted / unverified source text** ever enters the pipeline regardless of model suggestion.

(The audio itself is produced by a **human narrator or a licensed TTS engine**, never "by Claude" —
consistent with the Elyos rule that the CLI never invokes/authenticates an agent and never runs
headless.)

---

## 6. Ten concrete optimizations

1. **Embed durable disclosure (C2PA + EPUB metadata), not just credits text** — make the
   human/synthetic label survive re-hosting/podcast distribution, satisfying EU AI Act Art 50 / CA
   AB 942 ([rulebook](https://www.transparentaudio.ai/resources/the-2025-transparency-rulebook-for-voice-ai)).
2. **Pin the aligner per language with MFA as the word-level baseline**; reclassify aeneas as
   sentence-level-only, and state word-level highlighting as capability-gated
   ([arXiv 2406.19363](https://arxiv.org/html/2406.19363v1)).
3. **Add a DAISY ACE accessibility-conformance check + EPUB Accessibility 1.1 / WCAG metadata** to
   the QA gate, so every read-along carries verifiable a11y conformance.
4. **Make consent *specific*** — enumerate purpose, deployment contexts, languages, retention, and
   withdrawal-effect fields in the consent schema (blanket consent is insufficient).
5. **License-check TTS *model weights*, not just code** — XTTS-v2 is non-commercial (CPML); Piper is
   now GPL-3.0; prefer permissive engines (Piper/Kokoro/StyleTTS2) and record the weight license in
   `voiceProvenance`.
6. **Ship the pronunciation lexicon/SSML as a reusable open artifact** per work (feeds re-narration,
   other languages, and the `open-pronunciation-audio` sibling).
7. **Adopt an ASR-vs-source fidelity-diff pre-screen** (e.g. WhisperX transcript diffed against the
   text) to triage fidelity defects before human QA — speeds the hard 0-defect gate.
8. **Target Standard Ebooks / Internet Archive as the first channel** — Standard Ebooks already runs
   a clean GitHub PR contribution model and CC0 dedication, the lowest-friction "additive accessibility
   contribution" path ([SE contribution](https://standardebooks.org/about/what-makes-standard-ebooks-different)).
9. **Define a stable, machine-readable per-work record + claim/lock index** published openly so
   parallel donated sessions and sibling projects can dedupe and reuse (alignment, lexicon, rights).
10. **Publish a held-out, hand-aligned reference corpus** as a versioned open benchmark — turns the
    alignment-accuracy bar into a reproducible, sharable yardstick others can adopt.

---

## 7. Parallel & perpendicular spin-offs

- **`open-childrens-books` / `decodable-readers`** — these produce exactly the short, structured,
  age-appropriate texts that read-alongs help most; a tight pipeline tie (their text → our aligned
  audio) is the highest-impact pairing.
- **`open-pronunciation-audio`** — our pronunciation lexicons/IPA/SSML are *inputs* to (and outputs
  enriched by) the phonetics sibling; share the lexicon artifact and reviewer pool, keep the scope
  boundary the plan already draws.
- **`literacy-from-zero`** — read-alongs are a delivery format for a zero-to-literacy curriculum;
  align our works to its scope-and-sequence.
- **`braille-ready-texts`** — same source-rights + accessible-EPUB backbone; a refreshable-braille
  + synchronized-audio combined output serves deafblind/low-vision learners.
- **`public-domain-translations`** — multilingual read-alongs depend on translated source texts; their
  output becomes our multilingual narration backlog (with separate rights-checks the plan requires).
- **Synchronized text-audio pipeline (horizontal)** — the align→SMIL/VTT/JSON→EPUB MO packaging is a
  **reusable engine** any of the above can call; extract it as a shared adapter library.
- **An MCP server** — expose the pipeline (text-prep, lexicon/SSML draft, forced-alignment runner,
  EPUB MO packager, a11y/C2PA conformance checks) as MCP tools so any agent in the donated lane can
  drive a consistent, policy-gated read-along workflow.

---

## 8. Open questions

- **Disclosure mechanism:** adopt **C2PA Content Credentials** now, or wait for the host's preferred
  signaling? Which EPUB metadata property is canonical for "synthetic narration"?
- **Aligner-per-language:** is MFA the word-level default everywhere, with WhisperX/aeneas as
  sentence-level fallbacks — and what is the per-language accuracy bar?
- **First channel:** Standard Ebooks PR vs. Internet Archive deposit vs. Wikisource — and each host's
  explicit stance on **AI-assisted alignment** and **AI-synthesized narration** (still the M0 blocker).
- **Synthetic path in M0?** Including a labeled synthetic segment exercises the disclosure/provenance
  tooling early — but raises the channel-acceptance risk; in or out for the cold-start unit?
- **TTS engine + weight license:** which permissively-licensed engine (Piper/Kokoro/StyleTTS2) for the
  gated path, given XTTS-v2's non-commercial weights?
- **Pronunciation-reviewer credential bar** per language (native speaker vs. linguist), and how
  foreign-language QA is staffed.
- **Minor narrators:** excluded by default, or only via a partner with a vetted guardian-consent process?
- **Content-suitability authority:** who rules a dated PD text appropriate for a children's/literacy
  context — maintainer, partner, or a published selection rubric?
- **Multilingual ownership:** here, or split to siblings? (overlaps `open-pronunciation-audio`,
  `decodable-readers`, `public-domain-translations`.)
