---
name: obsidian-slides
description: Create presentation slide decks as Markdown (.md) files for the Obsidian Advanced Slides plugin (reveal.js-based). Use this skill whenever the user wants to create slides, presentations, a slide deck, or diapositivas in Obsidian Markdown format, or mentions "obsidian-advanced-slides", "reveal.js slides in Obsidian", "advanced slides", or asks to convert a document, notes, or content into a presentation. Also trigger when the user wants to edit, improve, or restructure an existing Obsidian slides file, add speaker notes to slides, change slide themes, or apply layouts like split/grid to existing slide content. Even if the user just says "make me a presentation" or "turn this into slides", use this skill — it produces .md files compatible with the obsidian-advanced-slides plugin.
---

# Obsidian Advanced Slides — skill for creating reveal.js presentations in Obsidian

This skill generates `.md` files that work with the [obsidian-advanced-slides](https://github.com/MSzturc/obsidian-advanced-slides) plugin for Obsidian. The output is a single Markdown file with YAML frontmatter and slide separators that renders as a reveal.js presentation inside Obsidian.

Before writing any slides, read `references/syntax-reference.md` in this skill folder for the full syntax details, layout components, frontmatter options, and examples. That file is your authoritative guide — do not guess at syntax.

## Workflow

1. **Analyze the source content.** Identify the main sections, key messages, supporting data, and natural groupings. Determine the audience and tone.

2. **Choose a theme and frontmatter settings.** Pick a theme that matches the tone (see reference). Set up frontmatter with appropriate options for controls, slideNumber, progress, transition, etc. Ask the user if they want any specific RevealJS features enabled (chalkboard, elapsed time bar, overview mode, laser pointer).

3. **Design the slide structure.** Plan horizontal slides (`---`) for main sections and vertical slides (`--`) for sub-topics within a section. Aim for one key idea per slide. Keep text concise — slides are visual aids, not documents.

4. **Write speaker notes.** Every content slide should have a `note:` section with what the presenter should say or emphasize. Speaker notes are the expanded explanation that doesn't belong on the slide itself.

5. **Apply layouts.** Use `<split>` and `<grid>` components where content benefits from multi-column or positioned layout. Use them sparingly — not every slide needs a complex layout. Note: `<split>` does **not** render bullet lists; for a two-column layout where a column has bullets, use two side-by-side `<grid>` blocks instead, with an empty `<p></p>` after the heading (and the grids wrapped in `<p>…</p>`) so the layout doesn't overlap the title. See the "Two columns with bullets" pattern in the reference.

6. **Add visual enhancements.** Use fragmented lists (`+` for unordered, `)` for ordered) when content should appear incrementally. Use slide backgrounds for section dividers or emphasis slides. Use element annotations for styling individual elements.

7. **Output the file.** Save as `.md` to `/mnt/user-data/outputs/` with a descriptive filename.

## Slide design principles

**Keep slides lean.** A slide with 3-5 bullet points or a single key statement plus supporting visual is ideal. If you find yourself putting a wall of text on a slide, split it into multiple slides or move detail to speaker notes.

**Use vertical slides for depth.** The main horizontal flow should tell the story at a high level. Vertical slides let the presenter dive deeper on a topic when needed without disrupting the main narrative.

**Section dividers matter.** Use a slide with a large heading and a background image/color to mark major topic transitions. This gives the audience a visual break and signals a new chapter.

**Speaker notes are essential.** The presenter needs to know what to say. Write notes in natural language as if coaching the presenter: "Emphasize that this correlation is lower than expected. Pause here for questions."

**Fragmented lists for storytelling.** When revealing points one at a time helps the narrative, use `+` instead of `-`. Don't fragment everything — only when the reveal order adds value.

## Handling user requests

**"Convert this document to slides"** — Read the document, identify 5-10 main topics, create a title slide, one section per topic with sub-slides as needed, and a closing slide. Add speaker notes derived from the document's detailed text.

**"Add speaker notes"** — Read existing slides, write contextual notes for each slide based on the content and flow.

**"Change the theme"** — Update the `theme:` frontmatter property. Adjust background colors if they conflict with the new theme.

**"Make it more visual"** — Add grid/split layouts, slide backgrounds, fragmented reveals, and section divider slides.

**"Enable/disable features"** — Toggle frontmatter properties like `enableChalkboard`, `enableOverview`, `enableTimeBar`, `controls`, `slideNumber`, `progress`, etc.

## Frontmatter quick reference

```yaml
---
theme: black          # black|white|league|beige|sky|night|serif|simple|solarized|blood|moon|consult
controls: true        # show navigation arrows
slideNumber: true     # show slide numbers
progress: true        # show progress bar
transition: slide     # none|fade|slide|convex|concave|zoom
transitionSpeed: default  # default|fast|slow
enableChalkboard: false   # enable drawing on slides
enableOverview: false     # show overview button
enableTimeBar: false      # show elapsed time bar
timeForPresentation: 120  # seconds for time bar
center: true          # vertical centering
width: 960            # presentation width
height: 700           # presentation height
margin: 0.04          # margin around content
maxScale: 2.0         # max scale factor
bg: '#ffffff'         # default background for all slides
defaultTemplate: null # template applied to all slides
---
```

## Critical syntax rules

- **Horizontal slide separator:** three dashes on their own line with blank lines above and below: `\n---\n`
- **Vertical slide separator:** two dashes on their own line with blank lines above and below: `\n--\n`
- **Speaker notes:** start with `note:` on its own line after the slide content (before the next separator)
- **Slide annotations:** `<!-- slide bg="color" data-background-opacity="0.5" -->` at the start of a slide
- **Element annotations:** `<!-- element class="fragment" style="color:red" -->` after the element
- **Fragmented unordered list:** use `+` instead of `-`
- **Fragmented ordered list:** use `)` instead of `.` (e.g., `2) Item`)
- **Images (Obsidian syntax):** `![[image.png]]` or `![[image.png|300x200]]`
- **Images (standard markdown):** `![alt](url)` — use for external URLs
- **Split layout:** `<split even gap="1">` ... `</split>` (children separated by blank lines)
- **Grid layout:** `<grid drag="width height" drop="x y">` ... `</grid>`
- **Split vs grid with bullets:** `<split>` does **not** render bullet lists. For two columns where a column has bullets, use two `<grid>` blocks (positive `drop` x for the left column, negative for the right) and add an empty `<p></p>` after the heading, wrapping the grids in `<p>…</p>`, so the layout doesn't overlap the title.
- **Block comments (for templates):** `::: blockname` ... `:::`

For complete syntax including grid attributes, animation, filters, opacity, rotation, padding, alignment, and all layout options, read `references/syntax-reference.md`.

## Example: minimal presentation

```markdown
---
theme: night
controls: true
slideNumber: true
progress: true
transition: slide
---

<!-- slide bg="https://example.com/hero.jpg" data-background-opacity="0.3" -->

## My presentation title
### Subtitle here

note: Welcome everyone. Today we'll cover three main topics.

---

## First topic

+ Key point one
+ Key point two  
+ Key point three

note: Walk through each point. Emphasize point two as the most important.

--

## First topic — details

<split left="2" right="1" gap="2">

This is the main explanation text that goes into more detail about the first topic.

Supporting sidebar content or an image placeholder.

</split>

note: This vertical slide gives extra depth. Only show if time permits.

---

<!-- slide bg="#2d2d2d" -->

## Second topic

A single powerful statement.

note: Let this statement sit for a moment before continuing.

---

## Closing

- Summary point A
- Summary point B
- Summary point C

note: Recap the key takeaways. Open for questions.
```
