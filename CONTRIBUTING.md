# TicketFlow — Git & Contribution Guidelines

This document defines the Git workflow, branch naming, commit messages, and pull request conventions used in the TicketFlow project.

## 1. Branches

Branches should be created from the latest `main` branch.

### Branch naming

Use:

```text
<type>/<issue-number>-<short-description>
```

Examples:

```text
feature/12-user-registration
feature/18-event-management
bugfix/24-duplicate-ticket-reservation
refactor/31-ticket-service
test/35-ticket-service
chore/5-configure-postgresql
docs/40-api-documentation
```

### Branch types

| Type       | Purpose                       |
| ---------- | ----------------------------- |
| `feature`  | New functionality             |
| `bugfix`   | Bug fixes                     |
| `refactor` | Code restructuring            |
| `test`     | Tests                         |
| `chore`    | Configuration and maintenance |
| `docs`     | Documentation                 |
| `perf`     | Performance improvements      |

Keep branch names short and descriptive.

---

## 2. Commit Messages

TicketFlow follows the **Conventional Commits** format:

```text
<type>: <description> (#<issue-number>)
```

Examples:

```text
feat: add user registration endpoint (#12)
feat: add event entity (#18)
fix: prevent duplicate ticket reservations (#24)
test: add ticket service tests (#35)
refactor: extract ticket validation logic (#31)
chore: configure PostgreSQL datasource (#5)
docs: document local development setup (#40)
```

### Commit types

| Type       | Purpose                                          |
| ---------- | ------------------------------------------------ |
| `feat`     | Introduces new functionality                     |
| `fix`      | Fixes a bug                                      |
| `refactor` | Changes code structure without changing behavior |
| `test`     | Adds or modifies tests                           |
| `chore`    | Maintenance, configuration, tooling              |
| `docs`     | Documentation changes                            |
| `perf`     | Performance improvements                         |
| `build`    | Build system or dependency changes               |

### Commit guidelines

* Use the imperative form.
* Keep the first line short and clear.
* Describe what the commit does, not why it was needed.
* Keep commits focused on one logical change.
* Avoid vague messages such as:

    * `update stuff`
    * `fix`
    * `changes`
    * `working`
    * `misc`

Prefer:

```text
fix: prevent users from reserving sold-out tickets
```

instead of:

```text
fix: stuff
```

---

## 3. GitHub Issues

Issues represent meaningful pieces of work rather than individual files or implementation steps.

### Issue title

Use:

```text
[TYPE] Short description
```

Examples:

```text
[FEATURE] Implement user registration
[FEATURE] Add event management
[FEATURE] Implement ticket reservation
[BUG] Prevent duplicate ticket reservations
[CHORE] Configure PostgreSQL
[TEST] Add ticket service tests
[REFACTOR] Extract ticket reservation logic
```

### Issue structure

A feature issue should contain:

```text
## Description

Brief explanation of the functionality.

## Requirements

- Requirement 1
- Requirement 2
- Requirement 3

## Acceptance Criteria

- [ ] Requirement is implemented
- [ ] Validation is handled
- [ ] Error cases are handled
- [ ] Tests are added
```

Issues should describe **what needs to be accomplished**, while implementation details can evolve during development.

---

## 4. Pull Requests

Pull requests should normally correspond to a GitHub Issue.

### PR title

Use the same Conventional Commit style:

```text
feat: add user registration endpoint (#12)
```

### PR structure

```text
## What

Brief description of the change.

## Changes

- Added ...
- Implemented ...
- Updated ...

## Testing

- Added unit tests
- Tested validation
- Tested error cases

Closes #12
```

Use:

```text
Closes #<issue-number>
```

when the PR completely resolves the issue.

---

## 5. Recommended Workflow

For each piece of work:

```text
1. Create GitHub Issue
2. Create branch from main
3. Implement the change
4. Commit using Conventional Commits
5. Push the branch
6. Open Pull Request
7. Review changes
8. Merge into main
9. Delete the feature branch
```

Example:

```text
Issue #12
[FEATURE] Implement user registration

        ↓

feature/12-user-registration

        ↓

feat: add User entity (#12)
feat: add user repository (#12)
feat: add registration service (#12)
feat: add registration endpoint (#12)
test: add registration tests (#12)

        ↓

Pull Request #12

        ↓

Merge into main
```

---

## 6. Commit Size

Commits should represent a single logical change.

Good:

```text
feat: add User entity (#12)
feat: add user repository (#12)
test: add user repository tests (#12)
```

Avoid one huge commit such as:

```text
feat: implement everything (#12)
```

However, don't create commits for every tiny edit either.

The goal is a Git history that clearly communicates how the feature was developed.

---

## 7. Main Branch

`main` should always represent a stable version of TicketFlow.

Direct commits to `main` should be avoided for feature work.

Normal development should happen through:

```text
Issue → Branch → Commits → Pull Request → main
```

---

## 8. Example

For implementing ticket reservation:

### Issue

```text
[FEATURE] Implement ticket reservation
```

### Branch

```text
feature/24-ticket-reservation
```

### Commits

```text
feat: add ticket reservation entity (#24)
feat: add ticket reservation service (#24)
feat: prevent reservation of sold-out tickets (#24)
test: add ticket reservation tests (#24)
```

### Pull Request

```text
feat: implement ticket reservation (#24)
```

The PR description ends with:

```text
Closes #24
```

This keeps the GitHub history, branch names, commits, and issues connected and easy to understand.
