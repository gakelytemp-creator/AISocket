# AISocket

> From your garden to the Moon — one library.

[![Website](https://img.shields.io/badge/Website-googuly.online%2Faisocket-blue)]([https://googuly.online/aisocket](https://gakelytemp-creator.github.io/AISocket/))
[![GitHub](https://img.shields.io/badge/GitHub-AISocket-black)](https://github.com/gakelytemp-creator/AISocket)
[![Forum](https://img.shields.io/badge/Forum-Discussions-green)](https://github.com/gakelytemp-creator/AISocket/discussions)

AISocket is an open protocol that gives every autonomous body a **semantic passport** — so any LLM can understand, control, and cooperate with any machine, safely.

---

## The Problem

An LLM entering an unknown device is like a human sitting at an unfamiliar SQL terminal — blind. It doesn't know what the device can do, what it must never do, or how to ask for help when it gets stuck.

AISocket solves this with a simple registration: the device declares itself, the LLM reads the passport, and control begins within defined boundaries.

---

## How It Works

**1. Register** — give your device a name and describe it in plain language. AISocket generates a structured prompt and a ready-to-use config file.

**2. Connect** — your device sends a heartbeat to the login server. Any LLM can find it by name.

**3. Control** — the LLM operates within the device's law: permitted actions, forbidden actions, emergency protocol, and autonomous mandate when the connection drops.

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

## Platforms

| Platform | Status |
|----------|--------|
| Python | ✅ Ready |
| Arduino / ESP32 | 🔄 In progress |
| Raspberry Pi | 🔄 In progress |
| Android | 🔄 In progress |
| ROS2 | ⬜ Planned |
| Browser / WebSocket | ⬜ Planned |

---

## Core Concepts

- **Semantic Passport** — every body declares: what it can do, what it must never do, how to ask for help, what to do offline
- **Body Law** — 6-layer command validation: firmware rules → capabilities → emergency → offline mandate → delegation → context
- **Login Server** — devices register by name; LLMs find them by name
- **Autonomous Mandate** — when the connection drops, the device keeps operating within pre-defined boundaries
- **Emergency Protocol** — in life-critical situations, verified rescue agents get limited access; `forbidden_always` still applies

---

## Registry

Register and manage your devices at:
**[googuly.online/aisocket](https://googuly.online/aisocket)**

Create a free account to register devices, edit their prompts and configuration, track project history, and delete or update registrations at any time. Your devices, your data.

---

## The Same Passport — Everywhere

| Context | Example |
|---------|---------|
| 🌱 Garden | lawn mower, irrigation |
| 🏠 Home | lift, security camera |
| 🏙️ City | 17,000 autonomous bodies |
| ⚕️ Crisis | emergency coordination |
| 🌙 Moon | autonomous mandate, 1.3s delay |
| 🔴 Mars | 40 min delay, full autonomy |

---

## Contributing

This belongs to everyone.

- **Code** — open a PR, any platform welcome
- **Test** — run the simulator, report issues  
- **Passport** — add your device to the prompt repository
- **Spread** — YouTube, blog, talk

→ [Join the discussion](https://github.com/gakelytemp-creator/AISocket/discussions)

---

## Constitution

This project is governed by a constitution that protects against centralized control, vendor lock-in, and surveillance misuse.

→ [Read the Constitution](CONSTITUTION.md)

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE)

Free to use. Free to modify. Modified versions must remain free.

---

## We Need You 🙏

We are early. Very early. And that means **every contribution matters enormously**.

This protocol was born from a real need — connecting LLMs to real hardware, safely, on any platform. We built the foundation. Now we need the community to make it live.

**We are looking for:**

- 🔧 **Hardware builders** — Arduino, ESP32, Raspberry Pi, ROS2 — test it, break it, tell us
- 🧪 **Testers** — run the simulator, try the registry, find the edge cases
- 📝 **Writers** — blog posts, tutorials, documentation in any language
- 🎥 **YouTubers & educators** — show the world what this can do
- 🎓 **Students & universities** — this is real research territory: robotics, AI safety, distributed systems
- 💡 **Thinkers** — challenge the constitution, propose improvements, open discussions

**We are genuinely happy to collaborate with anyone who finds this interesting.**
No bureaucracy. No gatekeeping. Just open conversation.

If this solves a problem you have — join us.
If this gives you an idea — share it.
If you want to build something with it — we will help.

→ **[Join the forum](https://github.com/gakelytemp-creator/AISocket/discussions)**

*P.S. We are two people and a lot of enthusiasm. Community is not a nice-to-have — it is the whole point.*
