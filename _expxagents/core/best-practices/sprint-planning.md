---
platform: software-house
format: sprint-planning
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: Sprint Planning

## Core Principles

Sprint planning transforms the product backlog into a committed, achievable sprint goal. A good sprint planning session is time-boxed, collaborative, and results in a shared understanding of what done looks like.

- **Commitment, not forecast.** The team commits to a goal; ticket count is an estimate.
- **Definition of Done must be agreed before work starts, not after.**
- **Sprint goal over ticket list.** A sprint with one clear objective is better than a full sprint board with no coherent direction.
- **Two-week sprints are the default.** Shorter is faster feedback; longer creates inertia.

## Pre-Planning Checklist (Product Owner / Scrum Master)

- [ ] Product backlog is groomed: top 2 sprints worth of stories are estimated and have acceptance criteria
- [ ] Sprint goal drafted and ready to propose to the team
- [ ] Previous sprint retrospective action items reviewed
- [ ] Dependencies on other teams identified and resolved or documented
- [ ] Team availability confirmed (holidays, OOO) for sprint duration

## Sprint Planning Meeting Structure (2 hours for 2-week sprint)

### Part 1: What (45 minutes)
1. Present the sprint goal (Product Owner, 5 minutes)
2. Review top backlog items (10 minutes)
3. Team asks clarifying questions on each story (15 minutes)
4. Team confirms which stories they can commit to (15 minutes)

### Part 2: How (75 minutes)
1. Break accepted stories into tasks (30 minutes)
2. Assign or self-assign tasks (15 minutes)
3. Identify risks and blockers (15 minutes)
4. Finalize sprint board (15 minutes)

## Story Format (User Story Template)

```
As a [type of user],
I want [a goal],
So that [a reason / benefit].

Acceptance Criteria:
- [ ] Given [precondition], when [action], then [expected result]
- [ ] Given [precondition], when [action], then [expected result]
- [ ] Edge case: [specific scenario handled correctly]

Definition of Done:
- [ ] Code reviewed and approved
- [ ] Unit tests written and passing
- [ ] Acceptance criteria verified by QA
- [ ] Deployed to staging
- [ ] Documentation updated (if applicable)
```

## Story Point Estimation

Use Fibonacci sequence (1, 2, 3, 5, 8, 13, 21) with this anchor:

| Points | Meaning |
|--------|---------|
| 1 | Under 1 hour; trivial change |
| 2 | Half a day; straightforward |
| 3 | One day; clear but requires care |
| 5 | 2–3 days; some unknowns |
| 8 | 4–5 days; significant unknowns; consider splitting |
| 13+ | Too large; must be broken down |

## Velocity and Capacity

- Calculate team capacity: `(team members) × (workdays) × (focus factor 0.7)`
- Focus factor accounts for meetings, interruptions, and non-sprint work
- Use trailing 3-sprint average velocity for planning; do not inflate
- Reserve 10–15% of capacity for bugs, unplanned work, and tech debt

## Guidelines

- Stories without acceptance criteria are not ready for sprint planning — send them back to backlog refinement.
- A story larger than 5 points must be split before it enters the sprint.
- The team should define the sprint goal collectively — the PO proposes; the team refines.
- Planning poker: use simultaneous reveal to prevent anchoring bias.
- Technical tasks (refactors, infrastructure) belong in the sprint alongside feature work — track them explicitly.
- Keep a "stretch goal" list of 1–2 stories the team can pull if they finish early.
- If planning takes more than 2 hours for a 2-week sprint, the backlog is not adequately groomed.
