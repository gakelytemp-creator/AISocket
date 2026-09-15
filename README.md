# AISocket

> **From your garden to the Moon — one library.**

[![Website](https://img.shields.io/badge/Website-googuly.online%2Faisocket-blue)](https://googuly.online/aisocket)
[![GitHub](https://img.shields.io/badge/GitHub-AISocket-black)](https://github.com/gakelytemp-creator/AISocket)
[![Forum](https://img.shields.io/badge/Forum-Discussions-green)](https://github.com/gakelytemp-creator/AISocket/discussions)

**AISocket is an open protocol and developing ecosystem for giving intelligence a formally bounded way to observe, investigate, and act inside devices, software, machines, and experimental environments.**

The intelligence does not need to contain the machine's control logic inside itself. The body keeps its own local skills, timing, limits, and safety rules. AISocket exposes what can be observed, what can be tested, what can be done, what is forbidden, and what feedback returns after an action.

The invited participant may be a large language model, a smaller local model, a specialized navigator, ordinary software, a human operator, or a combination of them.

The important distinction is not **AI versus machine**.

It is:

```text
what is already known locally
        ↓
keep it local, deterministic, fast

what needs interpretation or investigation
        ↓
invite intelligence
```

We are early. Some components exist, others are being developed, and several parts of the vision remain research goals. We intend to keep that boundary visible.

---

## The Core Idea

When an intelligence enters an unfamiliar local world, that world should be able to explain itself.

It should be able to say:

```text
this is what I am
this is what I can sense
this is what I can do
this is what I must never do
this is what you are allowed to do
this is how you can test me
this is how I report the result
this is what happens if communication disappears
```

AISocket is the handshake between intelligence and that local world.

It is not meant to replace the machine's controller, firmware, PLC, CNC kernel, robot servo loop, or other reliable local machinery.

It is meant to make those systems **legible and investigable** to an authorized intelligent participant without forcing that participant to rediscover the body's motor logic every time.

> **The body keeps the skills it already has. Intelligence is invited where intelligence is useful.**

---

## Control Is Only One Case

AISocket began from the problem of connecting LLMs to autonomous devices, but the broader problem is not merely control.

An intelligence may need to:

- observe;
- inspect;
- diagnose;
- compare hypotheses;
- choose a measurement;
- run a bounded experiment;
- teach;
- plan;
- repair;
- calibrate;
- adapt a procedure;
- or act.

A useful local interface therefore needs more than commands.

It needs **experimental affordances**.

A machine may expose a motion primitive. A laboratory instrument may expose a calibration test. A PCB investigator may expose two probes, a camera, a height sensor, a controlled power mode, and a set of safe measurements. A software system may expose state inspection and reversible operations.

The same general loop appears again and again:

```text
observe
   ↓
hypothesize
   ↓
choose a discriminating test
   ↓
measure / act
   ↓
observe the result
   ↓
compare
   ↓
revise understanding
```

This is why AISocket is not only a control interface.

**It is also an interface for investigation.**

---

## Three Responsibilities

AISocket separates three responsibilities that should not be confused.

### 1. The body

The body performs its ordinary work.

It owns the time-critical and safety-critical mechanisms that should not depend on a language model correctly interpreting a sentence.

Examples include:

- servo loops;
- torque or speed limits;
- interlocks;
- emergency stops;
- watchdogs;
- motion envelopes;
- local sequencing;
- deterministic recovery behavior;
- offline behavior.

### 2. The interface

The interface makes the local world legible.

It declares capabilities, tools, permissions, state, feedback, limits, and context.

It turns a closed machine into a bounded environment that an authorized participant can inspect and use without needing raw access to everything inside it.

### 3. The invited intelligence

The invited participant handles what benefits from interpretation, comparison, hypothesis formation, planning, diagnosis, teaching, or new synthesis.

It does not receive unlimited authority merely because it is intelligent.

It receives a **mandate**.

---

## Four Principles

### 1. Invitation, not intrusion

A device or environment declares itself through a passport. An authorized operator determines who may enter and under what conditions.

**No passport, no invitation — no control.**

More generally:

**No declared interface, no hidden authority.**

### 2. Safety-critical law belongs in the body

A prompt is not a safety mechanism.

Safety-critical constraints should be enforced by deterministic local machinery appropriate to the application.

The passport may describe those constraints, but the body must enforce them.

### 3. Known action should not repeatedly consume general intelligence

If a machine already knows how to move one axis, read a sensor, home itself, close a valve, or run a calibration cycle, a large model should not regenerate that low-level procedure every time.

AISocket tries to move already-known action into stable local machinery and reserve intelligence for novelty.

```text
known action      → local execution
unknown situation → intelligence
```

### 4. Experience should leave a usable trace

An investigation that disappears when the chat ends has lost part of its value.

AISocket therefore treats observation, action, conditions, and outcome as structured trace material that can later be inspected, compared, verified, and transformed into reusable knowledge.

A trace is not automatically truth.

It is evidence of what happened.

---

## Passport

A passport is the environment's structured self-description.

At minimum it should be able to describe:

```text
identity
capabilities
observable state
available tools
forbidden operations
permission frames
local safety constraints
offline behavior
feedback and reporting
version / configuration
```

A passport is a declaration, not a model's opinion.

A simple sensor may need only a few fields. A sophisticated robot, CNC machine, laboratory system, or industrial cell may need a layered passport with tools, diagnostics, roles, calibration procedures, and service operations.

Cryptographic signing and verification are intended so that critical declarations can eventually be authenticated rather than trusted merely because a registry or agent presents them.

---

## Body Law

The **Body Law** is the set of local constraints under which a body may operate.

The current architecture uses a layered idea:

```text
Firmware rules
    ↓
Capabilities
    ↓
Emergency constraints
    ↓
Offline mandate
    ↓
Delegation
    ↓
Context
```

The exact implementation will vary by device.

The architectural principle does not:

> **An invited intelligence may choose among permitted possibilities, but it must not be able to redefine the body's non-negotiable physical law.**

---

## Mandates and Permission Frames

The same machine may be entered by different participants for different reasons.

An owner, a service technician, a diagnostic model, a teaching assistant, and an emergency responder do not automatically receive the same powers.

AISocket therefore separates **capability** from **permission**.

A body may be physically capable of an action while the current participant is not authorized to request it.

The permission frame should be explicit, inspectable, and revocable.

---

## Interaction Tools

AISocket tools are the body's exposed hands, eyes, instruments, and bounded actions.

A tool may be:

- a sensor read;
- a camera view;
- a measurement primitive;
- a motion primitive;
- a self-test;
- a calibration procedure;
- a simulator;
- a reversible software action;
- a diagnostic probe;
- a bounded experiment;
- a request for human assistance.

The goal is not to expose every internal variable.

The goal is to expose enough structured capability that an intelligent participant can work effectively without being given uncontrolled access.

---

## The Investigator Pattern

Some AISocket bodies are not ordinary machines at all. They are **investigators**.

For example, an unknown PCB may be placed in a two-sided scanning machine with cameras, probes, height measurement, component recognition, and controlled electrical tests.

The body does not need to know the final schematic in advance.

It exposes safe experimental actions. Intelligence can then ask:

```text
What do I currently believe?
What observation would separate hypothesis A from hypothesis B?
Which measurement is cheapest or safest?
What changed after the test?
What should be tested next?
```

This turns AISocket into a bridge not only between intelligence and machinery, but between intelligence and **physical evidence**.

The same pattern can apply to electronics, laboratory experiments, machine diagnosis, calibration, inspection, and many other domains.

---

## Flight Recorder

A body should retain enough recent history to make its behavior investigable.

On a small microcontroller this may be a compact ring buffer. On a larger system it may include richer telemetry.

The recorder can preserve:

```text
state
command
measurement
alarm
context
tool invocation
result
recovery
```

The purpose is not surveillance.

The purpose is to avoid forcing every new investigator to begin in darkness.

---

## Trace Network

AISocket experiments and interventions should leave structured, addressable traces.

A useful trace can answer:

```text
what was observed?
what was attempted?
under which conditions?
with which tool or instrument?
what changed?
what result was obtained?
who or what initiated the operation?
```

A trace is **experience**, not automatically **knowledge**.

This distinction is important.

```text
AISocket
records what happened
        ↓
comparison / replication / interpretation
        ↓
Noepedia
preserves what has become reusable knowledge
```

AISocket should not grow an ever-larger prompt containing every incident.

It should preserve the evidence needed for later knowledge formation.

---

## AISocket + Noepedia

AISocket and [Noepedia](https://github.com/gakelytemp-creator/Noepedia) are separate projects with a common architectural direction.

AISocket moves already-known **action** into stable local machinery.

Noepedia moves already-known **knowledge** into a persistent, addressable semiotic structure.

Together they form a loop:

```text
Noepedia
validated local knowledge projection
        ↓
AISocket passport + Body Law
        ↓
observe / test / act
        ↓
flight recorder + trace
        ↓
real-world outcome
        ↓
comparison / replication / revision
        ↓
Noepedia
```

The world does not merely receive answers from intelligence.

**It returns evidence.**

And once that evidence becomes reliable knowledge, the next participant should not have to rediscover it from zero.

---

## AISocket + OpenPCB Commons

[OpenPCB Commons](https://github.com/gakelytemp-creator/OpenPCB-Commons) is a natural proving ground for the investigator pattern.

A board may begin as a black box.

AISocket can expose physical investigation tools. OpenPCB can preserve the object, measurements, provenance, repair history, donor-part information, and replication trail. Noepedia can later preserve generalized knowledge that escapes the single board: circuit motifs, prototypes, recurring failure modes, verified relations, and reusable procedures.

```text
black box
   ↓
AISocket investigation
   ↓
OpenPCB evidence trail
   ↓
replication
   ↓
Noepedia reusable knowledge
```

The three projects do not need to become one repository.

Their interfaces should simply fit together.

---

## The Socratic Participant

AISocket does not require the invited participant to know everything.

A useful participant may instead be very good at **working with what is known and identifying what is not**.

It may carry skills such as:

```text
find the relevant local knowledge
separate observation from inference
compare alternatives
notice contradiction
ask for a discriminating measurement
choose the next test
recognize when the field is insufficient
request stronger intelligence when needed
```

This is one reason AISocket should not be designed around one particular model class.

Sometimes a large frontier model is justified.

Sometimes a small local model, deterministic planner, human operator, or specialized navigator is enough.

The architecture should allow the expensive intelligence to appear **where novelty actually begins**.

---

## How It Works

A typical AISocket interaction follows this sequence:

**1. Register** — the body publishes its passport, capabilities, rules, version, and configuration.

**2. Connect** — the body becomes available to authorized participants through the chosen transport or registry.

**3. Operate locally** — routine work remains under local control.

**4. Enter with a mandate** — a participant receives only the permissions required for the task.

**5. Observe and investigate** — the participant uses declared tools rather than uncontrolled internal access.

**6. Act when justified** — actions pass through the body's local law and validation.

**7. Record the result** — observations, actions, and outcomes become structured trace material.

**8. Reuse what becomes known** — validated knowledge can later return through Noepedia or another knowledge layer as a bounded local projection.

---

## Why Not Just MCP?

MCP standardizes how an AI application can communicate with tools and resources.

AISocket is concerned with a different boundary:

- what an autonomous body declares about itself;
- what actions it can perform locally;
- what it refuses to perform;
- what permissions the current participant has;
- what happens offline;
- what evidence an intervention leaves;
- and how embodied action remains bounded independently of conversational fluency.

The approaches can be complementary.

An AISocket body may expose permitted tools through MCP or another transport.

**Use an appropriate protocol for communication. Use AISocket to describe and govern the local world being entered.**

---

## One Brain, Many Bodies

AISocket does not require every device to contain a large model.

A mower, elevator, robot arm, laboratory instrument, garage gate, accounting program, or PCB investigator may keep compact local logic while sharing access to one or more external intelligences.

The same intelligence may enter many bodies.

The same body may accept different intelligences.

```text
one intelligence
      ↓
many bounded bodies

one body
      ↓
many authorized participants
```

The body remains locally competent.

The intelligence remains replaceable.

The interface is the contract between them.

---

## Quick Start

The project is still developing, so the best starting point depends on what you want to do.

- Explore the registry: **[googuly.online/aisocket](https://googuly.online/aisocket)**
- Browse the repository: **[github.com/gakelytemp-creator/AISocket](https://github.com/gakelytemp-creator/AISocket)**
- Join discussion: **[GitHub Discussions](https://github.com/gakelytemp-creator/AISocket/discussions)**

The Python implementation is the current starting point. Additional platforms are under development.

We would rather mark a feature experimental than pretend it is finished.

---

## Platforms

| Platform            | Status         |
| ------------------- | -------------- |
| Python              | ✅ Ready        |
| Arduino / ESP32     | 🔄 In progress |
| Raspberry Pi        | 🔄 In progress |
| Android             | 🔄 In progress |
| ROS2                | ⬜ Planned      |
| Browser / WebSocket | ⬜ Planned      |

Platform support, examples, and maturity should remain explicitly versioned as development continues.

---

## Where This Leads

The long-term vision is not a world in which every device waits for a giant model to tell it what to do.

It is a world in which local systems keep their own competence while becoming understandable and usable by authorized intelligence when needed.

| Context       | Examples and directions |
| ------------- | ----------------------- |
| 🌱 Garden     | Mowers, irrigation, environmental sensing |
| 🏠 Home       | Household devices, accessibility tools, monitoring |
| 🧪 Laboratory | Measurement, calibration, experimental robots |
| 🎓 Education  | Reproducible experiments and affordable instruments |
| 🏭 Factory    | CNC, robot arms, diagnostics, integration |
| 🔧 Repair     | Investigation, service tools, OpenPCB-style black-box analysis |
| 🏙️ City      | Coordinated infrastructure with local authority |
| 🌙 Moon       | Remote systems with local autonomy and communication delay |
| 🔴 Mars       | Long-duration autonomy, maintenance, and reusable experience |

The off-world examples are long-term directions, not current capabilities.

They simply make one principle obvious: the farther the body is from its helper, the more important local autonomy, explicit law, and persistent knowledge become.

---

## Community

AISocket is intended to be built by people with different skills and reasons for participating.

Useful contributions include:

- code;
- hardware;
- adapters;
- experiments;
- testing;
- documentation;
- translations;
- security review;
- manufacturing experience;
- educational material;
- scientific criticism;
- real integration problems;
- new bodies and new investigative tools.

You do not need to agree with every current design choice.

If you see a better architecture, show it. If an experiment fails, preserve the failure. If you build something useful, leave enough of the road visible that the next person does not need to begin again from zero.

**No unnecessary bureaucracy. No gatekeeping. Reproducible work beats status.**

→ [Join the discussion](https://github.com/gakelytemp-creator/AISocket/discussions)

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE).

The license protects the freedom to use, study, modify, and redistribute the covered software under its terms.

Independent products and services may be built around the open protocol in accordance with the license and applicable agreements.

---

## Current Direction

The next architectural work is not only to add more device commands.

It is to make the boundary between **local skill, investigation, evidence, and reusable knowledge** increasingly explicit.

We want to test complete loops:

```text
passport
→ bounded tools
→ investigation
→ trace
→ replication
→ reusable knowledge
→ local projection
→ better next investigation
```

Success should be measured, not assumed:

- reliability;
- latency;
- recovery behavior;
- trace quality;
- portability across bodies;
- ability to reuse validated knowledge;
- reduction of unnecessary large-model computation;
- and the ability of an independent participant to understand a body without hidden context.

---

## We Need You

We are early. Very early.

That means there is still room to influence what AISocket becomes.

Bring a machine. Bring a sensor. Bring a broken device. Bring a laboratory problem. Bring a strange interface. Bring a criticism. Bring a tool that gives intelligence a new eye or a new hand.

A professional laboratory is welcome.

So is an old smartphone, a notebook, and a good question.

**The invitation is open.**

> **AISocket gives intelligence a bounded body.  
> Noepedia gives knowledge a persistent body.  
> The next discovery should begin where the last one ended.**
