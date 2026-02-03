---
name: git-commit
description: 'Execute git commit with conventional commit message analysis, intelligent staging, and message generation. Use when user asks to commit changes, create a git commit, or mentions "/commit". Supports: (1) Auto-detecting gitmoji and scope from changes, (2) Generating conventional commit messages from diff, (3) Interactive commit with optional gitmoji/scope/description overrides, (4) Intelligent file staging for logical grouping'
license: MIT
allowed-tools: Bash
---

# Git Commit with Conventional Commits

## Overview

Create standardized, semantic git commits using the Conventional Commits specification. Analyze the actual diff to determine appropriate gitmoji, scope, and message.

## Conventional Commit Format

```
<gitmoji> <description>

[optional body]

[optional footer(s)]
```

## Gitmoji

| Emoji | Code                          | Description                                                   | Name                        | Semver |
| ----- | ----------------------------- | ------------------------------------------------------------- | --------------------------- | ------ |
| 🎨    | `:art:`                       | Improve structure / format of the code.                       | `art`                       |        |
| ⚡️    | `:zap:`                       | Improve performance.                                          | `zap`                       | patch  |
| 🔥    | `:fire:`                      | Remove code or files.                                         | `fire`                      |        |
| 🐛    | `:bug:`                       | Fix a bug.                                                    | `bug`                       | patch  |
| 🚑️    | `:ambulance:`                 | Critical hotfix.                                              | `ambulance`                 | patch  |
| ✨    | `:sparkles:`                  | Introduce new features.                                       | `sparkles`                  | minor  |
| 📝    | `:memo:`                      | Add or update documentation.                                  | `memo`                      |        |
| 🚀    | `:rocket:`                    | Deploy stuff.                                                 | `rocket`                    |        |
| 💄    | `:lipstick:`                  | Add or update the UI and style files.                         | `lipstick`                  | patch  |
| 🎉    | `:tada:`                      | Begin a project.                                              | `tada`                      |        |
| ✅    | `:white_check_mark:`          | Add, update, or pass tests.                                   | `white-check-mark`          |        |
| 🔒️    | `:lock:`                      | Fix security or privacy issues.                               | `lock`                      | patch  |
| 🔐    | `:closed_lock_with_key:`      | Add or update secrets.                                        | `closed-lock-with-key`      |        |
| 🔖    | `:bookmark:`                  | Release / Version tags.                                       | `bookmark`                  |        |
| 🚨    | `:rotating_light:`            | Fix compiler / linter warnings.                               | `rotating-light`            |        |
| 🚧    | `:construction:`              | Work in progress.                                             | `construction`              |        |
| 💚    | `:green_heart:`               | Fix CI Build.                                                 | `green-heart`               |        |
| ⬇️    | `:arrow_down:`                | Downgrade dependencies.                                       | `arrow-down`                | patch  |
| ⬆️    | `:arrow_up:`                  | Upgrade dependencies.                                         | `arrow-up`                  | patch  |
| 📌    | `:pushpin:`                   | Pin dependencies to specific versions.                        | `pushpin`                   | patch  |
| 👷    | `:construction_worker:`       | Add or update CI build system.                                | `construction-worker`       |        |
| 📈    | `:chart_with_upwards_trend:`  | Add or update analytics or track code.                        | `chart-with-upwards-trend`  | patch  |
| ♻️    | `:recycle:`                   | Refactor code.                                                | `recycle`                   |        |
| ➕    | `:heavy_plus_sign:`           | Add a dependency.                                             | `heavy-plus-sign`           | patch  |
| ➖    | `:heavy_minus_sign:`          | Remove a dependency.                                          | `heavy-minus-sign`          | patch  |
| 🔧    | `:wrench:`                    | Add or update configuration files.                            | `wrench`                    | patch  |
| 🔨    | `:hammer:`                    | Add or update development scripts.                            | `hammer`                    |        |
| 🌐    | `:globe_with_meridians:`      | Internationalization and localization.                        | `globe-with-meridians`      | patch  |
| ✏️    | `:pencil2:`                   | Fix typos.                                                    | `pencil2`                   | patch  |
| 💩    | `:poop:`                      | Write bad code that needs to be improved.                     | `poop`                      |        |
| ⏪️    | `:rewind:`                    | Revert changes.                                               | `rewind`                    | patch  |
| 🔀    | `:twisted_rightwards_arrows:` | Merge branches.                                               | `twisted-rightwards-arrows` |        |
| 📦️    | `:package:`                   | Add or update compiled files or packages.                     | `package`                   | patch  |
| 👽️    | `:alien:`                     | Update code due to external API changes.                      | `alien`                     | patch  |
| 🚚    | `:truck:`                     | Move or rename resources (e.g.: files, paths, routes).        | `truck`                     |        |
| 📄    | `:page_facing_up:`            | Add or update license.                                        | `page-facing-up`            |        |
| 💥    | `:boom:`                      | Introduce breaking changes.                                   | `boom`                      | major  |
| 🍱    | `:bento:`                     | Add or update assets.                                         | `bento`                     | patch  |
| ♿️    | `:wheelchair:`                | Improve accessibility.                                        | `wheelchair`                | patch  |
| 💡    | `:bulb:`                      | Add or update comments in source code.                        | `bulb`                      |        |
| 🍻    | `:beers:`                     | Write code drunkenly.                                         | `beers`                     |        |
| 💬    | `:speech_balloon:`            | Add or update text and literals.                              | `speech-balloon`            | patch  |
| 🗃️    | `:card_file_box:`             | Perform database related changes.                             | `card-file-box`             | patch  |
| 🔊    | `:loud_sound:`                | Add or update logs.                                           | `loud-sound`                |        |
| 🔇    | `:mute:`                      | Remove logs.                                                  | `mute`                      |        |
| 👥    | `:busts_in_silhouette:`       | Add or update contributor(s).                                 | `busts-in-silhouette`       |        |
| 🚸    | `:children_crossing:`         | Improve user experience / usability.                          | `children-crossing`         | patch  |
| 🏗️    | `:building_construction:`     | Make architectural changes.                                   | `building-construction`     |        |
| 📱    | `:iphone:`                    | Work on responsive design.                                    | `iphone`                    | patch  |
| 🤡    | `:clown_face:`                | Mock things.                                                  | `clown-face`                |        |
| 🥚    | `:egg:`                       | Add or update an easter egg.                                  | `egg`                       | patch  |
| 🙈    | `:see_no_evil:`               | Add or update a .gitignore file.                              | `see-no-evil`               |        |
| 📸    | `:camera_flash:`              | Add or update snapshots.                                      | `camera-flash`              |        |
| ⚗️    | `:alembic:`                   | Perform experiments.                                          | `alembic`                   | patch  |
| 🔍️    | `:mag:`                       | Improve SEO.                                                  | `mag`                       | patch  |
| 🏷️    | `:label:`                     | Add or update types.                                          | `label`                     | patch  |
| 🌱    | `:seedling:`                  | Add or update seed files.                                     | `seedling`                  |        |
| 🚩    | `:triangular_flag_on_post:`   | Add, update, or remove feature flags.                         | `triangular-flag-on-post`   | patch  |
| 🥅    | `:goal_net:`                  | Catch errors.                                                 | `goal-net`                  | patch  |
| 💫    | `:dizzy:`                     | Add or update animations and transitions.                     | `dizzy`                     | patch  |
| 🗑️    | `:wastebasket:`               | Deprecate code that needs to be cleaned up.                   | `wastebasket`               | patch  |
| 🛂    | `:passport_control:`          | Work on code related to authorization, roles and permissions. | `passport-control`          | patch  |
| 🩹    | `:adhesive_bandage:`          | Simple fix for a non-critical issue.                          | `adhesive-bandage`          | patch  |
| 🧐    | `:monocle_face:`              | Data exploration/inspection.                                  | `monocle-face`              |        |
| ⚰️    | `:coffin:`                    | Remove dead code.                                             | `coffin`                    |        |
| 🧪    | `:test_tube:`                 | Add a failing test.                                           | `test-tube`                 |        |
| 👔    | `:necktie:`                   | Add or update business logic.                                 | `necktie`                   | patch  |
| 🩺    | `:stethoscope:`               | Add or update healthcheck.                                    | `stethoscope`               |        |
| 🧱    | `:bricks:`                    | Infrastructure related changes.                               | `bricks`                    |        |
| 🧑‍💻    | `:technologist:`              | Improve developer experience.                                 | `technologist`              |        |
| 💸    | `:money_with_wings:`          | Add sponsorships or money related infrastructure.             | `money-with-wings`          |        |
| 🧵    | `:thread:`                    | Add or update code related to multithreading or concurrency.  | `thread`                    |        |
| 🦺    | `:safety_vest:`               | Add or update code related to validation.                     | `safety-vest`               |        |
| ✈️    | `:airplane:`                  | Improve offline support.                                      | `airplane`                  |        |
| 🦖    | `:t-rex:`                     | Code that adds backwards compatibility.                       | `t-rex`                     |        |

## Workflow

### 1. Identify Agent's Changes

**CRITICAL**: Only stage and commit files that the agent actually modified. Never stage or commit changes made by others working in parallel.

```bash
# Check what's currently changed
git status --porcelain

# Review ALL unstaged changes to identify what belongs to others
git diff
```

### 2. Analyze Agent's Diff

```bash
# If files are already staged, verify they are YOUR changes
git diff --staged

# If nothing staged, check working tree for YOUR changes only
git diff path/to/file/you/modified
```

### 3. Stage ONLY Agent's Files

**IMPORTANT**: Be surgical - only stage the specific files the agent modified during this session.

```bash
# ✅ CORRECT: Stage specific files you modified
git add path/to/file1 path/to/file2

# ❌ WRONG: Broad patterns that might catch others' work
# git add .
# git add src/*
# git add *.php
```

**Rules**:

- **ONLY** stage files the agent explicitly created or modified
- **NEVER** use `git add .` or broad wildcards
- **ALWAYS** list files individually by full path
- **ALWAYS"** start description in git message with uppercase letter
- **NEVER** commit secrets (.env, credentials.json, private keys)
- **If unsure** what the agent changed, list each file explicitly

### 3. Generate Commit Message

Analyze the diff to determine:

- **Gitmoji**: What kind of change is this?
- **Scope**: What area/module is affected?
- **Description**: One-line summary of what changed (present tense, imperative mood, <72 chars, first letter uppercase)

### 4. Execute Commit

```bash
# Single line
git commit -m "<gitmoji> <description>"

# Multi-line with body/footer
git commit -m "$(cat <<'EOF'
<gitmoji> <description>
<optional body>

<optional footer>
EOF
)"
```

## Best Practices

- One logical change per commit
- Present tense: "add" not "added"
- Imperative mood: "fix bug" not "fixes bug"
- Reference issues: `Closes #123`, `Refs #456`
- Keep description under 72 characters

## Git Safety Protocol

- NEVER update git config
- NEVER run destructive commands (--force, hard reset) without explicit request
- NEVER skip hooks (--no-verify) unless user asks
- NEVER force push to main/master
- If commit fails due to hooks, fix and create NEW commit (don't amend)
