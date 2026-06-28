# Official reference navigation (local index)

This file is the **entry index** for the skill: first decide whether you are solving a BDD behavior-modeling problem, a Gherkin scenario-writing problem, or a Cucumber.js execution problem, then choose the matching local reference.

## Which reference should you read first?

- **To clarify required behavior, boundaries, and collaboration language**: read `bdd-practice-reference.md`.
- **To write/fix `.feature` files or discuss scenario quality and anti-patterns**: read `gherkin-cucumber-reference.md`.
- **To run scenarios or debug configuration, hooks, or result semantics**: read `cucumber-js-reference.md`.
- **To explain to a team “why we write it this way”**: first cite the source-fidelity and writing-standards sections in `SKILL.md`, then add external official links as needed.
- **If you are not sure where to start**: read this file first, choose a local reference from the responsibility boundaries below, and only open official external documentation when the local references are insufficient.

## Local reference responsibility boundaries

### `bdd-practice-reference.md`

- Focus: BDD as a collaboration and requirements-clarification method (Discovery / Formulation / Automation).
- Questions it answers:
  - What real business behavior should this scenario verify?
  - Are the requirement and boundaries already clarified?
  - Are counterexamples and unresolved questions recorded?
- Suitable stages: requirements clarification, review, Story slicing.

### `gherkin-cucumber-reference.md`

- Focus: maintainable Gherkin writing (Feature/Rule/Scenario/Scenario Outline, Given/When/Then, Tags, Data Tables).
- Questions it answers:
  - Are the statements written in business language rather than UI/API implementation detail?
  - Can the scenario run independently?
  - Are there frequent repeated step phrases or technical formulations?
- Suitable stages: writing scenarios, reviewing writing, refactoring test language.

### `cucumber-js-reference.md`

- Focus: Cucumber.js execution concerns (project structure, step definitions, World, hooks, configuration/Profiles).
- Questions it answers:
  - Is the run `undefined`, `pending`, `failed`, or `passed`?
  - What are the order and semantics of hooks, timeouts, filters, and tags?
  - Which kind of runner configuration needs to be located?
- Suitable stages: automation implementation, troubleshooting, preparation before CI integration.

## External official documentation paths (when local references are insufficient)

When the local references are not enough, prefer these external paths in order:

1. **Definition and practice first**
   - Behavior-driven development — Wikipedia: <https://en.wikipedia.org/wiki/Behavior-driven_development>
   - Cucumber BDD Guide: <https://cucumber.io/docs/bdd/>
   - Discovery Workshop: <https://cucumber.io/docs/bdd/discovery-workshop/>
   - Example Mapping: <https://cucumber.io/docs/bdd/example-mapping/>
   - Who does what / Three Amigos: <https://cucumber.io/docs/bdd/who-does-what/>
   - Myths about BDD: <https://cucumber.io/docs/bdd/myths/>
2. **Gherkin semantics and writing quality**
   - Gherkin Reference: <https://cucumber.io/docs/gherkin/reference/>
   - Step Organization: <https://cucumber.io/docs/gherkin/step-organization/>
   - Writing better Gherkin: <https://cucumber.io/docs/bdd/better-gherkin/>
   - Anti-patterns: <https://cucumber.io/docs/guides/anti-patterns/>
   - Step Definitions: <https://cucumber.io/docs/cucumber/step-definitions/>
   - Cucumber API/reference: <https://cucumber.io/docs/cucumber/api/>
3. **Cucumber.js configuration and behavior**
   - Cucumber state / World: <https://cucumber.io/docs/cucumber/state/>
   - Cucumber.js docs index: <https://github.com/cucumber/cucumber-js/tree/main/docs>
   - Configuration: <https://github.com/cucumber/cucumber-js/blob/main/docs/configuration.md>
   - Profiles: <https://github.com/cucumber/cucumber-js/blob/main/docs/profiles.md>
   - Hooks: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/hooks.md>
   - World: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/world.md>
   - JavaScript 10-minute tutorial: <https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript>

## Quick decision rules

1. If a local file can answer the question, do not open external links first.
2. Consult the official website only when:
   - you need exact CLI/formatter/plugin/reporter/concurrency/retry/sharding behavior;
   - behavior after a version upgrade is uncertain (Node / Cucumber / Cucumber.js);
   - you need to assert an exact official parameter boundary.
3. Always confirm first: **does the BDD problem come before the tool?**
