# Gherkin and Cucumber quick reference: writing high-quality scenarios

> Goal: turn `.feature` files from “looks runnable” into “readable, maintainable, and reusable” practice guidance.

## 1. Write the syntax skeleton first, then fill in behavior details

- `Feature`: one business capability.
- `Rule`: groups scenarios under the same rule.
- `Scenario`: one concrete executable example.
- `Scenario Outline + Examples`: several input sets for the same kind of scenario.
- `Background`: business background shared by scenarios.
- `Tags`: annotate classification dimensions and execution strategy.

## 2. Core semantics

- `Given`: establishes prerequisite context (observable business state).
- `When`: triggers an event (behavior/action).
- `Then`: asserts an observable outcome.
- `And` / `But`: continue the previous step type for readability.
- `*`: can be used as a list-like step keyword and is not a separate business semantic category.

Note: `Given` and `Then` are not interchangeable in business meaning; keep scenario expression semantically consistent.

## 3. Common writing rules (frequent corrections)

1. Keep language consistent; avoid using multiple phrases for the same business fact.
2. Use real concrete data (dates, quantities, amounts, objects).
3. **What, not how**: keep behavior language.
4. One step, one thing.
5. A `Scenario` runs independently and does not depend on order.
6. Use `Scenario Outline` instead of repeated copy-paste.
7. Keep `Background` short and avoid implementation details.

## 4. Common anti-patterns

- Writing UI interaction scripts: details such as “click a button” and “fill in a field” appear directly in the main statement.
- Putting technical parameters directly into `Given`.
- Losing control of reused/repeated step wording (`Given`/`When` are repeated but mean different things).
- Using `Background` for test-environment setup details.
- One step contains multiple business actions (conjunction steps).

## 5. Rewrite example

### Old (technical)

```gherkin
Scenario: Discount works
  Given a user has discount flag
  When the user enters "user1" into username field
  Then the discount should be shown
```

### New (behavior-focused)

```gherkin
Scenario: Discount expires after campaign
  Given Carla has a 20% summer discount
  And the campaign ends on 2026-08-31
  When Carla checks out on 2026-09-01
  Then the summer discount is not applied
```

## 6. Structured troubleshooting path

- Too much repeated wording: check for synonymous expressions first.
- Rule boundaries are unclear: add a negative case under `Rule` or `Examples`.
- Tags are over-generalized: split tag dimensions.
- The example is too long: consider splitting it into multiple scenarios.

## 7. Connecting to external links (key points first)

- Gherkin reference: keywords, structure, and example rules.
- Step organization: step organization and reuse boundaries.
- Writing better Gherkin: language-quality guidance.
- Step definitions: binding relationship with steps.
- Anti-patterns: long-term maintenance risks.

## 8. Scenario decision mnemonic

- Does this scenario answer an observable business question?
- Can business, testing, and development understand it together?
- Is it easy to run and debug independently?
- Does it have clear failure semantics (negative cases/counterexamples)?

## 9. Directory and file convention (default)

```text
features/
  *.feature
  step_definitions/
  support/
    hooks.js
```

The important thing is not the file name; it is whether the scenario is readable.
