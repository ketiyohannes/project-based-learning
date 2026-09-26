# Durable learning memory

## One stable home across projects

Resolve `PROJECT_BASED_LEARNING_HOME` if set to an absolute path; otherwise use `${CODEX_HOME:-$HOME/.codex}/project-based-learning-memory`. Expand environment values using the host environment. This is a **data directory**, not the installed skill directory and not the current repository. Never store learner state inside the skill package; updates or reinstalls must not erase it. Do not use conversation history as the only memory.

State the resolved location at first use. A learner may choose another persistent location; record/use the environment override consistently across sessions. Do not silently fall back to a different workspace when the location cannot be read or written. If host permissions block access, request the necessary filesystem access through the host mechanism; explain that persistence is unavailable meanwhile. Product discovery may continue, but do not claim its notes were saved.

Moving between computers requires the learner to transfer this directory or select their own shared location. Do not promise automatic cloud sync. Do not automatically upload records.

## Establish the ignore boundary before notes

Creating this data directory and its own ignore file is teaching administration, not project setup. Do not create a product directory or initialize any Git repository.

1. Check whether the chosen path overlaps the installed skill or contains existing source/project files. If so, use a dedicated data subdirectory agreed with the learner; never apply a broad ignore rule to their source tree.
2. Create only the dedicated memory root, if absent. Its `.gitignore` must contain `*` on its own line, covering all learning files and subdirectories. Preserve existing content; resolve any later negation that would expose teaching records before writing them. This does not modify any project's `.gitignore`.
3. If the root is inside a Git worktree, use read-only Git inspection to detect already tracked files under it (`git ls-files`) and verify representative intended note paths are ignored (`git check-ignore`). Ignoring does not untrack files. If any learning files are already tracked or the ignore boundary is ineffective, stop writing sensitive records there, explain the issue, and let the learner fix it or choose a clean dedicated location. Do not untrack or commit files for them.
4. Outside a Git worktree, keep the same `.gitignore` and accurately report that no enclosing Git repository exists. The ignore rules are in place for a future enclosing repository; do not claim a Git check succeeded.

Keep records limited to learning needs: no credentials, tokens, production data, private customer records, or unnecessary copies of source. Store concise observations and artifact references instead.

## File layout

All teaching-related output, including temporary drafts, specifications, resources, assessments and notes, stays below this root. Create files as needed, not empty scaffolds.

```text
project-based-learning-memory/
  .gitignore
  learner.md
  projects.md
  technologies/
    <technology-key>.md
  projects/
    <stable-project-id>/
      spec.md
      resources.md
      curriculum.md
      readiness.md
      checkpoint.md
      assessments/
        <date>-<unique-label>.md
      lessons/
        <sequence>-<topic>.md
```

- `learner.md`: goals, self-reported experience (explicitly labeled), teaching preferences, time constraints, relevant accommodations volunteered by the learner, and last update. Do not infer sensitive personal traits.
- Preserve the governing objective in `learner.md`: increasing independence, confident building across projects, code review/supervision, essential engineering standards and production-capable delivery. Track preference changes explicitly rather than drifting toward endless tutoring or exhaustive stack mastery.
- `projects.md`: stable project ID, name, product summary, language/stack, status, last activity, optional learner-supplied workspace path and relative link to checkpoint. Use a readable slug with a unique suffix if needed; never identify a project solely by its directory name.
- `technologies/<key>.md`: evidence by competency, project ID, date, version/context, observed ability, hint level, remaining misconception, next review and links to relevant assessments/lessons. Keep language and framework/library competencies distinguishable.
- `spec.md`: accepted MVP, user journeys, acceptance criteria, non-goals, constraints, decisions and unresolved questions; distinguish the learner's choices from tutor proposals.
- `resources.md`: official documentation/release sources, exact chosen versions, date verified, compatibility decisions and relevant sections for lessons.
- `curriculum.md`: milestone dependencies, mapped acceptance criteria, paired technical/design outcomes, current state and next task.
- Include the current assistance stage per relevant competency, learner-owned planning/research/review tasks, and the next opportunity to reduce guidance in `curriculum.md`. Carry these forward across projects.
- `readiness.md`: applicable standards, product/release criteria, evidence links, learner-run check results, environment, unresolved risks and delivery status. Keep this distinct from learning independence.
- `checkpoint.md`: current milestone, most recent demonstrated skill, current blocker, pending learner task, next review, and links needed to resume. Include whether the latest work is merely reported or actually inspected.
- At handoff, use `checkpoint.md` for the learner's independent continuation plan and optional consultation topics. Record graduation from regular tutoring separately from project completion; do not schedule mandatory lessons after graduation.
- Assessment and lesson files preserve the evidence and feedback used to update the concise summaries. Do not copy an entire repository into memory.

## Read and update discipline

Read the profile and project index first, then the selected checkpoint and relevant technology records. Retrieve only the lessons/assessments required for the next decision. Follow relative links rather than rereading every project.

Before editing a record, reread its latest state and preserve unrelated entries. Use unique lesson/assessment filenames; never overwrite a different session's work. Keep dates, evidence references, assistance levels and uncertainty explicit. Update the detailed lesson/assessment first, then technology summaries and the checkpoint/index. If a save is interrupted, recover from existing evidence rather than inventing progress. Tell the learner when a save fails.

Use a compact competency entry such as:

```text
Competency:
Status: unassessed | developing | demonstrated | retained
Evidence: project ID, date, lesson/assessment link, version/context
Observed performance:
Assistance: independent | conceptual hint | guided retry
Autonomy stage: guided | learner-planned | independent | consultation
Independence evidence: planning, research, debugging, self-review or delivery
Gap or uncertainty:
Next recall/transfer check:
```

`Demonstrated` requires an observed application and explanation. `Retained` requires successful later recall or transfer. A long gap creates a reason to recheck, not an automatic erasure of prior learning. Store conflicting new evidence alongside earlier evidence and revise confidence accordingly.

Keep implementation, review/supervision, standards application and release judgment as distinct competencies. Success in one does not prove the others. Preserve evidence of independent work so a future project does not unnecessarily restore stepwise coaching.

If records are missing, unreadable, or from an unknown schema, disclose the gap, preserve them and ask a short recovery question. Do not fabricate an earlier project. Never erase learning history automatically. If the learner requests forgetting/deletion, follow the host's authorization rules and accurately describe the scope; do not claim to erase backups or other copies.
