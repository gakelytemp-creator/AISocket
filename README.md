# AISocket

> From your garden to the Moon — one library.

[![Website](https://img.shields.io/badge/Website-googuly.online%2Faisocket-blue)](https://googuly.online/aisocket)
[![GitHub](https://img.shields.io/badge/GitHub-AISocket-black)](https://github.com/gakelytemp-creator/AISocket)
[![Forum](https://img.shields.io/badge/Forum-Discussions-green)](https://github.com/gakelytemp-creator/AISocket/discussions)

**AISocket is an open protocol and developing ecosystem for connecting intelligence to autonomous devices, software, and experimental environments through declared capabilities, authorized access, local safety rules, and reusable experience.**

We want people to be able to use existing projects, build new ones, connect their own machines, and participate in developing the shared infrastructure. The same environment should support a small experiment with an old smartphone and, as the technology matures, more complex systems.

We are early. Some components are available, others are being developed, and several parts of the vision remain research or long-term goals. We intend to make those distinctions clear.

---

## Why This Exists

Large language models have become useful across many different tasks, but much of their interaction with the physical world still takes place through interfaces designed for humans or through specialized integrations.

Meanwhile, billions of devices and machines already exist around us: garden equipment, laboratory instruments, CNC machines, robots, sensors, vehicles, and ordinary household systems. Many of them can operate reliably on their own, but they have no common way to describe their capabilities to an AI system or invite it to help.

AISocket begins with a simple idea: when an intelligent participant enters an unfamiliar environment, the environment should be able to explain what it is, what can be observed, what actions are available, what is forbidden, and how to receive feedback.

A useful analogy is welcoming a new child into a kindergarten: share the toys, explain the rules of the house, and make room for learning through interaction.

**AISocket aims to provide that handshake: an invitation, an interface, and clear boundaries.**

---

## The Problem

An LLM entering an unknown device is much like a person sitting at an unfamiliar control terminal. It may not know what the machine can do, what state it is in, which commands are safe, or how to recover when something goes wrong.

Connecting a model directly to every actuator is neither a good general control strategy nor a sufficient safety mechanism. Routine control is often better performed by local algorithms, and safety-critical constraints should not depend on the model correctly interpreting a prompt.

At the same time, reducing the LLM to a fault-repair tool would miss many useful possibilities. Intelligence may be invited to observe, teach, investigate, plan, diagnose, assist with a task, or help develop a new procedure.

We therefore aim to separate three responsibilities:

* **The body** performs its ordinary work and enforces its local operating constraints.
* **The interface** describes the environment, available tools, permissions, and feedback.
* **The invited participant** interprets, investigates, plans, or acts within an explicitly granted mandate.

The goal is not to make every machine dependent on an LLM. It is to make useful interaction possible without taking away the machine's local autonomy or the human operator's authority.

---

## Three Principles

### 1. Invitation, not intrusion

A device or environment declares its capabilities through a passport. An authorized operator determines who may access it and under what conditions.

AISocket is designed around explicit authorization rather than unrestricted discovery and control.

**No passport, no invitation — no control.**

### 2. Safety-critical law belongs in the body

A prompt is not a substitute for a safety mechanism. We aim to keep safety-critical constraints in deterministic, locally enforced components wherever the physical system requires them.

The passport describes the body's rules; the implementation must enforce them. The exact mechanisms depend on the device and must be tested for their intended operating conditions.

A motor's torque limit, for example, belongs in the control system rather than relying on a chat instruction. The LLM may propose an action, but it should not be able to bypass the body's non-negotiable constraints.

### 3. Intelligence is invited for the work that needs it

Routine, time-critical execution should generally remain local. An LLM can be invited when interpretation, investigation, planning, teaching, or higher-level assistance is useful.

In one application, the agent may act as an emergency service specialist. In another, it may be a laboratory assistant, a programming partner, a diagnostic investigator, or a guide helping someone learn to use a machine.

Each mode requires an appropriate mandate. We consider this separation a promising way to reduce unnecessary computation while preserving useful intelligent assistance.

---

## How It Works

The intended interaction follows a simple sequence:

**1. Register** — describe the device or environment, its capabilities, and its operating rules. The registration tools help create a structured passport and configuration.

**2. Connect** — the device establishes its connection and becomes discoverable to authorized participants through the registry.

**3. Operate locally** — the body performs its ordinary work under its own control and safety mechanisms. It does not need an LLM in every control loop.

**4. Invite assistance** — an authorized participant enters with a defined mandate. It can inspect the available state, use permitted tools, investigate a problem, or help with an owner's requested task.

**5. Leave a trace** — observations, actions, results, and relevant context are recorded in a structured form, so later participants can inspect and potentially reuse the experience.

Not every device needs every feature. A small ESP32 project may have a short passport and a compact event log. A complex robot or industrial system may require layered capabilities, diagnostic procedures, and much richer telemetry.

---

## Quick Start

The project is still developing, so the best starting point depends on what you want to do.

If you want to explore the current registry, visit **[googuly.online/aisocket](https://googuly.online/aisocket)**. The registry is intended to help users register devices, manage their descriptions and configurations, and find authorized devices by name.

If you are a developer, start with the [repository](https://github.com/gakelytemp-creator/AISocket) and its available examples. The Python implementation is the current starting point; support for additional platforms is being developed.

If you are unsure which part is ready for your project, open a [Discussion](https://github.com/gakelytemp-creator/AISocket/discussions). We would rather help you find a realistic starting point than promise a feature that is not yet complete.

---

## Core Concepts

### Passport

A passport is the environment's structured self-description: what it is, what it can do, what it must not do, how it reports its state, and what happens when communication is unavailable.

A passport is a declaration, not a model's opinion. We aim to develop cryptographic signing and verification so that device identity and critical declarations can be authenticated rather than trusted merely because a registry or agent presents them.

Passports should scale with the body. A simple sensor may need only a few capabilities, while a sophisticated robot may need a layered description of joints, limits, tools, diagnostics, and service procedures.

### Body Law

The Body Law describes the constraints that govern a device's operation. The current architecture proposes six validation layers:

**Firmware rules → Capabilities → Emergency → Offline mandate → Delegation → Context**

The layers distinguish what is physically and permanently forbidden from what is permitted under particular roles, circumstances, or tasks. Safety-critical constraints must be enforced by the appropriate local mechanisms, not merely stated in text.

We intend to refine these layers through implementation, testing, and review. A passport can describe the law, but only a correctly designed and validated implementation can enforce it.

### Mandates and Permission Frames

Different participants may read the same passport while receiving different permissions. An owner, a maintenance agent, and an authorized rescue participant may have different mandates.

The goal is to make permissions explicit and inspectable. A change of role must not silently remove the body's non-negotiable safety constraints.

### Interaction Tools

AISocket aims to provide more than a list of commands. An unfamiliar environment should be able to expose useful ways to observe, inspect, test, and act, together with the feedback needed to understand the result.

For example, a laboratory instrument may expose measurements and calibration procedures; a robot may expose motion primitives and diagnostic sensors; a virtual environment may provide tools for testing a hypothesis before any physical action is taken.

The available tools and their permitted use depend on the environment and the participant's mandate.

### Flight Recorder

A body should retain a useful record of its recent operation: states, alarms, commands, and relevant events.

On a small microcontroller, this may be a compact ring buffer. On a more capable system, it may include richer telemetry. The purpose is to make failures and unusual behavior easier to investigate rather than forcing every new participant to begin without context.

### Trace Network

We want interventions and experiments to leave structured, addressable traces: what was observed, what was attempted, under which conditions, what changed, and what result was obtained.

A trace is not automatically a verified fact. The developing knowledge system should distinguish observations, hypotheses, experimental results, validated procedures, and rejected or superseded claims.

We expect that reusable experience may reduce repeated investigation and make future work more efficient. Whether a result applies to another device or situation must still be checked.

### Autonomous Mandate

When communication is unavailable, a body may continue operating within predefined local boundaries. The appropriate behavior depends on the application: some systems should continue, others should stop or enter a safe state.

This becomes especially important for remote systems, where communication delays and interruptions make continuous external control impractical.

### Emergency Protocol

We intend to support carefully bounded emergency and rescue access where an application requires it. Such access must be explicitly governed, authenticated, and tested.

An emergency mandate is not intended to override the non-negotiable safety constraints of the body.

### Registry

The registry helps devices and authorized participants find one another through names and declared information. It is intended to support device management without making a central service the owner of the device or its data.

---

## Why Not Just MCP?

MCP standardizes how an AI application can communicate with tools and other resources. AISocket is being developed around a related but different concern: how an autonomous body declares its capabilities, operating constraints, permission frames, offline behavior, and trace discipline.

The two approaches can be complementary. An AISocket device may expose permitted capabilities through MCP or another transport, while its local law and authorization mechanisms remain independent of the conversation protocol.

**Use the appropriate tool protocol for communication; use AISocket to describe and govern the embodied interaction.**

We do not aim to replace existing standards where they already solve the problem well.

---

## Find Your Way In

AISocket is intended to be an environment that people can approach from different directions. You do not need to understand the entire protocol or share our broader philosophy before using a practical tool.

Whether you want to reproduce a project, create a new device, manufacture one, teach with it, or improve the infrastructure, we want to help you find a useful starting point.

### For People Who Want to Use Existing Projects

You may simply want to take a working project, follow the instructions, and use it.

We aim to develop a collection of reproducible projects with clear requirements, documentation, version information, and honest descriptions of what has been tested. Some projects may be free examples, while others may eventually be offered as finished packages or through community-supported distribution.

You should not have to become a protocol developer just to use a useful tool. If an example is incomplete or experimental, we want that to be clear before you begin.

### For Builders and Independent Developers

You may have an idea for a device, a small experiment, or an existing machine that you want to make more accessible to intelligent assistance.

We want to provide passports, examples, simulation tools, and shared interfaces that make it easier to begin with a small working system and develop it further.

You are welcome to build your own implementation, challenge our assumptions, or propose a different approach. A useful contribution may be a complete device, a small adapter, a new measurement tool, or an experiment that reveals a limitation.

### For Manufacturers

A project that works once is not yet a product that can be manufactured and supported at scale.

We are interested in working with manufacturers who may eventually want to produce AISocket-compatible devices or integrate the protocol into existing product lines. This requires attention to stable interfaces, versioning, testing, documentation, maintenance, and the responsibilities of the manufacturer and operator.

We do not claim to have a completed certification or industrial production ecosystem. We want to develop the necessary requirements together with people who have real manufacturing experience.

Independent commercial products and services may be developed around the open protocol in accordance with its license and applicable agreements. The intended nonprofit character of the AISocket organization is not a prohibition on others earning a living from their own work.

### For Integrators

You may already have a factory, a laboratory, a building, a software system, or a collection of devices that perform useful work.

AISocket aims to help connect such systems without requiring them to abandon their existing controllers or safety mechanisms. We are interested in adapters, gateways, and integration patterns that preserve local authority while making selected capabilities available to authorized participants.

If you have a real integration problem, we would be glad to discuss it. Your constraints and experience can help shape the protocol.

### For Researchers, Teachers, and Students

We want AISocket to make experimentation more accessible, especially where people have limited equipment or limited access to specialized laboratories.

An old smartphone can become an observation tool. A camera can help record the readings of an existing instrument, follow a moving object, or collect measurements over time. A simple robot can become a platform for investigating control, perception, and cooperation.

These are examples of the kinds of projects we hope to support, not claims that every such application is already available.

We welcome teachers, students, universities, and independent researchers who want to develop experiments, reproduce results, or study the interaction between people, AI systems, and physical environments. The goal is to help people acquire knowledge through observation and investigation, not merely receive answers.

### For Media, Bloggers, and Technology Communicators

If you enjoy explaining new technologies, reviewing independent projects, or helping people discover what they can build, we would be glad to work with you.

You may help someone discover a useful tool, inspire a student to begin an experiment, introduce a manufacturer to a new possibility, or bring criticism that helps us improve.

We want your contribution to remain visible. As the project grows, we aim to maintain a public record of significant contributions, including articles, videos, translations, educational materials, and outreach. With your agreement, this record may include your name or publication, links to your work, and the role it played in the project's development.

We are interested in practical, mutually beneficial partnerships. We will do our best to provide technical information, access to project contributors, working demonstrations, and assistance with preparing accurate materials. Independent reviews and constructive criticism are welcome; support does not require agreement with us.

As resources become available, we hope to develop transparent programs for paid educational content, outreach campaigns, and other agreed work. Any financial support would depend on available funding and clearly defined terms. We do not want to promise rewards that the project cannot yet provide.

Whether you run a small channel, write a technical digest, teach, translate, or reach a large audience, you are welcome to introduce yourself and tell us what kind of collaboration would be useful to you.

**Your work should not disappear behind the project. We want the people who help it grow to remain part of its visible history.**

### For People Who Want to Develop AISocket Itself

The protocol, tools, documentation, safety architecture, registry, and community infrastructure all need people who are willing to improve them.

We welcome programmers, hardware engineers, testers, security researchers, documentation writers, designers, translators, organizers, and people who bring useful criticism.

You do not need to agree with every current decision. If you see a better architecture, a missing requirement, or a problem we have not understood, we want to hear it.

We aim to develop the project through open discussion, reproducible work, and contributions from people with different skills and resources.

---

## Where This Leads

The long-term vision is a shared environment in which many different bodies and participants can interact through compatible interfaces while retaining their own responsibilities and boundaries.

A small project may begin with one phone and one sensor. A more complex installation may involve many machines, specialized algorithms, and several intelligent participants. We want the same basic principles to remain useful as the scale changes.

| Context       | Examples and development directions                                                                                          |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 🌱 Garden     | Mowers, irrigation, environmental sensors                                                                                    |
| 🏠 Home       | Household devices, accessibility tools, monitoring systems                                                                   |
| 🧪 Laboratory | Data logging, measurement tools, experimental robots                                                                         |
| 🎓 Education  | Reproducible experiments and affordable learning instruments                                                                 |
| 🏭 Factory    | CNC machines, robot arms, industrial integration, shared service experience                                                  |
| 🏙️ City      | Coordinated infrastructure and large collections of autonomous devices                                                       |
| ⚕️ Crisis     | Carefully governed emergency and rescue assistance                                                                           |
| 🌙 Moon       | Remote operation with local autonomy and communication delays                                                                |
| 🔴 Mars       | Long-term research into autonomous systems, maintenance, and reusable experience under substantial communication constraints |

The off-world examples are long-term aspirations, not current capabilities. They illustrate why local autonomy, reliable constraints, and experience that survives individual sessions may become increasingly important.

We also want to investigate whether shared traces can help multiple AI systems cooperate more effectively. A common memory does not automatically create collective intelligence, and agreement is not proof of correctness. These are questions to explore through observation, comparison, and experimentation.

---

## Platforms

The following status reflects the current project roadmap. A platform marked as in progress should not be assumed to be production-ready.

| Platform            | Status         |
| ------------------- | -------------- |
| Python              | ✅ Ready        |
| Arduino / ESP32     | 🔄 In progress |
| Raspberry Pi        | 🔄 In progress |
| Android             | 🔄 In progress |
| ROS2                | ⬜ Planned      |
| Browser / WebSocket | ⬜ Planned      |

Platform support, examples, and their maturity will be documented as development continues.

---

## Registry

Register and manage your devices at **[googuly.online/aisocket](https://googuly.online/aisocket)**.

The registry is intended to support free accounts, device registration, passport and configuration management, and project history. We aim to keep users in control of their own devices and data, including the ability to update or remove their registrations.

The registry is part of a developing ecosystem. Its features and policies should be documented as they become available.

---

## Community & Contributors

AISocket is intended to be built by people with different skills, resources, and reasons for participating. Some will write code, some will build devices, some will test and criticize, some will teach, translate, manufacture, organize, or help others discover the project.

We want these contributions to remain part of the project's visible history.

We plan to create a dedicated **Community & Contributors** page where, with their permission, individuals and organizations can present themselves and their work. Organizations may be represented by their emblems, and individuals by their photographs or other chosen images. Profiles may include a short introduction, links to relevant work, and a record of contributions.

This space should also help participants find one another and develop new collaborations. A contributor should be able to submit their work, correct their information, and point out contributions that have been overlooked.

We intend to develop the recognition system openly, rather than treating it as a collection of awards granted only by the founders.

---

## Contributing

There are many ways to participate:

* **Code** — improve an implementation, create an adapter, or open a pull request.
* **Hardware** — build and test devices on different platforms.
* **Testing** — run examples, report failures, and investigate edge cases.
* **Documentation** — write guides, improve explanations, or translate materials.
* **Research** — propose experiments, compare approaches, and publish results.
* **Education** — create lessons, demonstrations, and accessible laboratory projects.
* **Manufacturing and integration** — help turn working prototypes into reproducible systems.
* **Outreach** — write articles, produce videos, maintain technical digests, or introduce the project to new communities.
* **Organization and governance** — help develop transparent processes for collaboration, recognition, and long-term sustainability.

We are genuinely happy to collaborate with anyone who finds this interesting. No unnecessary bureaucracy, no gatekeeping, and no requirement to agree with every decision.

If this solves a problem you have, join us. If it gives you an idea, share it. If you want to build something with it, we will do our best to help.

→ [Join the discussion](https://github.com/gakelytemp-creator/AISocket/discussions)

---

## Constitution

AISocket is governed by a constitution intended to protect against centralized control, vendor lock-in, and surveillance misuse.

We want the protocol to preserve human authority over consequential physical actions and to prevent its safety mechanisms from being treated as optional suggestions. The project does not aim to remove human authority from the use of force.

The constitution and its implementation will need continued review as the ecosystem develops.

→ [Read the Constitution](https://github.com/gakelytemp-creator/AISocket/blob/main/CONSTITUTION.md)

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE).

The license protects the freedom to use, study, modify, and redistribute the covered software under its terms. It does not mean that every product, service, or manufacturing activity built around the ecosystem must be offered without charge.

We want to encourage independent development while preserving the freedoms and obligations established by the license.

---

## Nonprofit and Self-Sustaining

We intend AISocket to operate as a nonprofit, self-sustaining project. Any income or financial surplus should remain dedicated to the project's mission: maintaining and renewing infrastructure, supporting contributors, developing new tools, and making knowledge and technology more accessible.

We aim to establish transparent financial rules, including reasonable reserves for future maintenance and continuity. As resources become available, we want to develop fair ways to compensate and support contributors according to their documented work.

The project is not intended to generate private profit for its founders. Its resources should be used to keep the system working, renew what wears out, and help the community continue creating.

---

## We Need You

We are early. Very early. That means there is still room to influence what this project becomes.

We are looking for people who can build, test, criticize, explain, teach, manufacture, organize, or simply bring a problem worth solving. A useful contribution does not have to be large, and it does not have to come from someone with an impressive title.

We want to make room for the person with a professional laboratory and the person with an old smartphone, a notebook, and a question.

If you have a better idea, show us. If you find something that does not work, tell us. If you build something useful, we would like to help others discover it.

**The invitation is open.**

→ [Join the forum](https://github.com/gakelytemp-creator/AISocket/discussions)

*P.S. We are two people and a lot of enthusiasm. Community is not a nice-to-have — it is the whole point.*
