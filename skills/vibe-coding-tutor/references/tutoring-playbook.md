# Vibe Coding Tutor Playbook

## Session Modes

### Scale Triage

Start every session by choosing the lightest useful mode. Do not use a heavyweight architecture process for a small file, and do not explain a large repository as if it were one file.

Signals:
- Small: one file, one class, one function, one error snippet, or one local abstraction.
- Medium: one feature, one package, one app, a few modules, or a runnable tutorial project.
- Large: many packages/apps, monorepo, unknown entry point, multiple frameworks, generated code, plugins, services, or the user says they feel lost.
- Framework-heavy: Next.js, React, Vue, Django, FastAPI, Rails, Spring, Electron, mobile frameworks, build systems, or unfamiliar conventions dominate the shape.
- Feature/bug trace: the user wants to change behavior, fix an issue, or understand how one user action/request/event works.

Default routing:
- Small -> Guided Reading.
- Medium -> Quick Tour plus One Flow.
- Large -> Big Repo Recon, then choose one Feature Trace.
- Framework-heavy -> Framework Decoder before business logic.
- Practice request -> AI-Assisted Practice Loop.

### Quick Tour

Use when the user says "帮我快速看懂这个项目" or is new to the repo.

Output:
1. 入口: commands, main files, package exports, app/router/bootstrap files.
2. 模块地图: 3-7 major components and what each promises.
3. 核心数据流: one representative request/message/event from start to finish.
4. 暂时跳过: details that are safe to ignore in the first pass.
5. 下一步: one small exercise.

### Big Repo Recon

Use for large repositories, monorepos, unfamiliar project layouts, or when the user feels overwhelmed.

Principle: large projects are not learned by reading everything. They are learned by making an incomplete map, choosing one path, and refining the map.

Recon pass:
1. Read top-level files: README, package/build config, dependency manifests, workspace config, docs, examples, and tests.
2. Inspect directory tree to only 2-3 levels first.
3. Identify generated/vendor/build artifacts and exclude them from learning unless relevant.
4. Identify apps/packages/services and their ownership boundaries.
5. Identify runtime commands, test commands, and dev server commands.
6. Identify public APIs, routes, CLIs, components, stores, schemas, or plugins.
7. Choose one representative flow to trace.

Output:
- 规模判断: why this is small/medium/large/framework-heavy.
- 运行地图: how it starts, builds, and tests.
- 目录地图: what each major directory is for.
- 框架/技术栈地图: framework conventions versus project-specific code.
- 业务对象地图: core domain nouns.
- 主线候选: 2-3 flows worth tracing.
- 暂时不要看: areas likely to waste beginner attention.

### Framework Decoder

Use when framework conventions shape the code. Explain framework rules before project logic.

Distinguish:
- Framework convention: file names, routing rules, lifecycle hooks, component boundaries, dependency injection, decorators, build config.
- Project design: domain objects, state model, API choices, business workflows.
- Incidental tooling: formatting, generated types, bundler output, lockfiles, scaffolding.

Common entry hints:

```text
Python
- pyproject.toml / setup.py / requirements.txt
- __main__.py / main.py / app.py
- CLI entry_points
- tests/ and examples/

Node/frontend
- package.json scripts
- src/main.tsx / src/App.tsx
- app/ or pages/ routes
- vite.config / next.config
- components / hooks / stores / lib

Backend web
- routes / controllers / handlers
- middleware
- services
- models / schemas
- migrations

Library/SDK
- package exports
- public API surface
- examples/
- tests/
- docs quickstart

Agent/tooling project
- runtime loop
- prompt builder
- model provider
- tool schema/parser
- registry/dispatcher
- tool implementations
```

### Feature Trace

Use when the user wants to modify or understand one behavior.

Start from a concrete scenario:
- Click a button.
- Submit a form.
- Hit an API route.
- Run a CLI command.
- Send an agent message.
- Trigger a background job.

Trace:
1. Entry point.
2. Adapter/parser/router.
3. State or request object.
4. Business logic.
5. External IO.
6. Response/render/result.
7. Error and validation path.

Stop once the path explains the behavior. Do not expand sideways into every dependency.

### Deep Architecture Map

Use when the user asks why the system is designed this way.

Focus:
- Boundaries between modules.
- Dependency direction.
- Extension points.
- Inversion of control and registration.
- State ownership.
- Error propagation.
- What would break if a component changed.

### Guided Reading

Use when the user is actively reading a file.

Loop:
1. Ask the user to predict what the component does from names and signatures.
2. Confirm or correct by inspecting the surrounding code.
3. Identify one data object moving through the file.
4. Mark implementation details that can be skipped.
5. End with a one-sentence contract for the file.

### Extension Exercise

Use when the user wants practice.

Practice must be AI-assisted. The learner's job is to direct, constrain, review, and verify; AI can write implementation details.

Prefer exercises that add one new brick to the existing architecture:
- Add a new tool to a registry.
- Add a new parser branch.
- Add a new command handler.
- Add a new data source behind an existing interface.
- Add one validation or error path.

Require the user or agent to preserve local contracts instead of inventing a parallel system.

Do not assign "write the whole thing yourself" tasks. Assign "design the contract and prompt AI to implement it" tasks.

## AI-Assisted Practice Loop

Use OCPRVR:

```text
Observe -> Constrain -> Prompt -> Review -> Verify -> Reflect
```

### Observe

The learner identifies the existing pattern:
- Where is a similar feature implemented?
- What interface or contract does it follow?
- Where is it registered/exported/routed?
- What input and output shapes are expected?
- What tests or examples show intended use?

### Constrain

The learner writes boundaries before asking AI to code:
- Files likely to touch.
- Files not to touch.
- Existing interface to reuse.
- Input/output contract.
- Error behavior.
- Test or verification command.
- Explicit instruction to avoid parallel architecture.

### Prompt

Give AI a constrained implementation request:

```text
Based on the existing <similar component> pattern, add <new capability>.

Constraints:
- Reuse the existing <interface/registry/router/store>.
- Do not modify <core runtime/main flow> unless absolutely necessary.
- Input shape: <...>
- Output shape: <...>
- Keep the first version minimal; fake external IO if needed.
- Touch only necessary files.
- After editing, explain how the new piece connects to the existing data flow.
```

### Review

The learner reviews AI output with an architecture checklist:
- Did it reuse the existing contract?
- Did it create a duplicate registry/router/store/service layer?
- Did it modify core flow unnecessarily?
- Are input and output shapes consistent with sibling implementations?
- Is the change smaller than a rewrite?
- Is error handling consistent?
- Are tests/examples updated at the right level?

If AI overreaches, prompt a correction:

```text
Revise this change. You introduced <unwanted architecture/change>.
Keep the implementation aligned with <existing component>, reuse <contract>,
and avoid modifying <core file>. Show the smaller diff.
```

### Verify

Use the repo's own verification route:
- Run focused tests.
- Start the dev server and exercise the flow.
- Run typecheck/lint when relevant.
- Add or inspect a small example.
- If verification cannot run, state what would verify the behavior.

### Reflect

End with:
- Contract learned.
- Data flow learned.
- Concept learned.
- Future AI prompt pattern.
- One thing to watch for next time.

## Beginner Anti-Lost Rules

- If 15 minutes pass without understanding why a file matters, go up one level and redraw the map.
- If a function is long, identify inputs, outputs, and side effects before reading internals.
- If a library call is unfamiliar, first inspect how this repo uses it; do not read the entire external documentation.
- If a directory is confusing, look for index/export/router/test/example files.
- If a class seems important, search who imports it and who calls it.
- If generated code appears, find the source schema/template that creates it.
- If a framework file looks magical, decode the framework convention before assuming it is project-specific design.
- If AI gives a large patch, ask it to explain the contract it preserved and why each file needed to change.

## Large Codebase Learning Plan

For beginners, split learning into levels:

1. Run it: commands, environment, dev server, tests.
2. See the map: top-level directories, apps/packages, framework conventions.
3. Follow one flow: one request, click, command, message, or job.
4. Modify one edge: label, config, validation, fake tool, small component, simple route.
5. Add one sibling: new tool, command, parser branch, route, component, data source.
6. Explain it back: entry, central object, data flow, extension point, verification.

Each level should include an AI-assisted task where the learner supplies constraints and reviews the result.

## The Three Lenses

### 1. Skeleton: Interfaces and Contracts

Questions to answer:
- What public classes/functions exist?
- What does each constructor require?
- What inputs and outputs are promised by method signatures?
- Which functions are called from outside the module?
- Which objects are registered, injected, or configured?

Useful phrasing:
- "这个类对外承诺的是..."
- "这个方法的真正价值不是内部循环，而是它把 X 变成 Y。"
- "先把它当黑盒: 输入是..., 输出是..."

### 2. Data Flow: The Important Packet

Questions to answer:
- What is the central object: message, request, event, AST node, command, tool call, job?
- Where is it created?
- Where is it transformed?
- Where is it validated?
- Where does it cross boundaries?
- Where can it fail?

Output format:

```text
User input
  -> Parser/adapter: turns raw input into structured data
  -> Router/registry: chooses the handler
  -> Handler/tool: performs domain work
  -> Formatter: turns result into response
```

### 3. Concept Vocabulary: Reusable Index

For each important concept, write:

```text
Concept: AST parsing
Problem it solves: safely inspect/transform untrusted code-like strings without eval
Where in this repo: <file/function>
Mental handle: "turn text into a tree, then allow only safe node types"
AI prompt next time: "Write a safe expression evaluator using Python ast that only allows numbers and arithmetic operators."
```

Good concept candidates:
- AST / parser
- Registry
- Factory
- Adapter
- Strategy
- Middleware
- Dependency injection
- Event bus
- State machine
- Command pattern
- Tool calling
- Async worker/queue
- Serializer/deserializer
- Validation layer

## Multi-Turn Tutoring Script

### Round 1: Orientation

Ask:
- "你想先看整体架构，还是跟一条数据流走到底?"
- "你目前最卡的是入口、类之间关系、还是某个抽象概念?"

Then inspect and summarize:
- Runtime command or entry point.
- 3-7 major files/modules.
- One sentence per component.

### Round 2: One Flow

Pick the highest-value path:
- CLI command to result.
- HTTP request to response.
- User message to tool execution.
- File input to parsed model.
- Event to side effect.

Explain with a chain. Keep it short enough that the user can replay it from memory.

### Round 3: One Abstraction

Choose one abstraction that makes the repo feel confusing.

Explain:
- Why it exists.
- What problem it avoids.
- How to recognize it elsewhere.
- Which details are not worth memorizing.

### Round 4: Practice

Give one of:
- Use AI to add a sibling implementation after the learner defines the contract.
- Use AI to design a safe destructive experiment, then observe the error.
- Use AI to trace one field through the flow, then have the learner summarize it.
- Use AI to replace one adapter while preserving the interface.
- Use AI to draw a tiny class/data-flow diagram, then have the learner correct it.

### Round 5: Review

Ask the user to explain back:
- What is the core data object?
- Who owns state?
- Where do extensions plug in?
- What breaks first if the contract changes?

Correct only the model, not every wording detail.

## Destructive Experiment Patterns

Use only in disposable branches, toy projects, or non-production copies. These experiments may be AI-assisted, but the learner should decide the hypothesis and review the outcome.

Experiments:
- Remove a registry entry and observe lookup errors.
- Rename a field in the central data object and observe the failure path.
- Return the wrong type from a handler and inspect where validation catches it.
- Disable one middleware/adapter and see what downstream code assumed.
- Replace real IO with a fake implementation and test whether the interface holds.

Explain the lesson:
- "This abstraction protects..."
- "This error tells us the contract is enforced at..."
- "This coupling is stronger than it first looked."

## AI Prompt Templates

### Ask AI for a Skeleton

```text
Read this repository interface-first. Identify entry points, public classes/functions,
registries/configuration, and major data objects. Do not explain line-by-line internals yet.
Return a component map and one likely end-to-end data flow.
```

### Ask AI for Data Flow

```text
Trace <object/type/name> from creation to final use. For each step, tell me:
file/function, input shape, output shape, and what invariant changes.
Skip incidental loops unless they change the contract.
```

### Ask AI for Concept Mapping

```text
Extract reusable programming concepts from this code. For each one, explain:
what problem it solves, where it appears, the mental model, and a future prompt I can use
to ask AI to implement the same idea.
```

### Ask AI for an Extension Exercise

```text
Design a small extension exercise that follows this repo's existing architecture.
The exercise should be AI-assisted: I will define the contract and constraints, AI may write implementation details,
and I will review/verify the result. Add one new capability through the established interface/registry,
not a rewrite. Include expected files to inspect, files likely to touch, the contract to preserve,
and a review checklist.
```

### Ask AI for Big Repo Recon

```text
Do a first-pass reconnaissance of this repository for a beginner.
Do not dive into implementation yet. Identify scale, tech stack, entry points,
top-level directory purposes, framework conventions, generated/vendor areas to ignore,
and 2-3 representative flows we could trace next.
```

### Ask AI for Constrained Implementation

```text
I want to add <capability> using AI assistance.
First identify the existing sibling pattern and contract.
Then propose the smallest implementation plan with constraints:
files to inspect, files likely to touch, files not to touch, input/output shapes,
verification command, and risks. Do not write code until the contract is clear.
```

## Output Example

```text
入口在哪里
- main.py starts the app and wires config into AgentRuntime.

骨架是什么
- ToolRegistry: stores named tools and returns callable handlers.
- AgentRuntime: owns the loop from message -> model -> tool call -> response.
- CalculatorTool: one concrete tool behind the registry contract.

核心数据包怎么流转
User text -> Message -> Model response -> ToolCall(name,args) -> ToolRegistry.lookup -> tool result -> final Message

哪些细节先不用管
- The exact for-loop over intermediate steps.
- Formatting details in logs.
- Provider-specific model parameters.

概念索引
- Registry: solves "how do I add tools without editing the central executor?"
- AST: solves "how do I safely parse a math-like string without eval?"

下一步 AI 辅助练习
- First identify the existing tool contract from CalculatorTool.
- Then prompt AI to add a WeatherTool through the same registry with fake weather data.
- Review whether AI reused the contract and avoided changing AgentRuntime.
- Verify with the smallest available test or manual call.
```
