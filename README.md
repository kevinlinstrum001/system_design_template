# System Design Template

A practical learning, documentation, and experimentation project for designing human-centered digital workflows.

This repository is used to study how people, physical work, devices, software, stored data, automation, and records can cooperate as one understandable system.

It has two primary purposes:

1. **Build and test small workflow systems** using tools such as Google Apps Script, Google Forms, Google Sheets, Google Keep, Google Tasks, Gmail, static web pages, phones, watches, and related services.
2. **Document the reasoning behind those systems** so the project gradually becomes a small textbook and reference library for practical system design.

The project is not intended to force every function into one large application. It is intended to discover which parts are needed, what responsibility each part should have, and how those parts should communicate.

---

## Core model

A practical workflow may involve three broad domains.

### Human

The human:

* receives information;
* interprets instructions;
* makes decisions;
* performs work;
* tracks personal progress;
* reports results, problems, or completion.

### Physical world

The physical world includes:

* rooms;
* carts;
* supplies;
* tools;
* equipment;
* observable conditions;
* physical actions;
* the work being performed.

### Digital system

The digital system includes:

* software;
* stored data;
* scripts;
* automated processes;
* connected services;
* interfaces;
* notifications;
* event state;
* permanent records.

Phones, computers, tablets, and watches are usually best understood as **interfaces to the digital system**, rather than as the entire system themselves.

The project studies how these three domains cooperate without requiring them to contain identical information or depend too heavily on one another.

---

## General workflow under study

A common workflow in this project may follow this pattern:

```text
Trigger
   ↓
Event created
   ↓
Human notified
   ↓
Procedure or reference provided
   ↓
Human performs physical work
   ↓
Completion or exception signal submitted
   ↓
Digital system responds
   ↓
Useful record preserved
```

Not every experiment will use every step, and different tools may perform different responsibilities.

---

## Central design question

A central question in this project is:

> How does the human tell the digital system that the state of an event has changed?

Possible signals may include:

* form submission;
* button press;
* task completion;
* message;
* QR-based action;
* spreadsheet edit;
* web application action;
* explicit completion signal;
* exception or problem report.

The project will test these approaches rather than assume that one mechanism is correct for every workflow.

---

## Guiding principles

### Design for ease of use

A system that is difficult to use will not be used reliably.

Ease of use is a functional requirement, not decoration.

### Describe the work before choosing the software

The work, responsibilities, information, handoffs, and desired outcomes should be understood before selecting tools.

A product such as Google Forms or Google Sheets may become part of a system, but it should not define the problem.

### Give each part a clear responsibility

A notification does not need to contain an entire procedure.

A checklist does not need to become a database.

A database does not need to manage every detail of human working progress.

Each tool should do the job it is best suited to perform.

### Separate human working state from digital system state

The human may know:

* which steps are complete;
* what remains;
* what problem occurred;
* what they are currently doing.

The digital system may know only:

* an event was created;
* a notification was sent;
* the event is active;
* a completion signal has or has not been received.

These states are related, but they do not need to be identical.

### Reference stable information

Large, reusable, or stable information should usually be referenced rather than copied through every part of the system.

> Reference the procedure. Transport only the data that must cross between parts.

### Preserve progress

A person should be able to:

* leave the interface;
* allow a device to sleep;
* switch applications;
* pause the work;
* return later;
* continue without losing their place.

### Separate current state from permanent history

Current state describes what is true now.

History describes what happened and when.

A state may change. A historical record should remain available.

### Use fast, deliberate triggers during testing

A system intended to run daily or weekly should often be tested first using a button, form submission, or other immediate trigger.

Testing should not require waiting for the final production schedule.

### Record only useful information

The system should preserve enough information to answer meaningful questions later, without collecting data that serves no clear purpose.

---

## Important distinctions

### Task definition and task instance

A **task definition** is the reusable description of a kind of work.

Example:

> Inspect the cart using the seven-step procedure.

A **task instance** is one actual occurrence of that task.

Example:

> Cart inspection requested on July 21 at 8:14 AM.

The definition may be reused many times. Each instance receives its own identity, state, timestamps, and record.

### Trigger and function

A **trigger** causes a process to begin.

Examples include:

* a form submission;
* a scheduled time;
* a button press;
* a QR scan;
* a spreadsheet edit;
* completion of another event.

A **function** is what the digital system does after the trigger occurs.

The same function may be tested with a manual trigger and later connected to a schedule.

### State and history

State describes what the system currently believes:

```text
Status: active
Completion signal: not received
Last updated: 8:17 AM
```

History describes what occurred:

```text
8:14 AM — Event created
8:15 AM — Notification sent
8:17 AM — Human acknowledged event
8:29 AM — Completion submitted
```

A useful system may require both.

### Reference and transport

A reference tells a person or system where to find another resource.

Transport moves the actual data from one component to another.

A task event may reference a procedure without copying the complete procedure into every notification, form, task, and record.

### Current files and archived files

Active files describe or support the present project.

Archived files are no longer current but remain valuable for:

* history;
* comparison;
* recovery;
* studying failed experiments;
* understanding why a design changed.

Archived material should not be treated as current guidance.

---

## Repository structure

```text
system_design_template/
│
├── README.md
├── overview.md
├── index.html
│
├── archive/
│   └── README.md
│
├── assets/
│   └── README.md
│
├── config/
│   ├── README.md
│   └── resources.json
│
├── docs/
│   └── README.md
│
├── examples/
│   ├── README.md
│   │
│   └── 01-task-app/
│       ├── README.md
│       ├── design.md
│       ├── index.html
│       │
│       ├── assets/
│       │   └── README.md
│       │
│       └── data/
│           └── README.md
│
└── shared/
    └── README.md
```

The structure may expand as real needs appear. New folders should not be created merely because they are common in other repositories.

---

## Directory responsibilities

### Root files

#### `README.md`

The main repository charter.

It should explain:

* the purpose of the project;
* the current conceptual model;
* the repository structure;
* project-wide principles;
* the development method;
* the current stage of work.

#### `overview.md`

The initial long-form system-design lesson and conceptual foundation.

It contains expanded explanations of:

* the three-domain model;
* task definitions and task instances;
* state and history;
* references and transported data;
* triggers, signals, events, records, and responses;
* system goals and design priorities.

Material from this document may later be reorganized into polished lessons under `docs/`.

#### `index.html`

The planned public entrance to the repository.

When GitHub Pages is enabled, this page should provide access to:

* project documentation;
* lessons;
* examples;
* demonstrations;
* diagrams;
* current experiments.

---

### `docs/`

Repository-wide documentation and instructional material.

Use this folder for:

* system-design lessons;
* vocabulary;
* guiding principles;
* architecture notes;
* design methods;
* workflow explanations;
* decision records;
* comparison documents;
* diagrams;
* lessons learned across several examples.

Documentation that applies only to one experiment should remain inside that experiment.

---

### `examples/`

Self-contained applications, prototypes, experiments, and case studies.

Each example should preserve both:

1. the working system or interface;
2. the reasoning and learning that produced it.

An example should answer a clear design question.

Possible examples include:

* notification tests;
* completion-signal experiments;
* Apps Script workflows;
* Forms and Sheets integrations;
* watch and phone interfaces;
* event-state models;
* task-management prototypes;
* static web interfaces;
* failed experiments that produced useful lessons.

A typical example may contain:

```text
example-name/
├── README.md
├── design.md
├── index.html
├── assets/
└── data/
```

---

### `examples/01-task-app/`

The first prepared application sandbox.

Its intended responsibilities are:

#### `README.md`

Explain:

* what the example does;
* how to use it;
* what question it is testing;
* its current status;
* important limitations.

#### `design.md`

Preserve the reasoning behind the example:

* problem statement;
* assumptions;
* design question;
* proposed workflow;
* component responsibilities;
* hypotheses;
* decisions;
* test plan;
* observations;
* conclusions;
* unresolved questions.

#### `index.html`

The working static interface or demonstration page for the example.

#### `assets/`

Images, icons, diagrams, screenshots, and styles used only by this example.

#### `data/`

Structured data used by the example, such as:

* task definitions;
* event samples;
* mock form submissions;
* test records;
* lookup tables;
* exported results;
* JSON configuration.

---

### `shared/`

Reusable technical material intended for more than one example.

Possible contents include:

* shared CSS;
* JavaScript utilities;
* JSON schemas;
* reusable interface components;
* HTML fragments;
* helper functions;
* templates;
* common configuration patterns.

Material should remain inside an individual example until it has a real reuse case.

Do not move something into `shared/` merely because it might be reusable someday.

---

### `assets/`

Visual and media resources used across the repository.

Possible contents include:

* diagrams;
* infographics;
* icons;
* logos;
* illustrations;
* screenshots;
* printable reference images;
* reusable interface graphics.

Assets used only by a single example should remain inside that example.

---

### `config/`

Repository-level configuration, registries, and non-secret metadata.

Possible contents include:

* resource registries;
* project metadata;
* environment labels;
* shared settings;
* lookup tables;
* feature settings;
* paths to external resources;
* non-secret connection information.

#### `resources.json`

A structured registry of important resources used by the project.

Resources may include:

* Google Sheets;
* Google Forms;
* external documents;
* repository files;
* web applications;
* safety documents;
* other services.

A resource record may describe:

```json
{
  "id": "resource-id",
  "name": "Readable Resource Name",
  "type": "google-sheet",
  "url": "https://example.com",
  "purpose": "Explains why the resource exists",
  "status": "active",
  "access": "private",
  "tags": ["events", "records"],
  "notes": ""
}
```

Do not place passwords, API keys, tokens, private credentials, or other secrets in this file.

---

### `archive/`

Material that is no longer active but remains useful.

Use this folder for:

* superseded documents;
* retired examples;
* failed prototypes;
* old data structures;
* replaced diagrams;
* discontinued pages;
* earlier versions;
* files retained for recovery or comparison.

Whenever practical, archived material should include enough context to explain:

* why it was archived;
* what replaced it;
* whether any part remains useful.

---

## Development approach

The project favors **small, deliberate sandbox experiments** over large speculative builds.

A useful experiment should answer one or two questions clearly.

Examples:

* Can a form submission create a work event?
* Can the event generate a watch-visible notification?
* Can a person use a separate checklist while the system tracks only event status?
* Can a completion signal update the event and preserve a useful record?
* Can progress survive interruption?
* What information must the system store itself?
* What information can remain in referenced resources?
* How should duplicate signals be handled?

---

## Recommended experiment lifecycle

Each experiment should move through a simple lifecycle.

### 1. Describe the real problem

State what the human is trying to accomplish in the physical world.

Avoid beginning with a product name.

### 2. Identify the design question

Write one or two questions the experiment should answer.

### 3. Identify the parts

List:

* human responsibilities;
* physical-world objects or conditions;
* digital components;
* interfaces;
* triggers;
* signals;
* state;
* records;
* external references.

### 4. Assign responsibilities

Explain what each component should do and what it should not do.

### 5. Build the smallest useful test

Use the minimum implementation necessary to answer the design question.

### 6. Test deliberately

Prefer fast triggers and visible outputs.

Record what actually happened rather than what was expected to happen.

### 7. Preserve observations

Document:

* successful behavior;
* failures;
* confusion;
* interruption problems;
* duplicate events;
* missing information;
* unnecessary complexity;
* human effort.

### 8. Draw conclusions

State:

* what was learned;
* what remains unknown;
* what should be repeated;
* what should be changed;
* whether the experiment should continue.

### 9. Reuse or archive

Reusable material may later move into `shared/`.

Completed or superseded experiments may remain in `examples/` for study or move into `archive/` when they are no longer active.

---

## Design documentation standard

Each substantial example should eventually explain the following:

```text
Purpose
Design question
Human role
Physical-world role
Digital-system role
Trigger
Event
Task definition
Task instance
Procedure reference
Human working state
System state
Completion signal
Response
Permanent record
Failure cases
Test method
Observations
Conclusions
Open questions
```

Not every small experiment requires a long document, but the reasoning should remain inspectable.

---

## Failure and interruption

Systems should be designed with the expectation that normal interruptions will occur.

Examples include:

* notifications being missed;
* devices going to sleep;
* the human switching applications;
* work being paused;
* forms being abandoned;
* connectivity being lost;
* duplicate signals being submitted;
* an event remaining incomplete;
* a resource becoming unavailable;
* a person forgetting the current step;
* state and history becoming inconsistent.

A workflow should not be judged only by how it behaves under ideal conditions.

---

## Working vocabulary

| Term                | Working meaning                                                               |
| ------------------- | ----------------------------------------------------------------------------- |
| System design       | Deciding what parts exist, what each part does, and how they cooperate        |
| Human               | The person receiving information, deciding, acting, and reporting             |
| Physical world      | The environment, objects, tools, conditions, and real work                    |
| Digital system      | Software, stored data, automation, connected services, and records            |
| Interface           | The place where a human interacts with the digital system                     |
| Trigger             | Something that causes a process or function to begin                          |
| Function            | An action performed by the digital system                                     |
| Event               | A meaningful occurrence represented in the system                             |
| Workflow            | The sequence through which work moves                                         |
| Task definition     | The reusable description of what a task means                                 |
| Task instance       | One particular occurrence of a task                                           |
| Procedure           | Instructions for carrying out the task                                        |
| Procedure reference | A link or identifier pointing to instructions                                 |
| Reference           | Information describing where another resource can be found                    |
| Transport           | Moving actual data from one part to another                                   |
| State               | What is currently believed to be true                                         |
| Human working state | The human’s current progress through the work                                 |
| System state        | The digital system’s current understanding of an event                        |
| Signal              | A small input communicating that something happened                           |
| Completion signal   | The input indicating that work has finished                                   |
| Exception signal    | An input reporting that normal completion was not possible                    |
| Record              | Preserved information about what occurred                                     |
| Response            | What the digital system does after receiving an event or signal               |
| Handoff             | A point where responsibility or information passes between parts              |
| Acknowledgment      | Confirmation that an input or signal was received                             |
| Identifier          | A value distinguishing one event or task instance from another                |
| Loose coupling      | Parts cooperating without depending heavily on one another’s internal details |
| Archive             | Material preserved for history or recovery but no longer treated as current   |

---

## Project status

The project is currently in the **foundation and first-experiment stage**.

Work completed so far includes:

* defining the human, physical-world, and digital-system domains;
* distinguishing task definitions from task instances;
* distinguishing human progress from digital system state;
* identifying triggers, events, signals, records, responses, references, and interfaces;
* separating current state from permanent history;
* defining ease of use as a functional requirement;
* establishing repository-wide folder responsibilities;
* creating a resource-registry pattern;
* preparing the first application sandbox;
* outlining an initial workflow involving a trigger, notification, human procedure, completion signal, response, and event record.

No final architecture has been selected.

The next major step is to complete the first small experiment and preserve:

* its design question;
* its implementation;
* its data;
* its test method;
* its observations;
* its conclusions.

---

## Static site

The root `index.html` file is intended to become the main static entrance for the project.

When GitHub Pages is enabled, the site may be published from the `main` branch and repository root.

The site should eventually provide clear navigation to:

* project orientation;
* lessons;
* vocabulary;
* examples;
* current experiments;
* diagrams;
* design records;
* archived material where appropriate.

---

## Project philosophy

> Reference the procedure. Transport only the data that must cross between parts.

> Describe the work before choosing the software.

> Ease of use is a functional requirement.

> Human working state and digital system state are related, but they are not identical.

> A current state may change. A useful historical record should remain.

> Build only enough to answer the present design question.

The goal is not to force every tool into one application.

The goal is to make the system serve the human and the work, while preserving enough reasoning that future systems can be designed more clearly, tested more intelligently, and explained more precisely.
