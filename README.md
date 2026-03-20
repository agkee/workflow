# AI Team Delivery Workflow

This workspace captures a planning-first workflow for teams that want humans to stay focused on what to build while agents handle structured planning and implementation.

## Contents
- [Process guide](docs/team-delivery-workflow.md)
- [Meeting-note task extraction prompt](prompts/extract-tasks-from-meeting-notes.md)
- [User clarification prompt](prompts/clarify-ideas-into-task-pack.md)
- [Task list schema](schemas/task-list.schema.md)
- [Example task list](schemas/task-list.example.yaml)
- [Structured meeting template](templates/structured-meeting-template.md)

## Quick start
1. Before a team meeting, ask each participant what they want to get out of it.
2. Have each person clarify their thinking with the user clarification prompt.
3. Run the meeting using the structured template so decisions, tasks, and parking-lot topics are clearly separated.
4. Feed the meeting notes into the task extraction prompt to generate `task-list.yaml`.
5. Send `task-list.yaml` into your Ralph-method implementation harness.
6. Optionally insert a human approval checkpoint before implementation or before merge.

## Assumption
This documentation treats the "Ralph method" as your downstream implementation workflow. The documents here focus on the upstream process that makes `task-list.yaml` explicit enough for Ralph to execute with minimal human interruption.
