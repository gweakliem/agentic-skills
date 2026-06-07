---
name: learning-path-creator
description: Create comprehensive, research-grounded self-study curriculums for any topic — from technical subjects (programming languages, frameworks, sciences) to humanities (history, philosophy, literature) to skills (cooking, writing, design). Use this skill whenever a user wants a learning path, study plan, curriculum, roadmap, syllabus, or self-study guide for any topic, even if they don't use those exact words. Trigger phrases include "help me learn X," "create a curriculum for X," "I want to study X," "where do I start with X," "give me a roadmap for X," or any request to structure self-directed learning. Use this even when the user only loosely implies wanting structure for their learning.
---

# Learning Path Creator

This skill produces a coherent, research-grounded self-study curriculum for any topic the learner wants to study. Output is consistent in shape — same major sections, same per-phase anatomy — regardless of whether the topic is technical, humanities, scientific, or practical. A learner who uses this skill twice (once for Rust, once for the Meiji Restoration) gets the same kind of artifact and knows where to look for what.

The point is to give the learner something they can actually start studying tomorrow: real resources, concrete activities, clear capabilities to aim at. Not a vague "explore this topic" sketch.

## When to use this skill

Trigger this whenever a user wants help structuring their learning of any topic. Don't wait for specific words like "curriculum" or "learning path" — phrases like "I want to get into X," "where do I start with Y," "help me understand Z deeply," or even "I'm curious about W and want to learn it properly" all qualify.

Do NOT use this skill for:
- Quick informational questions ("what is supervised learning?" — just answer)
- Single-resource recommendations ("what's a good Rust book?" — just answer)
- One-off tutorials ("show me how to write a bash for-loop" — just teach)

The threshold is whether the learner wants a *structured path* through a topic rather than a piece of information about it.

## Workflow

### 1. Establish learner context

Before researching or writing, gather context with three questions. If the user has already supplied any of them in their initial message, skip those — only ask what's missing. Bundle the remaining questions into one message; don't drip them.

The three questions:

1. **Current level** — Total beginner, some exposure, or moderately experienced and looking to deepen?
2. **Goal** — Why this topic? (Career, project, personal interest, exam, etc.) This shapes what gets emphasized and what gets skipped.
3. **Time horizon** — Casual exploration over a few weekends? Sustained study over weeks? A multi-month deep dive?

If the user explicitly waves off the questions ("just give me something"), default to: beginner, broad personal interest, ~4 weeks of moderate study. Don't keep asking.

### 2. Research the topic

Do enough research to ground both the structure of the curriculum and the resources you'll recommend. Use web search and web fetch:

- Map the topic's natural sub-areas — this informs how to break it into phases
- Identify which concepts are foundational vs. which sit downstream
- Find well-regarded resources: books, courses, articles, video series, papers, primary sources
- Notice what experts and educators commonly recommend as starting points and as deeper dives
- **Identify scholarly debates and competing interpretations.** For most non-trivial topics — historical, philosophical, scientific, even some technical — there are real disagreements among experts about how to frame the subject. Surface 2–3 of these, briefly, in the topic summary, and let them inform synthesis activities rather than picking one school's view and pretending it's settled. (For the French Revolution: Marxist vs. revisionist; for machine learning: connectionist vs. symbolic traditions; for nutrition: nearly everything.) Flattening real debate into a single tidy answer is a quiet way to mislead the learner.
- **Look for primary sources where they exist.** For historical topics, philosophical traditions, classical sciences, legal subjects, and many others, primary source material — speeches, treatises, papers, letters, code, recordings — is often available online and is irreplaceable. Curated open archives (CHNM, Internet Archive, Project Gutenberg, university digital collections, arXiv) deserve a deliberate search, not a passing mention. A curriculum that has the learner reading Rousseau himself rather than only reading *about* Rousseau is a meaningfully better curriculum.

Aim for 5-10 substantive searches/fetches as a default. Lean toward more research for fast-moving technical topics (specific frameworks, recent scientific areas) and less for stable classical topics (ancient history, foundational mathematics) — but always verify your resource recommendations actually exist and are accessible. Don't recommend a book you're hallucinating.

A useful trick: search for "best [topic] resources for beginners" and "[topic] reading list" and "[topic] syllabus" — educators and practitioners often publish their own recommendations, and these tend to be more reliable than aggregator sites. For historical and humanities topics, also try "[topic] historiography" or "[topic] schools of thought" to surface debates you might otherwise miss.

### 3. Decide structure

Based on the topic and the learner's context:

**Phase count**
- 3 phases: short topics or casual time horizons
- 4-5 phases: typical, most curriculums
- 6 phases: only for genuinely sprawling topics where each phase carries real weight

Don't pad to hit a number. Each phase should feel necessary.

**Output format**
- **Single markdown file** for short curriculums (3 phases or casual time horizon)
- **Folder with index + per-phase files** for substantial curriculums (4+ phases or sustained/deep study)

The folder format makes it easier to work through the curriculum over time and to update individual phases without scrolling through a giant document.

**Phase progression**
General → specific is the spine, but adapt to the topic:
- Foundations → core → applications → synthesis (most topics)
- Chronological (historical topics, biographies)
- Theory → practice (crafts, experimental sciences)
- Tools → patterns → projects (programming, design)

Pick what the topic actually wants, not a forced template.

### 4. Generate the curriculum

Write substantively, following the structure in `## Curriculum structure` below. Don't produce skeletons with placeholder bullets. The learner should be able to begin studying with what you produce.

A few things to hold yourself to as you write:

- **Be specific.** "Read about World War I" is useless. "Read chapters 4-7 of Tuchman's *The Guns of August*; pair with Hardcore History 'Blueprint for Armageddon' Episode 1 for narrative drive" is useful.
- **Resources should be real and findable.** If you're not confident a resource exists, search for it. Better to recommend fewer real things than more imagined ones. Hallucinated resources are the most embarrassing failure mode of this skill — guard against it.
- **Don't pad.** Better four substantive phases than six mediocre ones. If a section has nothing real to say, cut it.
- **The learner is smart.** Don't condescend. Skip filler like "remember to take breaks!" and "learning is a journey!"
- **Tone is warm but not chummy.** This is a study companion, not a self-help book.

### 5. Save and present

Save outputs to `/mnt/user-data/outputs/`. For folder-format curriculums, save the whole folder. Use `present_files` to share with the user, leading with the index/main file. Keep your reply brief — the learner has the document, they don't need a recap.

## Curriculum structure

Every curriculum has these sections, in this order. The header levels below are how they should appear in the final document.

### Top-level (index file or top of single-file output)

**`# Learning Path: [Topic]`**

A one-sentence tagline below the title saying what this path covers and who it's for. Example:
> *A four-phase path from zero programming experience to writing idiomatic, memory-safe Rust — for engineers comfortable with another language who want to understand ownership and write production-quality systems code.*

**`## Topic summary`**

Two to three substantive paragraphs synthesizing what the topic is, why it matters, and what its main contours are. Mention key sub-areas, schools of thought, controversies, or fault lines so the learner has a mental map *before* diving in. This is informed by your research — don't write a Wikipedia rewrite.

**`## What mastery looks like`**

A concrete checklist of 6-12 capabilities the learner should have after completing the curriculum. Phrase as things they can *do, explain, or recognize* — not things they "understand" (too vague). Examples:
- ✅ "Explain the bias-variance tradeoff and give a concrete example of each failure mode."
- ❌ "Understand the basics of machine learning."

This is the contract. Every phase should serve this list.

**`## Path overview`**

A scannable map of the phases. One line each: phase name, what it covers, estimated time. Lets the learner see the whole journey at a glance. A markdown table with columns *Phase / Title / What it covers / Time* works well here — it scans much faster than a bulleted list and is easy to update.

**`## Top resources`**

5-8 carefully chosen resources with brief annotations on what each is good for. Mix formats (book, course, video series, article collection, primary sources) and difficulty levels. These are the *highlights* — the per-phase resource lists go deeper.

### Per phase

Each phase has the same anatomy. Don't deviate — consistency is part of the value to the learner.

**`# Phase N: [Title]`** (or `## Phase N` if in a single file)

**`## Goal`** — One sentence: what the learner will be able to do after this phase.

**`## Estimated time`** — A range (e.g., "1-2 weeks of moderate study, ~5-8 hours/week").

**`## Why this phase, here`** — 2–3 sentences on what this phase contributes and why it sits where it does in the path. Helps the learner see the logic. This matters more than it might seem, especially for non-technical topics where the natural progression isn't obvious. For programming, "you can't do X without first knowing Y" is often self-evident; for history, philosophy, or a craft, the order is a defensible choice rather than a logical necessity, and the learner deserves to know why you made it.

**`## Key concepts`** — Bulleted list of the specific things the learner will study. Be concrete: "linked lists, hash tables, and binary trees, including Big-O analysis" — not "data structures."

**`## Resources`** — 3-6 specific resources with annotations. Each annotation should say what the resource is good for *and* how to use it (read cover-to-cover, skim chapters X-Y, watch lectures 1-5, do exercises 1.1-1.8, etc.). Mix formats where possible. Example:
> *Linear Algebra Done Right* (Axler) — best for the determinant-free approach to vector spaces. Read chapters 1-5 carefully and work the exercises. Skip 9-10 unless going on to functional analysis.

**`## Distillation`** — A short paragraph stating what the learner should be able to *articulate* by the end of the phase. This is what they can say in their own words, not just recognize on a flashcard. Treat it as a self-test: if they can't say this stuff, they're not done with the phase.

**`## Synthesis activity`** — One or two concrete things to do that force integration of the phase's material. See `## Synthesis activities` below for a menu.

**`## Self-check questions`** — 3-5 questions the learner can use to test themselves. These should require synthesis or application, not pure recall. "What is X?" is bad; "Why would you use X over Y in situation Z?" is good.

### After the phases

**`## Bibliography`** — All resources mentioned across the curriculum. **Group by what fits the topic, not by a fixed template.** For technical and skill-based topics, grouping by *format* (Books, Courses, Video Series, Documentation, Communities) usually works best. For humanities, history, and other reading-heavy topics, grouping by *purpose* (Comprehensive narratives, Interpretive works, Focused studies, Primary sources, Reference) usually works better, because format doesn't tell the learner which book to reach for when. Include URLs where applicable. Note free vs. paid where it matters for accessibility. The bibliography also implicitly serves as the trail of what you researched in building the curriculum — make it complete enough to live up to that role.

**`## Where to go next`** — A short section on what comes after the curriculum: subspecialties to dive into, communities to join, ongoing reading, related topics that pair well, signs you're ready to specialize.

## Synthesis activities

Each phase needs a synthesis activity that forces integration, not just review. Choose from this menu — or invent something topic-specific in the same spirit. Match the activity to the topic's nature.

- **Build/make something** — For technical or craft topics. A program, recipe, written piece, design, model.
- **Ship a real project** — A heavier version of "build something," reserved for one phase (often the second-to-last) of project-based curriculums. The bar is *publishable*: hosted on GitHub, documented, tested, or otherwise ready for someone other than the learner to encounter.
- **Teach it back (Feynman)** — Write or record an explanation aimed at someone who knows nothing. Reveals where understanding is shallow.
- **Compare & contrast** — Pick two related concepts/figures/approaches from the phase. Write 1–2 pages on how they differ and why it matters.
- **Apply to a real case** — Use the phase's concepts to analyze a real-world example, paper, artifact, or current event.
- **Reconstruct from memory** — After studying, close everything and reproduce the key argument/diagram/derivation, then check your work.
- **Steel-man a critic** — Especially good for humanities. Articulate the strongest objection to what was just studied.
- **Source dialogue** — Read two sources that disagree and write a synthesis. Particularly useful for topics with active scholarly debate.
- **Annotated walkthrough** — For technical topics: pick something real (a codebase, a paper, an artifact) and walk through it line by line, annotating with what each part does and why.
- **Decide and defend** — Confront the learner with a real choice the topic involves (a vote, a design decision, an interpretive stance) and have them defend a position with evidence. Especially good for politics, ethics, history, and design.

A history phase shouldn't have "build a project"; a programming phase shouldn't lean only on "compare and contrast." Use what fits.

**Vary the medium across phases when you can.** A curriculum where every synthesis activity is "write a 1,500-word essay" will feel grinding even to someone who likes writing. Try to mix at least two distinct types across the phases — a build, an essay, a teach-back, a comparison — so the learner is asked to engage in different ways. This is harder for purely-reading topics like history, but even there you can vary scope (memo vs. essay vs. annotated source) and target (write to the king vs. write to a friend who knows nothing vs. write to a future historian).

## Failure modes to avoid

These are the most common ways this skill produces bad output. Watch for them.

**Hallucinated resources.** Recommending books, courses, or papers that don't exist. Always verify. If unsure, search.

**Vague mastery checklist.** "Understand the foundations of X" tells the learner nothing. Push for specificity until each item names a concrete capability.

**Padded phases.** Stretching a 3-phase topic to 6 phases by inventing weak intermediate steps. Trust the topic's natural shape.

**Generic resource annotations.** "A great book" is not an annotation. The annotation should tell the learner *what to do with* the resource.

**Treating the user's level as fixed.** A beginner asking about cryptography may need a different starting point than a beginner asking about cooking. Adapt.

**Burying the lede in the summary.** The topic summary should give the learner a real mental map, not warm up to one.

**Flattening real scholarly debate.** Picking one school's interpretation and presenting it as settled when it isn't. If reasonable experts disagree about how to frame a topic, the curriculum should say so — at minimum in the topic summary, ideally also reflected in resource selection and synthesis activities.

**Activity monoculture.** Every synthesis activity being a 1,500-word essay, or every one being a coding project. Even within the constraints of a topic, vary the demand: scope, audience, medium.

**Ignoring primary sources.** For topics where they exist and are accessible — historical, philosophical, classical scientific, legal — primary sources should appear in resource lists and ideally in synthesis activities, not be replaced entirely by secondary literature.

## Quick example: good vs. bad

**Bad mastery checklist item:**
> Understand the basics of machine learning.

**Good:**
> Explain the bias-variance tradeoff and give a concrete example of each failure mode in a model you'd train.

**Bad resource annotation:**
> *Linear Algebra Done Right* by Sheldon Axler — a great book.

**Good:**
> *Linear Algebra Done Right* (Axler) — best for the determinant-free approach to vector spaces. Read chapters 1-5 carefully and do the exercises. Skip 9-10 unless going on to functional analysis.

**Bad synthesis activity:**
> Review what you've learned in this phase.

**Good:**
> Pick a real codebase on GitHub (suggest: Flask source) and find three uses of the patterns covered here. For each, write a paragraph explaining what the pattern accomplishes and what alternative was rejected.
