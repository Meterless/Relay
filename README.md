# Meterless Relay

**Turn natural-language instructions into real desktop workflows.**

Meterless Relay is a Tauri + Rust desktop automation engine that takes a plain-English goal, compiles it into a schema-validated mission plan, executes that plan across real desktop windows, verifies critical steps with vision, and saves outputs as reusable artifacts.

Relay is built for the part of automation most tools still fail at:

**the messy, shifting reality of the actual desktop.**

---

## The Problem

Most automation breaks for boring reasons.

Windows move.  
Focus changes.  
Z-order changes.  
Handles drift after an app restarts.  
A tiny UI change causes a silent failure.  
Brittle scripts assume the world has not moved.

That is why so much automation feels impressive in a demo and fragile in real work.

Relay fixes the root problem by grounding automation in the real desktop state before it acts.

Not vague assumptions.  
Not fuzzy window titles.  
Not blind clicking.

A real workflow engine for real desktop environments.

---

## What Relay Does

You type something like:

> “Open my trading platform, check positions, export today’s report, and save the result.”

Relay does not jump straight into random clicks.

It can:

1. Research the goal when needed
2. Capture the live desktop context
3. Inject tracked windows, Z-order, tools, and procedural memory into the planner
4. Compile a structured `MultiWindowMissionPlan`
5. Repair and normalize the JSON plan
6. Let the user inspect the workflow before execution
7. Resolve stable tracked windows
8. Execute actions through native desktop APIs
9. Verify critical screens with vision
10. Save outputs into a reusable artifact store

The result feels less like **“AI trying stuff”** and more like **a desktop workflow engine that knows what machine it is operating on.**

---

## Why Relay Is Different

### 1. It Plans Before It Acts

Relay compiles every mission through explicit phases:

```text
Goal → Research → Brain Inject → Plan → JSON Repair → Prepare → Execute → Verify → Capture → Complete
