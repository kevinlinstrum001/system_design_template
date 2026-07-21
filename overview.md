Yes. We are describing the same document.

It would be a **small instructional HTML textbook on practical system design**, using our watch–human–digital-system sandbox as the main example. Its purpose would not be merely to document this one experiment. It would teach you how to think about systems, name their parts, describe how they interact, and communicate designs clearly enough that we can build them together.

A suitable working title would be:

# Practical System Design

## Learning to describe people, software, data, events, and workflows

The first lesson could be:

# Lesson 1: Separating the Human, the Physical World, and the Digital System

## What the document should accomplish

By the end of the lesson, you should be able to:

* describe a system without immediately deciding how to build it;
* identify its human, physical, and digital parts;
* distinguish a goal from an implementation;
* describe how an event moves through a workflow;
* distinguish human working state from system state;
* explain the difference between carrying data and referencing data;
* identify triggers, signals, records, responses, and interfaces;
* state priorities and design principles;
* communicate an idea using a small shared vocabulary.

## The main subject

The lesson would use this general problem:

> A digital system receives an event, informs a human that work is needed, gives the human access to instructions, allows the human to manage progress, receives a completion signal, responds, and preserves a useful record.

Our examples might mention Forms, Apps Script, Keep, Gmail, Sheets, a phone, and a watch. However, those products would be presented as **possible parts**, not as the definition of the system.

The lesson should make clear that we are currently learning the shape of the problem rather than locking ourselves into a particular implementation.

## What we have learned so far

### 1. The system has three broad domains

**The human**

* receives information;
* interprets instructions;
* makes decisions;
* performs work;
* tracks personal progress;
* reports outcomes.

**The physical world**

* rooms;
* carts;
* supplies;
* equipment;
* tools;
* observable conditions;
* the work being performed.

**The digital system**

* software;
* stored data;
* automated processes;
* web services;
* scripts;
* forms;
* interfaces;
* notifications;
* records.

Devices such as the phone and watch are often best understood as **interfaces to the digital system**, rather than as the entire system themselves.

### 2. Human state and system state are different

The human may know:

* which steps have been completed;
* what remains;
* what problem was encountered;
* what they are doing at this moment.

The digital system may know only:

* an event was created;
* the human was notified;
* the event is active;
* a completion signal has or has not been received.

The two sides do not need to possess identical information.

### 3. Data does not need to travel through every part

A Keep note may help the human perform a procedure without containing:

* an event ID;
* the original form submission;
* requester information;
* system timestamps;
* the permanent event record.

The event can merely reference the Keep note.

This leads to one of our strongest guiding principles:

> **Reference the procedure; transport only the information that must cross between parts.**

### 4. Different tools can perform different jobs

One program does not need to handle the entire workflow.

For example:

* one tool receives the original input;
* another creates the event;
* another notifies the human;
* another displays the procedure;
* another preserves human checklist progress;
* another receives the completion signal;
* another stores history.

The parts cooperate through references, signals, and shared identifiers.

### 5. A task definition is different from a task occurrence

A **task definition** describes what the task generally means.

A **task instance** is one actual occurrence of that task.

Example:

**Definition**

> Inspect the cart using these seven steps.

**Instance**

> Cart inspection requested on July 21 at 8:14 AM.

The definition can be reused. Each instance gets its own status and record.

### 6. State is different from history

**State** describes what is true now:

```text
Status: active
Progress: incomplete
Completion signal: not received
```

**History** describes what happened:

```text
8:14 AM — Event created
8:15 AM — Notification sent
8:17 AM — Human acknowledged task
8:29 AM — Completion submitted
```

A good system may need both.

### 7. A trigger and a function are separate concepts

A **trigger** causes something to happen.

Examples:

* form submission;
* scheduled time;
* button press;
* QR scan;
* edit to a spreadsheet;
* completion of another task.

A **function** is what the digital system does after the trigger occurs.

This means the same function can be tested with a form submission and later used with a scheduled trigger.

### 8. The completion signal is a central design question

The human may use a separate checklist while working. The digital system does not necessarily need to observe every checkbox.

It may only need a final signal such as:

> This event is complete.

That signal could also include:

* completion time;
* result;
* message;
* exceptions;
* quantities;
* observations;
* attachments;
* other reusable data.

## Current vocabulary

The lesson should define these terms in plain language:

| Term                | Working meaning                                                              |
| ------------------- | ---------------------------------------------------------------------------- |
| System design       | Deciding what parts exist, what each part does, and how they cooperate       |
| Digital system      | The software, data, automated processes, and connected services              |
| Human               | The person receiving information, deciding, acting, and reporting            |
| Physical world      | The environment, objects, tools, and real work                               |
| Interface           | The place where a human interacts with the digital system                    |
| Trigger             | Something that causes a process or function to begin                         |
| Event               | A meaningful occurrence represented in the system                            |
| Workflow            | The sequence through which work moves                                        |
| Task definition     | The reusable description of what a task means                                |
| Task instance       | One particular occurrence of a task                                          |
| Procedure           | Instructions for carrying out the task                                       |
| Reference           | Information telling someone or something where to find another resource      |
| Transport           | Moving actual data from one part to another                                  |
| State               | What the system currently believes to be true                                |
| Human working state | The human’s current progress through the work                                |
| System state        | The digital system’s current understanding of the event                      |
| Signal              | A small input that communicates that something happened                      |
| Completion signal   | The input indicating that work has finished                                  |
| Record              | Preserved information about what occurred                                    |
| Response            | What the system does after receiving an event or signal                      |
| Handoff             | A point where responsibility or information passes between parts             |
| Acknowledgment      | Confirmation that an input or signal was received                            |
| Identifier          | A value used to distinguish one event or task instance from another          |
| Loose coupling      | Parts cooperating without depending heavily on each other’s internal details |

## Goals

The system should eventually be capable of helping a person know:

1. **When** it is time to do something.
2. **What** needs to be done.
3. **What has already been done.**
4. **What remains.**
5. **When and how the work was completed.**
6. **What the digital system should do next.**

## Priorities

Your most important priority is correct:

> **The system must be easy to use, because a system that is not used cannot accomplish its purpose.**

That produces several supporting priorities:

### Reduce human effort

The human should not need to:

* search repeatedly for instructions;
* enter information the system already knows;
* navigate through many unrelated screens;
* remember complex technical steps;
* manually copy identifiers between tools.

### Preserve progress

A person should be able to:

* leave the interface;
* let the watch sleep;
* use another program;
* return later;
* continue from the same place.

### Make the next action obvious

At any point, the human should be able to determine:

* what am I doing;
* what is next;
* how do I report completion;
* how do I report a problem.

### Separate responsibilities

Each part should have a clear job. A note does not need to become a database. A database does not need to become a checklist. A notification does not need to carry the whole event.

### Avoid unnecessary data movement

Data should cross boundaries only when another part actually needs it.

### Preserve useful records

The system should retain enough information to answer later:

* what happened;
* when;
* why;
* who or what initiated it;
* what response occurred;
* whether it completed;
* what exceptions were reported.

### Design for failure and interruption

The system should account for:

* notifications being missed;
* the watch going to sleep;
* the human switching applications;
* work being paused;
* forms being abandoned;
* tasks being incomplete;
* connectivity being lost;
* duplicate signals.

## Guiding principles

These could appear as highlighted lesson cards:

> **Describe the work before choosing the software.**

> **A tool should have a clear responsibility.**

> **The human and the digital system do not need identical information.**

> **Reference large or stable information; transport only necessary data.**

> **Human progress and system status are related, but they are not the same thing.**

> **Every important event should have an identifiable instance.**

> **A current state can change; a historical record should remain.**

> **Testing should use fast, deliberate triggers even when the final system will use slower schedules.**

> **Ease of use is a functional requirement, not decoration.**

## Suggested HTML document structure

The document could be one polished, mobile-friendly lesson with:

1. **Hero section**
   Title, subtitle, and lesson objectives.

2. **The design problem**
   The human–physical–digital scenario in plain language.

3. **Three-domain diagram**
   Human, physical world, and digital system.

4. **Core workflow diagram**
   Trigger → event → notification → human work → completion signal → response → record.

5. **Vocabulary section**
   Terms with short definitions and examples.

6. **What we have learned**
   The major distinctions described above.

7. **Guiding principles**
   Highlighted cards.

8. **Goals and priorities**
   Including ease of use, preserved state, clear next actions, and recordkeeping.

9. **Worked example**
   A generic event with a referenced checklist and separate completion signal.

10. **Known versus unknown**
    What we understand conceptually and what future sandbox tests must discover.

11. **Reflection questions**
    Small questions to practice system-design thinking.

12. **Summary sheet**
    A compact visual reference that can be used during future discussions.

## What the document should not do yet

It should not yet:

* prescribe the final Google products;
* provide implementation code;
* decide whether Keep or Forms is the final checklist;
* settle how completion will be detected;
* build the sandbox;
* claim the watch supports something we have not tested;
* turn the lesson into project documentation alone.

It should teach the thinking that allows us to make those decisions intelligently later.

The document is therefore best described as:

> **An introductory textbook lesson in practical system design, developed from a real workflow problem but written to teach reusable concepts, vocabulary, distinctions, priorities, and reasoning methods.**
