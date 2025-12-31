# GitHub Project Setup 📋

**How to configure a GitHub Project board for Fire/Growth/3S tracking.**

---

## Quick Setup Checklist

For each repository:

- [ ] Enable Issues, Discussions, Projects (repo settings)
- [ ] Create or link to a GitHub Project
- [ ] Apply the label taxonomy (below)
- [ ] Add issue templates
- [ ] Add PR template

---

## Label Taxonomy

Use prefixes to keep lists scannable.

### Fire Triangle

```
fire:fuel
fire:oxygen
fire:heat
```

### Growth Path

```
growth:project
growth:party
growth:practice
```

### 3S Stage

```
stage:sense
stage:stabilize
stage:strengthen
```

### Utility Labels

```
type:todo
type:proposal
type:decision
good-first-sniff
help-wanted
blocked
```

---

## Project Custom Fields

Add these fields to your GitHub Project:

| Field | Type | Options |
|-------|------|---------|
| **Fire** | Single select | Fuel, Oxygen, Heat |
| **Growth** | Single select | Project, Party, Practice |
| **Stage** | Single select | Sense, Stabilize, Strengthen |
| **Owner** | Single select | Team members + "unclaimed" |
| **Next Touch** | Date | — |
| **Blocker** | Text | One line |

---

## Recommended Views

### Board View (Primary)

**Group by:** Stage

| Sense | Stabilize | Strengthen |
|-------|-----------|------------|
| Items being discovered | Items being scoped | Items being shipped |

This is your default view. Shows work maturity at a glance.

### Table View (Analysis)

**Group by:** Fire

Shows resource distribution:

- Are we heavy on Heat but light on Fuel?
- Do we have enough Oxygen to sustain what we're doing?

### Roadmap View (Optional)

**Sort by:** Next Touch date

Good for deadline-driven work and event planning.

---

## Issue Templates

Place these in `.github/ISSUE_TEMPLATE/`:

### `00-freeforall-todo.md`

Low-ceremony entry point. Use for quick tasks and ideas.

### `01-proposal.md`

For work that needs scope, resources, or a decision.

### `02-decision.md`

For bounded decisions with deadlines. Integrates with [Async Decision Protocol](../governance/async-decisions.md).

---

## PR Template

Place in `.github/PULL_REQUEST_TEMPLATE.md`:

Every PR should indicate:

- What changed
- Why
- How to review
- Linked issues
- Stage movement (sense → stabilize → strengthen)

---

## Automation Ideas

GitHub Actions can help with:

- Auto-labeling based on file paths
- Stale issue reminders
- Next Touch notifications
- Fire Party agenda generation

Keep automation simple. Manual triage during Fire Party is often better than complex rules.

---

## Multi-Repo Setup

For organizations with multiple repos:

1. Create one **org-level Project** that spans repos
2. Use consistent label names across all repos
3. Put shared templates in a `.github` repository (GitHub will inherit them)

---

## See Also

- [Community Workflow](community-workflow.md) — The full framework
- [Fire Party](fire-party.md) — How to use the board in practice
- [GitHub Docs: Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects)

---

*Structure enables flow.* 📋🐾
