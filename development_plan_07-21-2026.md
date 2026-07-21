The upgraded root README now acts as the project charter, so several subordinate files should be revised to agree with its terminology, boundaries, and development method. 

The updates should be done in the following order.

# Step 1 — Upgrade `config/README.md`

This should be first because it governs `resources.json`, and that file should not be edited until its rules are settled.

## Recommended fixes

Add sections covering:

* the exact scope of `config/`;
* what belongs there;
* what does not belong there;
* the distinction between `config/`, `shared/`, and example-specific `data/`;
* the purpose of `resources.json`;
* field definitions;
* security restrictions;
* formatting expectations;
* lifecycle rules for active, replaced, inactive, and archived resources.

The current file is accurate but only provides a broad folder description and a list of possible contents. 

## Key rule to establish

```text
config/                  Repository-wide settings and registries
shared/                  Reusable technical definitions and components
examples/<example>/data/ Data belonging to one experiment
```

## Recommended `resources.json` statuses

Use a small controlled vocabulary:

```text
planned
active
inactive
replaced
archived
```

Avoid loosely interchangeable values such as `old`, `unused`, `finished`, or `deprecated` unless they are formally defined.

---

# Step 2 — Repair and formalize `config/resources.json`

Once the config policy is established, update the registry itself.

## Current likely issues

The present registry contains illustrative URLs such as `EXAMPLE` and `example.com`. These should either:

* be clearly identified as templates;
* be replaced with actual resources;
* or be removed until the resources exist.

An entry marked `active` should not point to a placeholder URL.

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

Using a `location` object is cleaner than allowing some entries to use `url` and others to use `path` without an explicit distinction.

## Add validation rules

Every resource should have:

* a stable unique `id`;
* a readable `name`;
* a defined `type`;
* one location;
* a clear `purpose`;
* a controlled `status`;
* an access classification;
* a scope.

## Security fix

Do not include:

* credentials;
* API keys;
* login tokens;
* private form responses;
* personally identifying operational data;
* URLs whose possession grants access.

---

# Step 3 — Upgrade `shared/README.md`

The current README correctly describes reusable code, schemas, styles, helpers, and components, but it stops before defining the repository boundary.

## Recommended fixes

Add:

* criteria for promoting something into `shared/`;
* the distinction between actual reuse and hypothetical reuse;
* suggested subdirectories;
* dependency rules;
* documentation expectations;
* versioning expectations for schemas;
* the relationship between `shared/` and `config/`.

## Critical principle

A file should not enter `shared/` merely because it might someday be reusable.

A reasonable promotion rule is:

> Keep a component inside its original example until a second real example needs it or the component has been deliberately adopted as a repository standard.

## Suggested future structure

Do not create these until needed, but document them as allowed categories:

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

## Boundary to clarify

* a shared event schema belongs in `shared/schemas/`;
* repository resource locations belong in `config/`;
* actual test event records belong in an example’s `data/`.

---

# Step 4 — Upgrade `examples/README.md`

The current file already states the strongest central rule: each example should preserve both the working system and the reasoning that produced it, and each should answer a clear design question.

It should now be expanded into the operating standard for all experiments.

## Recommended fixes

Add:

* example naming conventions;
* required and optional files;
* experiment status values;
* the experiment lifecycle;
* minimum documentation requirements;
* criteria for completion;
* criteria for archiving;
* rules for moving reusable material into `shared/`.

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
* a name describing the design question rather than the technology.

Prefer:

```text
02-completion-signal/
```

over:

```text
02-google-form-test/
```

because the project is supposed to describe the work before selecting software.

## Recommended experiment statuses

```text
planned
active
paused
complete
superseded
archived
```

## Minimum example package

```text
example-name/
├── README.md
├── design.md
├── index.html
├── assets/
└── data/
```

Not every experiment must use every folder, but `README.md` and `design.md` should normally exist.

---

# Step 5 — Build `examples/01-task-app/README.md`

This file is currently empty, so it should be created after the general examples policy is settled.

It should describe the example from the user’s perspective.

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

The example README should explain **what the experiment is and how to inspect or use it**.

It should not contain all the design reasoning. That belongs in `design.md`.

---

# Step 6 — Build `examples/01-task-app/design.md`

This should become the engineering and reasoning record for the first experiment.

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
## Assumptions
## Test plan
## Observations
## Decisions
## Conclusions
## Open questions
```

## Important design rule

Separate these three categories explicitly:

### Known

Things established conceptually or through testing.

### Assumed

Things being temporarily accepted so testing can proceed.

### Unknown

Things the experiment is intended to discover.

That will help prevent an untested idea from becoming accidental architecture.

---

# Step 7 — Upgrade `examples/01-task-app/data/README.md`

The present file describes several possible data types but does not establish ownership or data rules.

## Recommended fixes

Clarify that this directory contains data used only by `01-task-app`.

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

Do not commit real workplace records, names, private form responses, credentials, or sensitive operational data.

All committed examples should be:

* fictional;
* anonymized;
* or deliberately safe for public viewing.

---

# Step 8 — Upgrade `examples/01-task-app/assets/README.md`

The local assets README should distinguish example-specific media from repository-wide assets.

## Recommended rules

Use this folder for:

* screenshots of this experiment;
* icons used only by this interface;
* experiment-specific diagrams;
* local styles, if styles are not yet shared;
* images used only by this example.

Move an asset to root `assets/` only when it is genuinely used across the repository.

Add naming guidance such as:

```text
task-app-workflow.svg
task-app-mobile-view.png
completion-state-diagram.svg
```

Avoid generic names such as:

```text
image1.png
diagram-new-final.png
screenshot2.png
```

---

# Step 9 — Upgrade root `assets/README.md`

The current file clearly establishes that root assets are shared across the repository and example-specific assets stay inside the example.

It needs a few operating rules.

## Recommended additions

* file naming conventions;
* preferred formats;
* source attribution;
* generated versus original artwork;
* accessibility requirements;
* whether editable source files should be retained;
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
* readable labels and contrast;
* captions where context is not otherwise clear.

---

# Step 10 — Upgrade `docs/README.md`

The current file correctly defines `docs/` as the repository-wide location for lessons, principles, vocabulary, architecture notes, methods, decision records, and cross-example findings.

It should now establish documentation categories.

## Suggested future organization

Only create folders as material appears:

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

A lightweight decision-record convention would be useful:

```text
docs/decisions/
├── 0001-separate-human-and-system-state.md
├── 0002-reference-procedures.md
└── README.md
```

These should record durable project-level decisions, not every temporary choice.

---

# Step 11 — Decide the future of `overview.md`

The root README describes `overview.md` as the initial long-form lesson and conceptual foundation, while noting that its material may later move into `docs/`. 

The file does not need an immediate rewrite, but it does need a declared lifecycle.

## Recommended near-term action

Add a short status header at the top:

```markdown
> **Document status:** Active foundation draft  
> This document contains the original long-form conceptual overview.  
> Material may later be reorganized into formal lessons under `docs/`.
```

## Later options

After formal lessons exist:

1. keep `overview.md` as the original foundation document;
2. replace it with a shorter orientation page linking to lessons;
3. move the original into `archive/documents/`;
4. rename it to something more explicit, such as `foundation-overview.md`.

Do not move or rename it yet because the root README and `resources.json` currently reference it.

---

# Step 12 — Upgrade `archive/README.md`

The current archive README correctly explains the purpose of preserving inactive but valuable material.

It needs lifecycle and labeling rules.

## Recommended additions

Require archived material to identify:

* original path;
* date archived;
* reason archived;
* replacement, if any;
* whether recovery is expected;
* whether the item is safe to delete later.

## Suggested archive note

Each archived directory could include a small metadata file:

```markdown
# Archive Note

- Original path: `examples/01-old-task-app/`
- Archived: 2026-07-21
- Reason: Replaced by event-based task experiment
- Replacement: `examples/02-event-task-app/`
- Reusable findings: Notification test and completion-state model
```

## Important rule

Archive should not become an undifferentiated storage dump.

Archived content must remain understandable enough to support comparison or recovery.

---

# Step 13 — Build the root `index.html`

The upgraded root README now gives this page a defined responsibility: become the static entrance to project orientation, lessons, vocabulary, examples, diagrams, and current experiments. 

It should be built only after the README hierarchy is settled, otherwise its navigation will be based on unfinished structure.

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

The first version should be an index, not the entire textbook.

---

# Step 14 — Perform a repository consistency pass

After the files above are updated, inspect the entire repository for consistency.

## Verify terminology

Use the same expressions throughout:

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

Check that each README agrees on:

* root versus example assets;
* config versus data;
* example reasoning versus repository documentation;
* active versus archived material;
* local versus shared components.

## Verify structural accuracy

The root directory tree should match the actual repository.

Each folder README should list its actual current contents separately from possible future contents.

## Verify links

Check:

* repository-relative Markdown links;
* HTML navigation;
* paths in `resources.json`;
* links to examples;
* links to documentation;
* eventual GitHub Pages paths.

---

# Recommended working sequence

We should make the updates in these practical batches:

## Batch 1 — Repository control layer

1. `config/README.md`
2. `config/resources.json`

This establishes how the repository references and identifies resources.

## Batch 2 — Experiment boundaries

3. `shared/README.md`
4. `examples/README.md`
5. `examples/01-task-app/README.md`
6. `examples/01-task-app/design.md`
7. `examples/01-task-app/data/README.md`
8. `examples/01-task-app/assets/README.md`

This establishes how experiments are created, documented, and separated from reusable material.

## Batch 3 — Knowledge and media layer

9. `assets/README.md`
10. `docs/README.md`
11. `overview.md`
12. `archive/README.md`

This establishes how knowledge, media, and historical material are preserved.

## Batch 4 — Presentation and verification

13. `index.html`
14. full consistency pass
15. update the root README directory tree if anything changed during the process

The best starting point is **Batch 1, beginning with a complete replacement for `config/README.md`**.
