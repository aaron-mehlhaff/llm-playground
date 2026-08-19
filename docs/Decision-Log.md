# Decision Log - What we decided and why

This log records consequential project decisions, why they were made, the alternatives considered, and the conditions that should trigger reconsideration.

## 2026-08-07: Use Python

### Decision

Use Python as the primary programming language for LLM Playground.

### Why

* Python is readable and relatively easy to debug.
* It has a strong ecosystem for LLM development.
* It keeps the learning focus on software engineering and architecture rather than language mechanics.
* It fits naturally with the broader data-science context of the project.

### Alternatives considered

* Other general-purpose languages such as JavaScript/TypeScript, Go, or Rust.
* No strong alternative was required by the current project goals.

### Revisit when

Reconsider only if Python creates a concrete limitation for the project's requirements.

## 2026-08-07: Keep the Application Terminal-Based Initially

### Decision

Use the Mac Terminal as the initial user interface.

### Why

* A terminal interface keeps the project simple.
* It avoids introducing web or GUI frameworks before they are needed.
* It keeps the learning focus on application structure, LLM integration, testing, and architecture.
* The first milestones do not require a richer interface.

### Alternatives considered

* Web application.
* Desktop GUI.
* Notebook-based interface.

### Revisit when

Reconsider when a milestone becomes genuinely awkward in the terminal, such as comparing multiple responses or presenting structured data in a way that materially benefits from a richer interface.

## 2026-08-18: Separate Application Orchestration From LLM Provider Logic

### Decision

Keep high-level application flow in `main.py` and isolate provider-specific LLM communication in a separate module such as `llm_client.py`.

### Why

User interaction and external API communication are meaningfully different responsibilities.

Keeping provider-specific details outside `main.py` makes the overall application flow easier for a human to understand and reduces coupling between the application and a particular LLM provider.

### Alternatives considered

* Put all logic directly in `main.py`.
* Introduce a larger services or provider abstraction immediately.

### Revisit when

Reconsider if the boundary stops improving comprehension, or when multiple providers create requirements that justify a different structure.

## 2026-08-18: Do Not Introduce a `src/` Hierarchy Yet

### Decision

Keep the small number of Python modules at the repository root for now.

Do not introduce nested folders such as `src/`, `services/`, `providers/`, or `config/` yet.

### Why

The codebase is currently too small for those organizational layers to improve navigation.

A flatter structure makes the project easier to scan and avoids adding folders that merely redistribute simple code across more locations.

### Alternatives considered

A conventional structure such as:

```text
src/
    llm_playground/
        main.py
        services/
        providers/
        config/
```

### Revisit when

Reconsider when the number of Python modules makes the repository root visually cluttered or when a new organizational layer clearly improves navigation or comprehension.

## 2026-08-18: Keep the API Key Outside Source Code and Let the LLM Client Retrieve It

### Decision

Supply the LLM provider API key through the runtime environment.

`llm_client.py` should retrieve the key directly rather than requiring `main.py` to retrieve and pass it.

### Why

* Secrets must stay outside source code and Git.
* Provider authentication is an implementation detail of the LLM integration.
* Keeping credential handling inside the LLM client allows `main.py` to remain focused on application flow.
* A separate configuration system is not currently necessary.

### Alternatives considered

* Hard-code the API key in source code.
* Have `main.py` read the environment variable and pass the key to `llm_client.py`.
* Create a dedicated configuration or settings module.

### Revisit when

Reconsider if configuration becomes shared across multiple components, provider selection becomes application behavior, or dependency injection would materially improve testing or flexibility.

## 2026-08-18: Keep Trivial Prompts Inline for Now

### Decision

Do not move the initial predefined prompt into a separate prompt file.

Trivial prompts may remain inline while that is the clearest implementation.

### Why

A separate file and loading mechanism would add structure without improving comprehension for a single simple prompt.

The project's principle of keeping important prompts outside code should apply when prompts become substantial or meaningful project artifacts, not to every string literal.

### Alternatives considered

* Create a top-level `prompts/` directory immediately.
* Store prompts inside application source.
* Create prompt-loading infrastructure in advance.

### Revisit when

Reconsider when prompts become substantial, reusable, independently editable, user-facing, or important to understanding application behavior.

## 2026-08-18: Treat Structured Data Q&A as a Future Direction, Not a Committed Architecture

### Decision

Include Structured Data Q&A as a future roadmap direction without committing now to a particular Chat BI implementation.

One candidate architecture to explore later is:

```text
User question
    ↓
LLM generates query
    ↓
Application executes query against authoritative data
    ↓
Results return to the LLM
    ↓
LLM explains results
    ↓
User
```

### Why

The direction gives LLM Playground a meaningful future path for exploring data-grounded reasoning while preserving flexibility.

A key architectural idea is to keep the LLM distinct from the source of truth: the model may interpret, generate queries, reason, and explain, while authoritative numbers come from the underlying data system.

The current project has not yet produced enough evidence to choose SQL generation, a database, a semantic layer, or another Chat BI architecture.

### Alternatives considered

* Commit immediately to SQL generation.
* Introduce SQLite or another database now.
* Design a full Chat BI architecture before reaching the Structured Data Q&A milestone.
* Leave structured data entirely outside the roadmap.

### Revisit when

Reconsider when the Structured Data Q&A milestone becomes current and earlier milestones have provided enough experience to evaluate the simplest useful architecture.
