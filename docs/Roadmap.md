# Roadmap - Where we might go

This roadmap describes the current direction of the project, not a fixed commitment. Later milestones may change as we learn from earlier ones.

## Completed: Project Foundation

* [x] Set up Python development environment
* [x] Create Git repository
* [x] Connect repository to GitHub
* [x] Create and run initial Python program
* [x] Establish project vision and engineering principles

## Milestone 1: Send a Prompt to One LLM

**Outcome:** The application can send a predefined prompt to one LLM and display the response in the terminal.

This establishes the smallest end-to-end LLM interaction before adding user input or additional functionality.

### Acceptance Criteria

Milestone 1 is complete when:

* The application uses one LLM provider.
* A predefined prompt is sent to the LLM.
* The returned response is displayed in the terminal.
* Provider-specific API logic is kept outside `main.py`.
* The API key is supplied outside source code and is not committed to Git.
* Missing credentials produce a clear, understandable error.
* No user-entered prompt is required yet.
* No session history, persistent storage, multi-provider support, configuration framework, web interface, or other later-milestone functionality is added.
* Appropriate automated tests cover the new behavior without requiring a real paid API call where practical.
* The application is run successfully against the real provider.
* README setup/run instructions are updated if the implementation changes what a user needs to configure or run.
* Relevant tests pass before the milestone is considered complete.

### Explicit Non-Goals

This milestone does not include:

* interactive prompting
* multiple LLM providers
* prompt comparison
* response history
* persistent storage
* structured data Q&A
* generalized provider abstractions
* a `src/` hierarchy unless implementation reveals a concrete need


## Milestone 2: Interactive Prompting

**Outcome:** A user can enter a prompt in the terminal, send it to the LLM, and see the response.

At this point, the application becomes a simple but genuinely usable LLM Playground.

## Milestone 3: Session History

**Outcome:** A user can make multiple requests and review previous prompts and responses during the current session.

History only needs to be retained while the application is running. It does not need to survive application restarts. Persistent storage should be introduced later only if there is a demonstrated need for it.

## Milestone 4: Compare LLM Responses

**Outcome:** A user can send the same prompt to two LLMs and compare their responses.

Provider-specific implementation should remain localized so adding or replacing an LLM does not require rewriting unrelated parts of the application.

## Milestone 5: Compare Prompts

**Outcome:** A user can experiment with different prompts against the same task and compare the resulting responses.

The exact interaction design should be determined based on what we learn from using earlier milestones.

## Milestone 6: Structured Data Q&A

**Outcome:** A user can ask natural language business questions about a small, predefined dataset (perhaps 2-3 CSVs) and receive answers grounded in that data.

The implementation approach should be determined based on what we learn from earlier milestones. This milestone should begin with the simplest useful approach rather than assuming a particular database, query-generation method, or Chat BI architecture in advance.

## Milestone 7: Evaluation

**Outcome:** A user can evaluate responses using explicit criteria rather than relying only on informal comparison.

The evaluation approach should be designed when we reach this milestone rather than assumed in advance.

## Milestone 8: Reliability and Usability

**Outcome:** Common failures are handled clearly and the application is straightforward for a non-developer to configure and use.

Review error handling, setup instructions, configuration, and README usability based on what we have learned from using the application.

## Testing

Testing is part of every milestone rather than a final milestone.

Each new behavior should receive appropriate tests, and relevant tests should pass before a milestone is considered complete.

## Future Chat BI Lab scope

**Notes:** 
* simple candidate architecture: User question → LLM generates SQL → application runs SQL → results go back to LLM → LLM explains results
* goal: keeping "the LLM" and "the source of truth" as distinct - The model can interpret, reason, generate queries, and explain, but the actual numbers should come from the data system.
