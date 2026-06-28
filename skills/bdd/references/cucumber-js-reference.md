# Cucumber.js reference: from scenarios to execution

> This is not complete API documentation; it is a high-frequency decision map for using Cucumber.js to automate scenarios.

## 1. When to read this

- You already have an executable scenario draft and need to run it.
- A run produces `undefined`, `pending`, `failed`, or `ambiguous`.
- You need to debug hooks, tags, configuration, or CI compatibility.

## 2. Core objects

- `features/`: the default feature root directory (subject to project convention).
- `Given/When/Then`: bind to steps.
- Step definitions: define the mapping between scenarios and steps.
- World: per-scenario context state.
- Hooks: `Before/After` (including tag filtering).
- Configuration files: `cucumber.json` / `cucumber.yml` / `cucumber.js`.

## 3. Typical execution loop

1. Write a scenario.
2. Run `cucumber-js` (usually seeing `undefined` first).
3. Add matching step definitions.
4. Run to `pending/failed`.
5. Implement the smallest passing behavior.
6. Refactor and add boundaries.

## 4. Step definitions and language

- Common expressions: `{string}`, `{int}`, `{float}`, `{word}`.
- Use regular expressions only for complex matching.
- When `this` (World) is needed, use `function`; do not use arrow functions.

```javascript
const assert = require('assert');
const { Given, When, Then } = require('@cucumber/cucumber');

Given('the cart has {int} items', function (count) {
  this.cartCount = count;
});

When('the customer checks out', async function () {
  this.result = await this.api.checkout();
});

Then('the order status is {string}', function (expected) {
  assert.strictEqual(this.result.status, expected);
});
```

## 5. World and state isolation

- Scenarios are independent units; avoid sharing state across scenarios.
- Put environment setup and cleanup in `Before/After`.
- Do not use global variables as a substitute for World state.

## 6. Hooks and configuration

- Common hooks: `Before`, `After`, `BeforeStep`, `AfterStep`.
- Common use case: starting/stopping resources by tags.
- The configuration file determines execution entry points, require/import, formatter, and format combinations.
- Common search order by convention: `cucumber.json`, `cucumber.yaml`, `cucumber.yml`, `cucumber.js`, `cucumber.cjs`, `cucumber.mjs`.

## 7. Result semantics

- `passed`: passed.
- `undefined`: no matching step.
- `pending`: the step implementation is marked pending.
- `failed`: implementation or assertion failed.
- `ambiguous`: multiple steps matched.
- `skipped`: skipped as a consequence of an earlier failure.
- `dry-run`: lookup/validation only; no execution.

## 8. Quick troubleshooting checklist

- undefined: confirm the step text matches the regular expression/expression.
- ambiguous: narrow the matching rule.
- pending: complete the implementation.
- failed: add/fix assertions or asynchronous handling.
- hook timeout: check hook timeout settings and resource lifecycle.
- concurrency/retry: confirm version behavior and configuration semantics.

## 9. When to consult official docs

- Formatter/plugin parameters, parallel execution, retry, sharding, CI/publish flow.
- Your project does not match the Node/Cucumber.js version.
- A parameter, return value, or boundary behavior is uncertain.
