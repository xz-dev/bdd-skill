---
name: bdd
description: Use Behavior-Driven Development (BDD) as a collaboration/specification practice, with Cucumber/Gherkin and Cucumber.js as the bundled executable-specification reference. Use when defining behavior, examples, acceptance criteria, .feature files, Cucumber.js step definitions, or reviewing whether automation still expresses business behavior rather than implementation details.
version: 0.2.0
author: Xiangzhe and AI assistant
license: MIT
metadata:
  hermes:
    tags: [bdd, behavior-driven-development, examples, shared-understanding, cucumber, gherkin, acceptance-tests, executable-specifications, javascript]
  source:
    primary_definition: "Behavior-driven development — Wikipedia: https://en.wikipedia.org/wiki/Behavior-driven_development"
    cucumber_docs: "https://cucumber.io/docs/"
    cucumber_javascript_tutorial: "https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript"
---

# Precompiled BDD (Behavior-Driven Development) Manual

## Quick use: BDD writing and testing steps

1. **Clarify behavior first**: write down Who / What / Why, business rules, concrete positive and negative examples, and unanswered questions; do not start from a test framework or UI steps.
2. **Draft Gherkin**: express the `Given` context, `When` event, and `Then` observable outcome in domain language; run the wording through the quality gate in section 7 before writing glue code.
3. **Run the specification for feedback**: run `.feature` files with Cucumber/Cucumber.js and first observe `undefined`, `pending`, or `failed` results to prove the scenario can drive the missing behavior.
4. **Add step definitions and the smallest implementation**: step definitions only connect scenarios to system behavior; production code should only do enough to pass the current example.
5. **Refactor and add boundaries**: keep scenario language stable, extract helpers/World/hooks, add important boundary cases or counterexamples, and report the red/green process plus unresolved questions.

If you are only reviewing BDD/Gherkin, stop at steps 1–2 and the checklist in section 14. Enter steps 3–5 only when the user explicitly asks for implementation or testing.

## Preflight decision: do not default to Cucumber

Use this small decision filter before treating something as a BDD/Cucumber candidate:

- **Stable, clear behavior**: the code or behavior to be tested is not temporary scaffolding, pure framework code, migration glue, or an exploratory implementation that has not taken shape yet.
- **Business purpose first**: the scenario explains a business purpose in the project, user intent, or an observable outcome, not internal implementation details.
- **Sentences fit the project domain**: after writing a BDD sentence, check whether it helps people imagine — and genuinely fits — this project's actual real use cases.
  - If the sentence is abstract or fragmented, or is merely a natural-language translation of a technical test, first rewrite the scenario or reconsider whether this point needs a BDD test at all.

## 0. The standard definition comes before tools

**Behavior-driven development — Wikipedia:** <https://en.wikipedia.org/wiki/Behavior-driven_development>

> “Behavior-driven development (BDD) is an agile software development method centered around collaboration between business and IT professionals that have a stake in finding a solution for a complex problem. The core objective is to achieve a shared understanding of the problem.”

> “BDD involves use of a domain-specific language (DSL) using natural-language constructs ... that can express the behavior and the expected outcomes.”

This skill starts from that definition: **BDD is an agile development method centered on collaboration, shared understanding, business language, concrete examples, and expected behavior**. BDD can be implemented with Cucumber/Gherkin, other frameworks, or lightweight documentation; **Cucumber is not BDD itself, but the classic executable-specification reference bundled with this skill**.

When using this skill, ask first: “Have we reached shared understanding through concrete examples?” Then ask: “Do these examples need to be automated with Cucumber.js?” Do not reverse the order by equating BDD with “writing `.feature` tests.”

## 1. What this skill is: precompiled documentation, not a link list

This skill precompiles Wikipedia’s BDD definition, the official Cucumber BDD/Gherkin/Cucumber.js documentation, anti-patterns, and the JavaScript 10-minute tutorial into a manual an AI agent can use immediately. Future agents using this skill should treat this document as the default standard reference instead of assuming they will return to the web and reinterpret the docs.

Bundled content covers:

- BDD’s definition, goals, misconceptions, roles, and collaboration workflow.
- The Discovery → Formulation → Automation workflow.
- Minimal rules for Example Mapping, Three Amigos, User Stories, and Acceptance Criteria.
- Gherkin syntax, scenario writing style, good/bad examples, and anti-patterns.
- Cucumber.js project layout, step definitions, World/state, hooks, configuration, result semantics, and the official JavaScript example.

Intentionally not bundled: complete API documentation, every formatter/plugin/parallel/retry/sharding option, and every language implementation detail. When exact configuration parameters or library-version behavior matters, consult the official API/README.

## 2. Source fidelity: reference layers

### Layer 1: BDD definition

- **Behavior-driven development — Wikipedia**: defines BDD around collaboration between business and IT stakeholders, with the goal of forming shared understanding of the problem; it often uses a natural-language DSL to express behavior and expected outcomes; BDD has a historical relationship with TDD, but its purpose is not test syntax — it is shared understanding and business language.

### Layer 2: BDD practice model

- **Cucumber BDD guide**: BDD is an ongoing collaborative practice that uses concrete real-world examples for Discovery, Formulation, and Automation.
- **Cucumber myths**: conversations are more important than capturing conversations, and captured conversations are more important than automating conversations; automating scenarios after code is written can be test automation, but it is not the full BDD practice; using Cucumber does not mean you are doing BDD.
- **Discovery workshop / Example Mapping / Who does what**: explain how team roles and card-based examples clarify scope.

### Layer 3: executable-specification implementation reference

- **Gherkin reference**: Feature, Rule, Scenario/Example, Given/When/Then, Background, Scenario Outline, Examples, Doc Strings, Data Tables, Tags, language.
- **Cucumber.js docs and 10-minute tutorial**: demonstrate the minimal JavaScript loop from undefined → pending/failed → passing → refactor/Examples.
- **Anti-patterns / Better Gherkin / FAQ**: provide maintainability boundaries and anti-patterns.

## 3. Core BDD standards

### 3.1 Goal: shared understanding, not test coverage

The core BDD question is not “Did the tests run?” It is whether business, development, and testing/quality have reached shared understanding of the same problem space, business rules, and observable behavior.

Signs you are actually doing BDD:

- Did the team discuss concrete examples before writing implementation?
- Is behavior expressed in business language instead of technical implementation language?
- Are examples written as checkable specifications rather than abstract wishes?
- Can a business stakeholder or user representative read and confirm them?
- Does automation serve specification feedback instead of replacing specification discussion?

### 3.2 Relationship between BDD and TDD

BDD was historically influenced by TDD, but do not reduce BDD to TDD with “Given/When/Then test syntax.” The Wikipedia summary emphasizes understanding the problem space and writing it down with business language, real data, intention-revealing wording, and necessary, focused examples.

Remember **BRIEF**:

- **Business language**: business terms, not class names, table names, or button names.
- **Real data**: real/concrete data, not `foo`, `bar`, or `user1`.
- **Intention revealing**: reveal intent so readers understand why the behavior matters.
- **Essential**: keep only essential semantics, not irrelevant implementation steps.
- **Focused**: each example focuses on one behavior/rule.

### 3.3 BDD is not these things

- **Not Cucumber-specific**: Cucumber/Gherkin is a common implementation, not the definition of BDD.
- **Not post-hoc automation after code is complete**: that can be acceptance automation / characterization testing, but it is not the full BDD practice.
- **Not a UI interaction script**: `.feature` files describe what, not how.
- **Not a giant test-case repository**: excessive data combinations belong in helpers/builders; feature files should keep the key examples.
- **Not something one person writes in isolation**: Discovery requires collaboration.

## 4. BDD workflow: Discovery → Formulation → Automation

The Cucumber BDD documentation describes day-to-day BDD as three kinds of practice: Discovery, Formulation, and Automation. The order matters: **conversation first, capture second, automation last**.

### 4.1 Discovery: discover behavior and scope

Goal: technical and non-technical stakeholders explore a small user story together, finding rules, examples, boundaries, counterexamples, and questions.

Working rules:

- Discuss one small story or small change at a time. If it cannot be clarified in 25–30 minutes, the story may be too large or may require more research.
- Hold discovery just in time before development so details are not lost and plans can still adapt to new facts.
- Cover at least the Three Amigos perspectives: product/business, development, and testing/quality.
- Ask for examples before asking for technical implementation.
- Record unknowns explicitly instead of guessing.

When no real three-way meeting exists, an AI agent should simulate the three perspectives, but it must mark which points are inference and which require user confirmation.

### 4.2 Three Amigos: three necessary voices

- **Product owner / business representative**: decides scope, value, and which boundaries belong to the current story.
- **Tester / quality voice**: raises boundaries, failure paths, missing stories, and ways the system can break.
- **Developer / technical voice**: identifies implementation constraints, dependencies, hidden complexity, and automation feasibility.

Important: scenario language should initially be established by the whole team; once the team matures, developers and testers may pair on Gherkin, but active product/business review is still needed.

### 4.3 Example Mapping: separate stories, rules, examples, and questions

Before development, use Example Mapping to clarify acceptance criteria quickly:

- **Story (yellow card)**: the current user story.
- **Rules / acceptance criteria (blue cards)**: constraints, rules, and acceptance criteria.
- **Examples (green cards)**: concrete examples that illustrate rules.
- **Questions (red cards)**: unanswered questions or assumptions.
- **New stories (record separately)**: discovered work that is deferred out of scope.

Continue the conversation until the team believes the current story scope is clear, or time runs out. Do not hard-code unanswered questions into the specification.

### 4.4 User Story and Acceptance Criteria

A User Story is a small slice of valuable functionality used for planning and prioritization. Good stories often satisfy INVEST: Independent, Negotiable, Valuable, Estimable, Small, Testable.

Common story format:

```text
As an <actor>
I want a <feature>
So that <benefit>
```

BDD does not require every feature file to use that format, but it does require answers to:

- Who: who benefits?
- What: what capability is needed?
- Why: why is it valuable?
- Acceptance: what concrete behavior proves it is done?

### 4.5 Formulation: write examples as readable, automatable specifications

Goal: write clearly discussed examples in a form both people and tools can understand. In the Cucumber ecosystem, this is usually Gherkin.

Formulation requirements:

- Use domain language.
- Be concrete without becoming technical.
- Describe behavior (what), not implementation (how).
- Keep each scenario focused on one behavior/rule.
- Keep scenarios independent and runnable in any order.
- Verify only observable outcomes in `Then`.

### 4.6 Automation: connect specifications to the system

Goal: automate one example at a time, using failure feedback to drive the smallest implementation.

Standard rhythm:

1. Write the scenario, run Cucumber, and see `undefined`.
2. Add step definitions, run again, and see `pending` or failed results.
3. Have the step definition call system behavior, and assert in `Then`.
4. See a failure first (red), proving the example catches the missing behavior.
5. Implement the smallest code needed to pass (green).
6. Refactor implementation and step definitions while keeping scenario language stable.
7. Add the next example or `Scenario Outline`, and continue the loop.

If the user only asks to “write Gherkin,” do not implement production code on your own. Enter full automation and red/green only when the user asks to “implement with BDD.”

## 5. Cucumber’s place in this skill

Cucumber is a tool that connects Gherkin executable specifications to code. It reads `.feature` files, matches step definitions, executes system behavior, and reports results. It is the classic implementation of BDD automation, but not the only possible implementation.

When using Cucumber, still follow the BDD order:

1. First discuss examples.
2. Then write Gherkin.
3. Finally write step definitions and implementation.

Do not skip Discovery just because a project already has Cucumber installed. Do not assume every BDD task is a JavaScript project just because this skill includes Cucumber.js examples. If the project uses another language/framework, carry over the principles and Gherkin language, and replace the automation layer.

## 6. Precompiled Gherkin quick manual

### 6.1 Files and top-level structure

A `.feature` file can contain only one `Feature`.

```gherkin
@billing
Feature: Subscription billing
  Customers should be charged according to their active plan
  so that access and revenue remain aligned.

  Rule: Active paid subscribers keep access

    Scenario: Paid subscriber can read paid article
      Given Priya has an active basic subscription
      When Priya opens the paid article "Scaling Rails"
      Then Priya can read the article
```

Recommended: indent by two spaces. Comments can only be added at the start of a new line with `#`; Gherkin does not support block comments.

### 6.2 Feature

`Feature:` gives the high-level capability and groups related scenarios. Keep the title short; use the free-form description underneath for business context, value, and a rule list. The free-form description does not affect execution, but it appears in reports.

A good Feature description answers Why / Who / What:

```gherkin
Feature: Account balance
  As a mobile bank customer
  I want to see balances for my accounts
  So that I can make informed spending decisions
```

Do not write a Feature as a technical module name:

```gherkin
Feature: AccountController GET /api/v1/accounts JSON serializer
```

Unless your product is the API contract itself, this is not business language.

### 6.3 Rule

`Rule:` represents a business rule and groups several scenarios that illustrate it. A rule should have one or more examples.

```gherkin
Feature: Transfer limits

  Rule: Transfers above the daily limit are rejected

    Scenario: Alice exceeds her daily limit
      Given Alice has already transferred $900 today
      When Alice tries to transfer $200 to Bob
      Then the transfer is rejected
      And Alice is told her remaining daily limit is $100
```

Using `Rule` prevents feature files from becoming unstructured lists of scenarios.

### 6.4 Scenario / Example

`Scenario` and `Example` are synonyms in Gherkin. A scenario is a concrete example that illustrates a business rule and is also an executable test.

The official guidance is that each example should have roughly 3–5 steps; too many steps weaken the specification/documentation value. If a one-sentence title cannot explain the purpose of a scenario, it usually needs to be split.

### 6.5 Given / When / Then

- `Given`: initial context that puts the system into a known state. Avoid user-interaction details.
- `When`: the event or action triggered by a user or external system.
- `Then`: the expected outcome, which must verify the actual result with assertions.
- `And` / `But`: continue the previous step type for readability.
- `*`: can be used to write a list of similar steps.

```gherkin
Scenario: Transfer within the daily limit
  Given Alice has $430 in her checking account
  And Alice has not transferred money today
  When Alice transfers $125 to Bob
  Then Alice's checking balance is $305
  And Bob receives a $125 transfer notification
```

### 6.6 Important step-matching limitation

When Cucumber matches step definitions, it ignores the `Given` / `When` / `Then` keyword and only matches the step text that follows. Therefore these steps conflict:

```gherkin
Given there is money in my account
Then there is money in my account
```

Rewrite them with clearer domain language:

```gherkin
Given my account has a balance of £430
Then my account should have a balance of £430
```

### 6.7 Background

`Background` is for shared context that every scenario needs readers to know. It runs before each scenario, after Before hooks.

```gherkin
Feature: Blog posting

  Background:
    Given a global administrator named "Greg"
    And a customer named "Dr. Bill"

  Scenario: Customer posts to own blog
    Given I am logged in as Dr. Bill
    When I try to post to "Expensive Therapy"
    Then I should see "Your article was published."
```

Usage rules:

- If setup is important to business readers, use `Background` or `Given`.
- If setup merely starts a browser or clears a database, use hooks.
- Keep Background short; if it exceeds roughly 4 lines, consider raising the abstraction level or splitting the Rule/Feature.
- Use vivid names and states in Background; avoid `User A` / `Site 1`.

### 6.8 Scenario Outline / Examples

When the same behavior needs several sets of inputs/outputs, use `Scenario Outline` + `Examples` instead of copying and pasting near-identical scenarios.

```gherkin
Scenario Outline: Today is or is not Friday
  Given today is "<day>"
  When I ask whether it's Friday yet
  Then I should be told "<answer>"

  Examples:
    | day            | answer |
    | Friday         | TGIF   |
    | Sunday         | Nope   |
    | anything else! | Nope   |
```

`<day>` / `<answer>` are replaced with table values before step-definition matching. The Outline itself does not run directly; each row in Examples runs once.

### 6.9 Doc Strings

Doc Strings pass multiline text to a step definition. The Doc String is passed as the last argument.

```gherkin
Given a blog post named "Random" with Markdown body
  """markdown
  # Some Title

  Here is the first paragraph.
  """
```

You can use either `"""` or triple backticks; many editors support `"""` more consistently. A Doc String can include a content type such as `"""markdown`.

### 6.10 Data Tables

Data Tables pass structured lists/tables to a step definition as the last argument.

```gherkin
Given the following users exist:
  | name   | email             | role  |
  | Alice  | alice@example.com | admin |
  | Bob    | bob@example.com   | user  |
```

Do not treat Data Tables as a replacement for Excel/CSV test matrices. Feature files should keep key examples, not massive test data.

### 6.11 Tags

Tags use `@` to annotate Feature, Rule, Scenario, or Examples for grouping, filtering, conditional hooks, and reports. Example:

```gherkin
@billing @smoke
Scenario: Paid subscriber keeps access
  ...
```

Common uses:

- `@smoke` / `@critical`: fast feedback subsets.
- `@wip`: temporary work marker; clean it up before committing, or define an explicit policy.
- `@browser` / `@api`: execution-environment groups.
- Conditional hooks: start a browser or clean external resources only for tagged scenarios.

Do not use tags to hide messy scenarios; tags are not a substitute for a clear classification structure.

### 6.12 Localized languages

Gherkin supports many natural languages. The language should match the language the users and domain experts use to discuss the domain, avoiding translation loss.

You can put a language marker on the first line of a feature file when needed; for English this can be explicit:

```gherkin
# language: en
```

This skill’s examples use English Gherkin keywords by default because the Cucumber.js tutorial and most projects default to English; a concrete project may choose the team’s language.

## 7. Good BDD/Gherkin writing standards

### 7.0 Gherkin quality gate: validate scenarios before glue code

When writing/reviewing `.feature` files, first treat Gherkin as a product specification, not as runner input. Before any scenario moves into step definitions or implementation, it must pass at least this gate:

1. **One observable business behavior**: the scenario explains a rule, boundary, or outcome, not a vague test case.
2. **Domain language first**: readers can understand it with business vocabulary; unnecessary URLs, CSS selectors, database columns, class names, and HTTP details are absent.
3. **Concrete without being technical**: it has real roles, amounts, dates, states, or objects; it does not use placeholders such as `user1`, `foo`, or `result is correct`.
4. **Clear Given/When/Then semantics**: `Given` establishes business context, `When` triggers an event, and `Then` asserts an externally observable result.
5. **Short, independent, and reviewable**: usually 3–5 steps; it does not depend on another scenario; `Background`, `Examples`, and Data Tables carry only necessary semantics.
6. **If wording fails the gate, fix it first**: if the scenario needs explanation to be understood, or can only be expressed through implementation details, return to Discovery/Formulation instead of writing glue code.

### 7.1 Concrete, but not technical

Good examples use concrete names, places, dates, amounts, roles, and domain facts:

```gherkin
Scenario: Discount expires after campaign end date
  Given Carla has a 20% summer discount expiring on 2026-08-31
  When Carla checks out on 2026-09-01
  Then the summer discount is not applied
```

Bad examples are too abstract:

```gherkin
Scenario: Discount works
  Given a user has a discount
  When the user checks out
  Then the result is correct
```

Do not make them technical either:

```gherkin
Scenario: Discount expires after campaign end date
  Given row id 42 exists in discounts table
  When POST /api/v1/checkout returns 200
  Then order_discounts.applied equals false
```

Cucumber’s “Imagine it’s 1922” heuristic: write behavior that can be understood even without computers; keep technical details inside step definitions.

### 7.2 What, not how

Good:

```gherkin
Scenario: Subscriber can access paid content
  Given Paid Patty has a basic-level paid subscription
  When Paid Patty logs in
  Then she can read the paid article "Building Reliable Systems"
```

Bad:

```gherkin
Scenario: Subscriber can access paid content
  Given I am on the login page
  When I type "paid@example.com" in the email field
  And I type "validPassword123" in the password field
  And I press the "Submit" button
  Then I see "Building Reliable Systems" inside div.article-title
```

UI interactions can be implemented in helpers; the scenario should keep the business intent.

### 7.3 Each step expresses one thing

Bad conjunction step:

```gherkin
Given I have shades and a brand new Mustang
```

Good:

```gherkin
Given I have shades
And I have a brand new Mustang
```

If several lower-level actions need to form one high-level action, compose helper methods instead of writing compound Gherkin step text.

### 7.4 Keep language consistent

Do not use several different sentences for the same state across scenarios:

```gherkin
Given I am logged in
Given I have logged in to the site
Given my session is authenticated
```

Choose one domain expression and reuse it. Inconsistent language expands step definitions, creates matching ambiguity, and raises maintenance cost.

### 7.5 Every scenario is independent

Scenarios must run individually, in any order, and in parallel. Do not let one scenario depend on another scenario creating data first.

- Business-readable context: `Given` / `Background`.
- Technical environment: hooks / fixtures / builders.
- External services: test doubles or controlled test environments.
- Shared cross-scenario state: do not use it.

## 8. Precompiled Cucumber.js quick manual

### 8.1 Minimal project shape

```shell
mkdir hellocucumber
cd hellocucumber
npm init --yes
npm install --save-dev @cucumber/cucumber
mkdir -p features/step_definitions features/support
```

`package.json`:

```json
{
  "scripts": {
    "test": "cucumber-js"
  },
  "devDependencies": {
    "@cucumber/cucumber": "^13.0.0"
  }
}
```

Node.js version note: `@cucumber/cucumber@13` requires a recent Node.js version (current npm metadata is Node `22 || 24 || >=26`). If the project still uses Node 20 or older, run this first:

```shell
npm view @cucumber/cucumber engines
```

Choose a compatible version; do not blindly copy the latest version number.

### 8.2 Common directories

```text
features/
  billing.feature
  account.feature
  step_definitions/
    billing_steps.js
    account_steps.js
    authentication_steps.js
  support/
    world.js
    hooks.js
```

Cucumber.js looks for these by default:

- features: `features/**/*.{feature,feature.md}`.
- support code: when features are under `features/`, the default is `features/**/*.@(js|cjs|mjs)`.

If you manually configure `import` or `require`, the default support-code search is replaced, so list everything explicitly.

### 8.3 Configuration files

Cucumber.js looks in the project root in this order:

- `cucumber.json`
- `cucumber.yaml`
- `cucumber.yml`
- `cucumber.js`
- `cucumber.cjs`
- `cucumber.mjs`

You can also use `--config`.

CommonJS example:

```javascript
module.exports = {
  default: {
    format: ['progress-bar', 'html:cucumber-report.html'],
    require: ['features/**/*.js']
  }
};
```

ESM example:

```javascript
export default {
  format: ['progress-bar', 'html:cucumber-report.html'],
  import: ['features/**/*.mjs']
};
```

The tutorial used this setting so snippets are generated with synchronous functions:

```json
{
  "default": {
    "formatOptions": {
      "snippetInterface": "synchronous"
    }
  }
}
```

This is a learning convenience, not a universal project default.

### 8.4 Profiles

Profiles package different run configurations into command aliases.

```javascript
const common = {
  require: ['features/**/*.js'],
  worldParameters: {
    appUrl: process.env.APP_URL || 'http://localhost:3000/'
  }
};

module.exports = {
  default: {
    ...common,
    format: ['progress-bar']
  },
  ci: {
    ...common,
    format: ['html:cucumber-report.html'],
    publish: true
  }
};
```

Run:

```shell
cucumber-js --profile ci
# or
cucumber-js -p ci
```

Profiles can be applied repeatedly; options explicitly passed on the CLI can still override or append to them.

### 8.5 Official JavaScript tutorial loop: Is it Friday yet?

First write `features/is_it_friday_yet.feature`:

```gherkin
Feature: Is it Friday yet?
  Everybody wants to know when it's Friday

  Scenario: Sunday isn't Friday
    Given today is Sunday
    When I ask whether it's Friday yet
    Then I should be told "Nope"
```

Run `npm test` and first see undefined steps. Then write step definitions.

`features/step_definitions/stepdefs.js`:

```javascript
const assert = require('assert');
const { Given, When, Then } = require('@cucumber/cucumber');

function isItFriday(today) {
  // First implementation intentionally incomplete/failing.
}

Given('today is Sunday', function () {
  this.today = 'Sunday';
});

When('I ask whether it\'s Friday yet', function () {
  this.actualAnswer = isItFriday(this.today);
});

Then('I should be told {string}', function (expectedAnswer) {
  assert.strictEqual(this.actualAnswer, expectedAnswer);
});
```

This should fail because `actualAnswer` is `undefined`. Then write the smallest implementation:

```javascript
function isItFriday(today) {
  return 'Nope';
}
```

Add the Friday example and see it fail:

```gherkin
Scenario: Friday is Friday
  Given today is Friday
  When I ask whether it's Friday yet
  Then I should be told "TGIF"
```

Converge to a `Scenario Outline`:

```gherkin
Scenario Outline: Today is or is not Friday
  Given today is "<day>"
  When I ask whether it's Friday yet
  Then I should be told "<answer>"

  Examples:
    | day            | answer |
    | Friday         | TGIF   |
    | Sunday         | Nope   |
    | anything else! | Nope   |
```

Final step definitions:

```javascript
const assert = require('assert');
const { Given, When, Then } = require('@cucumber/cucumber');

function isItFriday(today) {
  if (today === 'Friday') {
    return 'TGIF';
  }
  return 'Nope';
}

Given('today is {string}', function (givenDay) {
  this.today = givenDay;
});

When('I ask whether it\'s Friday yet', function () {
  this.actualAnswer = isItFriday(this.today);
});

Then('I should be told {string}', function (expectedAnswer) {
  assert.strictEqual(this.actualAnswer, expectedAnswer);
});
```

This example demonstrates the small-step BDD/TDD feedback loop; it is not meant to represent business complexity.

## 9. Step definitions manual

### 9.1 Step definitions are glue code

A step definition uses an expression to connect Gherkin step text to code. When Cucumber executes a step, it searches for a matching step definition.

```javascript
const { Given } = require('@cucumber/cucumber');

Given('I have {int} cucumbers', function (count) {
  this.cucumbers = count;
});
```

Prefer Cucumber Expressions:

- `{string}`: quoted string.
- `{int}`: integer.
- `{float}`: floating-point number.
- `{word}`: word.

Use RegExp only when more complex matching is needed:

```javascript
Given(/^I have (\d+) cucumbers$/, function (count) {
  this.cucumbers = Number(count);
});
```

Do not let one step match multiple definitions; that is ambiguous.

### 9.2 Implement only steps required by real scenarios

Do not pre-write step definitions that “might be useful later.” Implement only steps that already appear in the current `.feature` files; refactor when reuse is needed.

### 9.3 Organize step files by domain concept

Recommended grouping by domain object/concept:

```text
features/step_definitions/
  employee_steps.js
  education_steps.js
  experience_steps.js
  authentication_steps.js
```

Not recommended: mechanical one-to-one binding with feature files:

```text
features/step_definitions/
  edit_work_experience_steps.js
  edit_languages_steps.js
  edit_education_steps.js
```

The latter tends to create feature-coupled step definitions: non-reusable, repetitive, and expensive to maintain.

### 9.4 Reuse helper methods; do not have steps call steps

Good:

```javascript
function logInAs(world, userName) {
  world.currentUser = findUser(userName);
  world.session = createSession(world.currentUser);
}

Given('{word} is logged in', function (name) {
  logInAs(this, name);
});
```

Do not call another Gherkin step text from a step definition to reuse logic. Composition and reuse belong in the programming-language layer, through helpers, builders, fixtures, and domain services.

### 9.5 Step result semantics

Cucumber step results:

- **Success**: a matching step definition is found and executes without throwing/rejecting.
- **Undefined**: no matching step definition is found; subsequent steps are skipped.
- **Pending**: the step definition explicitly marks the step as pending; work remains.
- **Failed**: execution throws/rejects.
- **Skipped**: follows undefined/pending/failed and is not executed.
- **Ambiguous**: multiple definitions match the same step.

Important: return values do not mean pass/fail; `return false` and `return null` do not fail a step.

Correct:

```javascript
Then('the balance should be {int}', function (expectedBalance) {
  assert.strictEqual(this.account.balance, expectedBalance);
});
```

Wrong:

```javascript
Then('the balance should be {int}', function (expectedBalance) {
  return this.account.balance === expectedBalance;
});
```

### 9.6 Async step definitions

Cucumber.js supports async/promise step definitions:

```javascript
When('Alice transfers ${int} to Bob', async function (amount) {
  this.response = await this.api.transfer({ from: 'Alice', to: 'Bob', amount });
});
```

Failure should be expressed through an assertion error, `throw`, or a rejected promise.

## 10. State / World manual

### 10.1 Do not share state across scenarios

The core rule from the Cucumber state documentation: do not share state between scenarios. Cross-scenario state leakage makes tests brittle and prevents scenarios from running individually.

Avoid:

- global/static variables that hold business state.
- database records reused across scenarios without cleanup.
- browser session/cookie leakage.

Allowed:

- a `Before` hook that cleans the database.
- a `Before` hook that clears cookies.
- each scenario building its own test data.

### 10.2 Cucumber.js World

Cucumber.js creates an isolated World for each scenario. In ordinary `function () {}` step definitions/hooks, `this` points to the current World and can share state between steps within the same scenario.

```javascript
Given('Alice has $430', function () {
  this.account = new Account('Alice', 430);
});

When('Alice withdraws $30', function () {
  this.account.withdraw(30);
});

Then('Alice has $400', function () {
  assert.strictEqual(this.account.balance, 400);
});
```

Do not use arrow functions in steps/hooks that need `this`:

```javascript
// Wrong: arrow functions bind lexical this and cannot use the Cucumber World.
Given('Alice has $430', () => {
  this.account = new Account('Alice', 430);
});
```

This skill recommends ordinary functions for Cucumber.js step definitions and hooks by default, unless the step clearly does not need World and the team already has a convention.

### 10.3 World parameters

Cucumber.js can pass environment parameters to World with `worldParameters`, such as app URL, browser type, and test tenant. This is appropriate for environment configuration, not business-rule decisions.

```javascript
module.exports = {
  default: {
    worldParameters: {
      appUrl: process.env.APP_URL || 'http://localhost:3000/'
    }
  }
};
```

Do not put secrets in feature files or commit them in configuration.

## 11. Hooks manual

Hooks are code blocks that run during the Cucumber execution cycle, usually for environment setup/teardown.

### 11.1 Before / After

```javascript
const { Before, After } = require('@cucumber/cucumber');

Before(async function () {
  this.browser = await startBrowser();
});

After(async function () {
  await this.browser?.close();
});
```

Cucumber explicitly warns that things done in a Before hook are invisible to someone who only reads the feature. If setup matters to business understanding, use `Background` or `Given`; keep only low-level logic in hooks, such as starting a browser, deleting database data, or resetting a test environment.

### 11.2 Conditional hooks

Hooks can be limited with tags:

```javascript
Before({ tags: '@browser' }, async function () {
  this.browser = await startBrowser();
});
```

This is useful for starting a browser only for UI scenarios or cleaning a type of external resource only for some scenarios.

### 11.3 BeforeStep / AfterStep

Use these to insert logic before or after every step, such as debugging, screenshots, or logs. Do not overuse them; if every step performs complex work, the test architecture may need refactoring.

```javascript
const { AfterStep } = require('@cucumber/cucumber');

AfterStep(async function ({ pickleStep }) {
  if (this.debug) {
    this.log(`finished step: ${pickleStep.text}`);
  }
});
```

Failure screenshots are usually handled in an `After` hook based on scenario status instead of polluting business scenarios.

## 12. Anti-patterns and corrections

### 12.1 “Using Cucumber means doing BDD”

Wrong: Cucumber is installed and feature files exist, but there is no collaboration, no example discussion, and no business feedback.

Correction: restore Discovery → Formulation → Automation. At minimum, start the next story from concrete examples.

### 12.2 Adding scenarios after code is done and calling it BDD

Wrong: after implementation is complete, `.feature` files are added for test coverage.

Correction: call it acceptance automation / characterization; use the BDD process again for future changes.

### 12.3 Procedural UI scripts

Wrong:

```gherkin
When I enter "Bob" in the "user name" field
And I enter "tester" in the "password" field
And I press the "login" button
```

Correct:

```gherkin
When "Bob" logs in
```

### 12.4 Feature-coupled step definitions

Wrong: each feature file has a same-named steps file containing sentences that only serve that feature.

Correction: group step definitions by domain concepts and use domain-related names.

### 12.5 Conjunction steps

Wrong: one step does several things.

Correction: split it into several steps, or compose low-level actions with helper methods inside the step definition.

### 12.6 Steps calling steps

Wrong: a step definition invokes another Gherkin step text to reuse logic.

Correction: extract ordinary JavaScript functions, domain helpers, and builders.

### 12.7 Conditionally skipping scenarios or steps

If a scenario skips itself or its steps based on runtime conditions, it usually means one scenario covers too many behaviors, or data/environment is not controlled. Split the scenario and fix the root cause.

### 12.8 Excel/CSV test cases replacing feature files

The Cucumber FAQ does not recommend storing test cases in Excel/CSV and then reading them from Cucumber. Feature files themselves should be readable executable specifications. If there is too much data, the scenario abstraction level is usually wrong.

### 12.9 Verifying deep implementation details

Wrong: `Then` checks internal database columns, private object fields, or logging implementation details.

Correction: verify output observable by a user or external system: UI, API response, message, report, notification, or public manifestation of a state change.

## 13. AI agent operating protocol

When the user asks to “develop/design/accept with BDD”:

1. **Start from the BDD definition**: is this a collaboration/specification problem, or only a Cucumber automation problem? Do not jump directly to tooling.
2. **Read evidence**: requirements, issues, code, existing tests, domain vocabulary, and product documentation.
3. **Slice small stories**: break a large requirement into small behaviors that can be clarified in one discovery conversation.
4. **Discover examples**: list happy-path examples, boundary examples, rejection/failure examples, and unanswered questions.
5. **Simulate Three Amigos**: separately list product scope, test boundaries, and development constraints; ask the smallest user question when a decision is needed.
6. **Draft Gherkin and run the quality gate first**: business language, concrete data, what not how; before writing step definitions, check scenario semantics and writing quality against section 7.
7. **Confirm product semantics**: confirm rules, scope, and boundaries first; do not put guesses into code.
8. **Automate**: if the user asks for implementation, add/update `.feature` files and step definitions, and first observe undefined/pending/failed results.
9. **Smallest implementation**: write only enough code to pass the current example.
10. **Refactor**: organize steps by domain, extract helpers, and deduplicate language.
11. **Report evidence**: list scenarios, run commands, the red/green process, and remaining questions.

If the user only asks for “BDD review,” do not modify files on your own; report concrete findings and the smallest correction suggestions.

## 14. BDD/Gherkin review checklist

### BDD layer

- [ ] Does the work aim for shared understanding, not just test coverage?
- [ ] Were concrete examples discussed before implementation?
- [ ] Are Who / What / Why explicit?
- [ ] Are unanswered questions and assumptions marked?
- [ ] Does it avoid equating Cucumber usage with BDD itself?

### Scenario layer

- [ ] Does each scenario explain one concrete business rule/behavior?
- [ ] Does it use concrete real data instead of abstract placeholders?
- [ ] Does it describe what, not how?
- [ ] Does it avoid implementation details such as URLs, buttons, CSS, and database columns?
- [ ] Are there roughly 3–5 steps?
- [ ] Is the scenario independent and runnable in any order?
- [ ] Does `Then` verify an observable outcome?
- [ ] Is Background short and business-readable?
- [ ] Is Scenario Outline used to eliminate repeated examples?
- [ ] Does it avoid dumping massive data into Examples/Data Tables?

### Step/code layer

- [ ] Are only steps that appear in existing scenarios implemented?
- [ ] Are step definitions organized by domain concept?
- [ ] Does it avoid feature-coupled steps?
- [ ] Does it reuse helper methods instead of steps calling steps?
- [ ] In Cucumber.js, do steps/hooks that need World use `function () {}`?
- [ ] Does `Then` use assertion/throw/reject instead of returning false?
- [ ] Do hooks contain only low-level technical setup/cleanup?
- [ ] Does it avoid sharing state across scenarios?
- [ ] Is at least one failing feedback loop recorded?

## 15. Quick templates

### 15.1 Discovery output template

```markdown
## Story
As a <actor>
I want <capability>
So that <benefit>

## Rules
- Rule 1: ...
- Rule 2: ...

## Examples
- Example: <concrete case>
  - Given ...
  - When ...
  - Then ...

## Questions
- [ ] ...

## Out of scope / new stories
- ...
```

### 15.2 Feature template

```gherkin
Feature: <business capability>
  <why this matters>

  Rule: <business rule>

    Scenario: <concrete example title>
      Given <known business context>
      When <observable event/action>
      Then <observable expected outcome>
```

### 15.3 Step definition template

```javascript
const assert = require('assert');
const { Given, When, Then } = require('@cucumber/cucumber');

Given('<context with {int} or {string}>', function (value) {
  // Arrange known state through helpers/builders.
});

When('<actor does business action>', async function () {
  // Act through public behavior/API/UI helper.
});

Then('<observable result>', function () {
  // Assert, do not return boolean.
  assert.strictEqual(this.actual, this.expected);
});
```

## 16. When to return to the official docs

This skill already includes most common standards. Return to official docs only when:

- You need exact CLI/config options or formatter, plugin, parallel, retry, or sharding behavior.
- The project uses a non-JavaScript Cucumber implementation and needs language-specific APIs.
- The Cucumber.js version differs from this skill’s examples and you must confirm Node engines or breaking changes.
- You need the complete DataTable/DocString API or custom parameter types.
- You need debugging details for formatters/reporting/publishing.

By default, use this manual directly when writing/reviewing BDD scenarios; do not treat “go read the links” as a substitute for doing the work.

## 17. References

### 17.1 Local references (preferred)

Default reading order for future AI agents:

- [official-reference-map.md](references/official-reference-map.md)
  - First decide whether the current problem is a practice problem, scenario-writing problem, or execution problem, then choose the next step.
- [bdd-practice-reference.md](references/bdd-practice-reference.md)
  - Discovery / Formulation / Automation, Example Mapping, Three Amigos, Story, and Acceptance Criteria.
- [gherkin-cucumber-reference.md](references/gherkin-cucumber-reference.md)
  - Gherkin syntax structure, scenario maintainability, and common anti-pattern corrections.
- [cucumber-js-reference.md](references/cucumber-js-reference.md)
  - Cucumber.js execution concerns: step definitions, World, hooks, configuration, and troubleshooting.

### 17.2 External official entry points (as needed)

- Definition and practice:
  - Behavior-driven development — Wikipedia: <https://en.wikipedia.org/wiki/Behavior-driven_development>
  - Cucumber BDD Guide: <https://cucumber.io/docs/bdd/>
  - Cucumber Discovery Workshop: <https://cucumber.io/docs/bdd/discovery-workshop/>
  - Cucumber Example Mapping: <https://cucumber.io/docs/bdd/example-mapping/>
  - Cucumber Who does what / Three Amigos: <https://cucumber.io/docs/bdd/who-does-what/>
  - Cucumber Myths: <https://cucumber.io/docs/bdd/myths/>
- Gherkin and writing style:
  - Gherkin reference: <https://cucumber.io/docs/gherkin/reference/>
  - Step organization: <https://cucumber.io/docs/gherkin/step-organization/>
  - Writing better Gherkin: <https://cucumber.io/docs/bdd/better-gherkin/>
  - Cucumber Anti-patterns: <https://cucumber.io/docs/guides/anti-patterns/>
  - Step definitions: <https://cucumber.io/docs/cucumber/step-definitions/>
  - Cucumber API/reference: <https://cucumber.io/docs/cucumber/api/>
- Cucumber.js (JavaScript execution):
  - Cucumber state / World: <https://cucumber.io/docs/cucumber/state/>
  - Cucumber.js configuration: <https://github.com/cucumber/cucumber-js/blob/main/docs/configuration.md>
  - Cucumber.js profiles: <https://github.com/cucumber/cucumber-js/blob/main/docs/profiles.md>
  - Cucumber.js hooks: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/hooks.md>
  - Cucumber.js world: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/world.md>
  - Look up plugins/formatters/parallel/retry/sharding and similar topics in the Cucumber.js docs as needed: <https://github.com/cucumber/cucumber-js/tree/main/docs>
- Tutorial and extension:
  - Cucumber 10-minute tutorial (JavaScript): <https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript>

### 17.3 Usage advice

- Do not open external links first by default. Do so only when local documentation cannot answer quickly, or when exact version parameters are needed (CLI, formatter, parallel/retry, etc.).
- Always confirm first whether the behavior-collaboration problem comes before the tool.
- If details conflict, combine the local references and official docs step by step.
