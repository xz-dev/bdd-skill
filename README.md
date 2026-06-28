# BDD Skill

A source-backed AI agent skill for **Behavior-Driven Development (BDD)** with Cucumber/Gherkin-style executable specifications.

The installable skill lives at:

```text
skills/bdd/SKILL.md
```

It is written in Chinese and uses JavaScript/Cucumber.js examples because the JavaScript setup is small and easy to follow.

## What it covers

- BDD as collaboration around shared understanding, not merely test automation.
- Discovery → Formulation → Automation workflow from Cucumber's BDD guide.
- Gherkin structure: `Feature`, `Rule`, `Scenario`, `Scenario Outline`, `Given`, `When`, `Then`, `And`, `But`.
- Cucumber.js project layout and step definitions.
- Correct vs incorrect Gherkin style: behavior over implementation, concrete examples without UI/protocol leakage.
- Cucumber anti-patterns: feature-coupled step definitions, conjunction steps, scenario dependency, conditional skipping, excessive technical data.
- A review checklist for AI agents writing or reviewing BDD specs.

## Install in Pi

```bash
pi install https://github.com/xz-dev/bdd-skill
```

Pi auto-discovers the top-level `skills/` directory and loads `skills/bdd/SKILL.md`.

## Install in other agent harnesses

Copy or symlink `skills/bdd/SKILL.md` into your agent's skill directory, or install the repository if your harness supports Agent Skills repositories.

## Source basis

Primary references:

- Behavior-driven development — Wikipedia: <https://en.wikipedia.org/wiki/Behavior-driven_development>
- Cucumber Introduction: <https://cucumber.io/docs/>
- Cucumber BDD guide: <https://cucumber.io/docs/bdd/>
- Cucumber 10-minute tutorial with JavaScript examples: <https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript>
- Gherkin reference: <https://cucumber.io/docs/gherkin/reference/>
- Writing better Gherkin: <https://cucumber.io/docs/bdd/better-gherkin/>
- Cucumber anti-patterns: <https://cucumber.io/docs/guides/anti-patterns/>

During creation, the Cucumber website docs repository was cloned and the full `docs/` Markdown/MDX set was reviewed/indexed. The Cucumber.js repository docs and executable feature files were also sampled/reviewed for JavaScript-specific details such as World, hooks, snippets, and configuration. See:

- `skills/bdd/references/source-notes.md`
- `skills/bdd/references/cucumber-docs-reviewed.md`
- `skills/bdd/references/cucumber-js-docs-reviewed.md`
- `skills/bdd/references/upstream-source.json`
- `skills/bdd/references/cucumber-website-license.txt`
- `skills/bdd/references/cucumber-js-license.txt`

## License

This skill repository is MIT licensed. Cucumber website documentation is MIT licensed by Aslak Hellesøy and contributors, and Cucumber.js is MIT licensed by Julien Biezemans and contributors. See `skills/bdd/references/cucumber-website-license.txt` and `skills/bdd/references/cucumber-js-license.txt` for upstream license notices.
