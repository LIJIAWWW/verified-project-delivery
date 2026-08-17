---
name: verified-project-delivery
description: Manage long-running, multi-step, or multi-agent projects with evidence-based status, truthful running-state reports, dependency-aware parallel work, merge validation, adaptive project documentation, and concise milestone handoffs. Use when starting or continuing a substantial project, splitting work across agents, checking progress, claiming background execution, completing a milestone, or handing work to a new task without rereading full chat history.
---

# Verified Project Delivery

Keep project governance proportional to project complexity. Prefer verified delivery over process overhead.

## Select the documentation level

- For a small, bounded change, create no governance documents.
- For a medium multi-step project, create or maintain `PROJECT_STATUS.md` from `assets/PROJECT_STATUS.md`.
- For a long-running project, also create or maintain `PROJECT_CONTEXT.md` from `assets/PROJECT_CONTEXT.md`.
- For multi-agent work, add a short root `AGENTS.md` from `assets/AGENTS.md` when no applicable file already defines ownership and verification rules.
- Add `API_CONTRACT.md` only when independently developed components exchange non-trivial data.
- Add `DATA_DICTIONARY.md` only when shared data definitions, classifications, labels, or metrics are substantial.

Never overwrite useful existing project documents. Merge missing sections and preserve project-specific instructions.

## Plan executable work

Record each meaningful task with an owner, status, dependencies, allowed file scope, acceptance criteria, and verification evidence.

Allow as many parallel tasks as are genuinely independent. Do not present dependent stages as parallel. Prevent concurrent agents from editing the same files unless coordination is explicit.

Prioritize the critical path. A completed supporting task does not advance a blocked downstream task by itself.

## Report status truthfully

Track delivery state separately from execution activity. Use only these delivery states:

- `pending`: not started.
- `blocked`: cannot proceed without a dependency, decision, permission, or resource.
- `implemented`: changes exist but have not passed the required verification.
- `verified`: the task's own acceptance checks passed.
- `integrated`: merged with dependent work and integration checks passed.
- `completed`: the user-visible acceptance condition is satisfied.

Report execution activity as a separate field:

- `active`: an agent or process is currently executing and has recent evidence.
- `inactive`: no agent or process is currently executing.
- `waiting`: execution is paused for a named dependency, decision, permission, resource, or scheduled checkpoint.

Never claim `active` merely because work was planned or previously delegated. An active report must include the task or agent, recent effective output time, changed artifact or processing count, current blocker if any, and next checkpoint.

If no active evidence exists, report `inactive` or `waiting` and state that no background task is running. Preserve the delivery state: a task can be both `completed` and `inactive`, or `blocked` and `waiting`.

Do not estimate progress from intuition. Derive it from passed acceptance criteria and distinguish implementation, data completeness, integration, testing, and deployment when relevant.

## Verify before merging or completing

Run the checks appropriate to the project before integration: build, type check, tests, schema validation, data validation, render review, or smoke test.

Treat a subtask completion message as a claim to verify, not proof. Mark work `implemented` until direct checks pass. After merging, rerun the checks affected by integration.

Never describe scaffolding, mocks, placeholders, or unreviewed extracted data as a usable completed feature.

## Maintain concise handoffs

At each milestone, update the minimum applicable documents with:

- what is complete and how it was verified;
- what remains, is blocked, or is only implemented;
- current task states and dependencies;
- the next checkpoint;
- the exact files the next task should read.

When a new task takes over, read in this order:

1. `PROJECT_STATUS.md` when present.
2. `PROJECT_CONTEXT.md` when relevant.
3. Only the applicable contract or dictionary.
4. Only code and artifacts directly related to the assigned task.

Do not reread the full conversation or scan the entire repository unless the handoff is missing, stale, or contradicted by verified code and tests.

## Keep the process light

Do not create empty documents, duplicate facts across files, add governance scripts by default, impose a fixed parallel-agent limit, or introduce fixed percentage checkpoints. Add structure only when it reduces ambiguity, rework, or context cost.

