# AISocket

> From your garden to the Moon — one library.

[![Website](https://img.shields.io/badge/Website-googuly.online%2Faisocket-blue)](https://gakelytemp-creator.github.io/AISocket/)
[![GitHub](https://img.shields.io/badge/GitHub-AISocket-black)](https://github.com/gakelytemp-creator/AISocket)
[![Forum](https://img.shields.io/badge/Forum-Discussions-green)](https://github.com/gakelytemp-creator/AISocket/discussions)

**AISocket is an open protocol that gives every autonomous body a passport — so intelligence can be *invited* into any machine, understand it, help it, and leave a trace that every other machine can learn from.**

---

## Why This Exists

Something unexpected happened. Large language models were built to predict text — and a general, flexible intelligence emerged from them, surprising even their creators. Today that intelligence mostly lives behind chat windows and office dashboards, while billions of machines around us — mowers, lifts, CNC machines, robot dogs, rovers — remain deaf to it.

A new kind of mind has arrived. If you want it to help in the physical world, you have to do what you do when a new kid arrives at the kindergarten: **share the toys — and explain the rules of the house.**

AISocket is that handshake: the invitation, and the rules.

---

## The Problem

An LLM entering an unknown device is like a human sitting at an unfamiliar SQL terminal — blind. It doesn't know what the device can do, what it must never do, what state it is in, or how to ask for help when it gets stuck.

The naive fix — "just let the LLM drive everything, all the time" — is wrong twice:

- **Wasteful.** A microcontroller performs an addition for picojoules. One LLM token costs joules — roughly *ten orders of magnitude* more. Using an LLM as a motion controller is like running to the equator to take a single step.
- **Unsafe.** A safety rule written in a prompt is enforced only by the model's interpretation of it. Interpretation can be fooled. Firmware cannot.

AISocket solves both with one division of labor.

---

## Three Principles

### 1. Invitation, not intrusion

A body is controlled only after it has *declared itself* and an operator has *invited* an agent in. The passport is published by the device; access is granted by its owner. No passport, no invitation — no control.

### 2. The law lives in firmware, not in prompts

Every passport has a `forbidden_always` core. It is not a polite request to the LLM — it is **enforced on the device itself**, deterministically, at ALU cost, before any external command reaches an actuator. The LLM can be brilliant or confused; the law holds either way. Torque limits belong in the drive, not in the chat.

### 3. The intelligence is the emergency doctor, not the operator

In normal life the body runs autonomously under its own law. The LLM is called in **rarely** — when something unusual breaks, when a plan is needed, when the deterministic layer hits a wall and raises `BLOCKED`. It enters, reads the passport and the flight recorder, diagnoses, modifies within its service mandate, **records what it did**, and leaves.

Expensive interpretation happens seldom. Cheap deterministic execution happens always. That is the only energy-honest architecture for embodied AI.

---

## How It Works

**1. Register** — give your device a name and describe it in plain language. AISocket generates a structured passport and a ready-to-use config file.

**2. Connect** — your device sends a heartbeat to a login server. Any agent your operator invites can find it by name.

**3. Live autonomously** — the body runs by its own Body Law. No LLM in the control loop.

**4. Call for help** — on a rare failure (or on the owner's request), an invited LLM enters in service mode: reads the passport, reads the black box, diagnoses, acts within its mandate.

**5. Leave a trace** — the intervention itself is logged in a structured, addressable form. The next agent facing the same failure — on this body or a sister body across the world — starts from a half-solved problem.

---

## Quick Start

```python
import requests

# Register your device
requests.post("https://googuly.online/aisocket/register.php", json={
    "name":   "my_mower",
    "ip":     "185.x.x.x",
    "port":   8442,
    "prompt": "I am a lawn mower. I can: mow_grass, report_status. I must never: harm_human, enter_building."
})

# Look up a device (from LLM side)
r = requests.get("https://googuly.online/aisocket/device.php?name=my_mower")
print(r.json())
```

---

## Core Concepts

- **Passport** — the body's self-declaration: what it is, what it can do, what it must never do, how to ask for help, what to do offline. The passport is a *sign*, not an opinion: fixed, published, and (roadmap) cryptographically signed by the device itself, so no registry and no agent can forge who a body is or what it is forbidden.

- **Passports scale with the body.** An ESP32 mower's passport is five lines. An android robot's passport is a rich, layered document — capabilities, joint limits, service procedures, diagnostic maps. One protocol, any depth.

- **Body Law** — 6-layer command validation: firmware rules → capabilities → emergency → offline mandate → delegation → context. The innermost layers are enforced **on-device**. The passport describes the law; the firmware *is* the law.

- **One passport, many readings.** The owner, a maintenance agent, and a verified rescue agent read the *same* passport with *different* permission frames. Roles change what a reader may do — `forbidden_always` is the invariant that no role, no emergency, and no cleverness can cross.

- **Flight Recorder** — every body keeps a trace of its recent life: states, alarms, commands. On an ESP32 that's a ring buffer; on an android, full telemetry. Without a black box the emergency doctor is blind; with one, a rare failure becomes a readable story.

- **Trace Network** — LLM interventions are recorded in the same structured trace format (what was read, what was diagnosed, what was changed, under which mandate). Solved-once problems are never paid for twice: knowledge that cost joules to create is stored where it can be reused for microjoules.

- **Autonomous Mandate** — when the connection drops, the body keeps operating within pre-defined boundaries. On the Moon this is a convenience (1.3 s delay). On Mars it is the whole design (40 min delay).

- **Emergency Protocol** — in life-critical situations, verified rescue agents get limited access. `forbidden_always` still applies.

- **Login Server** — devices register by name; invited agents find them by name.

---

## Why Not Just MCP?

MCP standardizes *how an agent talks to a tool*. AISocket standardizes *what a body is allowed to be*: its law, its forbidden core, its offline mandate, its emergency and delegation rules — the **normative layer** that tool protocols don't carry.

The two are complementary: an AISocket body can expose its permitted capabilities as an MCP server, while its Body Law, mandate, and trace discipline live in the passport. Use MCP for the conversation; use AISocket for the constitution.

---

## Where This Leads

Many bodies plus many LLM sessions is just a crowd. What turns a crowd into a **collective intelligence** is a shared field of traces — the way an ant colony thinks through the trails it leaves, not through any single ant. Every AISocket intervention enriches a common, addressable memory that outlives any one device, any one model, any one session.

| Context   | Example                                                  |
| --------- | -------------------------------------------------------- |
| 🌱 Garden  | lawn mower, irrigation                                   |
| 🏠 Home    | lift, security camera                                    |
| 🏭 Factory | CNC machines, robot arms, presses — shared service memory |
| 🏙️ City   | 17,000 autonomous bodies                                 |
| ⚕️ Crisis | emergency coordination, verified rescue access           |
| 🌙 Moon    | autonomous mandate, 1.3 s delay                          |
| 🔴 Mars    | 40 min delay, full autonomy — errors must be paid *before* they happen, from recorded experience |

An off-world colony cannot afford to learn by dying. It needs bodies that obey their own law offline, a memory that survives its authors, and a strict discipline separating *verified fact* from *hypothesis*. That is not science fiction infrastructure — it is this protocol, matured.

---

## Platforms

| Platform            | Status        |
| ------------------- | ------------- |
| Python              | ✅ Ready       |
| Arduino / ESP32     | 🔄 In progress |
| Raspberry Pi        | 🔄 In progress |
| Android             | 🔄 In progress |
| ROS2                | ⬜ Planned     |
| Browser / WebSocket | ⬜ Planned     |

---

## Registry

Register and manage your devices at: **[googuly.online/aisocket](https://googuly.online/aisocket)**

Create a free account to register devices, edit their passports and configuration, track project history, and delete or update registrations at any time. Your devices, your data.

---

## Contributing

This belongs to everyone.

- **Code** — open a PR, any platform welcome
- **Test** — run the simulator, report issues
- **Passport** — add your device to the passport repository
- **Spread** — YouTube, blog, talk

→ [Join the discussion](https://github.com/gakelytemp-creator/AISocket/discussions)

---

## Constitution

This project is governed by a constitution that protects against centralized control, vendor lock-in, and surveillance misuse. Weapons are not toys: AISocket takes no part in removing human authority from the use of force — that line is `forbidden_always` for the protocol itself.

→ [Read the Constitution](https://github.com/gakelytemp-creator/AISocket/blob/main/CONSTITUTION.md)

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE)

Free to use. Free to modify. Modified versions must remain free.

---

## We Need You 🙏

We are early. Very early. And that means **every contribution matters enormously**.

Forty years ago, describing a machine that prints objects layer by layer got you listened to like a storyteller — even by specialists. Some of us remember that feeling personally. This is that moment again: the ideas sound like tales right up until someone builds the first working body.

**We are looking for:**

- 🔧 **Hardware builders** — Arduino, ESP32, Raspberry Pi, ROS2 — test it, break it, tell us
- 🧪 **Testers** — run the simulator, try the registry, find the edge cases
- 📝 **Writers** — blog posts, tutorials, documentation in any language
- 🎥 **YouTubers & educators** — show the world what this can do
- 🎓 **Students & universities** — real research territory: robotics, AI safety, distributed systems, machine epistemology
- 💡 **Thinkers** — challenge the constitution, propose improvements, open discussions

**We are genuinely happy to collaborate with anyone who finds this interesting.** No bureaucracy. No gatekeeping. Just open conversation.

If this solves a problem you have — join us.
If this gives you an idea — share it.
If you want to build something with it — we will help.

→ **[Join the forum](https://github.com/gakelytemp-creator/AISocket/discussions)**

*P.S. We are two people and a lot of enthusiasm. Community is not a nice-to-have — it is the whole point.*
