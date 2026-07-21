# System Design Template

A practical learning and experimentation project for designing human-centered digital workflows.

This repository has two purposes:

1. **Build and test small workflow systems** using tools such as Google Apps Script, Google Forms, Google Sheets, Google Keep, Google Tasks, Gmail, web pages, phones, and watches.
2. **Document the thinking behind those systems** so the project also becomes a small textbook on practical system design.

## Core idea

A useful workflow may involve three broad domains:

- **Human** — receives information, performs work, tracks progress, and reports completion.
- **Physical world** — rooms, carts, supplies, tools, equipment, and real conditions.
- **Digital system** — software, stored data, automation, notifications, interfaces, and records.

The project explores how these domains cooperate without requiring one application to do everything.

## Guiding principles

- Design for ease of use. A system that is difficult to use will not be used reliably.
- Describe the work before choosing the software.
- Give each tool a clear responsibility.
- Separate human working state from digital system state.
- Reference stable information instead of transporting it unnecessarily.
- Preserve progress so a person can leave and return without losing their place.
- Keep current state separate from permanent history.
- Use fast, deliberate triggers for testing before introducing real schedules.
- Record only the information that will be useful later.

## Current design question

A central question in this project is:

> How does the human tell the digital system that the state of an event has changed?

Possible answers include:

- form submission;
- button press;
- task completion;
- message;
- web app action;
- explicit completion signal.

The project will test these approaches rather than assume one final solution in advance.

## Repository contents

```text
system_design_template/
├── index.html      # Main static entry page for the project
├── overview.md     # Initial system-design lesson and brainstorming output
└── README.md       # Project purpose, principles, and repository guide
```

Additional folders will be added only when the project needs them. Likely future areas may include:

```text
docs/               # Project documentation and lessons
examples/           # Small sandbox experiments
assets/             # Images, diagrams, and styles
schemas/            # JSON structures and data definitions
```

These are proposed categories, not fixed requirements.

## Current status

The project is in the **early design and vocabulary stage**.

Work completed so far includes:

- defining the human, physical-world, and digital-system domains;
- distinguishing task definitions from task instances;
- distinguishing human progress from system state;
- identifying triggers, events, signals, records, responses, and references;
- defining ease of use as a functional requirement;
- outlining an initial sandbox involving a trigger, watch notification, human checklist, completion signal, and event record.

No final architecture has been chosen yet.

## Working vocabulary

| Term | Meaning |
|---|---|
| System design | Deciding what parts exist, what each part does, and how they cooperate |
| Trigger | Something that causes a process to begin |
| Event | A meaningful occurrence represented in the system |
| Workflow | The sequence through which work moves |
| Task definition | The reusable description of a task |
| Task instance | One particular occurrence of that task |
| Procedure reference | A link or identifier pointing to instructions |
| Human working state | What the person has completed so far |
| System state | What the digital system currently believes |
| Completion signal | The input indicating that work is finished |
| Record | Preserved information about what happened and when |
| Response | What the digital system does next |
| Loose coupling | Parts cooperating without depending heavily on one another’s internal details |

## Development approach

The project will favor small sandbox experiments over large speculative builds.

A typical experiment should answer one or two questions clearly, such as:

- Can a form submission create a work event?
- Can the event generate a watch-visible notification?
- Can a human use a separate checklist while the system tracks only event status?
- Can a completion signal update the event and preserve a useful record?
- What information must the system store itself?

## Static site

The root `index.html` file will serve as the main entry page for the project’s static documentation and experiments.

When GitHub Pages is enabled for the repository, the site can be published from the `main` branch and repository root.

## Project philosophy

> Reference the procedure. Transport only the data that must cross between parts.

The goal is not to force every tool into one application. The goal is to make the system serve the human and the work.
