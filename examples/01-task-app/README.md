This version is based on Step 5 of the development plan and the current `examples/README.md` rules. It treats `01-task-app` as a planned, bounded first experiment rather than as a finished application.  

# Task App

**Status:** planned

This directory contains the first prepared experiment in the **System Design Template** repository.

The experiment is intended to test a small, human-centered task workflow before any final software architecture is selected.

It is not yet a working production application.

---

## Purpose

The purpose of this example is to test how one identifiable task event can move through a simple digital workflow.

The example will explore how the digital system can:

* create one task instance;
* give that instance a stable identity;
* display its current state;
* allow a human to report completion;
* update the current state;
* preserve a separate history of what happened.

This experiment is designed to make the distinction between current state and permanent history visible and testable.

It is also intended to provide a small sandbox for applying the project’s core vocabulary and design principles.

---

## Design question

The primary design question is:

> Can a deliberate trigger create one identifiable task instance, display its current state, accept one explicit completion signal, and preserve a separate history record?

This question is deliberately narrower than building a complete task-management application.

The experiment does not yet attempt to determine the final notification system, device interface, database, form platform, or production workflow.

---

## Problem being explored

A human may need to perform a task in the physical world.

The digital system must be able to represent that occurrence as one distinct event rather than only as a reusable task description.

The system should help answer:

* What task instance exists?
* What is its current state?
* Has completion been reported?
* What happened to the event, and when?
* Can current state change without erasing history?

The experiment will use a simplified task so the design concepts can be tested without unnecessary operational complexity.

---

## What this example demonstrates

When implemented, this example should demonstrate:

* the difference between a task definition and a task instance;
* creation of a unique event;
* use of a deliberate test trigger;
* display of current system state;
* submission of a completion signal;
* transition from active to complete;
* preservation of event history;
* separation of reusable task information from event-specific information;
* basic handling of duplicate or invalid completion attempts.

The experiment should preserve both the interface and the reasoning behind it.

---

## Core model

The experiment uses the project’s three-domain model.

### Human

The human:

* starts or receives the task event;
* reads what must be done;
* performs or simulates the task;
* sends a completion signal;
* observes the system response.

### Physical world

The physical-world portion is represented by a small generic task.

The task should remain simple enough that the experiment focuses on system behavior rather than operational detail.

A possible placeholder task is:

> Inspect a work area and report completion.

The exact task definition may change before implementation.

### Digital system

The digital system:

* creates the task instance;
* assigns an identifier;
* records its initial state;
* displays task information;
* accepts a completion signal;
* updates current state;
* appends a history record;
* reports the resulting state to the human.

---

## Planned workflow

```text
Deliberate trigger
        ↓
Task instance created
        ↓
Unique identifier assigned
        ↓
Current state set to active
        ↓
Task displayed to human
        ↓
Human performs or simulates work
        ↓
Human submits completion signal
        ↓
Current state changes to complete
        ↓
History record is appended
        ↓
Updated state is displayed
```

The digital system does not need to observe every physical action or every checklist step.

For this experiment, it only needs an explicit completion signal.

---

## Scope

This example will test:

* one reusable task definition;
* one or more task instances;
* a deliberate manual trigger;
* unique event identity;
* current state;
* event history;
* an explicit completion signal;
* a visible interface;
* public-safe sample data;
* simple duplicate-signal behavior.

The example may initially operate entirely in a static web page using local in-memory sample data.

External services should be introduced only when they are necessary to answer a later design question.

---

## Non-goals

This experiment will not initially attempt to provide:

* production deployment;
* workplace integration;
* real employee tasks;
* real operational records;
* authentication;
* user accounts;
* supervisor access;
* email notifications;
* watch notifications;
* Google Forms integration;
* Google Sheets integration;
* Apps Script automation;
* scheduling;
* recurring tasks;
* multiple human roles;
* complex permissions;
* permanent remote storage;
* complete offline support;
* a final user-interface design.

These may become subjects of later experiments.

---

## Current workflow state

The experiment is currently in the planning and documentation stage.

Completed:

* directory structure created;
* repository-wide example policy established;
* initial experiment purpose identified;
* primary design question selected;
* intended workflow outlined.

Not yet completed:

* detailed design document;
* data model;
* sample task definition;
* sample event records;
* sample history records;
* working interface;
* test plan;
* observations;
* conclusions.

---

## How to inspect this example

At present, inspect the example by reading:

1. this README for the experiment’s purpose and current state;
2. `design.md` for detailed system reasoning once Step 6 is complete;
3. `data/README.md` for experiment-owned data rules;
4. `assets/README.md` for local media rules;
5. `index.html` once the working sandbox interface is created.

Because the experiment is still planned, opening `index.html` may not yet display a functioning interface.

---

## Planned interaction

The first interface should remain small.

A possible initial interaction is:

1. Press **Create task**.
2. Observe a new task instance.
3. Review:

   * task identifier;
   * task title;
   * current status;
   * creation time.
4. Press **Complete task**.
5. Observe:

   * state change from `active` to `complete`;
   * completion timestamp;
   * appended history entry.
6. Attempt completion again.
7. Observe how the system handles a duplicate signal.

The final interaction design will be determined in `design.md`.

---

## Files in this example

```text
01-task-app/
├── README.md
├── design.md
├── index.html
├── assets/
│   └── README.md
└── data/
    └── README.md
```

### `README.md`

Explains:

* why the example exists;
* what question it tests;
* its current status;
* what it should demonstrate;
* how it can be inspected;
* what remains incomplete.

### `design.md`

Will preserve the detailed reasoning for the experiment, including:

* problem statement;
* scope;
* non-goals;
* human role;
* physical-world role;
* digital-system role;
* components and responsibilities;
* event model;
* task-definition model;
* state model;
* completion signal;
* record model;
* failure cases;
* known, assumed, and unknown information;
* test plan;
* observations;
* decisions;
* conclusions;
* open questions.

### `index.html`

Will contain the smallest useful interface for testing the design question.

It should not become a complete task-management application.

### `assets/`

Will contain media used only by this example, such as:

* local diagrams;
* screenshots;
* example-specific icons;
* local styles not yet promoted to `shared/`.

### `data/`

Will contain public-safe structured data owned by this experiment, such as:

* task definitions;
* sample task instances;
* current-state examples;
* history examples;
* test fixtures.

Reusable schemas should eventually belong in `shared/schemas/`, not in this folder.

---

## Planned data categories

The experiment should keep these concepts separate.

### Task definition

The reusable description of the work.

Possible example:

```json
{
  "taskDefinitionId": "inspect-work-area",
  "title": "Inspect work area",
  "instructions": "Inspect the sample area and report completion."
}
```

### Task instance

One occurrence of the task.

Possible example:

```json
{
  "eventId": "event-0001",
  "taskDefinitionId": "inspect-work-area",
  "status": "active",
  "createdAt": "2026-07-21T08:14:00-06:00",
  "completedAt": null
}
```

### Current state

What the digital system currently believes.

Possible example:

```json
{
  "eventId": "event-0001",
  "status": "active",
  "completionSignalReceived": false
}
```

### History

What happened and when.

Possible example:

```json
[
  {
    "eventId": "event-0001",
    "eventType": "created",
    "timestamp": "2026-07-21T08:14:00-06:00"
  }
]
```

These examples are provisional. The actual structures should be defined in `design.md` before data files are created.

---

## Known

The following ideas are already established at the project level:

* a task definition is different from a task instance;
* current state is different from history;
* the human and digital system do not need identical information;
* a completion signal may be enough for the digital system;
* a deliberate trigger is appropriate for early testing;
* the experiment should remain small;
* all committed sample data must be safe for public viewing.

---

## Assumed

The experiment currently assumes:

* one human role is sufficient;
* one task definition is sufficient;
* a manual trigger is sufficient;
* one explicit completion action is sufficient;
* current state can be represented by a small object;
* history can be represented as an append-only list;
* a static interface is sufficient for the first test;
* local in-memory behavior is acceptable before remote persistence is tested.

These assumptions may change after design review or testing.

---

## Unknown

The experiment should help determine:

* the minimum fields required for a task instance;
* how identifiers should be generated;
* whether state and history should be stored separately;
* how duplicate completion signals should be handled;
* whether an acknowledgment state is needed;
* what information the human needs to see;
* what information should remain hidden from the interface;
* whether the first interface can remain entirely static;
* which findings should become reusable patterns;
* what the next experiment should isolate.

---

## Known limitations

The current example has several limitations:

* no working interface;
* no implemented event model;
* no persistent storage;
* no automated trigger;
* no external notification;
* no device testing;
* no interruption testing;
* no recorded observations;
* no validated conclusions.

These limitations are expected because the experiment is still planned.

---

## Current test state

No formal test has been run.

The first test should not begin until `design.md` defines:

* the event model;
* current-state model;
* history model;
* completion-signal behavior;
* duplicate-signal behavior;
* test steps;
* expected results.

The example should remain `planned` until meaningful implementation or testing begins.

---

## Dependencies

Current repository dependencies:

### Root project charter

```text
README.md
```

Defines the project model, principles, vocabulary, and repository responsibilities.

### Examples policy

```text
examples/README.md
```

Defines example naming, lifecycle, documentation, privacy, completion, promotion, and archive rules.

### Detailed design

```text
examples/01-task-app/design.md
```

Will define the experiment’s engineering and reasoning model.

### Resource registry

```text
config/resources.json
```

May register the example entry page and any important external resources.

The example should not depend on undocumented private files, personal device settings, or inaccessible external resources.

---

## Related registered resources

The repository resource registry may contain records for:

* the Task App example;
* a planned system-events sheet;
* a planned start-test form.

Those resources should remain marked `planned` until they exist and their locations are verified.

The first local static experiment should not require those external resources.

---

## Privacy and safety

This is a public repository.

This example must not contain:

* real workplace records;
* real employee names;
* client or patient information;
* private form responses;
* email addresses;
* private document identifiers;
* passwords;
* tokens;
* API keys;
* secret-bearing URLs;
* sensitive operational details.

All sample data must be:

* fictional;
* anonymized;
* or deliberately safe for public viewing.

---

## Completion criteria

This experiment may be marked `complete` when:

* the primary design question has been answered;
* a task instance can be created;
* the instance has a stable identity;
* current state is visible;
* an explicit completion signal is accepted;
* current state changes correctly;
* history is preserved separately;
* duplicate-signal behavior is defined and tested;
* test steps are documented;
* observations are recorded;
* limitations are stated;
* conclusions are written;
* private information has been excluded.

Completion does not require production deployment or external service integration.

---

## Next step

The next step is to complete:

```text
examples/01-task-app/design.md
```

That document should define the experiment in enough detail to support:

* the data model;
* the first sample records;
* the test plan;
* the smallest useful interface.

Implementation of `index.html` should begin only after the design document establishes those contracts.

---

## Possible follow-up experiments

Questions intentionally left for later experiments may include:

* Can a form submission create the event?
* Can an event produce a phone or watch notification?
* Can the human follow a referenced procedure?
* Can progress survive interruption?
* Can remote storage preserve state across devices?
* Can duplicate external signals be handled safely?
* Can several task instances remain distinct?
* Can an exception signal be handled separately from completion?

These should become separate examples when they represent distinct design questions.

---

## Design principle

This example should remain small enough to answer one useful question clearly.

Its purpose is not to become a complete task application.

Its purpose is to test whether one task instance can be created, understood, completed, and recorded without confusing reusable task information, current state, and permanent history.
