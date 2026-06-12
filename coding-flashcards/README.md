# Anki Coding Flashcard Prompt

A reusable prompt system for generating clean, import-safe Anki flashcards for coding learners.

The system is designed to produce practical flashcards for syntax, project setup, debugging recognition, code completion, architecture, and implementation concepts across common development tools and stacks.

## What this is for

This prompt helps generate coding flashcards for topics such as:

- Bash and terminal navigation
- Git and GitHub workflows
- Ruby and Rails syntax
- ActiveRecord, SQL, PostgreSQL, and SQLite
- HTML, CSS, Tailwind, and JavaScript
- Python scripts
- APIs, scraping, maps, deployment, and project architecture

The goal is not to create abstract computer science trivia. The goal is to create useful cards that help a learner remember commands, syntax patterns, framework conventions, and practical development decisions.

## Core principles

Generated cards should be:

- simple enough to review quickly
- specific and testable
- limited to one idea per card
- safe for Anki CSV import
- consistently formatted
- tagged precisely for long-term filtering
- visually clean without relying on inline styling

Cards should use basic Anki note types only. Cloze cards are not used by default.

## Card types

The prompt supports five visible card type labels:

- `[SYNTAX]`
- `[CONCEPT]`
- `[CODE COMPLETION]`
- `[DEBUGGING]`
- `[ARCHITECTURE]`

Each card should normally display one card type label and one main technology label. A second technology label should only be used when the card genuinely tests interaction between two technologies.

## CSV format

Final exports use exactly three columns:

```csv
"Front","Back","Tags"
```

Rules:

- every field must be wrapped in double quotes
- internal double quotes must be escaped by doubling them
- no extra columns unless explicitly requested
- no Markdown table formatting in the final CSV
- HTML wrappers are allowed inside fields for predictable Anki styling

## HTML wrapper structure

Cards use simple predefined HTML classes.

Typical front:

```html
<div class="card-meta">
  <span class="card-type">[SYNTAX]</span>
  <span class="card-technology card-technology--bash">Bash</span>
</div>
<div class="question">How do you print the current working directory in Bash?</div>
```

Typical back:

```html
<div class="answer-code"><code>pwd</code></div>
<div class="explanation">Prints the current working directory.</div>
```

Common wrapper classes include:

- `card-meta`
- `card-type`
- `card-technology`
- `question`
- `answer-code`
- `answer-text`
- `explanation`
- `example`
- `context`
- `common-mistake`
- `warning`

Do not use inline styles, JavaScript, tables, images, external CSS, or custom one-off visual designs inside individual cards.

## Tagging convention

Tags use Anki-compatible hierarchical tags with `::`.

Examples:

```text
tool::bash type::syntax area::setup difficulty::beginner source::inferred
language::ruby type::debugging area::backend difficulty::beginner source::provided
framework::rails database::postgresql type::architecture area::database difficulty::intermediate source::inferred
```

Use the most accurate category for each technology:

- `language::ruby`
- `framework::rails`
- `tool::git`
- `database::postgresql`
- `platform::render`

Do not force every technology into `language::`.

## Suggested workflow

1. Ask for the topic or project section.
2. Clarify the preferred number of cards.
3. Confirm the desired balance of syntax, concept, debugging, code completion, and architecture cards.
4. Ask whether to use only provided material or infer relevant cards.
5. Generate a preview table first, unless direct CSV is requested.
6. Export the final CSV only after approval.

Preview tables may include a temporary `Rationale` column, but that column must not appear in the final CSV.

## Quality checklist

Before finalising a CSV, check that:

- each card has exactly three fields
- every field is quoted correctly
- internal quotes are escaped
- the visible card type matches the type tag
- the visible technology label matches a relevant technology tag
- the card tests one idea only
- the answer is clear and unambiguous
- syntax and commands are correct
- warnings are included for destructive commands
- no unnecessary project-specific assumptions have been added

## CSS

The included CSS file styles the predefined wrapper classes inside Anki. It provides:

- badges for card type and technology labels
- prominent styling for code and command answers
- secondary styling for explanations
- highlighted common mistake and warning blocks
- normal mode and Anki night mode support

To use it, copy the CSS into the styling section of the relevant Anki note type.

## Repository contents

Recommended files:

```text
README.md
Model-Instructions-updated.txt
anki_formatting_instructions-updated.txt
anki_css_instructions.txt
```

## Example use

Ask the prompt something like:

```text
Create 30 beginner Anki cards for Bash, Git, and GitHub commands needed to set up a new Rails project. Use mostly syntax cards, with a few concept and debugging cards. Preview first.
```

Or:

```text
Generate an Anki CSV for the approved preview.
```

## License

MIT
