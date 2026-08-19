# Architecture - How does the work flow in this application and how are the files organized?

This document describes the current architecture of LLM Playground and the major boundaries that shape the system.

The architecture should remain simple and evolve as requirements become concrete.

## System Overview

LLM Playground is a small Python command-line application.

Its initial purpose is to:

1. obtain or define a prompt
2. send the prompt to an external LLM service
3. receive the response
4. display the response in the terminal

The initial application flow is:

```text
main.py
   ↓
llm_client.py
   ↓
External LLM service
```

The LLM is an external service used by the application. It is not itself part of the application's core logic.

## Component Responsibilities

### `main.py`

`main.py` coordinates the high-level application flow.

It should make the application's behavior easy for a human reader to understand.

Its responsibilities may include:

* defining or obtaining the current prompt
* requesting a response from the LLM client
* displaying the response
* coordinating later behavior such as repeated prompts or session history

Provider-specific API details do not belong in `main.py`.

### `llm_client.py`

`llm_client.py` owns communication with the external LLM service.

Its responsibilities may include:

* obtaining the credential required by the provider
* making the provider API call
* handling provider-specific request and response formats
* returning the useful response to the rest of the application

Keeping provider-specific behavior in this module allows the rest of the application to remain largely independent of the details of a particular LLM provider.

## Secrets and Configuration

Secrets must remain outside source code and source control.

For the initial one-provider implementation:

* the API key is supplied through the runtime environment
* `llm_client.py` retrieves the API key
* `main.py` does not need to know how provider authentication works
* the selected model may remain close to the provider implementation until model selection becomes application behavior

No separate configuration layer is currently required.

## Project Structure

While the application remains small, the Python modules will stay at the repository root.

The current intended structure is approximately:

```text
README.md
main.py
llm_client.py

docs/
    Vision.md
    Principles.md
    Roadmap.md
    Architecture.md
    Development-Guide.md
    Decision-Log.md
    Lessons-Learned.md

tests/
```

A `src/` directory may be introduced later if the number of Python modules makes the repository root harder to navigate.

## Prompts

Trivial prompts may remain directly in the code when that is easiest to understand.

Prompts may become separate version-controlled project artifacts when they become substantial, reusable, independently editable, or important to understanding application behavior.

Their eventual location has not yet been decided.

A top-level `prompts/` directory may be appropriate if prompts are intended to be visible or editable project artifacts.

A location within application source may be more appropriate if prompts function primarily as internal implementation resources.

## Application State

The application should own only the state required by the current milestone.

Milestones 1 and 2 require little state beyond the current prompt and response.

Milestone 3 introduces session history:

```text
session
├── prompt
│   └── response
├── prompt
│   └── response
└── ...
```

Session history only needs to exist while the application is running.

Persistent storage is not currently required.

## Multiple LLM Providers

A later roadmap milestone includes comparing responses from multiple LLMs.

The current architecture supports that future direction by keeping provider-specific behavior outside `main.py`.

The exact multi-provider design has not yet been chosen and will be revisited when multiple providers become a current requirement.

## Structured Data / Chat BI Direction

A future milestone may allow users to ask natural-language questions about structured data.

One candidate architecture to explore is:

```text
User question
    ↓
LLM generates query
    ↓
Application executes query against data
    ↓
Query results
    ↓
LLM explains results
    ↓
User
```

This is a possible future architecture, not a current design decision.

A central principle for this future direction is that the LLM and the source of truth should remain distinct.

The model may:

* interpret questions
* generate queries
* reason about returned data
* explain results

The authoritative numbers should come from the underlying data system rather than from the model itself.

The implementation approach will be chosen when the Structured Data Q&A milestone becomes current.

## Current Architectural Decisions

* The application uses an external LLM service.
* `main.py` coordinates high-level application behavior.
* Provider-specific communication lives outside `main.py`.
* The initial provider integration should be isolated in a small module such as `llm_client.py`.
* Secrets remain outside source code.
* The LLM client initially owns retrieval of its required API credential.
* No separate configuration layer is currently required.
* No `src/` hierarchy is currently required.
* No multi-provider abstraction is currently required.
* Trivial prompts do not require separate files.
* Persistent storage is not required for session history.
