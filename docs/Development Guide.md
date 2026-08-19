# Development Guide - What to do before, during and after making a change

This document describes the workflow for making changes to LLM Playground.

It applies to AI coding assistants and human contributors.

The project's engineering principles are defined in `Principles.md`, and the current system design is described in `Architecture.md`.

## Before Making Changes

Before implementing a significant change:

1. Read the relevant project documentation, including:

   * `Vision.md`
   * `Principles.md`
   * `Architecture.md`
   * `Roadmap.md`

2. Restate the problem in your own words.

3. Identify the simplest solution that satisfies the current requirement.

4. Explain the proposed approach.

5. Identify the files you expect to create or modify.

6. Identify any new external dependencies.

7. Explain any significant decisions that would be expensive to reverse.

8. Point out anything that conflicts with the current architecture or engineering principles.

9. If the requested change introduces unnecessary complexity, propose a simpler alternative.

Do not begin significant implementation until the proposed approach has been reviewed and approved.

## During Implementation

* Make small, understandable changes.
* Explain significant changes before making them.
* Do not make unrelated improvements.
* Do not build functionality that is not required for the current goal.
* Do not introduce architecture solely for anticipated future requirements.
* Do not install packages without explaining why they are needed and receiving approval.

## Architecture Changes

Preserve the current architecture unless a concrete requirement justifies changing it.

When considering a new module, folder, abstraction, dependency, configuration layer, or other structural change, evaluate it using:

### Change Test

What concrete change would this structure make easier?

### Comprehension Test

Does it make the system easier for a human to understand?

### Responsibility Test

Are the separated pieces performing genuinely different jobs?

If a proposed architecture change conflicts with `Architecture.md`, surface that conflict before implementation.

Do not silently change the architecture documentation to legitimize an implementation choice.

## External Dependencies

Before adding an external dependency:

1. Explain what current requirement it solves.
2. Consider whether the standard library or existing project code can reasonably solve the same problem.
3. Keep the dependency localized to the part of the application that needs it.
4. Avoid unnecessary abstraction layers around it.
5. Ask for approval before installation.

## Configuration and Secrets

* Never put API keys, credentials, passwords, or tokens into source code.
* Never commit secrets to Git.
* Keep configuration close to the code that uses it until a separate configuration layer clearly improves comprehension or reuse.
* Do not create configuration files, settings objects, or configuration frameworks without a current need.

For the current one-provider architecture, the LLM client owns retrieval of the provider API key from the runtime environment.

## Prompts

Trivial prompts may remain inline when that is easiest to understand.

Move prompts outside application code when they become:

* substantial
* reusable
* independently editable
* important project artifacts

Do not create prompt-loading infrastructure before there is a current requirement for it.

## Project Structure

Keep the repository structure simple while the codebase is small.

Do not introduce directories such as `src/`, `services/`, `providers/`, or `config/` merely because those structures are common in larger applications.

Introduce organizational layers when they improve navigation, comprehension, or support a concrete requirement.

## README and User Documentation

Treat README changes as part of implementation when a change affects how the project is:

* installed
* configured
* run
* used

When such a change occurs, propose the appropriate README update as part of the same work.

Keep the README organized for a non-developer reader.

Essential setup and run instructions should be gathered clearly near the top rather than scattered across the document.

Do not generate documentation changes for internal implementation details that do not affect a reader, user, or future maintainer.

## Verification

Before declaring a change complete:

1. Add or update tests appropriate to the new behavior.
2. Run the relevant tests.
3. Run the application when appropriate.
4. Report exactly what was tested.
5. Report the results.
6. Identify remaining limitations, assumptions, or known issues.

Do not declare work complete merely because code was generated successfully.

## Human Review

A human reviews every application change.

Coding assistants must not make consequential architectural decisions silently.

When uncertain about an architectural or product decision, surface the question rather than choosing a more complex implementation by default.
