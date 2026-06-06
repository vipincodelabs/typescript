---
name: create-typescript-doc
description: >
  Generates a fully self-contained HTML documentation page for one phase of
  the TypeScript learning path. Parses typescript.md, produces deep-dive
  concept panels with 14 teaching sections per topic, and writes phase-N.html
  with dark theme, sticky sidebar, collapsible panels, and copy buttons.
---

# Skill: create-typescript-doc

## Purpose

Generate a complete, self-contained HTML reference page for one phase of the
TypeScript learning path defined in `typescript.md`. Every concept gets a full
14-section deep dive written in plain human language — like a senior engineer
sitting next to you and explaining it from scratch.

## Invocation

```
/create-typescript-doc Phase N
```

Examples:
- `/create-typescript-doc Phase 1` → writes `phase-1.html`
- `/create-typescript-doc Phase 6` → writes `phase-6.html`

---

## Teaching Philosophy

These docs are for a developer who knows JavaScript but is learning TypeScript.
Write every explanation as if you are a patient human mentor, not a reference
manual. That means:

- **Start simple, then go deep.** Give the plain-English version first, then
  the technical version. Never lead with jargon.
- **Explain the "why" before the "how".** People remember concepts when they
  understand the problem being solved, not just the syntax.
- **Use analogies.** Compare TypeScript concepts to everyday things or familiar
  JavaScript patterns whenever it helps.
- **Show real code, not toy snippets.** Examples should look like code you'd
  actually write at work, not `foo`/`bar` placeholders.
- **Be honest about gotchas.** Don't sugar-coat edge cases or mistakes —
  point them out clearly so the reader doesn't get burned later.
- **Treat the reader as intelligent.** Don't over-explain obvious things, but
  never skip a step when the concept is genuinely subtle.

---

## Step 1 — Parse the Source

Read `typescript.md` and locate the requested phase. Each phase block looks like:

```
# PHASE N — Title

## Module N: Title

Topics:
* topic1
* topic2

Project:
* Project Name
```

Extract:
- Phase number and title
- All modules (number + title)
- Each module's topic bullet list
- Each module's project name

---

## Step 2 — Generate Content Per Module

For every module, produce the following. Do not skip any section.

### 2.1 Module Header

- Module number and title as `<h2>`
- A 2–3 sentence human intro: what this module covers, why it matters, and
  what the reader will be able to do after finishing it

### 2.2 Topics Table

A summary table with columns: **Topic** | **What You'll Learn** | **Difficulty**
One row per topic from `typescript.md`. Difficulty: Beginner / Intermediate / Advanced.

### 2.3 Deep-Dive Panel Per Topic

For **each topic** in the module, generate a collapsible panel with all 14
sections below. Every section must have real, substantive content — no
placeholder text.

---

#### Section 1 — Definition

Two-part definition:

**Simple explanation** (1–2 sentences, plain English, no jargon):
Write it so a complete beginner understands immediately. Use an analogy if
it helps.

**Technical explanation** (2–3 sentences):
Now introduce the correct terminology and explain it precisely. Connect back
to the simple explanation so the reader can bridge the two.

---

#### Section 2 — Why It Exists / What Problem It Solves

Tell the story of the problem first, then show how this feature fixes it.
Format: describe a realistic JavaScript scenario that goes wrong (wrong output,
runtime error, impossible to debug), then explain how TypeScript's feature
eliminates that exact problem. 3–5 sentences. Include a short "without
TypeScript" code snippet showing the bug, and a "with TypeScript" snippet
showing the error caught at compile time.

---

#### Section 3 — Why and When to Use It

A practical guide on when this feature is the right tool. List 3–5 concrete
situations with one-line explanations:

- "Use it when you need X because Y"
- "Use it when working with Z to get A"

Be specific. Mention real contexts: React components, API responses, database
models, utility functions, etc.

---

#### Section 4 — When NOT to Use It

Equally important. List 2–4 situations where this feature is the wrong choice
or causes more harm than good. Explain what to use instead.

Examples of what to cover:
- Over-engineering simple cases
- When `any` is actually acceptable (and when it is not)
- When an interface would be better than a type alias, or vice versa
- When generics add complexity without benefit

---

#### Section 5 — How It Works Internally

Explain what TypeScript actually does with this feature — what the compiler
checks, how it transforms the code, what the output JavaScript looks like.
Where the concept has interesting runtime behavior (enums, decorators, classes),
show the compiled JS output side-by-side with the TypeScript source. Where it
is purely compile-time (generics, utility types, conditional types), explain
what the type checker does step by step. 4–8 sentences or a numbered steps list.

---

#### Section 6 — Syntax Explanation

A fully annotated code block. Every TypeScript-specific piece of syntax gets
an inline comment explaining exactly what it means and why it is there.
Do not skip anything that could confuse a reader coming from JavaScript.

```typescript
// Every TypeScript-specific symbol gets explained
function greet(name: string): string {
//                   ^^^^^^   ^^^^^^
//                   |        return type annotation
//                   parameter type annotation
  return `Hello, ${name}`;
}
```

Follow up with a prose summary of the syntax rules (1–3 sentences covering
any edge cases or variants of the syntax).

---

#### Section 7 — Practical Code Example

A standalone, runnable TypeScript snippet (15–40 lines) that demonstrates the
concept clearly. Requirements:
- Valid TypeScript — no pseudocode
- Self-contained — no imports from packages unless clearly labelled
- Commented at key lines to explain what is happening
- Includes `// Output:` or `// Type:` comments showing expected results

---

#### Section 8 — Real-World Example

A production-realistic code snippet. Label the context at the top (e.g.
`// Express route handler`, `// React component`, `// Prisma schema helper`,
`// Zod validation schema`). Use tools relevant to the current phase:
- Phase 1–4: pure TypeScript, no framework dependencies
- Phase 5: design pattern implementations
- Phase 6: Express, Node.js, Prisma, Drizzle ORM, Zod
- Phase 7: React, Next.js, React Query, Zustand, tRPC
- Phase 8: library authoring, declaration files, recursive types

The snippet should be 20–50 lines and look like real code someone would
write at a company, not a tutorial exercise.

---

#### Section 9 — Real-World Use Cases

A bullet list of 4–6 concrete situations where developers use this feature
in production. Each bullet: one sentence describing the context + one sentence
explaining the benefit. Be specific — name actual libraries, frameworks,
patterns.

---

#### Section 10 — Common Mistakes and How to Avoid Them

3–5 numbered mistakes. For each:
- **Mistake name** (bold label)
- Wrong code block (labelled `// WRONG` or `// BAD`)
- Correct code block (labelled `// CORRECT` or `// GOOD`)
- 1–2 sentence explanation of why the wrong version fails or causes problems
  and what the fix actually achieves

---

#### Section 11 — Best Practices

5–7 numbered best practices. Each one:
- Stated as a clear rule ("Do X", "Prefer X over Y", "Always Z when W")
- Followed by 1–2 sentences explaining the reasoning
- Include a short code example if the rule is non-obvious

---

#### Section 12 — Interview Questions with Answers

5 interview questions. Mix of difficulty levels — label each one:
`[Easy]` / `[Medium]` / `[Hard]`

Format:
```
Q: Question text?

A: Answer in 3–5 sentences. Be precise but conversational. Include a one-line
   code snippet inside the answer if it makes the answer clearer.
```

Cover: conceptual understanding, practical application, edge cases, and
comparison with alternatives.

---

#### Section 13 — Practice Challenge / Exercise

A small, self-contained coding exercise. Format:

**Goal:** What to build in 1 sentence.

**Requirements:**
- Bullet list of 3–5 specific TypeScript constraints to practice

**Starter code:**
```typescript
// Skeleton with TODOs — enough scaffolding to get started without
// giving away the solution
```

**Expected result:**
What the finished code should produce (type shape, output, or behavior).

**Hint:** One sentence nudge if they get stuck.

---

#### Section 14 — Key Takeaways / Summary

5–7 bullet points. Each one is a single crisp sentence capturing the most
important thing to remember about this concept. Written so the reader can
glance at these bullets in 30 seconds and recall the whole topic.

End with one "mental model" sentence — a metaphor or one-liner that makes the
concept stick.

---

### 2.4 Module Mini-Project

After all topic panels, a dedicated project section containing:

- **Project name** from `typescript.md`
- **What you'll build**: 3–5 bullet features
- **TypeScript concepts used**: which topics from this module appear in it
- **Architecture overview**: a short diagram or description of the structure
- **Starter code**: a skeleton `.ts` file with types stubbed, TODOs marked,
  and comments pointing to which concept each section practices
- **Step-by-step instructions**: numbered build steps
- **Stretch goals**: 2–3 optional extensions to push further

---

## Step 3 — HTML Structure

One self-contained `.html` file. Zero external dependencies — all CSS and JS
inline. No CDN links.

### Layout

```
┌───────────────────────────────────────────────────────┐
│  Sticky Header: Phase N — Title          [progress █░░] │
├────────────────┬──────────────────────────────────────┤
│ Sticky         │  Main content area                   │
│ Sidebar        │                                      │
│                │  Module 1: Title          [✓ done]   │
│ [search box]   │    Topics Table                      │
│                │    [▶ Topic 1] (collapsed)            │
│ • Module 1     │    [▶ Topic 2] (collapsed)            │
│ • Module 2     │    …                                 │
│ • Module 3     │    Mini-Project                      │
│   …            │                                      │
│                │  Module 2: Title                     │
│                │    …                                 │
└────────────────┴──────────────────────────────────────┘
                                              [↑ Top btn]
```

### Required Features

1. **Dark theme** — `#0f1117` background, `#e2e8f0` text, `#3b82f6` accent
2. **Sticky sidebar** — fixed left column, jump links per module, active link
   highlighted via scroll-spy
3. **Sticky header** — phase title + thin scroll progress bar underneath it
4. **Collapsible panels** — `<details>/<summary>` per topic; collapsed by
   default; smooth CSS transition on open
5. **Syntax-highlighted code** — inline keyword/string/comment coloring via
   `<span>` + CSS only; no Prism, no highlight.js
6. **Copy button** — on every code block; shows "Copied!" for 1.5 s
7. **Module checkboxes** — checkbox on each module header; state saved in
   `localStorage`; checked modules show a strikethrough + green label
8. **Topic search** — text input in sidebar filters visible panels by name
   (case-insensitive substring match)
9. **Back-to-top button** — appears after 400 px of scroll; smooth-scrolls up
10. **Difficulty badges** — color-coded pill on each topic panel summary:
    Beginner (green) / Intermediate (yellow) / Advanced (red)
11. **Section tabs inside panels** — the 14 sections are navigable via
    small tab pills at the top of each open panel so the reader can jump
    directly to "Best Practices" or "Interview Questions" without scrolling

### CSS Variables

```css
:root {
  --bg:            #0f1117;
  --bg-card:       #1a1f2e;
  --bg-code:       #1e2433;
  --border:        #2d3748;
  --text:          #e2e8f0;
  --text-muted:    #94a3b8;
  --accent:        #3b82f6;
  --accent-hover:  #2563eb;
  --success:       #10b981;
  --warning:       #f59e0b;
  --error:         #ef4444;
  --sidebar-width: 260px;
  --header-height: 56px;
  --radius:        8px;
}
```

### HTML Skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Phase N — Title | TypeScript Learning Path</title>
  <style>/* all CSS here */</style>
</head>
<body>

  <div id="progress-bar"></div>

  <header id="site-header">
    <h1>Phase N — Title</h1>
  </header>

  <div id="layout">

    <nav id="sidebar">
      <input type="text" id="topicSearch" placeholder="Search topics…" />
      <ul id="module-nav">
        <li><a href="#module-1">Module 1: …</a></li>
        …
      </ul>
    </nav>

    <main id="content">

      <section id="module-1" class="module">
        <div class="module-header">
          <label>
            <input type="checkbox" class="module-check" data-id="module-1" />
            <h2>Module 1: Title</h2>
          </label>
        </div>
        <p class="module-intro">…</p>

        <table class="topics-table">…</table>

        <div class="topic-panels">
          <details class="topic-panel">
            <summary>
              <span class="topic-name">Topic Name</span>
              <span class="badge beginner">Beginner</span>
            </summary>
            <div class="panel-tabs">
              <button class="tab active" data-tab="definition">Definition</button>
              <button class="tab" data-tab="why-exists">Why It Exists</button>
              <button class="tab" data-tab="when-use">When to Use</button>
              <button class="tab" data-tab="when-not">When NOT to Use</button>
              <button class="tab" data-tab="internals">How It Works</button>
              <button class="tab" data-tab="syntax">Syntax</button>
              <button class="tab" data-tab="example">Example</button>
              <button class="tab" data-tab="real-world">Real-World</button>
              <button class="tab" data-tab="use-cases">Use Cases</button>
              <button class="tab" data-tab="mistakes">Mistakes</button>
              <button class="tab" data-tab="best-practices">Best Practices</button>
              <button class="tab" data-tab="interview">Interview Qs</button>
              <button class="tab" data-tab="exercise">Exercise</button>
              <button class="tab" data-tab="summary">Summary</button>
            </div>
            <div class="panel-content">
              <div class="tab-pane active" data-pane="definition">…</div>
              <div class="tab-pane" data-pane="why-exists">…</div>
              <!-- … one pane per section … -->
            </div>
          </details>
        </div>

        <div class="mini-project">…</div>
      </section>

    </main>
  </div>

  <button id="back-to-top">↑</button>

  <script>/* all JS here */</script>
</body>
</html>
```

### Code Block Template

```html
<div class="code-block">
  <div class="code-header">
    <span class="code-lang">typescript</span>
    <button class="copy-btn">Copy</button>
  </div>
  <pre><code class="ts-code">…</code></pre>
</div>
```

---

## Step 4 — JavaScript Requirements

All inline, no libraries:

1. **Scroll-spy** — `IntersectionObserver` on each `.module` section;
   highlights the matching sidebar link when the section enters the viewport
2. **Progress bar** — updates `width` on `scroll` event as
   `(scrollY / (docHeight - viewportHeight)) * 100`%
3. **Copy buttons** — `navigator.clipboard.writeText`; swap label to
   "Copied!" for 1.5 s then back to "Copy"
4. **Module checkboxes** — on `change`, save to `localStorage`;
   on page load, restore state and add `.completed` class to headers
5. **Topic search** — on `input`, show/hide `.topic-panel` elements whose
   `.topic-name` text does not include the query string
6. **Back-to-top** — show `#back-to-top` when `scrollY > 400`;
   on click, `window.scrollTo({ top: 0, behavior: 'smooth' })`
7. **Tab switching** — inside each panel, clicking a `.tab` button activates
   the matching `.tab-pane` and deactivates the rest
8. **Smooth scroll** — sidebar `<a>` clicks call `scrollIntoView`
   `({ behavior: 'smooth' })`

---

## Step 5 — Output

Write the file to:
```
d:\Practices\typescript\html-docs\phase-N.html
```

After writing, report:
1. File path written
2. Approximate line count
3. Modules and topic count included
4. Any content assumptions made

---

## Content Quality Rules

- All TypeScript code must be **syntactically valid** — no pseudocode
- No placeholder text — every section has real educational content
- Analogies must be **accurate** — do not use an analogy that breaks down
  at the technical level
- Interview answers must be **precise** — no vague hand-waving
- Real-world examples use tools from the curriculum where phase-appropriate:
  React, Next.js, Express, Prisma, Drizzle ORM, Zod, tRPC, Zustand,
  React Query, Node.js
- "When NOT to Use" sections must be **honest** — do not recommend a feature
  for every situation

---

## Phase Reference

| Phase | File | Title |
|-------|------|-------|
| 1 | phase-1.html | TypeScript Foundations |
| 2 | phase-2.html | Intermediate TypeScript |
| 3 | phase-3.html | Object-Oriented TypeScript |
| 4 | phase-4.html | Advanced TypeScript |
| 5 | phase-5.html | TypeScript Design Patterns |
| 6 | phase-6.html | TypeScript with Backend Development |
| 7 | phase-7.html | TypeScript with React |
| 8 | phase-8.html | Expert-Level TypeScript |
