# Midterm Study Guide

**AI-Augmented Software Engineering — Fall 2026**

| | |
| --- | --- |
| **When** | Friday, November 6, in class |
| **Format** | 25 multiple-choice questions, 1 hour, closed book |
| **Weight** | 30% of the final grade |
| **Covers** | Lectures 1–5 and the required readings for those weeks |
| **AI use** | None. The midterm is your own work. |

The exam tests whether you understood the *ideas*, not whether you memorized slide text. Most questions ask you to pick the right concept for a situation, tell two similar terms apart, or recall a specific claim from a required reading. Expect roughly five questions per week, with a few that cut across weeks.

---

## How to use this guide

1. Re-read each lecture's slides once (links below), then work through that week's section here.
2. For each **Key terms** entry, make sure you can define it in one sentence *and* say how it differs from its neighbours.
3. Re-read the **required** papers' abstracts and the "What to take away" notes in each `papers-to-read.md`. The exam asks about a reading's main claim and its evidence, not its details.
4. Finish with the **self-check questions** at the end. If you cannot answer one, go back to that week.

The five lectures were taught in this order: Week 1, Week 2, Week 3, Context Management, Codebase Structure. The repository folders number them `01`–`05` with the last two swapped. Nothing on the exam depends on the week numbers.

---

## Week 1 — The AI-Native Software Engineer

Slides: [`lectures/01-setup-environments/`](../lectures/01-setup-environments/) · Readings: [`resources/01-setup-environments/papers-to-read.md`](01-setup-environments/papers-to-read.md)

### Core ideas

- **Engineering is not programming.** Programming is a bounded act (hold the problem in your head, write the solution, make tests pass). Engineering is keeping systems working: requirements, design, validation, change. Coding shrinks with AI; everything else grows.
- **The spectrum: vibe coding → structured AI-assisted → agentic engineering.** The differentiator is *not* whether you use AI; it is **how outputs get verified**. Know the dimensions of the spectrum table: intent specification, verification, codebase understanding, error handling, appropriate scope, risk profile.
  - Vibe coding: casual prompts, "does it seem to work?", copy-paste errors back to the AI, prototypes and hackathons, high risk acceptable for disposable code.
  - Structured AI-assisted: detailed prompts with examples and constraints, manual testing and spot checks, features in established codebases, human judgment at checkpoints.
  - Agentic engineering: formal specs and architecture docs, automated test suites / CI gates / LLM judges, production systems at scale, systematic verification at every stage.
- **The role shift: implementer → orchestrator.** Less time typing; more time thinking, specifying, reviewing and deciding. When the agent gets it wrong, *fix the gap in the spec* rather than *rephrase and hope* (a random walk).
- **Human-in-the-loop is the non-negotiable checkpoint.** You own every commit. The agent is a collaborator, not a co-author. Stay close at high stakes (migrations, architecture, production data).
- **What AI-native engineers actually do.** *Before:* write behaviour, constraints, edge cases and acceptance criteria first; set up context (rules files are infrastructure). *During:* review against criteria, not gut feel; test for agent mistakes (edge cases, error paths, boundaries); diagnose the gap before re-running. *Throughout:* own every commit, invest in context, use AI for all the work (docs, PRs, design exploration).
- **The new skill stack:** spec literacy, context engineering, orchestration, verification discipline, risk ownership, systems thinking, communication and translation, harness engineering.
- **Five emerging patterns (Google I/O 2026):**
  1. *Shift up* — higher altitudes: the *why* (context) over the *what* (code).
  2. *Shift left* — structured intent: intent becomes a source of truth (e.g. `INTENT_SPEC.md`); intent > implementation.
  3. *System design: the environment* — build for continuous feedback and validation; verified output > faster code.
  4. *System design: the workforce* — capability > job title; small cross-functional teams at large scale.
  5. *System design: new values* — intelligent failure > the status quo; adaptability and learning.
- **Juniors in the age of AI.** AI writes the boilerplate juniors used to learn from, and "it's easier than ever to be wrong in a way nobody notices." Habits that build a foundation: reach for the harder problem, go one layer deeper, do the design work, read and write docs, understand every line, own it and keep learning. The skills above any technology: problem-solving, critical thinking, communication, working with AI.

### Numbers and studies to recognise

- DORA 2025: ~90% of software engineers use AI at work; ~40% rely on it a lot; ~3/4 of code at Google is AI-generated.
- Anthropic, *How AI assistance impacts the formation of coding skills* (2026): 52 mostly-junior engineers, Trio task. AI-assisted group was ~2 minutes faster (not significant) but scored **17 percentage points lower** on the knowledge quiz (50% vs 67%, p = 0.010). *Bottom line: AI may make you faster on a task while reducing how much you learn from it.*

### Required readings

- **Peng et al. 2023, *The Impact of AI on Developer Productivity: Evidence from GitHub Copilot*.** Controlled experiment; developers implemented a JavaScript HTTP server with or without Copilot. Copilot group finished **55.8% faster**. Know what it does *not* show: a universal productivity gain, or anything about quality, maintainability, review effort or learning. "Developer productivity" is a measurement choice.
- **Hassan et al. 2024, *Towards AI-Native Software Engineering (SE 3.0)*.** A *vision* paper, not evidence: intent-centric, conversation-oriented development where AI moves from task-level copilot toward teammate. Be able to tell a vision claim from an empirical result.
- **Course reading principle:** for every paper — what is the claim, what evidence supports it, where does the evidence apply and not apply, what would change your mind?

---

## Week 2 — Spec-Driven Development

Slides: [`lectures/02-specs-driven-development/`](../lectures/02-specs-driven-development/) · Readings: [`resources/02-specs-driven-development/papers-to-read.md`](02-specs-driven-development/papers-to-read.md)

### Core ideas

- **The SDLC became a loop.** Traditional SDLC is a line (plan → design → build → test → deploy → maintain). AI-native SDLC cycles in hours around coding AI. *Build shrinks; the work around it grows* (writing intent, spec review, verification, rules and evals). **Code is no longer the bottleneck** — planning, review and deployment set the pace, and human-speed approval steps stall.
- **Six stages, one artifact chain:** `intent.md` (plan; originator approves) → `spec.md` (design; product owner signs off) → `plan.md` (build; engineer interrogates it) → tests the agent can run itself (test; tests stay locked) → AI pre-review + named human approval (deploy) → alerts trigger read-only diagnosis and a PR; the fix starts as a new `intent.md` (maintain).
- **Autonomy goes down as risk goes up.** Development: act freely in a sandbox. Pull request: AI review + code owner. Production: nothing without a named human's approval; **the agent never approves its own work**. Incidents: small → log; larger → diagnose read-only; severe → propose a fix as a PR. Every allow / block / ask decision is logged.
- **Put team knowledge where the agent can read it:** project context file (conventions, commands, recurring mistakes — under a page), skills (team policies, versioned, *advisory*), hooks (scripts that block/allow/log — for rules that must hold with *no exceptions*).
- **User story vs requirements vs spec.**
  - *User story:* "As a [user], I want [goal] so that [reason]." Written by a PM, in user language, answers why and what — too vague to build from.
  - *Requirements:* "a condition or capability needed by a user to solve a problem or achieve an objective" (IEEE). What the system must do, never how. **Functional** (what it does: register, lock after 5 failures) vs **non-functional** (how well: < 300 ms, 99.9% uptime, 10 req/min per IP).
  - *Spec:* a written description of what a system must do and how well, agreed before building. Technical; written by an engineer. **Agents consume specs, not user stories.**
- **Definition of SDD:** a way of building software where a *written specification, not the code, is the source of truth*. Define what and why first; agents plan, build and verify against the spec. Chain: requirements → `spec.md` → `plan.md` → `tasks.md` → code.
- **Why ambiguity costs more with agents.** *Velocity:* a developer writes 50 lines on a wrong assumption; an agent writes 500. *Silence:* a human stops and asks; an agent resolves ambiguity on its own. Why models behave this way: they predict the *most likely* answer, not yours; context is their only memory; they are trained to finish, not ask; early choices compound. "Garbage in, clean-looking garbage out" — Song et al. (2023): many code-generation errors trace to requirements missing from the prompt.
- **Four human checkpoints:** spec review (before planning — highest leverage), plan review (before execution), code review (during execution), deployment review (before production).
- **Tell the agent when to stop and ask:** ambiguity (two valid options), divergence (a test still fails after 3 tries), contradiction (code contradicts the criteria), irreversibility (about to delete or migrate real data).
- **Let the agent interview you first** — answers replace guesses; make it a team activity.
- **Plan Mode is a bridge, not SDD.** Read-only until you approve; review the plan like a PR; its questions reveal gaps in your spec. But it is *transient* (lives in one chat) and *answers how, not what*. Workflow: Plan Mode on every non-trivial task → notice what you correct → write those things in `spec.md` first → use Plan Mode to check the agent read the spec.
- **Three levels of SDD maturity:**
  1. **Spec-first** — write the spec before the agent starts (goal, constraints, acceptance criteria). Use for any task over ~30 minutes of agent work.
  2. **Spec-anchored** — the spec lives in the repo and changes in the same PR, updated first. Use for code that keeps changing.
  3. **Spec-as-source** — people edit only the spec; code is generated from it. Still theoretical at scale; watch, don't adopt.
- **Two tiers of specs.** *Strategic:* rules file, ADRs, system requirements — living documents every session reads. *Tactical:* `spec.md` / `plan.md` / `tasks.md` per change — drive one feature, then stay as history.
- **What good specs look like.** Four headings: **Goal, Constraints, Acceptance criteria, Out of scope.** Beyond the happy path: failure mode, concurrency, observability, rollback. A bad spec ("add a caching layer to improve performance") lets the agent choose library, TTL, keys, invalidation and monitoring for you.
- **The SDD workflow.** One folder per change (`specs/001-feature/`) with `spec.md` (what and why — no file paths or tech choices), `plan.md` (how: approach, trade-offs, files, order), `tasks.md` (small tasks, each with a **done check**). One short prompt per phase: specify → plan → tasks → execute. Without a done check the agent stops too early or never stops; if a done check says "and" more than once, split the task.
- **SDD frameworks:** GitHub Spec Kit (constitution → specify → plan → tasks → implement → converge; open source, works with most agents), Kiro (AWS; EARS requirements → design → tasks; IDE with specs built in), OpenSpec (propose → apply → archive; lightweight on existing code), BMAD Method (analyst/PM/architect/developer agents; simulates a whole team), Tessl (one spec per code file; spec-as-source experiments).
- **Three things to remember:** the substrate changed, the discipline didn't; speed amplifies everything (a bad spec gets built fast too); match the ceremony to the risk.

### Required readings

- **Graziano, *AI-Native Software Engineering*, ch. 5 "Spec-Driven Development" (O'Reilly).** What makes a spec useful to an agent rather than merely descriptive to a human; which parts establish behaviour, constraints, verification and boundaries.
- **Piskala 2026, *Spec-Driven Development: From Code to Contract*.** A practitioner/position paper (not a controlled study). Specs become the source of truth; code is generated or verified against them. Defines **spec-first, spec-anchored, spec-as-source**. SDD has a cost — match rigor to risk, reversibility, domain complexity, coordination needs and lifetime.
- **Optional — Parnas & Clements 1986, *A Rational Design Process: How and Why to Fake It*.** Real design is messy and iterative; document the *rational* design without pretending requirements were always clear. Review must challenge premises, not just syntax and tests.

---

## Week 3 — Anatomy of Coding Agents

Slides: [`lectures/03-anatomy-of-coding-agents/`](../lectures/03-anatomy-of-coding-agents/) · Readings: [`resources/03-anatomy-of-coding-agents/papers-to-read.md`](03-anatomy-of-coding-agents/papers-to-read.md)

### How LLMs work

- An **LLM** is a neural network with billions of parameters trained on huge amounts of text and code to **predict the next token**. It stores statistical patterns, not its training text.
- **Tokens, not words.** `getUserById(userId)` ≈ 7 tokens; ~3–4 characters per token in English prose; a 600-line TypeScript file ≈ 4–5k tokens.
- **One token at a time.** No planning pass, no going back — early mistakes carry through.
- **Attention.** Each token looks at every other token and weights the relevant ones ("it" → "animal" when *tired*, → "street" when *wide*). The **Transformer** (Vaswani et al., 2017, "Attention Is All You Need"): text → tokens → vectors → dozens of attention + feed-forward layers → scores for every possible next token; the chosen token is appended and the pipeline runs again. It won because it reads all tokens in parallel, so it trains at huge scale.
- **Training:** hide the next word, model guesses a probability for each candidate, compare to the real word, nudge billions of weights; repeat for trillions of tokens. The weights are then **frozen** at a cutoff date.
- **Post-training with human preference feedback (RLHF):** generate alternatives → a person picks the better one → a reward model learns the preference → the LM learns to score higher. *Preference does not guarantee correctness.*
- **Post-training with verifiable feedback:** attempt the task → run tests/compilers/formal checks → reward passing results → the model learns strategies that produce verifiable success.
- **Two kinds of knowledge.** *In-weights (parametric):* learned during training, always available, fixed at the cutoff, may be stale or wrong. *In-context (non-parametric):* supplied with the request (prompt, files, docs, tool results), current and authoritative when trusted, uses the context window, not retained.
- **The context window is a budget.** Simple "needle in a haystack" lookup is solid up to the advertised window; harder multi-step reasoning degrades well before the limit.
- **Models are probabilistic.** Same prompt, different equally-correct outputs — even at temperature 0 outputs can vary across runs and hardware. **Test behaviour, not strings** (does it parse, do tests pass, is the edge case handled, does lint pass).

### The model landscape

- **Openness levels:** *fully open* (weights, data, code — most auditable, usually lower ceiling), *open weights* (Llama, Mistral, Qwen, DeepSeek — self-host and fine-tune; training data private), *closed* (GPT, Claude, Gemini — API only; can run in your cloud, never on your own servers). Choose by hard constraints: where data may go, fine-tuning needs, ops effort, vendor lock-in.
- **Kinds of models:** pre-trained (raw foundation), fine-tuned (adapted with task-specific data), reasoning (RL-trained to spend extra compute on step-by-step logic before answering), specialised (e.g. BioBERT, legal).
- **Reasoning models:** chain of thought by default; more tokens and compute (**test-time compute**); slower and costlier (hidden thinking tokens are billed). Use standard models for routine, well-specified work; reasoning models for ambiguous, multi-step, high-stakes work (a race condition, a schema with many invariants).
- Frontier models (Oct 2026) have context windows around **~1M tokens**.

### Why LLMs are good at coding (four reasons)

1. Seen it millions of times (GitHub, Stack Overflow, docs, tutorials).
2. It runs or it doesn't — strict rules give a clear training signal.
3. Boilerplate is predictable (CRUD endpoints, test setup, config files).
4. Code and docs together (source, README, docs and Q&A about the same library). Strongest for widely used languages and frameworks; weaker for internal, one-company frameworks.

### Coding agents under the hood

- **The messages array:** system / user / assistant roles. The API is **stateless** — no memory between calls; your app resends the full history every time, so cost grows with each turn. The **system prompt** is read first on every call — your highest-leverage input.
- **What is an agent?** A language model combined with **tools, context and a loop** — able to pursue a goal over several steps without approval at each step.
- **The agentic loop:** reason → act → observe, until the goal is reached or the run must stop. **ReAct** (Yao et al., 2022): a visible reasoning trace connects each decision to an action and its result.
- **Agent = Model + Harness.** Six components of a coding harness:
  1. **Live repo context** — turns a changing repository into stable prompt context.
  2. **The system prompt.**
  3. **Tool access and use** — read and search (Read, Glob, Grep), change files (Edit, Write), run (Bash), look things up (WebSearch, WebFetch), plan and delegate (Plan Mode, Agent).
  4. **Context reduction** — clip long outputs (first + last lines), dedupe repeated reads (latest only), compress older turns into a summary.
  5. **Session memory** — the model retains nothing between calls; the harness stores state on disk: a full **transcript** (append) and a distilled **working memory** (rewrite).
  6. **Delegation to subagents** — side questions run in parallel in their own context while the main agent keeps working.

### Required readings

- **Vaswani et al. 2017, *Attention Is All You Need*.** Self-attention, multi-head attention, positional information, parallel sequence processing. Be able to explain what attention buys compared with recurrence.
- **Video: *Visual representation of coding agents and their limitations*.** The system *around* the model: context gathering, planning, tool calls, feedback loops, and where they break. Distinguish a **model** failure (knowledge) from a **system / agent-loop** failure.
- **Stanford companions:** *Building a Coding Agent* (video), *Lessons from Building Claude Code*, *Dive into Claude Code*.
- **Reference lineage (know what each adds):** Transformers (2017) → learning from human preferences (Christiano 2017) → BERT pretraining (2018) → GPT-3 in-context learning (2020) → Codex / HumanEval and functional correctness (2021) → chain-of-thought prompting (Wei 2022) → InstructGPT / RLHF (Ouyang 2022) → ReAct (2022) → DPO, optimising directly from preference pairs without a separate reward model (2023) → GRPO, group-relative rewards without a critic (DeepSeekMath 2024) → o1 and test-time reasoning (2024) → DeepSeek-R1 reasoning via RL (2025).
- **Core takeaway:** a coding agent is a *system*, not a single model. Each layer (architecture, training, alignment, loop, tools) adds capability and its own failure modes.

---

## Advanced Context Management

Slides: [`lectures/05-advanced-context-management/`](../lectures/05-advanced-context-management/) · Readings: [`resources/05-advanced-context-management/papers-to-read.md`](05-advanced-context-management/papers-to-read.md)

### Why context engineering

- **The same agent, the wrong output.** "Add an endpoint" → used Moment.js, skipped Zod validation, wrote a unit test instead of an integration test. *Each mistake traces to missing context, not a weak model.*
- **Prompt engineering vs context engineering.** Prompt engineering phrases one request well (one input, one interaction). Context engineering designs *everything the model sees* across the session and the team. Karpathy: "filling the context window with just the right information for the next step."
- **The attention problem.** Every token looks at every other token: n tokens → n × n pairs; at 100k tokens that is 10 billion pairs. Result: a slow decline, not a sudden drop.
- **Context rot.** Symptoms: repeats the same mistake, breaks a rule it agreed to, loses the original goal, code that fit two steps ago. Countermeasures: one session per task, reset between tasks, keep key facts in files, summarise before the window fills, restate key rules each session.
- **Human working-memory parallel:** about four items at once; the budget per item shrinks as context grows.
- **The right-time problem:** present-but-irrelevant context still competes for attention. Load it when the task needs it.
- **Two failure modes:** *too little* (the agent fills gaps with common patterns from training — fine in the abstract, wrong for your system) and *too much* (noise competes for attention; critical lines buried in the middle; slower, costlier, less accurate).
- **Only the user's query is mandatory.** For everything else ask: how often does it improve the output, and what breaks if it is absent? Rarely useful and nothing breaks → load on demand.

### A taxonomy of context components

- **Always on** (loaded before you type; costs tokens every session, so keep it short) vs **on demand** (full skill text, referenced files, retrieved data) vs **custom agents** (same parts packaged under a name: instructions, a chosen model, a restricted tool set).
- **System prompts: precision over volume.** Role and goals, rules, output format. The **"curse of instructions"**: if each rule is followed 95% of the time, all rules are followed 0.95^n — 5 rules → 77%, 10 → 60%, 20 → 36% (Harada et al., 2024). Write rules as testable statements: *when [trigger], the system shall [action].*
- **User input and `@` references:** the request sets the task and its boundary; references pull in exactly the slice you need. Retyping the same context for a recurring task → move it into a rule or skill.
- **Rules, style guides, constraints:** always on; a good rule states its reason ("use date-fns instead of moment.js, because Moment is deprecated and adds 70 KB"). Hierarchy: global preferences → project conventions → file-specific rules.
- **Agent Skills:** an open standard; a reusable package saved with your code that teaches an agent one kind of task. `AGENTS.md` is *always on* (project rules every session); a *skill* is *loaded when needed*. How skills work — **progressive disclosure**: (1) discover: load name + description at startup; (2) decide: load full `SKILL.md` when the task matches; (3) use: open scripts/references/assets only when a step needs them. Or invoke with `/skill-name`.
- **Tools are a context component** (name, parameters, description live in the window and cost tokens on every request; more tools → higher baseline) *and* a way to fetch context. Rule: give a task only the tools it needs; *if a human could not choose between two tools, neither can the agent.* **The model only sees the description** — vague ("reads a file") vs clear (what it does, when to use it, when not to). Anthropic's SWE-bench agent: more time went into tools than the prompt; requiring absolute paths removed a whole class of error.
- **`AGENTS.md`:** a README for agents — one plain Markdown file telling any coding agent how to work on your project. Open format (Agentic AI Foundation / Linux Foundation), 20+ agents, 60k+ projects.
- **Conversation history and memory:** *inside the window* — in-context memory (gone when the session ends, summarised when the window fills); *outside* — long-term memory through files (`PROGRESS.md`, `spec.md`, `tasks.md`), retrieved memory with RAG (searchable index), agent-generated memory (handoff notes).

### Context assembly and discovery

- **The assembly process:** a **fixed part** set before the first message (same in every session) plus what is **added during the session** (files read, test output, tool results, replies). 5,000 tokens of setup leave 5,000 fewer for real work.
- **When an agent ignores a constraint, check in order:** (1) was it loaded? (2) where did it sit — start and end get more attention than the middle; (3) did it stand out? (4) was it contradicted by another rule, tool description or earlier turn? (5) has it been summarised away?
- **Autonomous context discovery:** what you provide (rules, referenced files, system prompts) vs what the agent finds in the codebase before it writes.
  - *Code indexing / semantic search:* matched by meaning; finds related code you did not name; fails on a stale snapshot, mismatched wording, and cannot know what it does not know.
  - *CLI exploration* (`grep -r`, `git log --oneline -20`): best for structural questions, more precise than embeddings; cost — every result stays in the window.
  - *Language servers (LSP):* go to definition, find references, diagnostics; live and symbolic, safer renames; cost — a server per language, confused by runtime-generated code.

### The runtime pipeline and session management

- **The iterative loop** — Reason→Act→Observe, Plan→Execute→Reflect, Think→Do→See — ends when the goal is met, it can't resolve something, or it hits a budget / step limit.
- **Context cost compounds with every call.** Results stay in the window; design tools to return less (the relevant table, a page of results).
- **When to reset a session:** old mistakes return; answers get vague; the window is nearly full.
- **The handoff artifact:** before closing, have the agent write `PROGRESS.md` with three short lists — *Decided / Done / Next*; start the next session from it. Automatic summaries keep the thread but lose detail.
- Raschka: "A lot of apparent 'model quality' is really context quality."

### MCP fundamentals

- **What MCP is:** an open standard that gives LLMs a secure, standardised way to reach external data, applications and services. Introduced by Anthropic in **November 2024**; builds on tool use / function calling. Analogy: a **USB-C port** — one connector instead of a custom cable per device. Solves the **N × M problem** (every model-and-tool pair needing its own connection).
- **Components:** **host** (the AI app containing the LLM, where the user interacts), **client** (inside the host; translates between LLM and server; finds available servers), **server** (the external service supplying data or capabilities). Key idea: *the LLM asks, the client routes, the server acts.*
- **Server features:** resources, prompts, tools.
- **Transport:** messages are **JSON-RPC 2.0**. **stdio** for local resources (a local process started with a command); **SSE** / **Streamable HTTP** for remote endpoints.
- **Benefits:** reduced hallucinations (a clear route to reliable external sources), increased utility and automation, easier connections.
- **Security:** user consent and control; data privacy; **tool safety** (tools can run code — do not trust tool descriptions from unverified servers; ask permission before a tool runs); secure output handling; supply-chain security; monitoring and auditing. The spec says MCP *cannot enforce these at the protocol level* — they fall to the host, the server author and the user.

### Required readings

- **Liu et al. 2023, *Lost in the Middle*.** Multi-document QA and key-value retrieval. Accuracy is highest when the relevant passage is at the **start or end** of the prompt and drops when it is in the **middle** (a U-shaped curve). Longer windows raise the ceiling, not the floor. The single most important fact behind context *management* rather than context *stuffing*.
- **Anthropic Engineering, *Effective context engineering for AI agents* (Sept 2025).** Introduces **context rot**; argues for **just-in-time retrieval** over pre-loading; three techniques for long-horizon work — **compaction, structured note-taking, sub-agent architectures**; system-prompt "altitude"; tool-set design. First-party engineering writing, not a controlled study.
- **MCP specification and announcement.** Hosts, clients, servers; resources, prompts, tools; JSON-RPC transport; security and trust. A tool's description and schema are part of the model's context — writing them well *is* context engineering; descriptions from an untrusted server are untrusted input.
- **Reference (recognise the idea):** RAG (Lewis 2020 — knowledge in an index, not weights), MemGPT (context window as RAM, external storage as disk), RULER (advertised vs reliable context length differ), context-engineering survey, Agentic Context Engineering (the context itself is what gets optimised).

---

## Agentic Codebase Structure

Slides: [`lectures/04-agentic-codebase-structure/`](../lectures/04-agentic-codebase-structure/) · Readings: [`resources/04-agentic-codebase-structure/papers-to-read.md`](04-agentic-codebase-structure/papers-to-read.md)

The lecture's framing: a repository can be *designed for agents*. Each mechanism has a definition, types, how it works, anatomy and examples. Know which mechanism to reach for and, above all, **which ones merely guide the model and which ones actually enforce**.

### Skills

- **A skill teaches an agent how to perform a specific task.** Three parts: instructions (a repeatable procedure), resources (scripts, references, templates), storage (files tracked with the project). Open standard supported by multiple agents.
- **Types** (origin, location and invocation are separate axes): built-in or custom; project or user; automatic (selected by relevance) or explicit (`/skill-name`); nested project skills.
- **How they work:** discover → select (by name and description) → read (the skill's instructions enter context) → use resources (supporting files load when needed). `/skill-name` attaches to one message; a Custom Mode lasts the session.
- **Anatomy** (`.cursor/skills/add-endpoint/SKILL.md`): frontmatter (`name`, `description`), procedure (the body), supporting files (`scripts/`, `references/`, `assets/`). Optional fields: `paths`, `disable-model-invocation`.
- **Examples:** add-endpoint, fix-bug (reproduce, add a regression test), deploy-app, file-specific skill. *The lab skills prescribe a test-first procedure; they do not enforce compliance.*

### Rules

- **Rules supply reusable instructions in the agent's context:** project knowledge, relevant context, shared guidance. **A rule guides the model. It does not execute a check.**
- **Types:** project rules (`.cursor/rules/*.mdc`), user rules (personal, across projects), team rules (managed in a dashboard), `AGENTS.md` (plain Markdown; nested files combine with parent instructions).
- **How rules load:** always (every session), intelligent (agent selects by description), file-scoped (a matching file is in context), manual (`@rule-name`).
- **Anatomy** (`.cursor/rules/api.mdc`): `description`, `globs` (matches files/directories), `alwaysApply`. Project rules require `.mdc`; a plain `.md` in that folder is ignored.
- **Rules vs skills:** rules state constraints and conventions ("keep ticket error bodies consistent") and load always / by files / by relevance / by mention. Skills describe a task procedure ("follow the endpoint workflow"), load when selected or invoked, and can package resources. *Both guide the model. Neither guarantees the result satisfies the instructions.* Keep rules focused; use formatters and linters for mechanical style checks.

### Hooks

- **Hooks run at defined events in the agent's work:** observe (record what happened), act (run a script after an event), control (allow or block supported actions). The host invokes a registered hook when its event occurs.
- **Types:** execution — command-based (runs a program) or prompt-based (a model assesses a condition); event categories — agent events (during a session) and tab/application lifecycle events.
- **How they work:** event → input (host sends event data as JSON on stdin) → execution (the command reads and evaluates it) → response (the host handles the result on stdout).
- **Anatomy** (`.cursor/hooks.json`): the event (`stop` = completion), the `command`, options `timeout` and `loop_limit`. The event determines the script's input and allowed response fields.
- **Examples:** after a file edit → run formatting; before a shell command → check whether it is allowed; after a completed turn → run the validation script; on validation failure → request another attempt with `followup_message`. The lab caps follow-ups at two.
- **Rules vs hooks:** a rule is an instruction the model reads ("do not run `git push`") — compliance depends on the agent following it. A hook is event-triggered execution (a shell-permission hook *rejects* a prohibited command). Coverage and failure settings matter; permissions and access controls are still needed for security boundaries.

### Subagents

- **A subagent handles delegated work in a separate context:** assignment (a bounded task from the parent), separate work (its own instructions and context window), result (a final report to the parent). The parent supplies the relevant information.
- **Types:** built-in (Explore — searches and analyses code; Browser) and custom (project- or user-scoped); **foreground** (parent waits) vs **background** (work continues independently). Task type and execution mode are separate choices.
- **How they work:** assign → work → report → continue. Delegation may be automatic or explicit.
- **Anatomy** (`.cursor/agents/reviewer.md`): identity (`name`, `description`), execution (`model`, `readonly`, `is_background`), instructions (task and expected report, e.g. "return ACCEPT or REVISE with reasons").
- **Examples / patterns:** planner (identify affected files, tests, risks), reviewer (check the diff against requirements and evidence), verifier (run checks, report what passed), parallel investigation (independent questions in separate contexts). A focused assignment and a defined report make the result useful.

### MCP and external tools (as covered in this lecture)

- MCP connects agents to external tools and data through a shared protocol: client (the host's connection), server (exposes capabilities), external system (the underlying data or operation).
- **Connection types:** stdio (local process started with a command), server-sent events, streamable HTTP.
- **How it works:** connect (configure and authenticate) → discover (host receives capabilities) → call (agent selects a tool) → return (tool supplies a result). Cursor asks for tool approval by default.
- **Configuration** (`.cursor/mcp.json`, global `~/.cursor/mcp.json`): a server name inside `mcpServers`; local process = `command`, `args`, optional `env`; remote = `url` with headers/auth.
- **APIs vs MCP vs skills:** an API exposes operations your code calls; MCP is a server exposing capabilities through a common agent protocol; a skill is a task procedure explaining how to complete work with available tools. *A skill can use an MCP tool; that server may call an application's API.*
- Example servers: Jira/Linear (issues), Notion/Confluence (docs), Datadog/Sentry (monitoring), Redshift (databases), Context7 (library docs), Arize (experiment tracking). Choose trusted servers; give each connection only the access it needs.

### Cloud agents

- Environment setup comes before implementation work: configure → install → run.
- Access: secrets via the supported secret store (prefer short-lived identity tokens), network allow-list, avoid dependencies on unreachable services.
- `AGENTS.md` for project orientation (commands, links to testing/debugging notes); skills for detailed procedures. Commit project instructions and skills with the repository. Rules at user, team and repository level — place instructions at the level where they apply.
- Tools: identify required systems, provide connections (tools or MCP servers), allow the needed permissions, verify the agent can use each tool. Improve tools by observing how the agent uses them, finding missed arguments or distracting output, and adjusting the interface.

### Required readings

- **Yang et al. 2024, *SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering*.** Introduces the **agent-computer interface (ACI)**: the commands, feedback formats and guardrails through which a model acts on a repository. Redesigning the interface *without changing the model* materially changed how often real GitHub issues were resolved. Principles: simple commands, concise feedback, guardrails against common mistakes (e.g. a file viewer that shows a limited window; an edit command that runs a linter and rejects broken edits). *An agent's behaviour is a product of model and interface — you control the interface.*
- **Gloaguen et al. 2026, *Evaluating AGENTS.md: Are Repository-Level Context Files Helpful?*** Controlled comparison of no context file vs LLM-generated vs developer-written. Headline: context files **generally did not improve task success** and raised inference cost by **more than 20%** on average. A context file is context — it competes for the same attention budget, so every line should change a decision the agent would otherwise get wrong.
- **Practitioner companions:** [agents.md](https://agents.md/) format; Anthropic *Agent Skills* (`SKILL.md`, progressive disclosure); Anthropic *Writing effective tools for agents* (fewer, well-scoped tools with descriptions that prevent specific mistakes).
- **Reference (know the one-line finding):** *Agent READMEs* — developers mostly write test procedures and implementation details, rarely security or performance. *Guardrails Beat Guidance* — **negative constraints help, positive directives tend to hurt**, largely independent of topic. *On the Impact of AGENTS.md* — repos with one showed lower median runtime and fewer output tokens (efficiency, not success; partly disagrees with Gloaguen). *Cursor Rules* taxonomy — conventions, guidelines, project information, LLM directives, examples. *Agentless* — a fixed localize/repair/validate pipeline with no autonomous tool use was competitive; harness structure can substitute for agent-discovered structure. *NeMo Guardrails* — programmable, deterministic rails around a model rather than prompt text.
- **Reading principle:** every instruction is a hypothesis about a failure mode. What mistake does it prevent? Is it enforced by code or only stated in prose? What does it cost in tokens? What evidence would show it helped?

---

## Cross-cutting themes

These ideas appear in more than one week, and the exam likes them.

1. **Verification is the differentiator.** Vibe coding vs engineering (W1), acceptance criteria and done checks (W2), test behaviour not strings (W3), hooks over rules (Codebase Structure).
2. **Guide vs enforce.** Rules, skills, `AGENTS.md`, system prompts and specs *guide* the model. Hooks, linters, tests, locked test files and permission systems *enforce*. The evidence (SWE-agent, Guardrails Beat Guidance, NeMo) favours enforcement and negative constraints for anything that must always hold.
3. **The context window is a finite budget with uneven attention.** Lost in the middle; context rot; the curse of instructions; always-on vs on-demand; progressive disclosure for skills; tool descriptions cost tokens; design tools to return less.
4. **Agents guess fast and silently.** A human writes 50 lines on a bad assumption, an agent writes 500 — and writes tests for its own guess. So: specs, interviews, stop conditions, and reviewing against criteria.
5. **Autonomy scales inversely with risk.** Sandbox → PR → production → incidents; a named human approves production; the agent never approves its own work.
6. **Agent = model + harness.** The same model behaves differently with a different interface, context, tools and loop. Many "model" failures are context or interface failures.
7. **Evidence literacy.** Know which readings are controlled experiments (Copilot study, Lost in the Middle, SWE-agent, Evaluating AGENTS.md, Anthropic skill-formation study) and which are vision or practitioner pieces (SE 3.0, Piskala, Anthropic engineering posts, MCP announcement) — and what each kind can and cannot prove.

---

## Required-reading checklist

Tick each off once you can state its main claim and the kind of evidence behind it.

- [ ] Peng et al. — GitHub Copilot productivity experiment (55.8% faster on one task)
- [ ] Hassan et al. — SE 3.0 vision paper
- [ ] Graziano — *AI-Native Software Engineering*, ch. 5 (Spec-Driven Development)
- [ ] Piskala — Spec-Driven Development: From Code to Contract (spec-first / spec-anchored / spec-as-source)
- [ ] Vaswani et al. — Attention Is All You Need
- [ ] Video — Visual representation of coding agents and their limitations
- [ ] Liu et al. — Lost in the Middle
- [ ] Anthropic — Effective context engineering for AI agents
- [ ] MCP specification overview, architecture, tools, security
- [ ] Yang et al. — SWE-agent and the agent-computer interface
- [ ] Gloaguen et al. — Evaluating AGENTS.md

---

## Self-check questions

Answer these without looking. Each is in the style of the exam. Answers are at the bottom.

1. A developer pastes an error message back into the chat, accepts whatever comes out, and ships it because "it seems to work." Which point on the spectrum is this, and what single factor places it there?
2. The Copilot study reported a 55.8% speed-up. What does that number *not* tell you, according to the reading notes?
3. In the Anthropic skill-formation study, which difference between groups was statistically significant: coding speed or quiz score?
4. Which artifact does an agent consume, and which is "too vague to build from": a user story, a requirements list, or a spec?
5. Name the four headings every spec should start from.
6. A team keeps its spec in the repo and updates it in the same PR as the code, spec first. Which SDD maturity level is this?
7. Which of these is a reason to make the agent *stop and ask*: (a) a test has failed once, (b) two valid designs exist and it cannot pick, (c) a linter warning appeared.
8. Why is Plan Mode "a bridge, not SDD"? Give two reasons from the slides.
9. What is the difference between in-weights and in-context knowledge, and which one is fixed at the training cutoff?
10. Why does the cost of a long agent session grow with every turn?
11. Which harness component clips, dedupes and compresses tool output?
12. What does RLHF teach a model, and what does it *not* guarantee?
13. Which type of model should you use to reformat JSON, and which for a race condition — and what is the cost of the second type?
14. If each of 10 rules is followed 95% of the time, roughly what is the chance all 10 are followed?
15. Where in a long prompt does a model attend *least* well, according to Liu et al.?
16. Rank the three steps of progressive disclosure for a skill, from what loads at startup to what loads last.
17. An agent ignored a constraint that was definitely in its rules file. Give three things to check, in order.
18. In MCP, which component contains the LLM, which routes requests, and which performs the action?
19. Which MCP transport is used for a local process, and what message format does MCP use?
20. A rule says "Never run `git push`." The agent ran it anyway. Which mechanism would have *prevented* it, and why?
21. What is the key difference between a rule and a skill in terms of *when they load*?
22. What did SWE-agent change to improve issue resolution — the model or the interface?
23. What was the headline finding of *Evaluating AGENTS.md* on task success and cost?
24. According to *Guardrails Beat Guidance*, which polarity of rule tends to help and which tends to hurt?
25. A subagent is configured with `is_background: true` and `readonly: true`. What do those two fields control?

### Answers

1. Vibe coding; outputs are verified only by "does it seem to work?" — verification is the differentiator.
2. Nothing about quality, maintainability, review effort, collaboration, learning or user value; and it does not generalise beyond that task and population.
3. The quiz score (17 points lower with AI, p = 0.010). The ~2-minute speed difference was not significant.
4. Agents consume specs; the user story is too vague to build from; requirements are partially usable.
5. Goal, Constraints, Acceptance criteria, Out of scope.
6. Level 2, spec-anchored.
7. (b) ambiguity. Divergence is a test still failing after three tries, not one.
8. It is transient (lives in one chat, a teammate cannot pick it up) and it answers *how*, not *what* — it takes your description at face value and will not surface missing requirements.
9. In-weights (parametric) knowledge is learned during training and fixed at the cutoff; in-context knowledge is supplied with the request and is current but not retained.
10. The API is stateless: the full message history is resent on every call, so each turn re-sends everything before it.
11. Context reduction.
12. What people prefer; it does not guarantee correctness.
13. A standard model for JSON reformatting; a reasoning model for the race condition — slower and more expensive because hidden thinking tokens are billed.
14. About 60% (0.95^10).
15. The middle; accuracy is highest at the start and end.
16. Name + description at startup → full `SKILL.md` when the task matches → scripts, references and assets only when a step needs them.
17. Was it loaded? Where did it sit (middle vs start/end)? Did it stand out? (Then: was it contradicted? Was it summarised away?)
18. Host contains the LLM; client routes; server acts.
19. stdio; JSON-RPC 2.0.
20. A hook (e.g. a shell-permission hook) — it is event-triggered execution that rejects the command, whereas a rule is only an instruction the model reads.
21. Rules load always / by file glob / by relevance / by `@mention`; skills load when selected by description or invoked with `/skill-name`.
22. The interface (ACI) — the model was held constant.
23. Context files generally did not improve task success and raised inference cost by more than 20% on average.
24. Negative constraints help; positive directives tend to hurt.
25. `is_background` sets whether the parent waits for the result; `readonly` restricts the subagent from making changes.
