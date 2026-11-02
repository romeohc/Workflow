<p align="center">
  <img src="assets/logo.png" alt="Workflow" width="96" />
</p>

# Workflow

**The same way of working on every app.** One plugin of skills for AI coding agents. Install it once in Cursor, Claude Code or Codex, and every app gets the same method: build, prove, debug, review, ship.

It lives in this repo only. It is never copied into application repos.

## Why

AI agents write code fast. The hard part is trusting what they ship.

This plugin gives every agent the same rules: change as little as possible, find the real cause of a problem, and prove the result on the running app, not just in a unit test. After each merge, it checks that what is live in production matches `main`.

## Skills

| Skill | What it does |
| --- | --- |
| `/setup` | Reads an app and installs its workflow pieces: a `radar` skill, path-based deploys, and a post-merge automation. Rewrites a piece when it no longer matches the app. |
| `/hard` | Implements the change, verifies it on the real app, and proves it with screenshots and a short video. |
| `/fast` | Implements the change with no verification, then opens the ports so you can test. |
| `/debug` | Finds an unknown cause from runtime evidence: reproduce, instrument, confirm, then the smallest fix. |
| `/think` | Read-only. Answers any product, growth or code question as both a founder and an engineer. |
| `/clean` | Read-only. Spawns several agents in parallel to find what to delete or simplify, proposes named PRs, and implements only the one you pick. |

## How it works

On an app, run `/setup` and say nothing else. It:

1. **Writes `radar`** (`.cursor/skills/radar/SKILL.md`), specific to that app. For each service it deploys, `radar` has the commands to read the live commit, the deploy state, the logs and the health check.
2. **Wires the deploys** so each service ships only when `main` changes and its own paths changed.
3. **Creates the automation** `Radar - <app name>`, which runs `radar` after every merge to `main`.

After a merge, `radar` compares each live service with `main`, waits for the deploys, reads the logs and the health checks, and replies `✅` only when everything is green. When something fails and the cause is clear, it fixes it; when the cause is unknown, it uses `/debug`.

When `/setup` cannot finish, it names the one thing you have to do.

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

## Update

Push a change to this repository, then update the plugin in each tool. The skills update everywhere. Run `/setup` again on an app when its radar or its deploy should change.

## Structure

```text
.
├── .cursor-plugin/    # Cursor plugin + marketplace manifest
├── .claude-plugin/    # Claude Code plugin + marketplace manifest
├── .codex-plugin/     # Codex plugin manifest
├── .agents/plugins/   # Agents marketplace manifest
├── assets/logo.png
└── skills/
    ├── setup/   # installs radar, deploys and the post-merge automation
    ├── hard/    # implement + prove on the real app
    ├── fast/    # implement, no verification
    ├── debug/   # runtime-evidence debugging
    ├── think/   # read-only founder + engineer judgment
    └── clean/   # read-only parallel cleanup review
```

---

Built by [Roméo HC](https://www.linkedin.com/in/romeo-hc/). Used daily to build and run [Novex](https://novex.trading).
