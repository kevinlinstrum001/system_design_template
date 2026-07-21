# System Design Template Development Plan

The upgraded root `README.md` acts as the project charter. Subordinate files should be revised so they agree with its terminology, folder boundaries, security rules, lifecycle concepts, and development method.

The work should proceed in dependency order. A governing file should be completed before the files it governs are revised.

---

# Step 1 — Upgrade `config/README.md`

This step should be completed first because `config/README.md` governs `resources.json`. The resource registry should not be redesigned until its scope, fields, security rules, and lifecycle vocabulary have been established.

## Recommended fixes

Add sections covering:

* the exact scope of `config/`;
* what belongs there;
* what does not belong there;
* the distinction between `config/`, `shared/`, and example-specific `data/`;
* the purpose of `resources.json`;
* resource field definitions;
* security restrictions;
* formatting expectations;
* maintenance rules;
* lifecycle rules for planned, active, inactive, replaced, and archived resources.

## Key repository boundary

```text
config/                  Repository-wide settings, metadata, and registries
shared/                  Reusable technical definitions, schemas, and components
examples/<example>/data/ Data belonging to one experiment
```

## Controlled resource statuses

Use:

```text
planned
active
inactive
replaced
archived
```

Avoid loosely interchangeable values such as:

```text
old
unused
finished
deprecated
dead
temporary
```

unless the controlled vocabulary is deliberately revised and documented.

## Completion condition

Step 1 is complete when `config/README.md` clearly defines:

* the folder’s repository-level scope;
* its relationship to `shared/` and example data;
* the structure and purpose of `resources.json`;
* allowed resource statuses;
* public-repository security rules;
* JSON formatting and maintenance expectations.

---

# Step 2 — Repair and formalize `config/resources.json`

Once the configuration policy is established, update the resource registry so it follows that policy.

## Problems to correct

The original registry contains illustrative URLs such as:

```text
EXAMPLE
example.com
```

These should not be marked as active resources.

Placeholder resources should be:

* removed until they exist;
* represented without a misleading location;
* or marked `planned`.

An entry marked `active` should point to a real, verified, public-safe location.

## Recommended top-level structure

```json
{
  "schemaVersion": "1.0",
  "project": {
    "id": "system-design-template",
    "name": "System Design Template",
    "repository": "https://github.com/kevinlinstrum001/system_design_template",
    "site": null
  },
  "resources": []
}
```

## Recommended resource structure

```json
{
  "id": "system-design-overview",
  "name": "System Design Overview",
  "type": "repository-document",
  "location": {
    "kind": "repository-path",
    "path": "overview.md"
  },
  "purpose": "Initial vocabulary, principles, and system-design lesson",
  "status": "active",
  "access": "public",
  "scope": "repository",
  "tags": [
    "documentation",
    "system-design"
  ],
  "replacedBy": null,
  "notes": ""
}
```

Using a `location` object is clearer than allowing some records to use `url` and others to use `path` without identifying the location type.

## Required resource fields

Every registered resource should have:

* a stable unique `id`;
* a readable `name`;
* a defined `type`;
* one primary `location`, or `null` for a planned resource;
* a clear `purpose`;
* a controlled `status`;
* an `access` classification;
* a `scope`;
* a tag list;
* a `replacedBy` value;
* a notes field.

## Security rules

Do not include:

* credentials;
* API keys;
* login tokens;
* OAuth secrets;
* private form responses;
* personally identifying operational data;
* real workplace records;
* sensitive employee or client information;
* URLs whose possession grants access.

## Completion condition

Step 2 is complete when:

* the JSON validates;
* placeholder active URLs are removed;
* repository resources are represented accurately;
* planned resources are clearly marked;
* all records follow the field definitions from `config/README.md`;
* the registry contains no secret or sensitive information.

---

# Change Record — Step 3 Revision

## Why Step 3 changed

The original Step 3 was written before the configuration policy and resource registry had been formalized.

Steps 1 and 2 established several repository-wide rules that now directly affect how `shared/README.md` should be designed.

The original Step 3 remains conceptually correct, but it must now incorporate those established rules rather than treating them as unresolved suggestions.

## What Steps 1 and 2 established

### Authoritative folder boundary

The repository now formally separates:

```text
config/                  Repository-wide settings, metadata, and registries
shared/                  Reusable technical definitions, schemas, and components
examples/<example>/data/ Data belonging to one experiment
```

Step 3 should adopt this boundary as an existing repository rule.

It should not redefine the boundary differently.

### Resource registry relationship

`config/resources.json` can register important resources located elsewhere in the repository.

This means a reusable file may physically exist in:

```text
shared/
```

while a registry record describing that file may exist in:

```text
config/resources.json
```

The registry describes and locates the resource. It does not contain or duplicate the resource itself.

### Controlled lifecycle vocabulary

The resource registry now uses:

```text
planned
active
inactive
replaced
archived
```

Significant shared resources may use compatible lifecycle language when they are documented or registered.

Status and version must remain separate concepts:

* status describes whether the resource is currently used;
* version identifies its structural or behavioral form.

### Public-repository security boundary

The configuration policy establishes that repository files must not contain:

* credentials;
* private records;
* sensitive operational data;
* secret-bearing URLs;
* embedded private configuration.

The shared policy should inherit this rule in a concise local form.

### Configuration versus configuration patterns

The original shared README listed “shared configuration patterns,” which is potentially ambiguous.

The revised rule is:

* actual repository-wide configuration values belong in `config/`;
* reusable configuration schemas, templates, or examples may belong in `shared/`;
* experiment-specific configuration belongs with the experiment.

## What will be done differently in Step 3

The updated Step 3 will:

1. Treat the config/shared/data boundary as authoritative.
2. Explain how shared resources relate to `config/resources.json`.
3. Distinguish actual configuration values from reusable configuration templates and schemas.
4. Add lifecycle guidance compatible with the resource registry.
5. Separate status from versioning.
6. Add concise public-repository security rules.
7. Define a documented promotion process rather than only a promotion principle.
8. Define dependency and consumer expectations for shared resources.
9. Clarify that the actual reusable file belongs in `shared/`, while its registry description may belong in `config/resources.json`.

## What does not change

The central promotion rule remains:

> Keep a component inside its original example until a second real example needs it or the component has been deliberately adopted as a repository standard.

The purpose of `shared/` also remains unchanged:

> Preserve genuinely reusable technical material without creating premature abstraction or unnecessary dependency.

---

# Step 3 — Upgrade `shared/README.md`

The current README correctly describes reusable code, schemas, styles, helpers, utilities, templates, and components. It does not yet define the operational rules that determine when material belongs there or how shared resources should be maintained.

## Required sections

The upgraded README should include:

```text
# Shared

Purpose
Scope
Repository boundary
What belongs here
What does not belong here
Promotion criteria
Promotion process
Suggested future structure
Dependency rules
Documentation requirements
Schema rules
Versioning and lifecycle
Relationship to config/resources.json
Security rules
Naming and formatting
Maintenance rules
Current contents
Design principle
```

## Repository boundary

The README should enforce:

```text
config/                  Repository-wide values, metadata, and registries
shared/                  Reusable technical resources
examples/<example>/data/ Records and data belonging to one experiment
```

Examples:

* a repository resource URL belongs in `config/`;
* a reusable event schema belongs in `shared/schemas/`;
* an actual event record belongs in an example’s `data/`;
* a reusable CSS file belongs in `shared/css/`;
* CSS used only by one experiment remains inside that experiment.

## What belongs in `shared/`

Possible contents include:

* shared CSS;
* shared JavaScript;
* reusable HTML fragments;
* common JSON schemas;
* helper functions;
* interface components;
* utility scripts;
* reusable templates;
* reusable configuration schemas;
* reusable configuration examples;
* technical conventions adopted by multiple examples.

## What does not belong in `shared/`

Do not place the following in `shared/`:

* repository-wide resource locations;
* live configuration values that belong in `config/`;
* actual event history;
* real operational records;
* data belonging to one example;
* components used by only one experiment without an adoption decision;
* credentials or secrets;
* duplicated copies of example files;
* speculative utilities with no real consumer;
* obsolete files retained only for history.

## Promotion criteria

A resource should normally remain inside its original example until one of the following is true:

1. A second real example needs it.
2. The project deliberately adopts it as a repository standard.
3. It represents a stable cross-project contract, such as a shared schema.
4. Moving it removes real duplication without creating excessive dependency.
5. Its responsibility can be explained independently of the original example.

Potential future reuse is not enough.

## Promotion process

When promoting a resource:

1. Identify the original example.
2. Identify the current or intended consumers.
3. Define the resource’s stable responsibility.
4. Remove example-specific assumptions.
5. Define its inputs, outputs, dependencies, and limitations.
6. Move or extract the reusable portion into `shared/`.
7. Update affected example references.
8. Document the shared resource.
9. Register it in `config/resources.json` when it is significant at repository level.
10. Avoid maintaining silent duplicate copies.

## Suggested future structure

Do not create these directories until they are needed.

```text
shared/
├── css/
├── js/
├── components/
├── schemas/
├── templates/
├── utilities/
└── README.md
```

## Dependency rules

Shared resources should minimize hidden dependencies.

Each significant resource should make clear:

* what it depends on;
* which examples use it;
* whether it can be used independently;
* whether it changes a shared contract;
* whether removing it would break existing examples.

An example may depend on `shared/`.

A shared resource should not depend on one example’s private structure or data.

Avoid circular dependencies such as:

```text
example → shared → same example
```

## Documentation requirements

A significant shared resource should explain:

* purpose;
* intended consumers;
* inputs;
* outputs;
* dependencies;
* usage;
* limitations;
* version;
* status;
* migration notes when replaced.

Small files may document this in comments or nearby Markdown. Larger shared resources may need their own README.

## Schema rules

Reusable schemas should live under:

```text
shared/schemas/
```

Each schema should define:

* the data structure it validates;
* required and optional fields;
* field meanings;
* allowed values;
* identifier rules;
* version;
* compatibility expectations;
* examples;
* migration requirements after breaking changes.

Actual event records should not be stored with the schema.

## Versioning and lifecycle

Version and status are different.

Example:

```text
Resource: event.schema.json
Version: 1.0
Status: active
```

Use lifecycle terms compatible with the repository registry:

```text
planned
active
inactive
replaced
archived
```

Increase a version when the shared contract changes meaningfully.

Do not increase a version for:

* whitespace changes;
* spelling corrections;
* comments;
* formatting;
* documentation-only edits.

A breaking structural change should normally require:

* a new version;
* migration guidance;
* consumer review;
* updated examples;
* a replacement relationship where appropriate.

## Relationship to `config/resources.json`

The actual reusable file belongs in `shared/`.

A significant shared file may also have a descriptive registry record in:

```text
config/resources.json
```

Example:

```text
shared/schemas/event.schema.json
```

contains the schema.

A resource record may point to it using:

```json
{
  "location": {
    "kind": "repository-path",
    "path": "shared/schemas/event.schema.json"
  }
}
```

The registry should not duplicate the schema contents.

## Security rules

Do not place the following in shared resources:

* passwords;
* tokens;
* API keys;
* private URLs;
* private form responses;
* employee or client records;
* personal data;
* restricted operational information;
* embedded credentials;
* real production secrets.

Reusable examples should use fictional, anonymized, or deliberately public-safe data.

## Completion condition

Step 3 is complete when `shared/README.md` clearly defines:

* the authoritative folder boundary;
* promotion criteria;
* promotion procedure;
* dependency rules;
* documentation expectations;
* schema rules;
* lifecycle and versioning;
* registry relationship;
* security rules;
* current and possible future structure.

---

# Step 4 — Upgrade `examples/README.md`

The current file already states the strongest central rule: each example should preserve both the working system and the reasoning that produced it, and each should answer a clear design question.

It should now become the operating standard for all experiments.

## Recommended fixes

Add:

* example naming conventions;
* required and optional files;
* experiment status values;
* the experiment lifecycle;
* minimum documentation requirements;
* completion criteria;
* archiving criteria;
* rules for promoting reusable material into `shared/`.

## Recommended naming convention

```text
01-task-app/
02-notification-test/
03-completion-signal/
```

Use:

* a two-digit sequence;
* lowercase words;
* hyphens;
* a name describing the design question rather than the selected technology.

Prefer:

```text
02-completion-signal/
```

over:

```text
02-google-form-test/
```

because the project should describe the work before choosing the software.

## Recommended experiment statuses

```text
planned
active
paused
complete
superseded
archived
```

These statuses apply to experiments.

They are related to, but not identical with, the resource statuses used in `config/resources.json`.

## Minimum example package

```text
example-name/
├── README.md
├── design.md
├── index.html
├── assets/
└── data/
```

Not every experiment must use every file or folder, but `README.md` and `design.md` should normally exist.

## Completion condition

Step 4 is complete when `examples/README.md` defines:

* how examples are named;
* what files they should contain;
* how their status is recorded;
* how experiments begin and end;
* how reusable material is promoted;
* when an example remains active, becomes complete, or moves to the archive.

---

# Step 5 — Build `examples/01-task-app/README.md`

This file should describe the example from the user’s and inspector’s perspective.

## Recommended sections

```text
# Task App

Status
Purpose
Design question
What the example demonstrates
Current workflow
How to use it
Files in this example
Known limitations
Current test state
Related resources
Next experiment
```

## Important distinction

The example README should explain:

* what the experiment is;
* what it demonstrates;
* how to inspect or use it;
* its current condition.

It should not contain all design reasoning. Detailed reasoning belongs in `design.md`.

## Completion condition

Step 5 is complete when a reader can understand:

* why the example exists;
* what question it tests;
* what files are involved;
* whether it currently works;
* what remains incomplete.

---

# Step 6 — Build `examples/01-task-app/design.md`

This file should become the engineering and reasoning record for the first experiment.

## Recommended sections

```text
# Task App Design

## Problem statement
## Design question
## Scope
## Non-goals
## Human role
## Physical-world role
## Digital-system role
## Workflow
## Components and responsibilities
## Event model
## Task-definition model
## State model
## Completion signal
## Record model
## Failure cases
## Known
## Assumed
## Unknown
## Test plan
## Observations
## Decisions
## Conclusions
## Open questions
```

## Known, assumed, and unknown

### Known

Things established conceptually or through testing.

### Assumed

Things temporarily accepted so the experiment can proceed.

### Unknown

Things the experiment is intended to discover.

This distinction prevents an untested idea from becoming accidental architecture.

## Completion condition

Step 6 is complete when the experiment’s reasoning can be inspected separately from its interface and implementation.

---

# Step 7 — Upgrade `examples/01-task-app/data/README.md`

Clarify that this directory contains data used only by `01-task-app`.

## Recommended fixes

Add:

* what belongs here;
* what belongs in `shared/schemas/`;
* sample versus live data;
* naming rules;
* privacy rules;
* whether generated data may be committed;
* how test records should be reset;
* the distinction between definitions, current state, and history.

## Suggested structure when needed

```text
data/
├── task-definitions.json
├── sample-events.json
├── sample-history.json
├── fixtures/
└── README.md
```

## Strong rule

Do not commit:

* real workplace records;
* names;
* private form responses;
* credentials;
* sensitive operational data.

Committed examples should be:

* fictional;
* anonymized;
* or deliberately safe for public viewing.

## Completion condition

Step 7 is complete when the folder’s ownership, data categories, privacy rules, and relationship to shared schemas are unambiguous.

---

# Step 8 — Upgrade `examples/01-task-app/assets/README.md`

The local assets README should distinguish example-specific media from repository-wide media.

## Recommended rules

Use this folder for:

* screenshots of this experiment;
* icons used only by this interface;
* experiment-specific diagrams;
* local styles not yet promoted to `shared/`;
* images used only by this example.

Move an asset to root `assets/` only when it is genuinely used across the repository.

Move a reusable style or interface resource to `shared/` only when it meets the promotion criteria established in Step 3.

## Naming guidance

Prefer:

```text
task-app-workflow.svg
task-app-mobile-view.png
completion-state-diagram.svg
```

Avoid:

```text
image1.png
diagram-new-final.png
screenshot2.png
```

## Completion condition

Step 8 is complete when local assets can be distinguished clearly from repository-wide assets and reusable technical resources.

---

# Step 9 — Upgrade root `assets/README.md`

The current file correctly establishes that root assets are shared across the repository and example-specific assets stay inside the relevant example.

It needs additional operating rules.

## Recommended additions

Add:

* file naming conventions;
* preferred formats;
* source attribution;
* generated versus original artwork;
* accessibility requirements;
* editable-source retention guidance;
* promotion rules from local assets;
* restrictions on sensitive screenshots.

## Recommended format guidance

```text
SVG   diagrams, icons, interface illustrations
PNG   screenshots and graphics requiring raster output
JPG   photographs
WEBP  optimized web imagery where supported
```

## Accessibility rule

Images used in HTML documentation should have:

* meaningful `alt` text when informative;
* empty `alt=""` when decorative;
* readable labels;
* adequate contrast;
* captions where context is not otherwise clear.

## Completion condition

Step 9 is complete when shared visual assets have clear ownership, naming, format, attribution, privacy, and accessibility rules.

---

# Step 10 — Upgrade `docs/README.md`

The current file correctly defines `docs/` as the repository-wide location for lessons, principles, vocabulary, architecture notes, methods, decision records, and cross-example findings.

It should now establish documentation categories.

## Suggested future organization

Create these folders only when material exists:

```text
docs/
├── lessons/
├── vocabulary/
├── methods/
├── decisions/
├── diagrams/
├── findings/
└── README.md
```

## Recommended fixes

Define the difference between:

* a lesson;
* a design method;
* a decision record;
* an experiment-specific design document;
* a cross-project finding;
* a reference document.

## Important boundary

```text
examples/01-task-app/design.md
```

explains one experiment.

```text
docs/findings/completion-signals.md
```

would explain a reusable conclusion drawn from one or more experiments.

## Decision records

A lightweight decision-record convention may use:

```text
docs/decisions/
├── 0001-separate-human-and-system-state.md
├── 0002-reference-procedures.md
└── README.md
```

Decision records should preserve durable project-level decisions, not every temporary experiment choice.

## Completion condition

Step 10 is complete when documentation types, ownership, naming, and promotion from experiment findings are clearly defined.

---

# Step 11 — Decide the future of `overview.md`

The root README describes `overview.md` as the initial long-form lesson and conceptual foundation.

The file does not need an immediate full rewrite, but it needs a declared lifecycle.

## Near-term action

Add a short status header:

```markdown
> **Document status:** Active foundation draft  
> This document contains the original long-form conceptual overview.  
> Material may later be reorganized into formal lessons under `docs/`.
```

## Later options

After formal lessons exist:

1. Keep `overview.md` as the original foundation document.
2. Replace it with a shorter orientation page linking to lessons.
3. Move the original into `archive/documents/`.
4. Rename it to `foundation-overview.md`.

Do not move or rename it yet because the root README and resource registry currently reference it.

## Completion condition

Step 11 is complete when the document’s present status and future lifecycle are explicit.

---

# Step 12 — Upgrade `archive/README.md`

The current archive README correctly explains the purpose of preserving inactive but valuable material.

It needs lifecycle and labeling rules.

## Recommended additions

Require archived material to identify:

* original path;
* archive date;
* reason archived;
* replacement, if any;
* whether recovery is expected;
* whether the item may eventually be deleted;
* reusable findings.

## Suggested archive note

```markdown
# Archive Note

- Original path: `examples/01-old-task-app/`
- Archived: 2026-07-21
- Reason: Replaced by event-based task experiment
- Replacement: `examples/02-event-task-app/`
- Reusable findings: Notification test and completion-state model
```

## Important rule

The archive must not become an undifferentiated storage dump.

Archived content should remain understandable enough to support:

* comparison;
* historical interpretation;
* recovery;
* study of failed approaches.

## Completion condition

Step 12 is complete when archived material has a documented reason, origin, lifecycle, and replacement relationship where applicable.

---

# Step 13 — Build the root `index.html`

The upgraded root README defines this page as the static entrance to project orientation, lessons, vocabulary, examples, diagrams, and current experiments.

It should be built after the README hierarchy is settled.

## Initial version should include

* project title and purpose;
* three-domain overview;
* current project status;
* link to `README.md`;
* link to `overview.md`;
* examples section;
* documentation section;
* resource/status note;
* GitHub repository link.

The first version should function as an index, not as the entire textbook.

## Completion condition

Step 13 is complete when a visitor can enter the project through one mobile-friendly page and navigate to its main active resources.

---

# Step 14 — Perform a repository consistency pass

After the preceding files are updated, inspect the entire repository for consistency.

## Verify terminology

Use the same terms throughout:

* `human`;
* `physical world`;
* `digital system`;
* `task definition`;
* `task instance`;
* `human working state`;
* `system state`;
* `completion signal`;
* `exception signal`;
* `record`;
* `reference`;
* `transport`;
* `loose coupling`.

## Verify folder boundaries

Check agreement on:

* root versus example assets;
* config versus shared resources;
* config versus example data;
* experiment reasoning versus repository documentation;
* active versus archived material;
* local versus shared components;
* actual resources versus registry descriptions.

## Verify structural accuracy

The root directory tree should match the actual repository.

Each folder README should distinguish:

* current contents;
* allowed future contents;
* files that are planned but do not yet exist.

## Verify registry accuracy

Check that:

* all repository paths exist;
* planned resources are not marked active;
* active resources have valid locations;
* replaced resources identify replacements;
* no secret or sensitive data is present;
* significant shared resources are registered when appropriate.

## Verify links

Check:

* repository-relative Markdown links;
* HTML navigation;
* paths in `resources.json`;
* links to examples;
* links to documentation;
* GitHub Pages paths.

## Completion condition

Step 14 is complete when the repository’s structure, terminology, links, status fields, documentation boundaries, and resource registry agree.

---

# Step 15 — Update the root README if the implementation changed the structure

The root README should be reviewed after the repository updates are complete.

Update it only when the completed work changed:

* the actual directory structure;
* repository-wide terminology;
* lifecycle conventions;
* experiment structure;
* navigation;
* project status;
* important governing principles.

The root README should remain the project charter rather than becoming a detailed copy of every subordinate README.

---

# Recommended Working Sequence

## Batch 1 — Repository control layer

1. Upgrade `config/README.md`.
2. Repair and formalize `config/resources.json`.

This establishes how the repository describes, locates, classifies, and protects important resources.

## Batch 2 — Experiment boundaries

3. Upgrade `shared/README.md`.
4. Upgrade `examples/README.md`.
5. Build `examples/01-task-app/README.md`.
6. Build `examples/01-task-app/design.md`.
7. Upgrade `examples/01-task-app/data/README.md`.
8. Upgrade `examples/01-task-app/assets/README.md`.

This establishes how experiments are created, documented, separated from shared resources, and promoted into reusable material.

## Batch 3 — Knowledge and media layer

9. Upgrade root `assets/README.md`.
10. Upgrade `docs/README.md`.
11. Add lifecycle status to `overview.md`.
12. Upgrade `archive/README.md`.

This establishes how knowledge, media, findings, decisions, and historical material are preserved.

## Batch 4 — Presentation and verification

13. Build root `index.html`.
14. Perform a full repository consistency pass.
15. Update the root README if implementation changed the project structure or policy.

---

# Current Progress

Completed:

* Step 1 — upgraded `config/README.md`;
* Step 2 — repaired and formalized `config/resources.json`;
* Step 3 review — identified changes required by Steps 1 and 2;
* development-plan revision — incorporated the Step 3 change record and revised implementation requirements.
* Step 4 - upgraded examples/README.md

Next:

* Step 5 - Build Examples/01-task-app/README.md
