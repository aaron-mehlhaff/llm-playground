# Engineering Principles - How the AI and I work together

These principles describe how we make engineering decisions for LLM Playground.

They apply whether implementation is performed by a human or an AI coding assistant.

## Human Responsibility

The AI may act as a senior software architect and implementation partner.

I remain responsible for understanding and approving the system and its changes.

I should be able to understand the purpose and overall behavior of the code even if I could not have written every implementation detail myself.

## Simplicity

The goal is not to produce the most code.

The goal is to produce a system that is easy to understand, easy to extend, and easy to maintain.

* Prefer the simplest solution that satisfies today's requirements.
* Build only what is required for the current goal.
* Make the smallest reasonable change.
* Prefer readable code over unnecessary abstractions or frameworks.
* Do not add speculative functionality merely because it may be useful later.

## Architecture Should Reduce Complexity

Architecture should compress complexity for the reader rather than merely redistribute it across more files, folders, abstractions, or configuration layers.

Create boundaries when they make responsibilities or application flow easier to understand.

Do not separate code merely because separation is possible.

## Design for Change Without Building the Future

Favor decisions that keep future options open.

Design for change does not mean implementing future changes now.

Before adding an abstraction or architectural layer, ask:

* What concrete change would this make easier?
* Does it make the system easier for a human to understand?
* Are the separated pieces performing genuinely different responsibilities?

Important decisions that are expensive to reverse should receive more deliberate consideration than decisions that are easy to change later.

## Application Flow Should Remain Visible

The high-level behavior of the application should remain easy for a human to follow.

For the current architecture, `main.py` should make the orchestration of the application visible.

Implementation details should be extracted when they begin to obscure that flow, not merely because they could live in another function or module.

## Keep External Dependencies Localized

External dependencies should be localized so they can be replaced without rewriting unrelated parts of the application.

Do not add abstraction layers solely to make dependencies theoretically replaceable.

A dependency should earn its place by solving a current requirement.

## Distinguish Application Choices From Implementation Details

Information representing application behavior or user choices should generally flow through the application explicitly.

Information required only for a component to perform its internal job may remain within that component.

For example, a user-selected model would be an application choice, while an API credential required internally by an LLM client is an implementation prerequisite.

## Documentation Is Part of the System

Documentation should remain useful to humans as the software evolves.

The README should make the project understandable and runnable by a non-developer.

Architecture documentation should describe how the system works rather than merely mirror whatever code happens to exist.

When implementation reveals that a documented assumption is wrong, reconsider the decision rather than silently rewriting history.

## Security

Secrets must remain outside source code and source control.

Never commit API keys, credentials, passwords, or tokens.

Authentication and other security machinery should not be introduced until required.

## Verification

Writing code is not sufficient evidence that a change works.

Changes should be verified in a way appropriate to their behavior, including tests and running the application when relevant.

