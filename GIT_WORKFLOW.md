# TicketFlow Git Workflow

This document defines the Git branching, commit, and pull request strategy used by TicketFlow.

## 1. Branching Strategy

TicketFlow uses a **feature-branch workflow**.

The `main` branch is the stable branch and should always contain code that is in a working state.

Development should never be done directly on `main`.

The standard workflow is:

```text
Issue
  ↓
Branch
  ↓
Development
  ↓
Commit
  ↓
Push
  ↓
Pull Request
  ↓
Review
  ↓
Merge into main
```

## 2. Main Branch

`main` represents the stable version of TicketFlow.

Rules:

* Do not commit directly to `main`.
* All changes should be introduced through pull requests.
* `main` should remain in a buildable and runnable state.
* Feature branches should be created from the latest `main`.

## 3. Branch Types

| Type        | Purpose                                      |
| ----------- | -------------------------------------------- |
| `feature/`  | New functionality                            |
| `bugfix/`   | Fix an existing bug                          |
| `refactor/` | Code restructuring without changing behavior |
| `test/`     | Test-related work                            |
| `chore/`    | Configuration and maintenance                |
| `docs/`     | Documentation                                |
| `perf/`     | Performance improvements                     |

## 4. Branch Naming

Branches should follow:

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

Use lowercase and hyphens for descriptions.

## 5. Creating a Branch

Branches should be created from the latest `main`.

Example:

```bash
git switch main
git pull
git switch -c feature/12-user-registration
```

The branch should correspond to a GitHub Issue whenever possible.

## 6. Commits

TicketFlow follows the **Conventional Commits** format:

```text
<type>: <description> (#<issue-number>)
```

Examples:

```text
feat: add user registration endpoint (#12)
fix: prevent duplicate ticket reservations (#24)
test: add ticket reservation tests (#35)
refactor: extract ticket validation logic (#31)
chore: configure PostgreSQL datasource (#5)
docs: document local development setup (#40)
```

### Commit Types

| Type       | Purpose                            |
| ---------- | ---------------------------------- |
| `feat`     | New functionality                  |
| `fix`      | Bug fix                            |
| `refactor` | Code restructuring                 |
| `test`     | Tests                              |
| `chore`    | Maintenance/configuration          |
| `docs`     | Documentation                      |
| `perf`     | Performance improvements           |
| `build`    | Build system or dependency changes |

Commits should be:

* Focused on one logical change
* Descriptive
* Small enough to understand
* Written using the imperative form

Avoid vague commits such as:

```text
update
changes
fix stuff
working
```

## 7. Pull Requests

Every feature or significant change should be merged through a pull request.

PR titles should follow the same convention as commits:

```text
feat: add user registration endpoint (#12)
```

A PR should contain:

* A short description of the change
* Important implementation details
* Testing performed
* Reference to the related issue

Example:

```text
## What

Adds user registration functionality.

## Changes

- Added User entity
- Added UserRepository
- Added UserService
- Added registration endpoint
- Added validation

## Testing

- Added UserService tests
- Tested duplicate email
- Tested invalid input

Closes #12
```

## 8. Merge Strategy

TicketFlow uses **squash merging** for feature branches.

Multiple development commits:

```text
feat: add User entity
feat: add registration service
test: add registration tests
fix: handle duplicate email
```

are combined into one meaningful commit on `main`:

```text
feat: add user registration (#12)
```

This keeps the `main` history clean while allowing detailed commits during development.

## 9. After Merging

After a pull request is merged:

1. Switch to `main`.
2. Pull the latest changes.
3. Delete the local feature branch.
4. Delete the remote branch if GitHub has not done so automatically.

Example:

```bash
git switch main
git pull
git branch -d feature/12-user-registration
```

## 10. Hotfixes

For urgent fixes to `main`, use a `bugfix/` branch:

```text
bugfix/42-payment-calculation
```

The same pull request and review process applies.

## 11. General Rule

Keep the Git history understandable.

A person who has never worked on TicketFlow should be able to look at the repository history and understand:

* What was added
* What was fixed
* Why the change was made
* Which issue it belongs to
* When it became part of `main`
