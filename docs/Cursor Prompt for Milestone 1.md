*This file is only stored here temporarily because I have a period without access to my primary laptop. Once development begins remove this file.*

You are helping implement Milestone 1 of the LLM Playground project.

Before doing anything, read the project documentation in `docs/`, especially:

* `Vision.md`
* `Principles.md`
* `Architecture.md`
* `Development-Guide.md`
* `Roadmap.md`
* `Decision-Log.md`

Also inspect the existing code and README.

## Current Goal

Implement Milestone 1: send one predefined prompt to one LLM and display the response in the Mac Terminal.

Use the Milestone 1 acceptance criteria in the project documentation as the definition of done.

## Before Coding

Do not modify files yet.

First:

1. Restate the goal in your own words.
2. Describe the simplest implementation that satisfies the current milestone.
3. Recommend one LLM provider for this first implementation and explain why.
4. Identify any external package you recommend adding and why it is necessary.
5. Identify every file you expect to create or modify.
6. Explain how the API key will be handled without putting secrets in source code or Git.
7. Describe how you would test the behavior without unnecessarily making real API calls.
8. Identify any proposed choice that conflicts with the existing architecture, principles, or development guide.
9. Identify any decisions that would be expensive to reverse later.

Do not implement anything until I approve the plan.

## Implementation Constraints

When implementation is approved:

* Make the smallest reasonable change.
* Keep high-level orchestration readable in `main.py`.
* Keep provider-specific API details outside `main.py`, using a small module such as `llm_client.py`.
* Do not introduce generalized multi-provider architecture.
* Do not add a configuration framework, `src/` hierarchy, persistent storage, interactive prompting, or unrelated functionality.
* Do not externalize the predefined prompt unless doing so clearly improves the current implementation.
* Do not install dependencies without approval.
* Do not commit secrets.
* Propose README updates if setup, configuration, or run instructions change.

## Verification

Before declaring Milestone 1 complete:

1. Add or update appropriate tests.
2. Run the relevant tests.
3. Run the application against the real LLM provider.
4. Report exactly what was tested and the results.
5. Report any limitations, assumptions, or known issues.
