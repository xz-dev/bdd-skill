---
name: bdd
description: Use Behavior-Driven Development (BDD) with Cucumber/Gherkin-style executable specifications. Use when defining behavior, writing acceptance criteria, creating or reviewing .feature files, implementing Cucumber.js step definitions, or turning user stories into concrete examples before code.
version: 0.1.0
author: Xiangzhe and AI assistant
license: MIT
metadata:
  hermes:
    tags: [bdd, behavior-driven-development, cucumber, gherkin, acceptance-tests, executable-specifications, javascript]
  source:
    wikipedia_bdd: "https://en.wikipedia.org/wiki/Behavior-driven_development"
    cucumber_docs: "https://cucumber.io/docs/"
    cucumber_javascript_tutorial: "https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript"
---

# BDD（Behavior-Driven Development）编程指南

## 这项技能的目标

用 BDD 帮助团队把“要做什么”说清楚，再把这些例子变成可执行规格（executable specification）。

本技能严格以以下材料为准：

- Wikipedia 对 BDD 的定义：BDD 是以业务和技术相关人员协作为中心的敏捷软件开发方法，核心目标是形成对问题的共享理解，并常用自然语言 DSL 表达行为和预期结果。
- Cucumber 官方文档：BDD 不是“写测试工具”本身，而是围绕具体例子持续进行 Discovery、Formulation、Automation。
- Cucumber/Gherkin 范式：用 `.feature` 文件、`Feature` / `Rule` / `Scenario` / `Given` / `When` / `Then` 表达行为，用 step definitions 将自然语言步骤连接到代码。
- Cucumber 10-minute tutorial：采用 JavaScript 示例，因为结构简单，能清楚展示从 undefined → pending → failing → passing → refactor / examples 的 BDD 工作流。

## 什么时候使用

使用本技能，当用户要：

- 设计或澄清用户故事、验收标准、业务规则、边界例子。
- 编写、评审或重构 Gherkin `.feature` 文件。
- 用 Cucumber.js / JavaScript 实现 BDD 自动化。
- 把“需求描述”改写成可讨论、可执行、可维护的例子。
- 检查 Cucumber 场景是否过度 UI 化、过度技术化、feature-coupled、步骤耦合或不可复用。

不要把本技能当成普通测试模板。只在真正需要用例子澄清行为、验收规则或可执行规格时使用。

## BDD 的核心定义

BDD 的中心不是“测试覆盖率”，而是**共享理解**。

按照 Wikipedia 和 Cucumber 文档，可以把 BDD 约束为：

1. **协作**：业务人员、开发者、测试/质量人员共同澄清问题。
2. **具体例子**：用真实、具体、领域化的数据来说明系统应该如何表现。
3. **自然语言 DSL**：用业务可读的半形式化语言描述行为；Gherkin 是 Cucumber 生态中的典型形式。
4. **可执行规格**：规格既是文档，也是自动化验收反馈。
5. **Outside-in**：从用户/外部系统能观察到的价值和行为出发，而不是从内部实现细节出发。

BDD 起源上与 TDD 有关系，但不要把它简化为 TDD 的测试语法。Cucumber 明确强调：BDD 是 discovery、collaboration、examples；Cucumber 只是支持这个过程的工具。

## 标准 BDD 流程：Discovery → Formulation → Automation

### 1. Discovery：发现“它可能应该做什么”

目标：通过对话发现业务规则、例子、反例、边界、例外和真正的验收语义。

执行方式：

- 选一个小的用户故事或小变更，不要一次讨论整个系统。
- 组织 Three Amigos 视角：业务/产品、开发、测试/质量；AI agent 在没有真人角色时要显式模拟这些视角并标注假设。
- 先谈例子，再谈实现。问：
  - 谁从这个行为获得价值？
  - 正常路径是什么？
  - 哪些输入应该被拒绝？
  - 边界值、异常状态、权限差异、时间/金额/库存等领域边界在哪里？
  - 用户或外部系统能观察到什么结果？
- 如果当前代码或文档能回答问题，先读取证据，不要过早问用户。
- 如果缺少业务决定，提出最小必要问题；不要用猜测代替领域决策。

产物：一组具体例子、业务规则、待确认假设。

### 2. Formulation：把例子写成可自动化文档

目标：把已达成共识的例子写成 Gherkin，使人和工具都能读。

要求：

- 使用业务语言和领域词汇。
- 描述行为（what），不要描述实现（how）。
- 例子要具体，不要抽象；但不要把技术/UI细节塞进场景。
- 每个场景尽量只测试一个行为，失败时原因清晰。
- 每个场景推荐 3–5 个步骤；步骤过多会削弱规格和文档表达力。
- `Then` 验证可观察结果：UI 显示、API 响应、消息、报告、外部效果；不要为了方便直接检查深层数据库内部状态。

产物：`.feature` 文件中的 `Feature` / `Rule` / `Scenario` / `Scenario Outline`。

### 3. Automation：把规格连接到系统并驱动实现

目标：一次自动化一个例子，用失败反馈推动最小实现。

标准节奏：

1. 先写场景，运行 Cucumber，看到 `undefined`。
2. 添加必要 step definitions，运行，看到 `pending` 或 failing。
3. 让 step definition 调用系统行为，并在 `Then` 中断言预期结果。
4. 先看到失败（red），确认例子确实能捕获缺失行为。
5. 做最小实现使其通过（green）。
6. 重构实现和 step definitions，保持场景语言稳定。
7. 增加新的具体例子或 `Scenario Outline`，继续循环。

如果代码已经写完后才补 Cucumber 场景，这可以是测试自动化，但不要声称这是完整 BDD；BDD 的发现和表述应该先参与设计。

## Gherkin 编写规则

### 基本结构

```gherkin
Feature: <能力或业务主题>
  <这个能力为什么重要，服务谁，解决什么问题>

  Rule: <一条业务规则>

    Scenario: <一个具体例子>
      Given <初始上下文>
      When <触发事件或动作>
      Then <可观察结果>
```

- 一个 `.feature` 文件只有一个 `Feature`。
- `Rule` 用来把同一 feature 下的多个场景按业务规则分组。
- `Scenario` 和 `Example` 在 Gherkin 中同义；本技能默认使用更常见的 `Scenario`。
- `Scenario Outline` + `Examples` 用于同一行为在多组输入/输出上的例子。
- `Background` 只放所有场景共同且需要读者知道的上下文；低层技术准备优先放 hook。

### Given / When / Then

- `Given`：初始上下文，让系统处于明确状态。避免写用户交互细节。
- `When`：发生的事件或动作。通常是用户或外部系统触发的单一行为。
- `Then`：预期结果。必须用断言验证实际结果与预期结果一致。
- `And` / `But`：只用于可读性，延续前一个步骤类型。
- `*`：可用于列表式步骤，但不要滥用。

注意：Cucumber 匹配 step definition 时不看 `Given` / `When` / `Then` 关键字，只匹配后面的文本。因此下面两句会冲突：

```gherkin
Given there is money in my account
Then there is money in my account
```

改成更明确的领域语言：

```gherkin
Given my account has a balance of £430
Then my account should have a balance of £430
```

### 好的场景语言

好的 Gherkin：

- 讲业务行为，不讲按钮、CSS、URL、数据库表。
- 使用具体领域数据：人名、日期、金额、角色、状态。
- 保持语言一致；同一个意思不要写三种句子。
- 每个步骤表达一件事；步骤中间出现 “and” 往往应该拆成两个步骤。
- 问自己：如果 UI 或实现换了，这个场景还应该成立吗？如果不成立，多半写得太实现化。

#### 正确：描述行为

```gherkin
Scenario: Subscriber with a paid subscription can access paid content
  Given Paid Patty has a basic-level paid subscription
  When Paid Patty logs in with her valid credentials
  Then she sees a Free article and a Paid article
```

#### 错误：描述 UI 操作过程

```gherkin
Scenario: Subscriber with a paid subscription can access paid content
  Given I am on the login page
  When I type "paid@example.com" in the email field
  And I type "validPassword123" in the password field
  And I press the "Submit" button
  Then I see "FreeArticle1" and "PaidArticle1" on the home page
```

UI 自动化可以在 step definition/helper 里做；`.feature` 里保留业务意图。

### 具体但不技术化

BDD 例子应具体，不要抽象：

```gherkin
Scenario: Transfer within the daily limit
  Given Alice has $430 in her checking account
  And Alice has not transferred money today
  When Alice transfers $125 to Bob
  Then Alice's checking balance is $305
  And Bob receives a $125 transfer notification
```

但不要写成：

```gherkin
Scenario: Transfer within the daily limit
  Given row id 42 exists in accounts table
  When POST /api/v1/transfer returns 200
  Then transfers.status column equals "sent"
```

除非你的产品本身就是 API contract，普通业务 BDD 不应该暴露内部实现。

## Cucumber.js 标准项目形态

最小 JavaScript 项目：

```shell
mkdir hellocucumber
cd hellocucumber
npm init --yes
npm install --save-dev @cucumber/cucumber
mkdir -p features/step_definitions
```

`package.json`：

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

Cucumber 官方 tutorial 为了让生成 snippets 使用同步函数，创建了 `cucumber.json`：

```json
{
  "default": {
    "formatOptions": {
      "snippetInterface": "synchronous"
    }
  }
}
```

这只是 tutorial 便利设置；实际项目可按团队需要选择 sync/async、ESM/CommonJS、profiles、formatters、parallel、tags 等配置。

Cucumber.js 应作为项目依赖安装，不要依赖全局安装；support files 需要 `require('@cucumber/cucumber')` 或 `import` 本项目依赖。

注意 Node.js 版本：`@cucumber/cucumber@13` 要求较新的 Node.js（当前 npm 元数据为 Node `22 || 24 || >=26`）。如果项目仍在 Node 20 或更旧版本上，先查看 Cucumber.js 安装文档/`npm view @cucumber/cucumber engines`，选择兼容版本，而不是盲目复制最新版本号。

## Cucumber.js 示例：Is it Friday yet?

### 1. 先写场景

`features/is_it_friday_yet.feature`：

```gherkin
Feature: Is it Friday yet?
  Everybody wants to know when it's Friday

  Scenario: Sunday isn't Friday
    Given today is Sunday
    When I ask whether it's Friday yet
    Then I should be told "Nope"
```

运行：

```shell
npm test
```

期望先看到 undefined steps。Cucumber 会提示可以实现的 snippets。这是正确进展：规格先于实现。

### 2. 加 step definitions，使其从 pending 进入 failing

`features/step_definitions/stepdefs.js`：

```javascript
const assert = require('assert');
const { Given, When, Then } = require('@cucumber/cucumber');

function isItFriday(today) {
  // Intentionally blank: first run should fail.
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

运行后应该失败，因为 `actualAnswer` 是 `undefined` 而不是 `"Nope"`。这证明场景确实能捕获缺失行为。

### 3. 做最小实现使第一个例子通过

```javascript
function isItFriday(today) {
  return 'Nope';
}
```

第一个例子通过，但实现显然还不完整。这是 BDD/TDD 的小步反馈，不是最终设计。

### 4. 添加第二个失败例子

```gherkin
Scenario: Friday is Friday
  Given today is Friday
  When I ask whether it's Friday yet
  Then I should be told "TGIF"
```

先添加最小 step：

```javascript
Given('today is Friday', function () {
  this.today = 'Friday';
});
```

运行应该失败：`"Nope"` 不等于 `"TGIF"`。

### 5. 使两个例子通过

```javascript
function isItFriday(today) {
  if (today === 'Friday') {
    return 'TGIF';
  }
  return 'Nope';
}
```

### 6. 用 Scenario Outline 收敛重复例子

```gherkin
Feature: Is it Friday yet?
  Everybody wants to know when it's Friday

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

对应 step definitions：

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

## Step definitions 编写规则

### 用 Cucumber Expressions 优先表达参数

优先：

```javascript
Given('today is {string}', function (givenDay) {
  this.today = givenDay;
});

Given('I have {int} cucumbers', function (count) {
  this.cucumbers = count;
});
```

必要时再用正则。不要同一个 step definition 同时混用 Cucumber Expression 和 regex 语义。

### 只实现真实场景需要的 steps

不要预先写一堆“将来可能用到”的 step definitions。Cucumber 文档建议只实现场景中已经出现的步骤；否则会产生 cruft、重复和歧义。

### 按领域概念组织 step 文件

推荐：

```text
features/
  account.feature
  transfer.feature
  step_definitions/
    account_steps.js
    transfer_steps.js
    authentication_steps.js
```

不推荐按 feature 文件机械绑定：

```text
features/
  edit_work_experience.feature
  edit_languages.feature
  step_definitions/
    edit_work_experience_steps.js
    edit_languages_steps.js
```

后者容易形成 feature-coupled step definitions，复用差、重复多、维护成本高。

### 使用 helper methods 复用实现，不要让 steps 调 steps

如果多个 step definitions 需要共同动作，抽取普通 JavaScript helper：

```javascript
function logInAs(world, userName) {
  world.currentUser = findUser(userName);
  world.session = createSession(world.currentUser);
}

Given('{word} is logged in', function (name) {
  logInAs(this, name);
});
```

不要通过“从一个 step definition 调另一个 Gherkin step”来复用。组合与复用应该用编程语言自身的函数、类、fixture、builder。

### 正确使用 World / this

Cucumber.js 为每个 scenario 提供隔离的 World 上下文。普通函数的 `this` 指向当前 World，可在步骤之间共享状态：

```javascript
Given('Alice has $430', function () {
  this.account = new Account('Alice', 430);
});
```

不要在需要 `this` 的 step/hook 中使用箭头函数：

```javascript
// 错误：箭头函数绑定词法 this，无法使用 Cucumber World。
Given('Alice has $430', () => {
  this.account = new Account('Alice', 430);
});
```

如果不需要 World，箭头函数也许能工作；但为了统一和避免未来维护陷阱，本技能建议 Cucumber.js step definitions 和 hooks 默认使用 `function () {}`。

### `Then` 必须断言；返回 false 不会失败

Cucumber step definition 成功/失败取决于是否抛出错误或 rejected promise。返回 `false`、`null` 等值不会让步骤失败。

正确：

```javascript
Then('the balance should be {int}', function (expectedBalance) {
  assert.strictEqual(this.account.balance, expectedBalance);
});
```

错误：

```javascript
Then('the balance should be {int}', function (expectedBalance) {
  return this.account.balance === expectedBalance; // Cucumber 不会因 false 自动失败
});
```

### Hooks 只放低层技术准备/清理

可以用 hooks：

```javascript
const { Before, After } = require('@cucumber/cucumber');

Before(async function () {
  this.browser = await startBrowser();
});

After(async function () {
  await this.browser?.close();
});
```

但 Cucumber 文档提醒：hook 中发生的事情对只读 feature 的人不可见。如果准备条件对业务理解重要，优先写成 `Background` 或 `Given`；hooks 只放启动浏览器、清理数据库、重置外部测试环境等低层技术逻辑。

## 常见反模式与修正

### 反模式：把 BDD 当成“自动化测试 after the fact”

症状：实现完成后才补 `.feature`，没有具体例子讨论，没有业务反馈。

修正：至少对下一个变更恢复 Discovery → Formulation → Automation。对既有代码补规格时，明确说这是 characterization/acceptance automation，不要假装已经完成 BDD。

### 反模式：过程化 UI 脚本

错误：

```gherkin
When I enter "Bob" in the "user name" field
And I enter "tester" in the "password" field
And I press the "login" button
```

正确：

```gherkin
When "Bob" logs in
```

UI 操作放到 step definition/helper 中。

### 反模式：conjunction step

错误：

```gherkin
Given I have shades and a brand new Mustang
```

正确：

```gherkin
Given I have shades
And I have a brand new Mustang
```

如果为了可读性需要组合多个底层动作，组合 helper methods，不要组合 Gherkin step 文本。

### 反模式：场景依赖顺序或复用另一个场景

每个 scenario 必须独立，可单独运行、任意顺序运行、并行运行。不要让一个 scenario 依赖前一个 scenario 创建的数据。共享动作抽 helper；共享上下文用 `Background` 或 fixtures；共享低层环境用 hooks。

### 反模式：过多技术细节或外部 CSV/Excel 测试用例

Cucumber FAQ 明确不建议用 Excel/CSV 保存测试用例，因为 feature 文件本身应该是可读的 executable specification。若数据太多，通常说明 feature 文件细节过多；把构造细节移到 step definitions、helper 或 builder 中。

### 反模式：条件跳过步骤

如果你想在 scenario 中根据条件跳过后续步骤，多半说明一个场景测试了太多事情，或测试环境/数据不可控。拆分场景并修复根因。

## AI agent 工作协议

当用户要求“用 BDD 开发/设计/验收”时，按下面协议执行：

1. **先找证据**：读取需求、issue、代码、现有测试、文档、领域词汇。
2. **识别小变更**：把大需求切成一个可讨论的小行为；不要一次写完整系统规格。
3. **发现例子**：列出正常例子、边界例子、失败/拒绝例子；缺业务决定时问最小必要问题。
4. **写 Gherkin 草案**：用业务语言，保持具体，避免 UI/技术细节。
5. **和用户确认**：如果例子表达了产品语义或边界决策，先确认再实现。
6. **自动化**：用 Cucumber.js 创建/更新 `.feature` 和 step definitions；先运行看到 undefined/pending/failing，再实现。
7. **最小实现**：只写让当前例子通过所需的代码。
8. **重构**：去重 step definitions，抽 helper，按领域概念组织。
9. **报告证据**：列出新增/修改的 scenarios、运行命令、红绿过程或无法验证的原因。

如果用户只要求“写 Gherkin”，不要擅自实现生产代码；如果用户要求“实现 BDD”，则需要完整 red-green 反馈。

## 评审清单

在提交 BDD 相关改动前检查：

- [ ] 是否先明确了用户故事或小变更？
- [ ] 是否至少有一个具体例子，而不是抽象规则？
- [ ] 例子是否使用领域语言和真实业务数据？
- [ ] 场景是否描述 what，而不是 how？
- [ ] 每个 scenario 是否只验证一个行为？
- [ ] 每个 scenario 是否独立、可任意顺序运行？
- [ ] `Then` 是否验证可观察输出？
- [ ] 步骤数量是否大致 3–5，且每步只表达一件事？
- [ ] 是否避免 feature-coupled step definitions？
- [ ] 是否只实现了已有场景需要的 step definitions？
- [ ] 是否用 helper methods 复用实现，而不是 steps 调 steps？
- [ ] Cucumber.js step/hook 中需要 World 时是否使用 `function () {}`？
- [ ] 是否运行 Cucumber 并记录结果？
- [ ] 是否有至少一次失败反馈证明新例子能捕获缺失行为？

## 参考资料

- Behavior-driven development — Wikipedia: <https://en.wikipedia.org/wiki/Behavior-driven_development>
- Cucumber Introduction: <https://cucumber.io/docs/>
- Cucumber BDD: <https://cucumber.io/docs/bdd/>
- Cucumber 10-minute tutorial (JavaScript): <https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript>
- Gherkin reference: <https://cucumber.io/docs/gherkin/reference/>
- Writing better Gherkin: <https://cucumber.io/docs/bdd/better-gherkin/>
- BDD examples: <https://cucumber.io/docs/bdd/examples/>
- Who does what / Three Amigos: <https://cucumber.io/docs/bdd/who-does-what/>
- Step organization: <https://cucumber.io/docs/gherkin/step-organization/>
- Step definitions: <https://cucumber.io/docs/cucumber/step-definitions/>
- Cucumber API/reference: <https://cucumber.io/docs/cucumber/api/>
- Anti-patterns: <https://cucumber.io/docs/guides/anti-patterns/>
- FAQ: <https://cucumber.io/docs/faq/>
