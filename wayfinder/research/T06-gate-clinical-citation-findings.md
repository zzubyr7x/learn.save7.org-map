---
ticket: T06
title: "Findings: cite-or-cut audit of the 20 clinical gate questions"
status: research complete
date: 2026-09-21
issue: 34
---

# Clinical Gate Question Citation Audit — Findings

Audits the twenty `scope = 'GATE'`, `gate = 'clinical'` questions (`c1`–`c20`) that sit in
`learn_review_items` at severity 3, uncleared, against the Source Corpus and the citations
they already carry. Feeds the Save7 sign-off that
[#34](https://github.com/zzubyr7x/Learn.save7.org/issues/34) requires.

**No review item was cleared and no question was edited.** `transplant-alchemy/HANDOVER.md` §7
forbids clearing a content-review item in code; this pass only establishes what each question
is actually worth, so Save7 can sign off or cut with the evidence in front of them.

## Headline: the premise was wrong

HANDOVER.md §6 and `prisma/content/questions-gate.ts`'s file comment both say the twenty items
"assert MELD thresholds, peak-VO2 figures, Milan criteria and HPCSA registration rules that
**no supplied source backs**." Read against the data and the corpus, that is inaccurate in
four ways:

1. **Nine of the twenty already carry specific, checkable citations** (`c1`–`c5`, `c17`–`c20`)
   — the National Health Act 61/2003 with Regulation 9 of GN R180, Thomson *et al.* SAJCC 2021,
   and de Jager *et al.* SAMJ 2019. Only **eight** (`c9`–`c16`) carry the non-citation
   `"Reviewed 23 August 2026 against standard published listing criteria for this organ"`,
   which names no source at all. Three more (`c6`–`c8`) name an organisation but no document.
2. **Several of the supposedly unsourced thresholds are backed verbatim by papers already in
   the corpus** — `weill-2015-lung-candidate-selection.pdf` states `c12`'s and `c13`'s figures
   exactly, and `satcs-red-file.pdf` states `c7`'s and `c8`'s exactly. The citations were never
   attached; the sources were there all along.
3. **There is no HPCSA question.** `c1`'s five-years-since-registration rule is a **National
   Health Act Regulation 9** requirement, not an HPCSA registration rule, and it is cited. The
   map has already independently verified this exact rule in
   [#27](https://github.com/zzubyr7x/Learn.save7.org/issues/27), including the correction that
   the five years attaches to *one* of the two doctors.
4. **MELD and Milan are the real gap** — and a narrower one than "twenty questions". The string
   `MELD` appears **zero** times across the entire corpus. `Milan` appears three times, all of
   them the surname "Milano C" in author lists, never the Milan criteria.

## Method

- All twenty questions pulled from `learn_questions` joined to the keyed `learn_choices` row on
  the shared Supabase project (`zbaoziisqroqxfwcnhlb`), read-only.
- `verifiedAgainst` strings cross-checked against `prisma/content/questions-gate.ts` in
  `transplant-alchemy` — the two agree.
- Corpus read directly: the ten PDFs in `transplant-alchemy/public/resources/`. Note that
  CONTEXT.md's Source Corpus path (`Desktop/Save7 Course/resources/`) **does not exist** on this
  machine; the live corpus is at `transplant-alchemy/public/resources/`, with
  `Desktop/Save7 Course/source-material/` holding the unprocessed originals. Flagged separately.
- Where a source is named but not held locally, that is stated as such. **No threshold below is
  asserted from model knowledge**; claims I could not check against a document in hand are
  marked "needs direct read" rather than confirmed.

## Where the questions actually came from

`transplant-alchemy-101-study-guide.pdf` is the proximate source for the organ-indication
questions, and its own reference list names the primary sources the gate questions never cite:

| Named in the study guide's references | Backs | In corpus? |
| --- | --- | --- |
| Mehra *et al.* 2016, ISHLT listing criteria for heart transplantation, *JHLT* 35(1):1–23 | `c9`, `c10` | No |
| Canter *et al.* 2007, *Circulation* 115(5):658–676 (AHA paediatric statement) | `c11` | No |
| Mancini & Lietz 2010, *Circulation* 122(2):173–183 | `c9`, `c10` | **Yes** |
| Weill *et al.* 2015, *JHLT* 34(1):1–15 (ISHLT lung consensus) | `c12`, `c13` | **Yes** |
| SATCS *Organ and Tissue Donation Reference File* (Red File) | `c6`, `c7`, `c8`, `c17` | **Yes** |
| AMBOSS *Transplantation*, accessed 10 Feb 2026 | `c14`, `c15` (only trace) | n/a — tertiary |

The study guide itself is a **tertiary** document. Under the primary-source standard this map
holds ([#2](https://github.com/zzubyr7x/Learn.save7.org/issues/2)/[#3](https://github.com/zzubyr7x/Learn.save7.org/issues/3)/[#4](https://github.com/zzubyr7x/Learn.save7.org/issues/4)/[#6](https://github.com/zzubyr7x/Learn.save7.org/issues/6)),
"the study guide says so" is not a citation — but its reference list is a map straight to the
sources that are.

---

## Per-question verdicts

### A. Already cited — recommend sign-off as-is (8)

`c1`, `c2`, `c3`, `c4`, `c5`, `c18`, `c19`, `c20`

- `c2`–`c5` (brain-death prerequisites, apnoea test, confounders, brainstem reflexes) cite
  Thomson *et al.* SAJCC 2021, which **is** in the corpus
  (`sa-guidelines-determination-of-death-sajcc.pdf`).
- `c1`, `c18`, `c20` cite the National Health Act directly. `c1` is further corroborated by
  #27's independent read.
- `c19` (maintain haemodynamic stability post-certification) cites de Jager *et al.* SAMJ 2019,
  not held locally, but the claim is a generic donor-management statement carrying little risk.

### B. Backed by a supplied source — attach the citation, then sign off (5)

| Q | Claim | Supplied source that states it |
| --- | --- | --- |
| `c7` | Cornea exclusions: HIV/TB, leukaemia/lymphoma, prior laser surgery; cataracts do **not** disqualify | Red File p.41 — **verbatim match** |
| `c12` | COPD: BODE ≥7 or FEV1 <15–20% predicted | Weill 2015, "Timing of listing" — **verbatim match** |
| `c13` | IPF: FVC decline ≥10% or DLCO decline ≥15% over 6 months | Weill 2015, "Timing of listing" — **verbatim match** |
| `c17` | GCS ≤4 mandates referral | Red File §2.4 — **verbatim match** |
| `c9` | NYHA IV with EF <20% | Mancini & Lietz 2010 (LVEF ≤20%, NYHA IV) + study guide |

Two small precision gaps worth fixing while the citation is attached:

- **`c17`** — the Red File says GCS ≤4 *"in a patient with a catastrophic brain injury"* and
  *"not explained by sedation"*. The keyed answer drops both qualifiers. As written it implies
  any GCS ≤4 triggers referral, including a sedated patient.
- **`c9`** — source says LVEF **≤**20%; the question says **<**20%.

### C. Backed by a supplied source, but the answer is *weaker* than the source (2)

- **`c6`** (extended/marginal criteria: donor age, comorbidity, organ-specific ischaemic time) —
  the Red File and study guide both cover extended-criteria donors with hypertension, diabetes
  and HIV. The substance holds; the citation should move off "Centre for Tissue Engineering"
  onto the Red File.
- **`c8`** (heart valve donation) — the exclusion half (cause of death unknown, direct cardiac
  trauma) matches the Red File exactly. But the age half hedges — *"age limits are set by the
  tissue bank"* — and the explanation tells the reader to *"quote the bank's own criteria rather
  than a remembered range"*, when the Red File states the SA range plainly: **6 months up to and
  including 55 years**. A previous reviewer softened this away from a figure the corpus actually
  supports. Recommend restoring the range and citing the Red File.

### D. Primary source named but not held — needs a direct read before sign-off (3)

- **`c11`** (paediatric: hypoplastic left heart, severe Ebstein, restrictive cardiomyopathy) —
  Canter *et al.* 2007 is named in the study guide's references and is the right authority.
  Not in the corpus. Obtain and check, or cut.
- **`c16`** (renal transplant for CKD 5 / ESRD) — stated in the study guide; clinically
  uncontroversial, but currently rests on a tertiary source. Cheap to ground in KDIGO or an SA
  nephrology guideline.
- **`c10`** — see below; it needs the read *and* a rewrite.

### E. No supporting source anywhere in the corpus (2)

- **`c14` — MELD ≥15.** Zero occurrences of "MELD" in the entire corpus. Traces only to AMBOSS.
  Genuine primary sources exist (Merion *et al.*, *Am J Transplant* 2005, on survival benefit
  above MELD 15; the OPTN "Share 15" allocation policy) but **neither has been read here**.
  Additional concern for an SA course: MELD ≥15 is a **US allocation** threshold. South Africa
  does not run UNOS-style MELD-based allocation, so even correctly cited this may warrant a
  **Source Note** under [#6](https://github.com/zzubyr7x/Learn.save7.org/issues/6)'s convention,
  or be the wrong question for this audience.
- **`c15` — Milan criteria** (one lesion ≤5 cm, or up to three each ≤3 cm, no macrovascular
  invasion). No corpus support. The primary source is Mazzaferro *et al.*, *NEJM*
  1996;334:693–699 — **not read here**. The criteria are stated accurately as far as I can tell,
  but that is not the same as verified, which is the whole point of the standard.

### F. Substantive accuracy problem, not merely a citation gap (1) ⚠️

**`c10` — peak VO2. Recommend cut or rewrite, not sign-off.**

The keyed answer is *"Peak VO2 <10–12 mL/kg/min (or <50% of predicted value)"*.

- Mancini & Lietz 2010, **in the corpus**, states the listing cutoff was *"lowered from a peak
  V̇O2 ≤14 to ≤12 mL·kg⁻¹·min⁻¹"* — a **single** threshold, not a 10–12 band. Its indications
  table lists *"peak V̇O2 ≤12"*.
- The lower bound of **10** appears in no source I can find, in the corpus or in the study
  guide's reference list.
- The clinically decisive detail is **missing entirely**: which number applies depends on
  beta-blocker tolerance (ISHLT 2016 uses ≤14 off beta-blockers, ≤12 on them). A question that
  keys a bare number without that conditional teaches the wrong thing even if a number in the
  range is defensible.
- `<50% of predicted` does appear in the literature for younger patients and women, but
  Mancini & Lietz mention percent-predicted VO2 only as *a parameter that has been examined*,
  citing Aaronson & Mancini 1995 — not as a listing threshold.

This is the one item where the problem is the content, not the paperwork.

---

## Summary for sign-off

| Bucket | Questions | Count | Recommendation |
| --- | --- | --- | --- |
| A — already cited | c1–c5, c18, c19, c20 | 8 | Sign off as-is |
| B — corpus-backed, attach citation | c7, c9, c12, c13, c17 | 5 | Attach source, fix 2 precision gaps, sign off |
| C — corpus-backed, answer too weak | c6, c8 | 2 | Restore the SA figures, cite Red File, sign off |
| D — source named, not yet read | c11, c16 | 2 | Obtain and read, then sign off or cut |
| E — no corpus support | c14, c15 | 2 | Read Mazzaferro / Merion, or cut. c14 also has an SA-relevance problem |
| F — accuracy defect | c10 | 1 | **Cut or rewrite** |

**Fifteen of twenty are already defensible or become so by attaching a source that is already
in hand.** The genuinely open set is five: `c11`, `c14`, `c15`, `c16` need a document read, and
`c10` needs cutting or rewriting.

## Carried forward

- **All forty gate questions key to option `'a'`.** HANDOVER §6 flags this; the portal survives
  it by shuffling at render. Out of scope here, and moot for Learn, which does not render GATE
  questions ([#33](https://github.com/zzubyr7x/Learn.save7.org/issues/33)) — but it must not be
  lost if anything ever renders them from stored order.
- **CONTEXT.md's Source Corpus path is wrong.** It reads `Desktop/Save7 Course/resources/`,
  which does not exist. The corpus is at `transplant-alchemy/public/resources/` (10 PDFs, as the
  definition says), with originals under `Desktop/Save7 Course/source-material/`. Two commits
  (`3f4f800`, `a22ff9e`) attempted this correction and it is still wrong.
