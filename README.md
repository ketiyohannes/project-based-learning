# Project Based Learning

An installable skill for learning a language or stack through a project you choose and build yourself. It starts with product discovery, evaluates your experience, verifies current stable tooling, and teaches technical skills together with design principles. It never implements or sets up the project for you.

The goal is to need the tutor less as you learn: confidently finish and extend projects, build different things, and supervise and review code. Guidance fades from short lessons to learner-planned features, independent milestones and optional consultation. Exhaustive stack mastery is not required.

Good practices, applicable standards and production/deployment readiness are essential curriculum outcomes. You learn to verify quality, prepare releases, rehearse deployment or distribution, and reason about operations and recovery. Readiness claims must match the evidence and intended environment. Learning independence and product delivery are tracked separately, so you can graduate from regular lessons and finish the remaining work yourself.

## Install

Copy the complete `project-based-learning` directory into your agent's skills directory. For Codex, run from this repository:

```sh
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R project-based-learning "${CODEX_HOME:-$HOME/.codex}/skills/"
```

If that destination already contains a `project-based-learning` installation, compare it first; the copy command can replace same-named files. Codex detects skill changes automatically; restart it if the skill does not appear. Other agents that support `SKILL.md` can use their own skill installation directory; `agents/openai.yaml` supplies optional Codex UI metadata.

## Invoke

The skill is named `project-based-learning`. In hosts with skill slash commands, invoke `/project-based-learning`. In Codex, use `$project-based-learning` or select it through `/skills`, as described in the [official skills documentation](https://developers.openai.com/codex/skills/). The skill also recognizes `/project-based-learning` when it is passed through as ordinary prompt text; this package does not register a custom native Codex slash command.

```text
$project-based-learning I want to build a small database in C. I know Python but have never used C.
```

For another project:

```text
$project-based-learning Let's start a networked chat server in C. Use my previous project to adapt the lessons.
```

The tutor asks focused specification questions first, then uses diagnostics and saved evidence to choose the curriculum. You write all code, perform setup, run commands and share results. The tutor reviews and guides without generating solution code.

## Memory and lesson files

All tutoring records live in `${CODEX_HOME:-$HOME/.codex}/project-based-learning-memory/`, separate from the installed skill and product repositories. Set `PROJECT_BASED_LEARNING_HOME` to another absolute path if needed, and keep that setting consistent across sessions. Use separate roots for different learners.

The tutor creates an internal `.gitignore` containing `*` before saving notes, checks the ignore boundary when inside a Git worktree, and keeps specifications, lessons, assessments, preferences and cross-project skill evidence there. Filesystem access may require host approval. Without that access the tutor cannot promise persistent memory.

Memory is local to this directory; transferring it to another machine is your responsibility. Reinstalling the skill does not reset it. No project repository is created or modified by the tutor.
