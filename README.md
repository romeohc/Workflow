# Workflow

The same way of working on every app. Install it once. It is not copied into application repos.

## Skills

| Skill | What it does |
| --- | --- |
| `/setup` | Installs this app's workflow pieces. Rewrites one when it no longer matches the app. |
| `/fast` | Implements the change. No verification. |
| `/hard` | Implements the change and proves it on the running app. |
| `/debug` | Finds an unknown cause from runtime evidence. |
| `/think` | Read-only. Product and engineering judgment. |
| `/clean` | Read-only cleanup proposals. Implements only the one you name. |

`radar` is written into each app by `/setup`. It describes that app.

## Install

**Cursor.** Customize, then import this GitHub repository.

**Claude Code.**

```text
/plugin marketplace add romeohc/workflow
/plugin install workflow@workflow
```

**Codex.**

```text
codex plugin marketplace add romeohc/workflow
```

Then install `workflow` from `/plugins`.

## Use

On an app, run `/setup` and say nothing else.

It writes `radar`. With `/automate`, it also creates the automation that runs radar after a merge to `main`.

## Update

Push a change to this repository. Update the plugin in each tool. The skills update everywhere. Run `/setup` again on an app when its radar should change.
