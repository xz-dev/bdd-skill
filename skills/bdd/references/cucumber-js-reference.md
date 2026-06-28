# Cucumber.js 参考：从场景到执行

> 这不是完整 API 文档；是落地 Cucumber.js 的高频决策地图。

## 1. 何时阅读

- 你已经有可执行场景草稿，需要把它跑起来。
- 运行时出现 `undefined`、`pending`、`failing`、`ambiguous`。
- 需要排查 hooks、tags、配置、CI 兼容。

## 2. 核心对象

- `features/`：默认 feature 根目录（按项目约定）。
- `Given/When/Then`：绑定到 steps。
- Step definitions：定义场景与 step 之间的映射。
- World：每个 scenario 的上下文状态。
- Hooks：`Before/After`（含标签过滤）。
- 配置文件：`cucumber.json` / `cucumber.yml` / `cucumber.js`。

## 3. 典型执行闭环

1. 写场景。
2. 运行 `cucumber-js`（通常先看到 `undefined`）。
3. 添加匹配 step definitions。
4. 运行到 `pending/failing`。
5. 最小实现通过。
6. 重构、补边界。

## 4. Step definitions 与语言

- 常用表达：`{string}`、`{int}`、`{float}`、`{word}`。
- 复杂匹配时再使用正则表达式。
- 需要 `this`（World）时使用 function，不要用箭头函数。

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

## 5. World 与状态隔离

- 场景是独立单元；避免跨场景共享状态。
- 把环境初始化和清理放进 `Before/After`。
- 不要用全局变量代替世界状态。

## 6. Hooks 与配置

- 常见 hooks：`Before`、`After`、`BeforeStep`、`AfterStep`。
- 常见场景：按 tags 启停资源。
- 配置文件会决定执行入口、require/import、formatter、format 组合等。
- 常见搜索顺序（按约定）：`cucumber.json`、`cucumber.yaml`、`cucumber.yml`、`cucumber.js`、`cucumber.cjs`、`cucumber.mjs`。

## 7. 结果语义

- `passed`：通过。
- `undefined`：缺少匹配 step。
- `pending`：步实现标记为待完成。
- `failed`：实现或断言失败。
- `ambiguous`：多个 step 匹配。
- `skipped`：前序失败后的连带跳过。
- `dry-run`：仅做查找/验证，不执行。

## 8. 快速排查清单

- undefined：确认 step 文案与正则/表达式一致。
- ambiguous：缩窄匹配规则。
- pending：补实现。
- failed：添加/修正断言或异步处理。
- hook timeout：检查钩子超时设置与资源生命周期。
- 并发/重试：确认版本行为与配置语义。

## 9. 什么时候查官方文档

- formatter/插件参数、并行、重试、分片、CI/发布流程。
- 你的项目与 Node/Cucumber.js 版本不匹配。
- 参数、返回值、边界行为不确定时。
