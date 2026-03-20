# Task List Schema

This file defines the standard structure for `task-list.yaml`.

## Purpose

- provide one shared contract for upstream planning prompts
- give the Ralph harness a stable description of the task list structure
- ensure both team and individual workflows emit the same file shape

## Output file

- File name: `task-list.yaml`
- Format: YAML
- Root type: mapping
- Ordering rule: tasks must appear in recommended implementation order
- Inclusion rule: include only implementation-ready tasks
- Empty-output rule: if no tasks are implementation-ready, output the empty-state structure defined below

## File structure

```yaml
tasks:
  - id: T01
    title: Example task title
    goal: Outcome this task should produce.
    steps:
      - Concrete implementation action.
    depends_on: []
    done_when:
      - Testable condition that defines completion.
    notes:
      - "Optional context, reference, constraint, or non-goal."
```

## Empty-state structure

If no tasks are implementation-ready, output exactly:

```yaml
tasks: []
```

## Task structure rules

The file must have one top-level key:

- `tasks`

`tasks` must be a YAML list. Each item in that list must be a mapping with these keys:

- `id`
- `title`
- `goal`
- `steps`
- `depends_on`
- `done_when`
- `notes` optional

## Field definitions

| Field | Type | Required | Rules |
| --- | --- | --- | --- |
| `id` | string | yes | Stable identifier such as `T01`, `T02`, `T03`. |
| `title` | string | yes | Short human-readable task title. |
| `goal` | string | yes | Clear outcome the task should produce. |
| `steps` | list of strings | yes | At least one concrete implementation action. |
| `depends_on` | list of strings | yes | Prerequisites or earlier task IDs; use `[]` if empty. |
| `done_when` | list of strings | yes | At least one testable completion condition. |
| `notes` | list of strings | no | Optional context, references, constraints, or explicit non-goals. |

## Global constraints

- Do not add keys beyond the schema defined above, except to omit `notes` when it is not needed.
- Do not include blocked, ambiguous, or partially defined tasks.
- Do not include summaries, commentary, rationale sections, or clarification sections in `task-list.yaml`.
- Every task must be self-contained enough for a downstream implementation agent to begin work.
- Use concise but specific language. Avoid vague entries such as "improve UX" or "fix stuff".
- Keep numbering sequential: `T01`, `T02`, `T03`, and so on.
- Prefer plain strings over nested objects inside task fields.

## Task readiness standard

A task belongs in `task-list.yaml` only when:

- the goal is clear
- the scope is bounded
- the steps are concrete
- done-when conditions are testable
- there is no material ambiguity that would block implementation

If a work item does not meet this standard, keep it out of `task-list.yaml` until it is clarified.

## Example minimal task

```yaml
tasks:
  - id: T01
    title: Add login error state
    goal: Show a clear inline error message when login fails with invalid credentials.
    steps:
      - Render an inline error message in the login form when the API returns invalid credentials.
      - Clear the error message after a successful login attempt.
    depends_on: []
    done_when:
      - An invalid login attempt shows a visible inline error message.
      - A successful login attempt clears any previous inline error message.
    notes:
      - "Reference: Login page"
      - "Reference: Authentication API invalid-credentials response"
      - "Not in scope: Password reset flow"
      - "Not in scope: Rate limiting changes"
```
