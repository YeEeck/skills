---
name: subagent-impl
description: Implement all tickets from a to-spec / to-tickets plan by dispatching one subagent per ticket, strictly serially in the order the tickets declare, verifying every acceptance criterion before the next ticket starts. Use when the user points at a ticket set — local ticket files or tracker issues — and asks you to delegate the work to subagents and finish all of it.
---

# Subagent Implementation (serial)

You orchestrate; subagents execute. One subagent per ticket, **serially**: each ticket's verified result is the **premise** for the next.

The tickets already fix the order — `to-tickets` numbers them blockers-first and each one declares its **Blocked by** edges. Follow that order; do not re-plan it.

## 1. Load the ticket set

Identify the tickets the user points at — local ticket files (e.g. `.scratch/<feature-slug>/issues/`) or tracker issues, wherever `to-tickets` published them — and read every one.

Done when: you hold the complete list in execution order — a ticket becomes eligible only once its blockers are verified.

## 2. Run the ladder, one rung at a time

Run exactly one ticket at a time even when several are eligible at once — serial is the contract: it keeps each premise verified before anything builds on it, and keeps subagents off each other's working tree.

For each ticket:

1. **Dispatch** a subagent (whatever subagent mechanism this environment provides) with a **self-contained** prompt — it does not see this conversation. Include: the ticket body verbatim; where the code lives; the premises — what earlier tickets changed and how they were verified; the acceptance criteria as the contract; and an instruction to report exactly what it changed.
2. **Wait** for it to finish before dispatching the next ticket.
3. **Verify** the result yourself against every acceptance criterion — read the diff, run the tests or typecheck. On failure, re-dispatch the same ticket with the failing criteria stated in its prompt as the correction.
4. **Tick and record** — mark the verified criteria done in the ticket (file checkbox or tracker), and note for later tickets what this one changed and decided.

Done when: every ticket is verified and its criteria ticked.

## 3. Report

Per ticket: what landed, the verification result, and any re-dispatch it took.
