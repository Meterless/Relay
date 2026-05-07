meterless-gaia/README.md
<div align="center">

<img src="./assets/gaia-hero.png" alt="Meterless Gaia hero image" width="100%" />

# Meterless Gaia

### The local-first cognitive operating system for real work.

**Most AI tools generate answers. Gaia executes reality.**

[Website](https://meterless.ai) · [Docs](./docs) · [Examples](./examples) · [License](./LICENSE.md)

</div>

---

## What is Gaia?

**Meterless Gaia** is a local-first cognitive operating system that can see your environment, reason across what is happening, and act on your computer through a shared native execution layer.

Give it one instruction and it can:

- open apps
- browse the web
- read what is on screen
- click, type, and scroll
- run long multi-step work
- remember context across sessions
- route work across local and cloud models
- turn outputs into persistent artifacts

Gaia is not a chatbot with desktop tools attached.

It is a desktop-native cognitive system built around shared world state, long-horizon reasoning, memory, perception, and native execution.

---

## The Problem

Most AI products still stop too early.

They generate text.  
Maybe they call an API.  
Maybe they summarize what you should do next.  
Then they hand the work back to you.

That is fine for chat.

It is not enough for reality.

Real work happens across apps, windows, tabs, files, forms, long-running projects, and tasks that drift over time.

**Gaia exists because the intelligence layer should not live inside a chat box. It should live where work actually happens.**

---

## The Moment It Clicks

You type:

> “Research how to use Google AI Studio and build a particle simulation.”

Gaia can:

1. Open your browser through a native control session
2. Ground itself with live browser capture and search
3. Navigate to AI Studio
4. Write the right prompt
5. Generate the simulation
6. Return the result without you touching the keyboard

That is the shift.

**Not just telling you what to do. Actually doing it across the desktop.**

---

## How Gaia Works

```text
Input
  ↓
Preprocessor Routing
  ↓
Parallel Memory + Brain Collection
  ↓
Cortex Task Resolution
  ↓
Provider Readiness Validation
  ↓
Dynamic Enrichment
  ↓
Prompt Composition
  ↓
Desktop Session Target Injection
  ↓
Route: Swarm | Auto-Steward | Markovian | Standard Dispatch
  ↓
Response + Post-Turn Observation

Gaia is not one model call with a fancy skin.

It is a routed system.

Core services include:

brainPreprocessor
brainInjectionService
dynamicEnrichmentService
promptComposerService
modelOrchestrator
desktopAutomationService
post-turn H-MEM observation
Why Gaia Is Different
1. Gaia Can Actually Use Your Computer

Gaia controls desktop apps through a session-based desktop model.

Once a session is started, the active target window is cached and injected into the reasoning path. Gaia can execute typed desktop actions such as:

focus
click
type
keys
scroll
move
bounds

This same execution layer is reused by chat, missions, tools, desktop control, and routed desktop work.

2. Gaia Sees What Is Happening

Gaia folds screen perception into its reasoning path through Observer mode, local vision, browser grounding, and dynamic enrichment.

It can reason from:

live browser capture
recent page captures
screen state
local vision models
bookmarks and history
search evidence
active windows
workspace artifacts

This means Gaia does not only respond to what you typed.

It can ground itself in what is actually visible.

3. Gaia Does Not Collapse on Long Tasks

Long tasks usually break AI systems.

The prompt grows.
Context decays.
The original goal fades.
The system loses the thread.

Gaia uses a Markovian Thinking Engine to carry compressed state across long reasoning runs instead of blindly resending the entire conversation history.

That lets Gaia keep working across long horizons without collapsing under context growth.

4. Gaia Runs Like a System, Not a Prompt

Gaia’s cognitive model is built around Project Eywa, a 12-brain architecture split across four layers:

Layer	Role
Perception	Gather signals from the environment
Intelligence	Interpret patterns and reason
Autonomy	Shape goals, recover, and adapt
Execution	Produce artifacts and actions

Brains coordinate through ORAE loops:

Observe → Reason → Act → Evaluate

This is how Gaia can adapt mid-task instead of acting like a single frozen assistant call.

5. Gaia Operates on Shared WorldState

Every brain, tool, and interface reads and writes to a shared live WorldState.

That world state can track:

open windows
active artifacts
user goals
environmental signals
tool registries
memory
current workspace context

The planner and executor are not working from different realities.

They share the same ground truth.

6. Gaia Remembers

Gaia uses a 3-tier H-MEM system so it does not start every session as a blank slate.

It can preserve:

user context
constraints
preferences
prior decisions
project memory
contradictions
reusable patterns

The result feels less like a stateless assistant and more like an evolving operating system.

7. Gaia Can Run Locally

Gaia supports multiple local-first execution paths:

WebLLM
Ollama
local vision models
embedded GGUF sidecar runtime
local workspace files
native Tauri storage

Sensitive workflows can stay on your machine when needed.

Feature Snapshot
Capability	What it does	Why it matters
Native Desktop Control	Acts on real apps through typed desktop actions	Gaia can do work, not just describe it
Observer + Vision	Reads screen and browser state	Reasoning stays grounded in visible evidence
Markovian Engine	Carries compressed state across long tasks	Long workflows do not collapse
Project Eywa	Coordinates 12 specialized brains	Gaia behaves like a system, not a single prompt
Shared WorldState	Keeps brains, tools, and interfaces aligned	Planning and execution stop drifting apart
H-MEM	Preserves memory across sessions	Gaia does not restart from zero
Dynamic Enrichment	Injects live search, browser state, and capture	Responses are tied to current evidence
Universal Viewer	Hosts generated artifacts in durable interfaces	Outputs become usable surfaces
Universal @Mentions	Pulls files, tools, windows, brains, and modes into a turn	Context and execution can be steered precisely
Local-First Runtime	Supports WebLLM, Ollama, and embedded GGUF	Sensitive work can stay local
What You Can Do With Gaia
Manage email and daily desktop workflows
Run research-to-execution pipelines
Automate repetitive app-based tasks
Complete long multi-step work without losing the thread
Build and test outputs across browser, code, and desktop tools
Ground decisions in live browser and screen evidence
Steer the system through modes like @Control, @Swarm, @Research, and @Explorer
Run local workflows for sensitive data
Example Use Cases
Cross-Application Workflow Automation

A recruiter can ask Gaia to pull a job description from an ATS, research salary benchmarks, update a spreadsheet, and draft outreach emails while remembering the company’s compensation philosophy.

Learn a Tool, Then Use It

Ask Gaia to research how to set up a campaign in Google Ads, learn the flow, then operate the interface using your parameters.

AI Tool Orchestration

Gaia can coordinate between AI tools, such as using one product for images, another for copy, and another for layout, then combine the results in a workspace.

Multi-Day Project Continuity

Gaia can support architecture reviews, research projects, competitive analysis, and thesis writing that span multiple sessions.

Local-First Sensitive Work

Legal documents, medical records, financial models, HR data, and proprietary code can be processed through local-first paths when cloud use is not appropriate.

Architecture
React + TypeScript + Vite
        ↓
Tauri Desktop Shell
        ↓
Shared WorldState
        ↓
12-Brain Cognitive Stack
        ↓
H-MEM + Markovian Reasoning
        ↓
Model Orchestrator
        ↓
Desktop Automation + Browser Grounding
        ↓
Universal Viewer + Workspace Artifacts

Core runtime layers:

Layer	Stack
Frontend	React 19, TypeScript, Vite
Desktop Shell	Tauri 2 + Rust
Embedded Runtime	Axum, Tokio, llama-cpp
Persistence	IndexedDB, Tauri JSON storage, workspace files
Providers	Google, Anthropic, OpenAI, Groq, Mistral, WebLLM, Ollama, GGUF
Cognitive Services	Brains, H-MEM, context registry, enrichment, prompt composition, mission orchestration
Quickstart
git clone https://github.com/meterless-ai/meterless-gaia.git
cd meterless-gaia
npm install
npm run tauri:dev
Requirements
Node 18+
Rust 1.77+
Tauri toolchain
Windows or macOS desktop environment recommended for full native experience

Browser mode is useful for UI iteration.
Tauri desktop mode unlocks native storage, workspace files, shell integration, backup, and desktop automation.

Suggested First Run

Try:

Check my unread emails and draft replies for me to review.

The intended flow:

Launch Gaia
  ↓
Give it one real instruction
  ↓
Let it ground itself
  ↓
Let it reason and act
  ↓
Review before sensitive actions
How Gaia Fits the Meterless Stack
Gaia = The Mind
Swarms = The Workforce
Relay = The Hands

Use Gaia when you want:

broader autonomous reasoning
long-horizon intelligence
memory and continuity
environment awareness
desktop-native action

Use Swarms when you want:

parallel agents
many variants
DAG planning
merge and verification

Use Relay when you want:

reliable desktop execution
tracked windows
vision-verified workflows
reusable automation plans
FAQ
Is Gaia just a chatbot with tools?

No. Gaia is built around shared WorldState, a routed turn pipeline, a 12-brain cognitive stack, H-MEM memory, Markovian long-horizon reasoning, native desktop control, and persistent artifact surfaces.

Can Gaia control desktop apps?

Yes. In Tauri mode, Gaia uses a session-based desktop model and typed desktop action facade for focus, click, type, keys, scroll, move, and bounds.

What keeps Gaia from losing track on long tasks?

The Markovian engine carries forward compressed state instead of growing the prompt forever. Silent Observer helps detect semantic drift while tasks are underway.

Does Gaia work offline?

Gaia supports local-first paths including WebLLM, Ollama, local vision, and embedded GGUF inference. Not every workflow is offline-only, but the architecture supports sensitive local execution.

Is Gaia one provider under the hood?

No. Gaia routes across cloud and local providers through a model orchestrator.

The Takeaway

Most AI tools answer.

Gaia can answer, see, remember, route, ground itself, and act.

That is the shift.

Meterless Gaia turns the assistant from something you talk to into something that can operate in the same reality you do.

Image Slots

Add these images to /assets when ready:

/assets/gaia-hero.png
/assets/gaia-worldstate.png
/assets/gaia-12-brains.png
/assets/gaia-desktop-control.png
/assets/gaia-universal-viewer.png

Recommended sections:

![Gaia WorldState](./assets/gaia-worldstate.png)
![Gaia 12-Brain Architecture](./assets/gaia-12-brains.png)
![Gaia Desktop Control](./assets/gaia-desktop-control.png)
License

See LICENSE.md
.
