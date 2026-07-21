# Examples

This folder contains the applications, prototypes, experiments, and case studies created while developing the **System Design Template** project.

Each example should preserve both:

1. the working system, interface, or technical demonstration;
2. the reasoning, observations, and learning that produced it.

The goal is not only to keep finished applications.

The goal is to make each experiment understandable and inspectable later, including experiments that failed, changed direction, or revealed that an assumption was incorrect.

---

## Purpose

Use `examples/` for self-contained experiments that test practical system-design questions.

Possible examples include:

* workflow prototypes;
* notification tests;
* completion-signal experiments;
* watch and phone interfaces;
* Apps Script demonstrations;
* Google Forms and Sheets integrations;
* static web interfaces;
* event and state models;
* small task-management systems;
* data-flow experiments;
* interruption-recovery tests;
* failed experiments that produced useful lessons.

Each example should answer one or two clear design questions.

An example should not exist merely to demonstrate a product or programming language.

Prefer:

```text
Can a completion signal update event state and preserve a useful record?
```

over:

```text
Can we build something with Google Forms?
```

The design question should describe the work or system behavior before selecting the implementation.

---

## Scope

Each example should represent a reasonably bounded experiment.

An example may include:

* a human-facing interface;
* scripts or automation;
* sample data;
* diagrams;
* technical configuration;
* test instructions;
* design notes;
* observations;
* conclusions.

An example should not become an unbounded application containing unrelated experiments.

When one experiment begins testing a substantially different question, create another example rather than allowing the original folder to lose its purpose.

---

## Relationship to the rest of the repository

The repository separates experiment-owned work from shared resources, project-wide configuration, and general documentation.

```text
examples/                 Self-contained experiments and case studies
shared/                   Reusable technical resources used across examples
config/                   Repository-wide metadata, settings, and registries
docs/                     Project-wide lessons, methods, decisions, and findings
archive/                  Inactive material preserved for history or recovery
```

### Example-owned material

Keep material inside an example when it:

* is used only by that experiment;
* contains experiment-specific assumptions;
* exists to answer that experiment’s design question;
* has not demonstrated broader reuse;
* records observations or decisions unique to that experiment.

### Shared material

Move or extract material into `shared/` only when it meets the promotion rules established by the repository.

A resource should normally remain local until:

* a second real example needs it;
* it becomes a stable cross-project contract;
* or the project deliberately adopts it as a standard.

### Project-wide documentation

An experiment’s reasoning belongs in its own `design.md`.

A conclusion that applies across several experiments may later become:

```text
docs/findings/
docs/methods/
docs/decisions/
```

### Repository configuration

Repository-wide resource locations, status, access, and metadata belong in:

```text
config/
```

Example-specific data and configuration remain inside the example unless they are deliberately promoted.

---

## Naming convention

Example directory names should use:

* a two-digit sequence number;
* lowercase letters;
* hyphens between words;
* a short name describing the design question or workflow concept.

Recommended pattern:

```text
NN-descriptive-name/
```

Examples:

```text
01-task-app/
02-notification-test/
03-completion-signal/
04-interruption-recovery/
```

Avoid names based only on the selected technology.

Prefer:

```text
03-completion-signal/
```

over:

```text
03-google-form-test/
```

Prefer:

```text
04-event-history/
```

over:

```text
04-sheets-script/
```

Technology may change during the experiment. The design question should remain understandable.

---

## Sequence numbers

Sequence numbers identify the order in which examples were introduced.

They do not indicate importance or maturity.

Once assigned, a number should normally remain stable.

Do not renumber existing examples merely because another example was archived or removed.

Stable numbering helps preserve:

* links;
* references;
* documentation history;
* comparison between experiments;
* resource-registry entries.

---

## Example status

Each example should identify its current status near the top of its README.

Allowed experiment statuses are:

```text
planned
active
paused
complete
superseded
archived
```

These statuses apply to experiments.

They are related to, but not identical with, the lifecycle statuses used for resources in `config/resources.json`.

### `planned`

The experiment has been defined but meaningful implementation or testing has not begun.

A planned example may contain:

* its design question;
* its scope;
* placeholder files;
* an initial test plan.

It should not be described as operational.

### `active`

The experiment is currently being designed, built, or tested.

Its conclusions are not necessarily final.

### `paused`

Work has stopped temporarily, but the experiment may resume.

The README should explain:

* why it is paused;
* what remains;
* what would allow work to continue.

### `complete`

The experiment has answered its primary design question well enough to document conclusions.

Complete does not mean perfect, production-ready, or permanently finished.

A completed experiment may still contain limitations or unanswered secondary questions.

### `superseded`

Another example or approach has replaced this experiment’s active role.

The README should identify the replacement when possible.

A superseded example may remain in `examples/` when it is still useful for comparison or learning.

### `archived`

The experiment is no longer active and has been moved or designated for historical reference, recovery, or comparison.

Archived examples should follow the policy in `archive/README.md`.

---

## Minimum example package

A substantial example should normally contain:

```text
example-name/
├── README.md
├── design.md
├── index.html
├── assets/
└── data/
```

Not every experiment must use every file or folder.

However, `README.md` and `design.md` should normally exist.

### Required files

#### `README.md`

Explains the example from the user’s and inspector’s perspective.

It should answer:

* What is this experiment?
* Why does it exist?
* What question is it testing?
* What is its status?
* How can it be inspected or used?
* What is incomplete or limited?

#### `design.md`

Preserves the reasoning behind the experiment.

It should explain:

* the problem;
* the design question;
* scope;
* non-goals;
* roles;
* workflow;
* assumptions;
* data and state models;
* test plan;
* observations;
* decisions;
* conclusions;
* open questions.

### Optional files and folders

#### `index.html`

A static interface, demonstration page, or public entry point for the example.

#### `assets/`

Images, diagrams, screenshots, icons, and local styles used only by the example.

#### `data/`

Sample records, task definitions, fixtures, event data, and other structured information owned by the experiment.

#### Additional source files

An example may contain:

* JavaScript;
* Apps Script files;
* CSS;
* JSON;
* Python;
* shell scripts;
* configuration examples;
* exported safe test results.

Additional files should have clear responsibilities and should not duplicate material without explanation.

---

## Recommended example structure

```text
examples/
├── README.md
│
├── 01-task-app/
│   ├── README.md
│   ├── design.md
│   ├── index.html
│   ├── assets/
│   │   └── README.md
│   └── data/
│       └── README.md
│
├── 02-notification-test/
│   ├── README.md
│   ├── design.md
│   └── ...
│
└── 03-completion-signal/
    ├── README.md
    ├── design.md
    └── ...
```

Do not create empty examples merely to reserve names or numbers unless the planned experiment has at least:

* a defined purpose;
* a design question;
* an initial scope;
* a status.

---

## Example lifecycle

Each experiment should move through a deliberate lifecycle.

### 1. Describe the real problem

State what the human is trying to accomplish in the physical world.

Avoid starting with a product name.

Example:

```text
A person needs to receive a work event, follow instructions, and report completion.
```

Not:

```text
We need a Google Form and Apps Script project.
```

### 2. Define the design question

Write one or two questions the experiment should answer.

Examples:

* Can a form submission create a distinct event instance?
* Can a watch-visible notification direct a person to a procedure?
* Can a completion signal update current state and preserve history?
* Can progress survive interruption?
* What information must cross between components?

### 3. Define scope and non-goals

State what the experiment will test.

Also state what it will not attempt.

This prevents a small experiment from turning into an uncontrolled application build.

### 4. Identify the parts

Describe:

* the human role;
* the physical-world role;
* the digital-system role;
* interfaces;
* triggers;
* events;
* task definitions;
* task instances;
* references;
* signals;
* state;
* history;
* records.

### 5. Assign responsibilities

Explain what each part should do and what it should not do.

Example:

```text
The notification tells the human that work exists.
The procedure page explains how to perform the work.
The event record stores status and history.
```

### 6. Build the smallest useful test

Implement only enough to answer the current design question.

Avoid adding unrelated features merely because they may eventually be useful.

### 7. Test deliberately

Use fast and visible test triggers where practical.

Do not wait for a daily or weekly production schedule when a button or form submission can answer the same technical question immediately.

### 8. Record observations

Document what actually happened.

Include:

* successful behavior;
* failures;
* confusion;
* human effort;
* interruptions;
* duplicate events;
* missing information;
* unnecessary complexity;
* unexpected dependencies.

### 9. Draw conclusions

State:

* what was learned;
* which assumptions were confirmed;
* which assumptions were rejected;
* what remains unknown;
* whether the design question was answered;
* whether another experiment is needed.

### 10. Complete, continue, pause, or supersede

Assign the experiment’s next status deliberately.

Do not leave the experiment’s condition ambiguous.

### 11. Promote reusable material

Move or extract reusable technical resources into `shared/` only after they meet the promotion criteria.

### 12. Preserve or archive

Keep completed examples in `examples/` while they remain useful and current enough for study.

Move inactive material into `archive/` when it no longer belongs in the active experiment collection but still has historical or recovery value.

---

## Design question standard

Every example should have a clear design question.

A strong design question:

* describes observable system behavior;
* can be tested;
* is small enough for one experiment;
* does not assume the final implementation;
* produces a useful conclusion.

Strong:

```text
Can the human send one completion signal without the digital system tracking every checklist step?
```

Weak:

```text
Can we make an app?
```

Strong:

```text
What information must be stored to distinguish current state from permanent history?
```

Weak:

```text
How should everything work?
```

---

## Documentation requirements

Every substantial example should preserve enough context for another person—or the future project owner—to understand what happened.

### Example README

The example README should normally include:

```text
Title
Status
Purpose
Design question
What the example demonstrates
Current workflow
How to use or inspect it
Files in this example
Known limitations
Current test state
Related resources
Next step
```

### Design document

The design document should normally include:

```text
Problem statement
Design question
Scope
Non-goals
Human role
Physical-world role
Digital-system role
Workflow
Components and responsibilities
Event model
Task-definition model
State model
Completion signal
Record model
Failure cases
Known
Assumed
Unknown
Test plan
Observations
Decisions
Conclusions
Open questions
```

### Known, assumed, and unknown

The design document should distinguish:

#### Known

Things established conceptually or through testing.

#### Assumed

Things temporarily accepted so testing can proceed.

#### Unknown

Things the experiment is intended to discover.

This prevents untested assumptions from becoming accidental architecture.

---

## Current state and history

Experiments involving events should distinguish current state from permanent history.

Current state answers:

```text
What does the system currently believe?
```

History answers:

```text
What happened, and when?
```

An example should avoid storing both concepts in one ambiguous field or document without explanation.

Possible current state:

```text
status: active
completionSignalReceived: false
```

Possible history:

```text
08:14 — event created
08:15 — notification sent
08:29 — completion signal received
```

---

## Data ownership

Data inside an example belongs to that experiment unless deliberately promoted.

Example-specific data may include:

* sample task definitions;
* event fixtures;
* test records;
* mock form submissions;
* sample history;
* experiment configuration;
* exported public-safe results.

Reusable schemas belong in:

```text
shared/schemas/
```

Repository resource metadata belongs in:

```text
config/resources.json
```

Actual experiment records belong in:

```text
examples/<example>/data/
```

---

## Privacy and public-repository rules

This repository is public.

Examples must not contain:

* passwords;
* API keys;
* access tokens;
* private keys;
* private form responses;
* real workplace records;
* employee or client information;
* personal identifying information;
* secret-bearing URLs;
* private email addresses;
* restricted operational data;
* embedded credentials.

Committed example data should be:

* fictional;
* anonymized;
* or deliberately safe for public viewing.

Screenshots should be checked for:

* names;
* email addresses;
* document IDs;
* workplace information;
* account details;
* private URLs;
* hidden metadata.

---

## Failure and interruption

Examples should test normal failure and interruption where relevant.

Possible cases include:

* a notification is missed;
* a device sleeps;
* the human changes applications;
* work is paused;
* a form is abandoned;
* connectivity is lost;
* a signal is submitted twice;
* an event remains incomplete;
* a resource becomes unavailable;
* state and history disagree;
* the human cannot determine the next action.

An experiment should not be considered successful only because it works under ideal conditions.

---

## Completion criteria

An experiment may be marked `complete` when:

* its primary design question has been answered;
* the test method is documented;
* observations are preserved;
* important limitations are stated;
* conclusions are written;
* unresolved questions are identified;
* files are understandable;
* sensitive information has been removed;
* the README reflects the final experiment state.

Complete does not require:

* production deployment;
* perfect interface design;
* every possible feature;
* every secondary question to be answered;
* permanent architectural adoption.

---

## Pause criteria

An experiment may be marked `paused` when:

* required access is unavailable;
* testing equipment is unavailable;
* another dependency must be resolved first;
* the design question needs revision;
* the experiment is temporarily lower priority;
* implementation is blocked.

A paused experiment should state:

* why it is paused;
* the last confirmed state;
* what remains;
* the condition for resuming.

---

## Superseding an example

Mark an example `superseded` when another experiment or design now performs its active role better.

The superseded example should identify:

* its replacement;
* the reason for replacement;
* findings that remain useful;
* differences between the old and new approach;
* whether any consumers still depend on it.

Do not erase the older experiment merely because a better one exists.

Its value may include showing:

* what failed;
* why the design changed;
* which assumptions were incorrect;
* how the replacement improved the system.

---

## Archiving criteria

Move an example into `archive/` when:

* it is no longer active;
* it no longer belongs in the current examples collection;
* it has historical, comparison, or recovery value;
* it has been replaced and no active consumer depends on its current path;
* its lessons remain useful despite obsolete implementation.

Do not archive an example merely because it is complete.

A complete experiment may remain active reference material.

Archived examples should identify:

* original path;
* archive date;
* reason archived;
* replacement, if any;
* reusable findings;
* whether recovery is expected.

---

## Promoting reusable material

Reusable material should be promoted according to `shared/README.md`.

The normal rule is:

> Keep a resource inside its original example until a second real example needs it or the project deliberately adopts it as a repository standard.

Potential reuse is not enough.

### Promotion candidates

Possible candidates include:

* a common event schema;
* shared CSS;
* reusable date formatting;
* a standard status component;
* a common navigation fragment;
* a reusable validation utility;
* a design-document template.

### Promotion process

Before promotion:

1. identify consumers;
2. define the stable responsibility;
3. remove example-specific assumptions;
4. document dependencies;
5. document inputs and outputs;
6. update example references;
7. remove silent duplicates;
8. register the resource if it is significant at repository level.

---

## Experiment dependencies

An example may depend on:

* shared technical resources;
* public repository documents;
* registered external resources;
* public-safe sample data;
* clearly documented services.

Dependencies should be explicit.

The example README or design document should identify:

* dependency name;
* location;
* purpose;
* access requirement;
* failure effect;
* whether it is required or optional.

Avoid hidden dependencies such as:

* private files known only to the author;
* undocumented spreadsheet IDs;
* personal device settings;
* unexplained account permissions;
* local files outside the repository.

---

## Resource registry relationship

Important examples and external resources may be represented in:

```text
config/resources.json
```

The registry may describe:

* the example entry page;
* an external test form;
* a private event sheet;
* a shared schema;
* a public documentation page.

The registry should describe and locate the resource.

It should not duplicate:

* implementation code;
* event data;
* design documents;
* schema contents;
* test observations.

A planned example should not be represented as active merely because its folder exists.

---

## Naming files inside examples

Use clear, descriptive filenames.

Prefer:

```text
task-definitions.json
sample-events.json
completion-state-diagram.svg
event-handler.js
test-plan.md
```

Avoid:

```text
file1.json
new.js
final-final.html
copy.md
data2.json
```

File names should describe responsibility rather than editing history.

---

## Updating an example

When changing an active example:

1. identify the design question affected;
2. determine whether the change remains inside the experiment’s scope;
3. update the design document when assumptions or responsibilities change;
4. update test data when the data model changes;
5. record meaningful observations;
6. review privacy and security;
7. update status when necessary;
8. update resource-registry records if locations or lifecycle change;
9. review whether any material now qualifies for promotion.

---

## Change history

Not every small edit requires a formal changelog.

Record a meaningful change when it affects:

* the design question;
* scope;
* workflow;
* component responsibilities;
* state model;
* schema;
* interface contract;
* dependencies;
* conclusions;
* status;
* replacement relationship.

Meaningful changes may be documented in:

* `design.md`;
* an example changelog;
* Git commit history;
* a decision record;
* the resource registry.

---

## Current contents

```text
examples/
├── README.md
│
└── 01-task-app/
    ├── README.md
    ├── design.md
    ├── index.html
    │
    ├── assets/
    │   └── README.md
    │
    └── data/
        └── README.md
```

The first example is currently a prepared sandbox structure.

Its README, design document, interface, data policy, and asset policy are developed in later steps of the repository plan.

---

## Design principle

An example should preserve an answerable question, a testable system, and an inspectable record of what was learned.

A strong example:

* begins with the work rather than the software;
* has a bounded design question;
* separates the human, physical world, and digital system;
* identifies responsibilities;
* preserves assumptions and observations;
* distinguishes state from history;
* anticipates interruption and failure;
* protects private information;
* promotes only proven reusable material;
* concludes deliberately.

The goal is not to produce the largest or most polished application.

The goal is to learn something reliable about how a human-centered system should work.
