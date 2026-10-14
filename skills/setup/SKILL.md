---
name: setup
description: Install this app's workflow pieces. Write what is missing. Rewrite what no longer matches the app.
disable-model-invocation: true
---

# Setup

Read the repo.

For each piece below, look only in the repo. Missing, write it. Already there, check that it is perfectly up to date and matches this section exactly. If it does not, rewrite it.

Do not copy `hard`, `fast`, `debug`, `think`, or `clean` into the repo.

No app yet (no manifest and no start script): reply `⚠️ no app` and stop. Do not invent one.

Reply `✅` when nothing changed, or `⚙️` plus the piece names you changed. Use `⚠️` for a problem or something the user must do.

## Radar

Learn every service this app deploys. A service the repo does not use is out. Write one ready command per check from the repo files that define the deploy. Do not run those commands. Do not install a tool. Each command must exit on its own.

Write `.cursor/skills/radar/SKILL.md` with `disable-model-invocation: true`. Description: After main moves, check that everything this app deploys matches main.

Under `Commands`, one block per service: the paths that belong to it, the command that prints the live commit, the command that prints the deploy state, the command that prints the logs since that deploy, and the public address when it has one. These commands are specific to this repo. The rules below are copied word for word.

Rules:

- Run the commands in this skill. You own the current `origin/main`. Fetch at the start and before the verdict. If main moved, reply `🛑` and stop. That emoji is the whole reply.
- For each service, diff the live commit with main, only on that service's paths.
- No diff: that service already matches main. Skip it.
- A diff: wait until that deploy is live, or it has failed. If main moves while you wait, reply `🛑` and stop.
- For each service that just deployed: run its log command. Open its public address when the skill gives one.
- All of that is green: reply `✅` and stop. That emoji is the whole reply. Do not invent `✅`.
- Something failed and the cause is clear: fix it. The cause is unknown: use the debug skill, then fix it.

If this repo has a GitHub CI on `main`, add the command that prints whether that run for this commit is green, and add this rule: `The GitHub CI run on main for this commit is green.` If it has none, add neither.

Then one automation named `Radar - <app name>`. Trigger: a pull request is merged into `main`, so `main` updates. The prompt is exactly `Follow the radar skill at .cursor/skills/radar/SKILL.md and reply in french.` A newer merge cancels the running one. Create it yourself when you can. When you cannot, reply `⚠️` and three bullets: the name, the trigger, and the prompt.
