---
platform: universal
format: technical-writing
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: Technical Writing

## Core Principles

Technical writing translates complex information into clear, accurate, and usable documentation for a defined audience. Clarity and completeness are non-negotiable.

- **Know your audience's technical level.** A document for end-users is written differently from one for developers or system administrators.
- **One document, one purpose.** A reference guide, a tutorial, and a troubleshooting guide are three different documents — do not conflate them.
- **Accuracy is correctness, not precision.** Technical writing must be correct, complete, and current.

## Document Types

| Type | Purpose | Structure |
|------|---------|-----------|
| Tutorial | Learning-oriented; guides through a task | Step-by-step, linear |
| How-to Guide | Task-oriented; solves a specific problem | Steps + prerequisites |
| Reference | Information-oriented; lookup resource | Tables, definitions, indexes |
| Explanation | Understanding-oriented; concept clarity | Narrative, diagrams |

## Structure

```
[TITLE — action-verb + topic, e.g., "Configure SSL Certificates"]

[OVERVIEW — 2–4 sentences]
- What this document covers
- Who it is for
- Prerequisites or assumed knowledge

[PREREQUISITES]
- Software versions, permissions, or prior steps required

[PROCEDURE / CONTENT]
- For step-by-step: numbered steps, one action per step
- Code blocks for all commands, file paths, and code snippets
- Expected output shown after each command
- Notes, warnings, and tips called out in admonition blocks

[VERIFICATION]
- How to confirm the procedure was successful

[TROUBLESHOOTING]
- Common errors and their resolutions

[NEXT STEPS / RELATED DOCS]
- Links to follow-on documentation
```

## Guidelines

- **Active voice.** "Click Save" not "Save should be clicked."
- **Present tense.** "The system returns a 200 status code" not "the system will return."
- Avoid "you" when the subject is the system: "The installer prompts you" not "you will be prompted."
- Use admonition blocks consistently:
  - **Note:** supplementary, non-critical information
  - **Warning:** potential data loss, security, or breaking change
  - **Tip:** shortcut or best practice
- Code blocks must specify the language for syntax highlighting.
- Every parameter, flag, and argument should be documented — not just the ones you think people will use.
- Version-stamp documents that apply to specific software releases.
- Docs-as-code: treat documentation source files like code — version control, review, and CI/CD checks.
- Screenshots: annotate with numbered callouts; never rely solely on a screenshot without text explanation.

## Formatting Standards

- Headings: sentence case ("Configure the database" not "Configure The Database")
- File paths: `monospace` format
- UI elements: **bold** ("Click **Save**")
- Code inline: `monospace` single backtick
- Code blocks: triple backtick with language identifier
- Lists: numbered for sequential steps, bulleted for non-sequential items

## Examples

**Step format:**
```
1. Open a terminal and run the following command:

   ```bash
   npm install --save-dev jest
   ```

   Expected output:
   ```
   added 287 packages in 4.2s
   ```

2. Create a configuration file named `jest.config.js` in your project root.
```

**Warning admonition:**
```
> **Warning:** Running this command permanently deletes all data in the specified
> database. Ensure you have a current backup before proceeding.
```
