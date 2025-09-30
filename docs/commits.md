# 📜 Commit Message Guidelines

We follow the [**Conventional Commits**](https://www.conventionalcommits.org/) specification.
This ensures our commit history is **machine-readable, searchable, and automatable** (for changelogs, semantic versioning, release notes, etc.).

---

## ✅ Format

```
<type>(<scope>): <short summary>

[optional body]

[optional footer(s)]
```

---

## 🔠 Types

| Type         | Purpose                                                           |
| ------------ | ----------------------------------------------------------------- |
| **feat**     | A new feature for the user or the system                          |
| **fix**      | A bug fix                                                         |
| **chore**    | Routine tasks (e.g., dependency upgrades, CI config)              |
| **refactor** | Code change that neither fixes a bug nor adds a feature           |
| **docs**     | Documentation updates (README, comments, etc.)                    |
| **style**    | Formatting, missing semicolons, whitespace (no code logic change) |
| **perf**     | Performance improvements                                          |
| **test**     | Adding or updating tests                                          |
| **build**    | Changes that affect the build system or external dependencies     |
| **ci**       | Changes to CI/CD configuration files and scripts                  |
| **revert**   | Reverting a previous commit                                       |

---

## 🧪 Examples

### 🎯 Features

```bash
feat(auth): add JWT refresh token support
```

### 🐛 Bug Fix

```bash
fix(leaderboard): handle empty user list without crashing
```

### 📚 Documentation

```bash
docs(readme): add project structure and commit guidelines
```

### 🔨 Refactor

```bash
refactor(utils): simplify date formatting helper
```

### 🧪 Tests

```bash
test(api): add integration tests for login endpoint
```

---

## 🪶 Optional Body (When Needed)

Use the body if you need to **explain why** the change was made, **link issues**, or **describe side effects**.

```bash
feat(map): implement clustering for POIs

This adds Leaflet.markercluster to improve performance when rendering
hundreds of points. It reduces map lag significantly on low-end devices.
```

---

## 🏷️ Footer (Breaking changes or references)

* Use `BREAKING CHANGE:` to indicate a major change.
* Use `Closes #123` or `Refs #456` to reference issues.

```bash
feat(api): migrate to GraphQL

BREAKING CHANGE: All REST endpoints have been removed in favor of a new GraphQL API.
Clients must update queries to match the new schema.

Closes #42
```

---

## 📌 Best Practices

* ✅ **Keep the summary under 72 characters.**
* ✅ **Use imperative mood** — e.g., “add” not “added” or “adds”.
* ✅ Scope is optional but recommended (e.g., `feat(ui)`, `fix(router)`).
* ✅ Group related commits logically — don’t mix feature and refactor in the same commit.
* ✅ Use lowercase for `<type>` and `<scope>`.

---

## 🧠 Automation Ready

With this convention in place, tools like:

* 📦 `semantic-release` → automated versioning & CHANGELOG generation
* 🧰 `commitlint` → enforces correct commit messages
* 📊 GitHub Actions → auto-tagging and release notes

…can parse commits **without manual input**.

---

✅ **Example full commit with all sections:**

```
feat(auth): add support for passwordless login

Implements magic link authentication using the new /auth/magic endpoint.
This simplifies the onboarding flow and improves UX for first-time users.

BREAKING CHANGE: The old /auth/login endpoint has been removed.

Closes #108
```

---

**🔥 Recommendation:** Install [`commitlint`](https://github.com/conventional-changelog/commitlint) + [`husky`](https://typicode.github.io/husky/) to enforce this automatically before each commit.

