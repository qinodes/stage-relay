---
name: stage-relay
description: Use for large, multi-stage development tasks that need persistent progress tracking across sessions or agents, support per-stage or deferred batch acceptance, and require automated testing and user acceptance before completion.
---

# Development Task Relay Tracking

## Purpose

Large, multi-stage development tasks must use a file to continuously record:

- The final task objective.
- Each development stage created from the task.
- The current status of every stage.
- Automated test results.
- User acceptance status.
- Necessary development notes.

Development progress must not exist only in the conversation context. Once a tracking file has been created, it is the primary source of progress so that a new session or agent can continue correctly without the earlier conversation.

## Storage Location and Task Numbers

Store all tracking files under `stage-reley/tasks/`. Give each task its own directory with a three-digit sequential number. Its primary tracking file must be `stage-reley/tasks/<number>/task.md`:

```text
stage-reley/
└── tasks/
    ├── 001/
    │   └── task.md
    ├── 002/
    │   └── task.md
    └── 003/
        └── task.md
```

Before creating a task, inspect `stage-reley/tasks/` and find the highest existing task number. Use “current highest number + 1” for the new task. Create the directory if it does not exist. If there are no tasks, start at `001`.

For example, if these tasks exist:

```text
stage-reley/tasks/001/
stage-reley/tasks/002/
stage-reley/tasks/003/
```

Create the next task as:

```text
stage-reley/tasks/004/task.md
```

Always use a three-digit format, such as `001`, `009`, `010`, `099`, or `100`. Never:

- Reuse an existing number.
- Reuse a number because an older task is complete.
- Renumber tasks because one was deleted.
- Change the number of an existing task.

## Creating and Splitting a Task

When new development work matches this skill, you must:

1. Inspect `stage-reley/tasks/` and obtain the next task number.
2. Create `stage-reley/tasks/<number>/task.md`.
3. Record the task objective and set the Overall status to `In progress`.
4. Split the task into stages that can each be developed, tested, and accepted independently.
5. For each stage, record its name, objective, current status, acceptance criteria, automated test results, and necessary development notes.
6. Start the first unfinished stage.

For example, if the highest task number is `012`, create the new task at `stage-reley/tasks/013/task.md`.

Every stage should have:

- A clear objective and scope.
- Development work that can be performed independently.
- Relevant automated tests that can be run.
- Clear user acceptance criteria.

Avoid vague stages such as:

```text
Stage 1: Develop the feature
```

Use a description whose completion can be evaluated clearly:

```text
Stage 1: Build the user login API

Objective:
Complete the login API, token creation, and error handling.

Acceptance criteria:
- Valid credentials can log in.
- An incorrect password returns an error.
- A successful login returns a token.
```

## Status Workflow

### Overall Status

The Overall status may only be:

```text
In progress
Complete
```

A new task starts as `In progress`. Change it to `Complete` only after every stage is `Closed`. Never mark the Overall status as `Complete` while any stage remains unfinished.

### Stage Status

Each stage may only use the following statuses in this order. Do not skip a status:

```text
In progress
↓
Development complete
↓
Automated tests passed
↓
User acceptance complete
↓
Closed
```

- `In progress`: Code changes or related development work are underway.
- `Development complete`: The required implementation is finished, but the relevant automated tests have not all been confirmed as passing. This does not mean the stage is complete.
- `Automated tests passed`: The relevant tests were actually run and all passed, and the tests and results were recorded in `task.md`.
- `User acceptance complete`: After the automated tests passed, the user explicitly confirmed acceptance. The agent must never assume acceptance.
- `Closed`: This status is allowed only after `User acceptance complete` and means the stage is formally and fully complete.

Synchronize every stage status change to `task.md`; never report it only in the conversation:

```text
In progress → Development complete
Development complete → Automated tests passed
Automated tests passed → User acceptance complete
User acceptance complete → Closed
```

You may start the next unfinished stage only when either:

- The current stage is `Closed`.
- The current stage is `Automated tests passed`, and the user explicitly chooses to defer acceptance and continue to the next stage.

Deferring acceptance does not change the current stage status and does not mean the stage was accepted or closed. Record the user’s decision in the notes in `task.md`. Do not start the next stage unless the user explicitly chose to defer.

## Automated Testing

Before entering `Automated tests passed`, actually run the relevant tests. Update the status and record the results in `task.md` only when all relevant tests pass.

Do not mark a stage as `Automated tests passed` merely because:

- The tests are expected to pass.
- The code appears correct.
- The tests were not actually run.
- The tests cannot be run.
- Some tests failed.
- Testing is incomplete.

If a test fails, do not enter `Automated tests passed`. Record the results, fix the problem, and rerun the relevant tests until they all actually pass.

## User Acceptance

Passing automated tests does not complete a stage. When a stage reaches `Automated tests passed`, tell the user:

- What the stage completed.
- The automated test results.
- What they need to validate.

Base validation primarily on the stage’s acceptance criteria in `task.md`. Then handle one of these three outcomes according to the user’s explicit response:

1. **Accepted**
   - Update the status in order to `User acceptance complete`, then `Closed`.
   - The next unfinished stage may begin.
2. **Acceptance deferred**
   - Keep the status as `Automated tests passed`; do not mark it as `User acceptance complete` or `Closed`.
   - Record the user’s decision to defer acceptance in `task.md`.
   - The next stage may begin. The user may accept stages individually later or wait until every planned stage has passed automated testing and accept them together.
3. **Problem reported, acceptance failed, or changes requested**
   - Do not mark the stage as `User acceptance complete`, and do not start a new next stage.
   - Return the affected stage to `In progress` and record the user’s feedback in `task.md`.
   - Fix the problem, complete development again, and rerun the relevant automated tests. Do not reuse test results from before the change.
   - After every test passes, ask the user again whether they accept, defer acceptance, or have further feedback.

If the user both defers acceptance and reports a problem that requires a fix, follow the “Problem reported” branch and do not proceed to the next stage. The agent must not interpret an ambiguous response as either acceptance or a decision to defer.

For batch acceptance, gather every stage still at `Automated tests passed` and present each stage’s completed work, automated test results, and acceptance criteria together. The user may explicitly accept all stages at once or only some of them:

- For each explicitly accepted stage, update the status in order to `User acceptance complete`, then `Closed`.
- Keep deferred or not explicitly accepted stages at `Automated tests passed`.
- Return any stage with reported problems to `In progress` and prioritize fixing it. Do not begin a new stage until its fixes and retesting are complete.

## Resuming an Existing Task

If the user asks to resume an existing task, such as “continue task 013,” read `stage-reley/tasks/013/task.md` before modifying code and confirm:

1. The task objective.
2. The Overall status.
3. Which stages the task contains.
4. Which stages are already closed.
5. Which stages passed automated tests but have deferred or pending acceptance.
6. Which stage is currently in progress.
7. The current stage’s status.
8. The current stage’s acceptance criteria.
9. Which automated tests have been run.
10. The development notes.

Then continue from the state recorded in the file. Do not use the absence of earlier conversation context in a new session as a reason to:

- Create the same task again.
- Restart a completed stage.
- Ignore the existing tracking file.
- Assume earlier work was not completed.

## When Recorded and Actual State Differ

If the conversation context, `task.md`, actual code, Git state, or automated test results disagree, do not guess the current progress. Inspect, in order:

1. `task.md`.
2. The actual code.
3. Git diff / Git history, when applicable.
4. Automated test results.

After confirming the actual state, correct `task.md`. Never pretend unfinished work is complete merely to make reality match the file.

## Task Tracking File Template

Use this structure when creating a new `task.md`:

```markdown
# Development Task Tracking

## Task Objective

Describe the final objective of this large development task.

---

## Overall Status

In progress

---

## Stages

### Stage 1: <Stage name>

#### Objective

Describe what this stage must complete.

#### Status

In progress

#### Acceptance Criteria

- Criterion 1
- Criterion 2
- Criterion 3

#### Automated Tests

Not run yet.

#### Notes

None.

---

### Stage 2: <Stage name>

#### Objective

Describe what this stage must complete.

#### Status

In progress

#### Acceptance Criteria

- Criterion 1
- Criterion 2

#### Automated Tests

Not run yet.

#### Notes

None.

---

### Stage 3: <Stage name>

#### Objective

Describe what this stage must complete.

#### Status

In progress

#### Acceptance Criteria

- Criterion 1
- Criterion 2

#### Automated Tests

Not run yet.

#### Notes

None.
```

## Record Examples

Automated tests not yet run:

```text
#### Automated Tests

Not run yet.
```

Successful tests:

```text
#### Automated Tests

- Unit Tests: PASS
- Integration Tests: PASS
- Type Check: PASS
```

Failed tests:

```text
#### Automated Tests

- Unit Tests: PASS
- Integration Tests: FAIL
- Type Check: PASS

Failure reason:
The PaymentService integration test timed out.

Currently being fixed.
```

Do not mark a stage as `Automated tests passed` while any test is failing.

When the user defers acceptance:

```text
#### Status

Automated tests passed

#### Notes

The user chose to defer acceptance for this stage, continue to the next stage, and perform batch acceptance after all stages are complete.
```

If the stage is `Automated tests passed` but the user reports “Refreshing the page after login signs me out,” update it to:

```text
#### Status

In progress

#### Notes

User acceptance failed.

Problem:
Refreshing the page after login signs me out.

Fix the problem and rerun the automated tests.
```

After the fix, repeat:

```text
Development complete
↓
Automated tests passed
↓
Await user acceptance
```

## Task Completion and Retention

After every stage is `Closed`, change the Overall status from `In progress` to `Complete`. Never delete the tracking file after completion. For example, retain `stage-reley/tasks/013/task.md` as:

- Development history.
- A record of task design.
- A record of testing.
- A record of user acceptance.
- A reference for tracking future problems.

Continue using the next sequential number for subsequent tasks.
