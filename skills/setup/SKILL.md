---
name: setup
description: Install this app's workflow pieces. Write what is missing. Rewrite what no longer matches the app.
disable-model-invocation: true
---

# Setup

Read the repo.

For each piece below: missing, write it. Already there, it must match this section and the repo as it is now. If it does not, rewrite it.

Do not copy `hard`, `fast`, `debug`, `think`, or `clean` into the repo. Those are the user's Cursor skills.

No app yet (no manifest and no start script): reply `❌ no app` and stop. Do not invent one.

The whole reply is one line: `✅` when nothing changed, `⚙️` plus the piece names you changed, or `❌` plus why.

## Radar

Learn every service this app deploys, and every test it runs. A service the repo does not use is out. Write one ready command per check, so the agent who later runs radar does not rediscover the stack.

Write `.cursor/skills/radar/SKILL.md` with `disable-model-invocation: true`. Description: After main moves, check that everything this app deploys matches main.

Under `Commands`, one block per service: the paths that belong to it, the command that prints the live commit, the command that prints the deploy state, the command that prints the logs since that deploy, and the public address when it has one. Then one block for the tests this app runs on main, each as a command. These commands are specific to this repo. The rules below are copied word for word.

Rules:

- Run the commands in this skill. You own the current `origin/main`. Fetch at the start and before the verdict. If main moved, reply `🛑` and stop. That emoji is the whole reply.
- For each service, diff the live commit with main, only on that service's paths.
- No diff: that service already matches main. Skip it.
- A diff: wait until that deploy is live, or it has failed. If main moves while you wait, reply `🛑` and stop.
- For each service that just deployed: run its log command. Open its public address when the skill gives one.
- Run the test commands for this main.
- All of that is green: reply `✅` and stop. That emoji is the whole reply. Do not invent `✅`.
- Something failed and the cause is clear: fix it. The cause is unknown: use the debug skill, then fix it.

Then, with the automate skill, one automation named `Radar - <app name>`: push to `main` on this repo. The prompt is exactly `Use radar skill in /workspace/.cursor/skills/radar/SKILL.md. Follow this skill and reply in french.` A newer push cancels the running one.
