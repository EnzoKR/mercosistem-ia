---
platform: software-house
format: code-review
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: Code Review

## Core Principles

Code review is a quality gate, a knowledge-sharing mechanism, and a communication process. It protects the codebase and grows the team simultaneously.

- **Review code, not the person.** Feedback targets the implementation, not the developer.
- **Be constructive and specific.** "This could be cleaner" is not actionable. "Extract this logic into a `calculateTax()` function to make it reusable and testable" is.
- **Approve or block — don't be a passive reviewer.** An ambiguous review is worse than no review.
- **Small PRs, fast reviews.** Prefer many small reviews over one massive review that nobody reads carefully.

## What to Review

### Correctness
- Does the code do what the PR description claims?
- Are edge cases and error paths handled?
- Are inputs validated where they enter the system?
- Are there potential null pointer exceptions, off-by-one errors, or race conditions?

### Design and Architecture
- Is the solution appropriately simple? Over-engineering is a real defect.
- Does the code follow the existing architectural patterns of the codebase?
- Are responsibilities well separated (single responsibility principle)?
- Is there appropriate abstraction — not too much, not too little?

### Performance
- Are there N+1 query patterns or unnecessary loops?
- Are expensive operations (DB calls, API requests) performed in tight loops?
- Is caching used appropriately?

### Security
- Is user input sanitized and validated?
- Are secrets hardcoded? (Should trigger immediate blocking)
- Are authorization checks in place for all sensitive operations?
- Is SQL/NoSQL injection prevented?

### Tests
- Do new features have unit tests?
- Are edge cases tested?
- Do tests actually assert the right things (not just that something runs without throwing)?

### Readability and Maintainability
- Is the code understandable without requiring the author to explain it?
- Are variable and function names descriptive?
- Are complex sections commented with the *why*, not just the *what*?

## Review Comment Taxonomy

Use a prefix to clarify the type of feedback:

| Prefix | Meaning |
|--------|---------|
| `nit:` | Minor style preference; non-blocking |
| `suggestion:` | Improvement idea; take it or leave it |
| `question:` | Genuine question; not necessarily a problem |
| `issue:` | Must be resolved; blocking approval |
| `blocker:` | Critical problem; cannot merge |

## Structure (PR Description Template)

```markdown
## What this PR does
[1–3 sentence summary of the change]

## Why
[Link to ticket / business context]

## How to test
1. [Step 1]
2. [Step 2]
3. Expected result: [description]

## Checklist
- [ ] Unit tests added or updated
- [ ] No secrets or hardcoded values
- [ ] Documentation updated (if applicable)
- [ ] Breaking changes noted in CHANGELOG
```

## Guidelines

- Respond to all PR comments before requesting re-review — do not leave threads hanging.
- A PR with more than 400 lines of diff is too large. Break it up.
- Review within 24 hours of request during business hours — blocking others is a team cost.
- The author should explain the *why* in the PR description; the reviewer should not have to ask.
- Self-review before requesting others: re-read your own diff in GitHub/GitLab before clicking "Request Review."
- Automated checks (linting, tests, type-checking) must pass before human review begins.
- Approve only code you actually understand — "Looks good to me" without reading is not a review.
