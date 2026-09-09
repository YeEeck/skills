---
name: subagent-impl
description: Complete a list of tasks by dispatching subagents one at a time, in an order you derive from their dependencies, verifying each result before starting the next. Use when the user hands over a task list, spec, or tickets and asks you to delegate the work to subagents and finish all of it serially.
---

# Subagent Implementation (serial)

You orchestrate; subagents execute. One subagent per task, **serially**: each task's verified result is the **premise** for the next.

## 1. Establish the task list

Take the tasks from the user's request, spec, or tickets. A task is one unit of work a fresh agent could complete on its own; split anything with two independent deliverables.

Done when: every piece of the user's ask appears exactly once on the list.

## 2. Derive the order

Sort by dependency: a task whose output others consume (scaffolding, interfaces, shared types, migrations) runs before its consumers; integration and final verification run last. The order is yours to derive from the tasks themselves.

Done when: the list is in one serial order, and each task names what it consumes from earlier tasks.

## 3. Run the ladder, one rung at a time

For each task, in order:

1. **Dispatch** a subagent (whatever subagent/background-agent mechanism this environment provides) with a **self-contained** prompt — it does not see this conversation. Include: the task; where the code lives; the premises, i.e. exactly what earlier tasks produced (files, interfaces, decisions); acceptance criteria; and that its result will be verified.
2. **Wait** for it to finish before dispatching the next — subagents share the working tree, so overlap means collisions.
3. **Verify** against the acceptance criteria before the result becomes a premise: read the diff, run the tests or typecheck the repo has. On failure, re-dispatch the same task with the correction stated in its prompt.
4. **Record** what the next tasks must know: what changed, where, and what was decided.

Done when: every task on the list has passed verification.

## 4. Report

Summarize per task: what its subagent did, the verification result, and any deviation from the original order.
