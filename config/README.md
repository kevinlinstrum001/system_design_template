# Config

This folder contains repository-level configuration, registries, metadata, and non-secret references used across the **System Design Template** project.

Its purpose is to keep shared project information in one predictable, inspectable location.

The `config/` folder is not a general storage area for arbitrary JSON files. Material belongs here only when it describes the repository as a whole, applies across multiple examples, or identifies important shared resources.

---

## Scope

Use `config/` for information that applies to:

* the entire repository;
* multiple examples or experiments;
* repository-wide resource locations;
* shared project metadata;
* environment labels;
* feature settings used across the project;
* non-secret external service references;
* registries that help locate or describe important resources.

Configuration used by only one example should usually remain inside that example.

---

## Folder boundary

The repository separates configuration, reusable technical material, and experiment-specific data.

```text
config/                  Repository-wide settings, metadata, and registries
shared/                  Reusable technical definitions, schemas, and components
examples/<example>/data/ Data belonging to one experiment
```

### `config/`

Use for repository-wide descriptive or operational configuration.

Examples:

* resource registries;
* project metadata;
* external resource locations;
* shared environment names;
* repository-wide feature flags;
* shared lookup values;
* public configuration examples.

### `shared/`

Use for reusable technical material.

Examples:

* JSON schemas;
* reusable JavaScript;
* shared CSS;
* utility functions;
* HTML components;
* templates;
* technical conventions used by more than one example.

### `examples/<example>/data/`

Use for data owned by one experiment.

Examples:

* sample task definitions;
* test event records;
* mock submissions;
* experiment fixtures;
* local lookup tables;
* generated test output;
* example-specific configuration.

---

## What belongs here

Appropriate contents may include:

* external resource registries;
* repository metadata;
* project identifiers;
* environment labels;
* shared application settings;
* repository-wide lookup tables;
* public feature settings;
* configuration examples;
* non-secret connection information;
* paths to repository documents;
* references to external forms, sheets, documents, or services;
* status and access metadata for shared resources.

A file belongs in `config/` when another person should be able to inspect it and understand how the repository is organized or where an important shared resource is located.

---

## What does not belong here

Do not place the following in `config/`:

* passwords;
* API keys;
* access tokens;
* session cookies;
* login credentials;
* private keys;
* secrets of any kind;
* private form responses;
* real workplace records;
* personally identifying operational data;
* sensitive employee or client information;
* URLs that grant access merely by being known;
* large datasets;
* generated event history;
* example-specific test records;
* reusable source code;
* reusable schemas that belong in `shared/`;
* media files that belong in `assets/`;
* obsolete configuration retained only for history.

Sensitive or secret values should be stored outside the public repository using an appropriate private credential or environment-management system.

---

## Current contents

```text
config/
├── README.md       # Scope, rules, and maintenance policy for configuration
└── resources.json # Registry of important repository and external resources
```

Additional configuration files should be added only when a real repository-wide need exists.

Whenever a new file is added, update this README to explain:

* what the file controls or describes;
* who or what uses it;
* whether it is manually maintained;
* which values are permitted;
* whether it contains references to external systems.

---

## `resources.json`

`resources.json` is the central registry of important resources used by the project.

It may describe resources located:

* inside this repository;
* in Google Drive;
* in Google Sheets;
* in Google Forms;
* on GitHub Pages;
* on external websites;
* in other connected services.

The registry does not contain the resources themselves. It contains enough information to identify them, locate them, understand their purpose, and determine their current status.

This follows a central project principle:

> Reference stable information. Transport only the data that must cross between parts.

---

## Resource record requirements

Every resource record should contain the following information.

### `id`

A stable, unique machine-readable identifier.

Recommended format:

```text
lowercase-hyphenated-name
```

Example:

```text
system-design-overview
```

An `id` should not change merely because the readable name changes.

### `name`

A concise human-readable name.

Example:

```text
System Design Overview
```

### `type`

A controlled description of the resource category.

Possible values may include:

```text
repository-document
repository-page
google-sheet
google-form
google-document
google-calendar
web-application
external-web-page
external-pdf
image
dataset
service
```

Add new types deliberately and use them consistently.

### `location`

A structured description of where the resource can be found.

A repository resource may use:

```json
{
  "kind": "repository-path",
  "path": "overview.md"
}
```

An external resource may use:

```json
{
  "kind": "url",
  "url": "https://example.com/resource"
}
```

Each resource should have one primary location.

### `purpose`

A short explanation of why the resource exists and what responsibility it serves.

Avoid vague descriptions such as:

```text
Used by the project
```

Prefer descriptions such as:

```text
Stores event records and completion history for the task-workflow experiment
```

### `status`

A controlled lifecycle value.

Allowed values are:

```text
planned
active
inactive
replaced
archived
```

Definitions:

* `planned` — intended or reserved, but not yet available for use;
* `active` — current and expected to be usable;
* `inactive` — retained in the registry but not currently in use;
* `replaced` — superseded by another identified resource;
* `archived` — preserved only for historical reference or recovery.

Do not use loosely interchangeable values such as:

```text
old
unused
finished
deprecated
dead
temporary
```

unless the controlled vocabulary is formally revised.

### `access`

A description of the expected access level.

Recommended values:

```text
public
restricted
private
unknown
```

Definitions:

* `public` — accessible without special permission;
* `restricted` — accessible only to an approved group or authenticated user;
* `private` — accessible only to the owner or a very limited set of users;
* `unknown` — access has not yet been confirmed.

The access field describes expected access. It does not provide access control.

### `scope`

The area of the project that owns or uses the resource.

Recommended values:

```text
repository
shared
example
external-reference
```

An example-specific resource may also identify the example in a separate field such as:

```json
{
  "scope": "example",
  "exampleId": "01-task-app"
}
```

### `tags`

A list of short labels supporting organization and search.

Example:

```json
[
  "documentation",
  "system-design",
  "foundation"
]
```

Tags should be lowercase and hyphenated where necessary.

### `replacedBy`

The `id` of the resource that replaced this one.

Use `null` when the resource has not been replaced.

A resource marked `replaced` should normally identify its replacement.

### `notes`

Optional human-readable context.

Use this field for information that does not belong in the formal fields, such as:

* temporary limitations;
* maintenance reminders;
* migration details;
* unresolved access questions.

Do not place secrets or sensitive data in notes.

---

## Recommended resource record

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
    "system-design",
    "foundation"
  ],
  "replacedBy": null,
  "notes": ""
}
```

---

## Project metadata

`resources.json` may include a top-level project object.

Recommended structure:

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

### `schemaVersion`

Identifies the format used by the file.

Increase this value only when the structure changes in a way that may require existing readers or records to be updated.

### `project.id`

A stable machine-readable project identifier.

### `project.name`

The human-readable project name.

### `project.repository`

The canonical repository location.

### `project.site`

The public project site, when one exists.

Use `null` rather than an example or placeholder URL when the site has not yet been established.

---

## Placeholder policy

Do not mark a resource as `active` when its location is only a placeholder.

Example values such as:

```text
EXAMPLE
example.com
replace-me
temporary-url
```

must not appear in active records.

A resource that does not yet exist should either:

* be omitted until it exists; or
* be included with `status: "planned"` and no misleading location.

Example:

```json
{
  "id": "project-site",
  "name": "Project Website",
  "type": "repository-page",
  "location": null,
  "purpose": "Public entry point for project documentation and examples",
  "status": "planned",
  "access": "public",
  "scope": "repository",
  "tags": [
    "website"
  ],
  "replacedBy": null,
  "notes": "Location will be added after GitHub Pages is configured."
}
```

---

## Lifecycle rules

Resource records should reflect the current lifecycle of the resource.

### Planned

Use when the resource is intended but does not yet exist or is not ready.

A planned resource should not be described as operational.

### Active

Use only when:

* the resource exists;
* its location is valid;
* its purpose is current;
* its expected access has been verified;
* it is part of the working project.

### Inactive

Use when the resource still exists but is temporarily or indefinitely not used.

An inactive resource may later return to active status.

### Replaced

Use when another resource now performs the same responsibility.

A replaced record should normally include:

```json
{
  "status": "replaced",
  "replacedBy": "replacement-resource-id"
}
```

### Archived

Use when the resource is retained only for historical understanding, comparison, or recovery.

When possible, archived material should also be represented in the repository archive with enough context to explain why it was archived.

---

## Removing records

Do not automatically delete a resource record merely because the resource is no longer active.

Keep the record when it remains useful for:

* understanding project history;
* locating a replacement;
* interpreting an older example;
* recovering previous work;
* explaining a design decision.

A record may be removed when:

* it was entered by mistake;
* it duplicated another record;
* it contains unsafe information;
* it never represented a real or planned resource;
* it has no continuing historical or operational value.

---

## Security rules

This repository is public. Treat every committed configuration value as publicly visible.

Before adding a resource or configuration value, ask:

* Does this expose a credential?
* Does this reveal private personal information?
* Does this expose internal workplace information?
* Does this URL grant access without authentication?
* Does this identify a person who should remain anonymous?
* Does this reveal a private document name or location?
* Would this be safe to display on a public web page?

Never commit:

```text
passwords
API keys
OAuth secrets
access tokens
private keys
session identifiers
private form submissions
personal records
employee records
client records
restricted operational data
secret-bearing URLs
```

When a resource is private or restricted, the registry may describe its purpose and access category without exposing a sensitive access mechanism.

---

## Formatting rules

Configuration files should remain easy for both people and programs to inspect.

### JSON requirements

* Use valid JSON.
* Use UTF-8 encoding.
* Use two spaces for indentation.
* Do not include comments inside JSON.
* Do not use trailing commas.
* Use double quotation marks.
* Keep field names consistent.
* Use arrays consistently for multiple values.
* Use `null` for intentionally absent values.
* Do not use empty placeholder strings when `null` is more accurate.
* Keep records in a predictable field order.
* Validate JSON before committing changes.

### Identifier rules

Identifiers should be:

* unique;
* stable;
* lowercase;
* hyphenated;
* descriptive;
* independent of display names where practical.

Good:

```text
system-design-overview
task-events-sheet
task-start-form
```

Avoid:

```text
Resource1
new-file
thing
test-final
sheet-copy-2
```

### File naming rules

Configuration filenames should be:

* lowercase;
* hyphenated when necessary;
* descriptive of their responsibility.

Examples:

```text
resources.json
environments.json
feature-settings.json
```

Avoid creating multiple overlapping files that describe the same responsibility.

---

## Maintenance rules

When adding or changing configuration:

1. Confirm that the information is repository-wide.
2. Confirm that it does not belong in `shared/` or example-specific `data/`.
3. Confirm that no secret or sensitive information is included.
4. Validate the file format.
5. Use stable identifiers.
6. Update status and access fields accurately.
7. Replace placeholders with real values before marking resources active.
8. Identify replacements when resources are superseded.
9. Update this README when new configuration files or conventions are introduced.
10. Check references from the root README, documentation, examples, and static site.

---

## Design principle

The `config/` folder should remain a small, reliable control and reference layer.

It should make the project easier to understand by answering questions such as:

* What shared resources exist?
* Where are they located?
* What purpose does each one serve?
* Is each resource current?
* Who is expected to have access?
* Which resource replaced an older one?
* Which configuration applies across the repository?

It should not become a dumping ground for arbitrary JSON, application data, duplicate content, or secrets.
