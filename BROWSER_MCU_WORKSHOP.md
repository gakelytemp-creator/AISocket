# Browser-First Microcontroller Workshop

**Status:** architectural target / not yet implemented in this repository.

AISocket should make it possible to take a supported microcontroller from an empty or existing firmware project to a tested, flashed AISocket body **from the browser, without requiring a desktop IDE**.

The browser is the workshop.

It is not the body's safety boundary.

The device firmware must still enforce its own Body Law locally.

---

## Goal

For supported boards, the intended user flow is:

~~~text
open browser
→ select / identify board
→ load or create passport
→ edit firmware
→ inspect generated capabilities and Body Law
→ compile
→ flash
→ open serial / telemetry console
→ run self-test
→ inspect traces
→ revise
~~~

The entire visible development workflow should be available through the web interface.

A human, LLM-assisted editor, or other authorized participant may help prepare the firmware, but the resulting body remains locally responsible for time-critical and safety-critical constraints.

---

## Browser responsibilities

The browser workshop should eventually provide:

- source editor;
- board and toolchain selection;
- passport editor;
- Body Law / permission-frame editor;
- compile diagnostics;
- firmware build;
- direct flashing where the browser/device transport permits it;
- serial / telemetry console;
- device discovery;
- version and configuration inspection;
- self-test invocation;
- flight-recorder inspection;
- trace export;
- firmware hash / version visibility;
- rollback or recovery workflow where supported.

The aim is that a beginner should not first need to install and configure a traditional embedded IDE before experimenting with AISocket.

---

## Transport

Possible browser-device transports include technologies such as Web Serial and WebUSB where supported.

The exact transport is board- and browser-dependent and must remain replaceable.

AISocket should not confuse transport with the protocol itself.

~~~text
browser workshop
      ↓
transport adapter
      ↓
bootloader / firmware
      ↓
AISocket body
~~~

A board that uses another transport should still be able to expose the same higher-level development workflow.

---

## Compilation

The preferred direction is browser-resident compilation where practical, including WebAssembly-hosted toolchains or equivalent browser-side machinery.

If a particular toolchain cannot reasonably run inside the browser, a remote build service may be used as an implementation fallback while keeping the **user workflow** browser-only.

In either case the interface should make the build provenance visible:

- board target;
- toolchain version;
- source revision;
- build options;
- firmware hash;
- signing status where applicable.

A remote compiler must not become a hidden source of firmware authority.

---

## Safety boundary

The browser may help author or inspect Body Law.

It must not replace Body Law.

~~~text
browser suggestion
      ↓
compile / validate
      ↓
firmware
      ↓
LOCAL ENFORCEMENT
~~~

Servo limits, watchdogs, emergency behavior, offline rules, hard motion envelopes, and other application-specific safety mechanisms remain local to the body.

Closing the browser tab, losing the network, or replacing the assisting model must not erase the body's non-negotiable constraints.

---

## Knowledge and traces

The browser workshop should make it easy to move between:

~~~text
known board / device knowledge
→ firmware work
→ physical test
→ trace
→ reusable knowledge
~~~

AISocket itself records evidence and device traces.

When generalized knowledge is later promoted into Noepedia, that promotion should occur through Noepedia's Socratic Daimonion rather than by treating every firmware log or model interpretation as settled knowledge.

Likewise, future browser tooling may request a task-relevant knowledge cut from Noepedia through the Daimonion instead of making the microcontroller project carry a giant static manual.

---

## First target

A useful first target is a small Arduino / ESP32-class board with:

- one browser-supported connection path;
- a minimal passport;
- one sensor;
- one actuator or harmless observable output;
- local Body Law;
- compile + flash;
- serial telemetry;
- self-test;
- a small flight-recorder trace.

The prototype should prove the end-to-end workflow before adding a large board catalog.

---

## Short formula

> **Program the body from the browser.**
>
> **Keep the law in the body.**
>
> **Keep the evidence visible.**
