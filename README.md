# BDD Skill

A source-backed AI agent skill for **Behavior-Driven Development (BDD)** as a collaboration/specification practice, with Cucumber/Gherkin and Cucumber.js bundled as a classic executable-specification reference.

The installable skill lives at:

```text
skills/bdd/SKILL.md
```

It is written in Chinese. The skill is intentionally a **precompiled manual**: it starts from Wikipedia's BDD definition, then embeds the practical Cucumber/Gherkin/Cucumber.js guidance an AI agent usually needs, instead of merely linking out to docs. JavaScript/Cucumber.js examples are used because the JavaScript setup is small and easy to follow.

## What it covers

- BDD's standard definition: collaboration between business and IT stakeholders to form shared understanding, often written with natural-language DSL examples.
- BDD as a practice distinct from Cucumber: Cucumber is included as a classic implementation reference, not treated as the definition of BDD.
- Discovery → Formulation → Automation workflow, including Three Amigos, discovery workshops, Example Mapping, user stories, and acceptance criteria.
- Gherkin quick manual: `Feature`, `Rule`, `Scenario`/`Example`, `Background`, `Scenario Outline`, `Examples`, `Given`, `When`, `Then`, `And`, `But`, `*`, Doc Strings, Data Tables, tags, and language selection.
- Cucumber.js quick manual: project layout, config/profiles, step definitions, World/state, hooks, step results, and the official JavaScript "Is it Friday yet?" workflow.
- Correct vs incorrect Gherkin style: behavior over implementation, concrete examples without UI/protocol/database leakage.
- Cucumber anti-patterns: feature-coupled step definitions, conjunction steps, steps-calling-steps, scenario dependency, conditional skipping, excessive technical data.
- Review checklists and templates for AI agents writing or reviewing BDD specs.

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
- Cucumber myths: <https://cucumber.io/docs/bdd/myths/>
- Cucumber discovery workshop: <https://cucumber.io/docs/bdd/discovery-workshop/>
- Cucumber Example Mapping: <https://cucumber.io/docs/bdd/example-mapping/>
- Cucumber Who does what / Three Amigos: <https://cucumber.io/docs/bdd/who-does-what/>
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

The Wikipedia BDD page is referenced and briefly quoted with attribution as the definition anchor; this repository does not relicense Wikipedia content.
