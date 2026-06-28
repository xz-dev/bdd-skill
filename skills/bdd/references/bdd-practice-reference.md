# BDD practice reference: the BDD collaboration loop

> Purpose: answer “what behavior, requirements, and acceptance criteria must be clarified?” before deciding whether to proceed to Cucumber.js automation.

## 1. Core stance (before tools)

- BDD is not “a specific test framework”; it is a behavior-specification method centered on collaboration.
- The goal is for business and development to form **shared understanding**:
  - the same goal;
  - clear rule boundaries;
  - executable examples that can be broken or updated by counterexamples.
- Automation is a means, not the definition. Cucumber/Gherkin can be an implementation approach, but they are not BDD itself.

## 2. Discovery: clarify behavior before implementation

In Discovery, resolve these first:

- What business problem are we actually solving?
- Which rules, boundaries, and exceptions apply?
- Which questions remain unanswered?

Recommended outputs:

- Story
- Rules
- Examples
- Questions

### Common triggers

- The team disagrees about whether “the same requirement” means the same thing.
- A new story keeps changing and has not stabilized.
- Written scenarios still lead to repeated arguments about boundary behavior.

### Quick judgment

- Ask first: Who / What / Why.
- Clarify first: what counts as success? How are failure cases defined?
- Preserve first: assumptions that cannot be confirmed; do not write them into confirmed rules.

## 3. Formulation: turn discovery into communicable specifications

### Example Mapping model

- **Story (yellow card)**: describes the goal or story.
- **Rules (blue cards)**: acceptance rules and boundary conditions.
- **Examples (green cards)**: verifiable positive and negative examples.
- **Questions (red cards)**: questions still awaiting confirmation.

### Three Amigos

- **Product/business**: value and scope.
- **Testing/quality**: boundaries and failure paths.
- **Development**: implementation constraints and feasibility.

Recommended minimal output:

```markdown
## Story
As a <actor>
I want <capability>
So that <benefit>

## Rules
- R1: ...
- R2: ...

## Examples
- Example: <concrete executable example>
  - Given ...
  - When ...
  - Then ...

## Questions
- [ ] ...

## Out of scope
- ...
```

### User Story and Acceptance Criteria

- A User Story answers “who / needs what / why it is valuable.”
- Acceptance Criteria must be verifiable and at least describe:
  - observable outcomes;
  - boundary conditions;
  - counterexamples.

## 4. Automation: close the loop with feedback

Typical rhythm for each small behavior:

1. Write a scenario or rule example (do not try to cover everything immediately).
2. Run it and see `undefined`.
3. Add step definitions.
4. See a failure (assertion or boundary failure).
5. Implement the smallest change that makes it pass.
6. Refactor and add key boundary examples.

Automation checks whether behavior is executed correctly; it does not replace requirements clarification.

## 5. Common anti-patterns

- Adding scenarios after code is written (the loop is reversed).
- Replacing business language with technical actions.
- Creating run-order dependencies between scenarios.
- Treating unanswered questions as confirmed rules.
- Replacing scenario abstraction with large data tables.

## 6. When to return to official sources

- For `Discovery / Formulation / Automation` and practice frameworks: Cucumber BDD documentation / Three Amigos / Example Mapping.
- For anti-patterns and writing style: Cucumber Better Gherkin / Anti-patterns.
- For version-specific or implementation details: confirm with the corresponding official documentation.

## 7. Compact external entry list

- Wikipedia: Behavior-driven development: https://en.wikipedia.org/wiki/Behavior-driven_development
- Cucumber BDD Guide: https://cucumber.io/docs/bdd/
- Cucumber Discovery Workshop: https://cucumber.io/docs/bdd/discovery-workshop/
- Cucumber Example Mapping: https://cucumber.io/docs/bdd/example-mapping/
- Cucumber Who does what: https://cucumber.io/docs/bdd/who-does-what/
- Cucumber Myths: https://cucumber.io/docs/bdd/myths/
- Cucumber Better Gherkin: https://cucumber.io/docs/bdd/better-gherkin/
- Cucumber Anti-patterns: https://cucumber.io/docs/guides/anti-patterns/
- User story: https://cucumber.io/docs/terms/user-story/
