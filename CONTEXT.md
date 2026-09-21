# Context: learn.save7.org Course Spec

Glossary for the wayfinder map planning a curriculum + assessment spec for Save7's organ donation education platform, learn.save7.org. Spec-only effort: output hands off to a separate build.

## Terms

### Curriculum & Assessment

**Course**
The whole learn.save7.org program, all three Levels combined. Singular, capital-C when referring to the whole thing.

**Level**
One of the three depth-based tiers of the Course: Beginner, Intermediate, Advanced (see below). Not "course" — "course" is reserved for the whole program to avoid the ambiguity in early discussion ("one of the courses" meant one Level).

- **Beginner Level**: awareness and myth-busting. Primary audience: general public.
- **Intermediate Level**: donation process, ethics, South African legal framework. Audience: general public + healthcare-adjacent.
- **Advanced Level**: advocacy and greater depth for healthcare-adjacent learners (not full clinicians — deep surgical/clinical papers in the source corpus are background/citation material, not direct course content).

**Stage**
A module/unit within a Level. A Level is composed of one or more Stages.

**Source Corpus**
The reference material set grounding course content: the files in `Desktop/resources/` (10 PDFs + 1 video as of 2026-09-03), prioritizing South African–specific guidance. May grow; new sources get folded in without changing this definition.

**Baseline Assessment**
A single fixed-form MCQ test, cross-Level in scope (samples Beginner + Intermediate + Advanced content at reasonable/moderate difficulty), reused verbatim (not randomized) across all sittings so results are comparable over time. Purely diagnostic — no pass/fail; its value is the before/after comparison across sittings, not gating anything.

**Baseline Sitting**
One instance of a learner taking the Baseline Assessment. Every learner has 4 sittings on a fixed schedule: initial (at signup, before any Level) → after completing Beginner Level → after completing Intermediate Level → after completing Advanced Level.

**Certificate**
A per-Level completion artifact: learner's name + Save7 branding, downloadable, issued on completing each Level (so a learner who finishes all three Levels holds three Certificates, not one).

**Curriculum Spec**
The destination of this map: module list + learning objectives + source-to-content mapping per Level/Stage, plus the Assessment Blueprint. Does not include fully drafted lesson content or the actual Baseline question bank — those are downstream, ticketed separately.

**Assessment Blueprint**
The design of the Baseline Assessment and the per-Stage Quizzes: topic coverage, difficulty calibration, question count and structure. Not the question banks themselves.

**Stage Quiz**
A short comprehension-check quiz for one Stage, separate from the Baseline Assessment. Doesn't gate movement between Stages within a Level, but passing every Stage Quiz in a Level is required before that Level's Certificate is issued; each Level's Stages (3-5 per Level) each get one.

**Source Note**
An inline flag in the Curriculum Spec marking content drawn from a non-South-African-derived source (e.g. the Excellence in Deceased Donation course manual's Australian OTA/DonateLife-derived process framework), so lesson drafters never mistake it for South African-specific fact. Applies wherever such content appears in any Level, not just where first identified.

### Accounts, Login & Dashboard

**Student**
The only account type on learn.save7.org; anyone taking the Course. "Volunteer" describes a Student's intent, not a distinct account type — there is no separate volunteer account.
_Avoid_: Volunteer, Learner, User

**Admin**
A Save7 staff / program-coordinator account with oversight-only visibility into Students' progress. No content-management capability — content stays a separate, hand-edited concern outside this account type's scope. A single flat role, not tiered: every Admin sees the same global pool view (its Growth Indicators) and can drill into any Student's complete Progress Record unrestricted, and can edit the Eligibility Rule's required-flags list.
_Avoid_: Coordinator, Staff account

**Growth Indicator**
One of the aggregate, cohort-wide metrics Admin's pool view shows, derived at read time across every Student's Progress Record: cohort size, per-Level completion rate, per-Stage Quiz pass rate, average per-Level Baseline improvement, and cohort-wide Baseline trend. Scoped only to what the Progress Record already stores — distinct from the richer engagement metrics (time-on-task, login frequency, quiz-attempt history, etc.) still left as fog.

**Progress Record**
The stored state tracking one Student's advancement through the Course: their Baseline Sittings (up to 4, one per fixed slot, each holding score-by-Level sub-scores + a total, never raw answers), the pass/fail state and score of their latest attempt on each Stage Quiz, and timestamped completion flags for Stage, Level, and Certificate issuance. Feeds both the student-facing progress dashboard and admin oversight views.

**Improvement**
The before/after comparison a Student's Progress Record supports: the delta between their initial Baseline Sitting's per-Level sub-score and the Sitting taken after completing that Level, plus the full 4-point trend across all Sittings. Always computed from the Progress Record at read time — never a value stored in its own right.

**Nerve Center**
A separate, future Save7 platform for Save7 volunteers, mapped and built independently of learn.save7.org. This Course only produces the completion signal Nerve Center will eventually consume for its own account-eligibility decisions — it does not design Nerve Center's intake, validation, or accounts.
_Avoid_: Save7 OS (informal name for the same future platform)

**Eligibility Rule**
The admin-configurable, versioned condition that determines Nerve Center eligibility: a list of completion flags from a Student's Progress Record (e.g. which of Beginner/Intermediate/Advanced Level-complete) that must all be true. Editing the rule creates a new version; it never keys off Baseline Sitting scores or engagement data. The exact default set of required flags is not yet settled.

**Nerve Center Eligibility Signal**
The per-Student record produced by evaluating a Student's Progress Record against an Eligibility Rule: an eligible flag, the timestamp it was evaluated, and a reference to the Eligibility Rule version that produced it. This is what would eventually be exported to Nerve Center — never raw Baseline scores or completion history.
