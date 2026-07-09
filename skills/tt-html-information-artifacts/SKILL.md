---
name: tt-html-information-artifacts
description: Use when a user asks for an HTML artifact, HTML file, visual explainer, interactive report, rich spec, code review explainer, implementation plan, research synthesis, comparison grid, lightweight dashboard, playground, custom editor, copy/export UI, or any information presentation that would be hard to read, compare, tune, or share as plain Markdown. Also use when the user wants small one-off visualization or interaction, not only deployable web apps.
---

# TT_HTML Information Artifacts

## Overview

Use HTML as a high-bandwidth medium for thinking with the user: dense information, visual structure, diagrams, small interactions, and shareable review surfaces. Treat the output as an information artifact first, not as a deployable product unless the user explicitly asks for a real app or website.

## Core Principle

Choose HTML when the user benefits from seeing relationships, tradeoffs, states, or controls that Markdown would flatten.

Do not treat this skill as a fixed template library. Each artifact needs a custom information architecture shaped by the subject matter, reader, decision, and data. The examples below are starting points, not layouts to copy.

HTML artifacts are best for:

- Specs, plans, explorations, and side-by-side option grids.
- Code review explainers, PR walkthroughs, annotated diffs, architecture maps, and data-flow diagrams.
- Research reports, learning guides, incident reports, weekly updates, and leadership summaries.
- Design prototypes, animation tuners, component comparisons, and visual system references.
- Throwaway editors for one piece of structured data, ending with copy/export output.

Use Markdown instead when the answer is short, linear, mostly prose, or will be edited by hand as plain text.

## Output Contract

When creating an HTML information artifact:

1. Prefer a single self-contained `.html` file with inline CSS and JavaScript.
2. Save the file in the user-facing output location when one exists; otherwise save it in the current workspace and link it.
3. Make the first screen immediately useful. Do not add a marketing landing page.
4. Use semantic structure, tables, cards only for repeated items, SVG/canvas only when they carry real meaning, and interactions only when they help the user decide, compare, tune, or export.
5. Include enough source notes, assumptions, or provenance inside the artifact for a reader to trust it later.
6. Add a practical export path when the artifact is interactive: copy as Markdown, copy as JSON, copy prompt, copy diff, download CSV, or similar.
7. Verify the file renders without obvious layout breakage. For substantial artifacts, open it in a browser or use a screenshot-capable workflow when available.
8. In the final response, link the HTML file and briefly say what it contains.

## Artifact Patterns

Use these as prompts for invention, not as templates. Combine, bend, or discard them when the topic suggests a better structure.

| User need | Artifact pattern | Useful elements |
|---|---|---|
| Compare directions | Option grid | thumbnails, criteria, tradeoffs, recommendation badges |
| Understand code | Annotated explainer | module map, call flow, diff snippets, severity-colored notes |
| Review a plan | Rich implementation plan | timeline, data flow, mockups, risk table, acceptance checks |
| Learn a system | Interactive explainer | progressive sections, diagrams, key snippets, gotchas |
| Tune behavior | Playground | sliders, toggles, live preview, copied parameter output |
| Edit structured data | Custom editor | grouped forms, validation warnings, dependency graph, copy diff |
| Summarize research | Report | source-backed sections, charts, comparison tables, glossary |
| Share status | Briefing page | KPI strip, decisions, blockers, timeline, owner table |

## Custom Architecture

Before writing HTML, design the artifact's structure from the content itself:

- If the topic is a system, make the architecture follow components, flows, states, and failure modes.
- If the topic is a decision, make the architecture follow options, criteria, evidence, tradeoffs, and recommendation.
- If the topic is research, make the architecture follow claims, sources, conflicts, confidence, and open questions.
- If the topic is code, make the architecture follow modules, data/control flow, changed surfaces, risks, and review findings.
- If the topic is a workflow, make the architecture follow actors, stages, handoffs, bottlenecks, and interventions.
- If the topic is tuning or editing, make the architecture follow controls, preview, validation, and export.

Invent topic-specific sections, diagrams, interactions, and visual metaphors when they make the artifact easier to understand. Avoid reusing the same page skeleton across unrelated tasks just because it worked once.

## Design Rules

- Optimize for scanning first, deep reading second.
- Use layout to express information hierarchy: summary, details, evidence, next actions.
- Prefer real tables for tabular data and SVG diagrams for workflows or relationships.
- Use color sparingly and semantically: severity, category, status, confidence, or ownership.
- Keep interactions small and obvious. Every control should change visible output or produce an export.
- Make it responsive enough to read on laptop and mobile.
- Avoid decorative complexity: no generic hero sections, no vague gradient backgrounds, no visual noise that does not encode information.
- Do not expose hidden chain-of-thought. If rationale is useful, provide concise, user-facing reasoning and make long rationale panels collapsed by default.

## Workflow

1. Identify the reader and job: decide, compare, understand, review, tune, share, or edit.
2. Identify the content's natural shape: hierarchy, sequence, network, comparison, map, timeline, matrix, simulation, or editor.
3. Choose or invent an artifact architecture that fits that shape; use the pattern table only as inspiration.
4. Gather or derive the minimum evidence needed: files, diffs, data, sources, examples, or user-provided text.
5. Sketch the reading order before coding: summary, main visualization, details, evidence, export/action. Rename and reshape these sections to fit the topic.
6. Build the single-file HTML with stable dimensions and readable responsive layout.
7. Add interactions only after the static artifact communicates the core point.
8. Verify rendering and fix overflow, overlapping text, broken controls, missing exports, and unreadable contrast.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Treating every HTML artifact as a deployable web app | Make a self-contained file focused on the current information job |
| Reusing one familiar artifact skeleton | Derive a custom architecture from the topic, reader, and decision |
| Recreating Markdown inside HTML | Add visual hierarchy, diagrams, tables, comparisons, or interactions |
| Adding interaction without an export | Add copy/download output so user edits can return to the agent workflow |
| Making a pretty but low-density page | Put the evidence, comparison, or diagram above decoration |
| Hiding the conclusion | Put the recommendation, status, or key takeaway near the top |
| Creating hard-to-review noise | Keep CSS/JS compact, named, and local to the artifact |

## Example Requests

- "Make this implementation plan as an HTML artifact with mockups and data flow."
- "Create an HTML explainer for this PR, especially the streaming logic."
- "Turn these research notes into a readable HTML report with diagrams."
- "Build a small HTML editor so I can rank these tickets and copy the final ordering."
- "Prototype several animation timings with sliders and a copy-parameters button."
