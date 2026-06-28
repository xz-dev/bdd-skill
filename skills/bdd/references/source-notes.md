# Source Notes

This BDD skill is a structured, precompiled guide derived from primary BDD/Cucumber references rather than a verbatim copy of any one source. It intentionally starts from the Wikipedia definition of Behavior-driven development and treats Cucumber as a bundled implementation/manual section, not as the definition of BDD.

## Main sources

- Wikipedia, **Behavior-driven development**: defines BDD as an agile software development method centered on collaboration between business and IT stakeholders, aiming for shared understanding, and using natural-language DSL constructs to express behavior and expected outcomes.
- Cucumber docs, **Introduction**: describes Cucumber as a tool that reads executable specifications written in plain text, validates software behavior, and uses Gherkin plus step definitions.
- Cucumber docs, **Behaviour-Driven Development**: frames BDD as Discovery, Formulation, and Automation, with concrete examples and continuous collaboration.
- Cucumber docs, **Myths about BDD**, **Discovery workshop**, **Example Mapping**, **Examples**, **Who does what**, and **User story**: provide the non-tooling BDD practice material added to the skill body.
- Cucumber docs, **10-minute tutorial**: provides the tutorial workflow used here: write a scenario before production code, see undefined/pending/failing feedback, make it pass, then generalize with `Scenario Outline` and `Examples`. The skill uses the JavaScript flavor of this tutorial.
- Cucumber docs, **Gherkin reference**, **Writing better Gherkin**, **Step organization**, **Step definitions**, **Cucumber reference**, **State**, **Anti-patterns**, and **FAQ**: provide the practical style rules and anti-pattern guidance.
- Cucumber.js docs, **Configuration**, **Profiles**, and support-file documentation: provide the JavaScript-specific runtime manual summarized in the skill without copying the full API reference.

## Key interpretation decisions

- The skill treats BDD primarily as a collaborative specification practice, not as a synonym for Cucumber or acceptance-test automation.
- Cucumber is presented as a classic bundled implementation reference. BDD guidance appears first; Cucumber/Gherkin/Cucumber.js guidance appears as a practical manual after the BDD standard.
- The skill deliberately embeds most frequently needed reference material directly in `SKILL.md`; only complete API/formatter/plugin/advanced runtime details are left as external lookups.
- The examples use Cucumber.js CommonJS syntax because it is compact and directly follows the official JavaScript tutorial shape.
- The guide intentionally emphasizes behavior-level wording over UI/protocol/database details, following Cucumber's better-Gherkin guidance.
- The checklist requires at least one failing feedback signal when implementing behavior, matching the tutorial's undefined/pending/failing/passing progression.
