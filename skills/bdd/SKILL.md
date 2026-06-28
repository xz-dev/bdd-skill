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

# BDD（Behavior-Driven Development）预编译手册

## 快速使用：BDD 编写和测试步骤

1. **先澄清行为**：写下 Who / What / Why、业务规则、具体正反例、未回答问题；不要从测试框架或 UI 步骤开始。
2. **写 Gherkin 草案**：用领域语言表达 `Given` 上下文、`When` 事件、`Then` 可观察结果；先按第 7 节质量门槛修文字，再写 glue code。
3. **运行规格看反馈**：用 Cucumber/Cucumber.js 跑 `.feature`，先看到 `undefined` / `pending` / failing，证明场景能驱动缺失行为。
4. **补 step definitions 和最小实现**：step definitions 只连接场景与系统行为；生产代码只做到让当前例子通过。
5. **重构并补边界**：保持场景语言稳定，抽 helper/World/hooks，补关键边界或反例；报告红绿过程和仍待确认的问题。

如果只是 review BDD/Gherkin，停在第 1–2 步和第 14 节清单；如果用户明确要求实现/测试，再进入第 3–5 步。

## 0. 标准定义先于工具

**Behavior-driven development — Wikipedia:** <https://en.wikipedia.org/wiki/Behavior-driven_development>

> “Behavior-driven development (BDD) is an agile software development method centered around collaboration between business and IT professionals that have a stake in finding a solution for a complex problem. The core objective is to achieve a shared understanding of the problem.”

> “BDD involves use of a domain-specific language (DSL) using natural-language constructs ... that can express the behavior and the expected outcomes.”

本技能从这个定义开始：**BDD 是一种围绕协作、共享理解、业务语言、具体例子和预期行为的敏捷开发方法**。BDD 可以用 Cucumber/Gherkin 实现，也可以用其他框架或轻量文档实现；**Cucumber 不是 BDD 本身，只是本技能内置的一套经典可执行规格实现参考**。

使用本技能时先问：“我们是否已经通过具体例子形成共享理解？”再问：“这些例子是否需要用 Cucumber.js 自动化？”不要反过来把 BDD 等同于“写 `.feature` 测试”。

## 1. 本技能是什么：文档预编译，而不是链接清单

本技能把 Wikipedia 的 BDD 定义、Cucumber 官方 BDD/Gherkin/Cucumber.js 文档、反模式和 JavaScript 10-minute tutorial 预编译成 AI 可立即使用的手册。未来 agent 使用本技能时，应直接从这里查标准，不要假设自己会主动回到网页重新理解。

内置内容覆盖：

- BDD 的定义、目标、误解、角色和协作流程。
- Discovery → Formulation → Automation 的工作流。
- Example Mapping、Three Amigos、User Story / Acceptance Criteria 的最小规则。
- Gherkin 语法、场景写作风格、好/坏例子、反模式。
- Cucumber.js 的项目结构、step definitions、World/state、hooks、配置、结果语义和官方 JavaScript 示例。

刻意不内置：完整 API 文档、所有 formatter/plugin/parallel/retry/sharding 选项、所有语言实现细节。需要精确配置参数或库版本时，再查官方 API/README。

## 2. Source fidelity：参考资料分层

### 第一层：BDD 定义

- **Behavior-driven development — Wikipedia**：定义 BDD 的核心是业务与 IT 相关人员协作，目标是对问题形成共享理解；常用自然语言 DSL 表达行为和预期结果；BDD 与 TDD 有历史关系，但目的不是测试语法，而是共享理解和业务语言。

### 第二层：BDD 实践模型

- **Cucumber BDD guide**：BDD 是用具体真实例子进行 Discovery、Formulation、Automation 的持续协作实践。
- **Cucumber myths**：会话比记录会话更重要，记录会话比自动化会话更重要；代码写完后再自动化场景可以是测试自动化，但不是完整 BDD；使用 Cucumber 不等于正在做 BDD。
- **Discovery workshop / Example Mapping / Who does what**：规定如何用团队角色和卡片化例子澄清范围。

### 第三层：可执行规格实现参考

- **Gherkin reference**：Feature、Rule、Scenario/Example、Given/When/Then、Background、Scenario Outline、Examples、Doc Strings、Data Tables、Tags、language。
- **Cucumber.js docs and 10-minute tutorial**：用 JavaScript 演示从 undefined → pending/failing → passing → refactor/Examples 的最小闭环。
- **Anti-patterns / Better Gherkin / FAQ**：提供可维护性边界和反模式。

## 3. BDD 核心标准

### 3.1 目标：共享理解，不是测试覆盖率

BDD 的核心问题不是“测试有没有跑”，而是：业务、开发、测试/质量是否对同一个问题空间、业务规则和可观察行为形成了共享理解。

判断是否真的在做 BDD：

- 是否先围绕具体例子对话，而不是先写实现？
- 是否用业务语言表达行为，而不是技术实现语言？
- 是否把例子写成可检查的规格，而不是抽象愿望？
- 是否让业务方/用户代表能读懂并确认？
- 自动化是否服务于规格反馈，而不是代替规格讨论？

### 3.2 BDD 与 TDD 的关系

BDD 起源上受 TDD 影响，但不要把 BDD 简化为 TDD 的 “Given/When/Then 测试语法”。Wikipedia 摘要中强调，BDD 的目的在于对问题空间形成共享理解，并用业务语言、真实数据、意图揭示、必要且聚焦的方式写下来。

可记为 **BRIEF**：

- **Business language**：业务语言，而不是类名、表名、按钮名。
- **Real data**：真实/具体数据，而不是 `foo`、`bar`、`user1`。
- **Intention revealing**：揭示意图，让读者知道为什么这个行为重要。
- **Essential**：只保留必要语义，不写无关实现步骤。
- **Focused**：每个例子聚焦一个行为/规则。

### 3.3 BDD 不是这些东西

- **不是 Cucumber 专属**：Cucumber/Gherkin 是常见实现，不是 BDD 的定义。
- **不是代码写完后的自动化补档**：那可以是 acceptance automation / characterization tests，但不是完整 BDD。
- **不是 UI 操作脚本**：`.feature` 文件描述 what，不描述 how。
- **不是大而全的测试用例仓库**：过多数据组合应被抽象到 helpers/builders，feature 文件保留关键例子。
- **不是让一个人闭门写场景**：Discovery 需要协作。

## 4. BDD 工作流：Discovery → Formulation → Automation

Cucumber 的 BDD 文档把日常 BDD 分为三类实践：Discovery、Formulation、Automation。顺序很重要：**先会话，再记录，再自动化**。

### 4.1 Discovery：发现行为和范围

目标：技术与非技术相关者一起探索某个小用户故事，找出规则、例子、边界、反例和疑问。

执行规则：

- 一次只讨论一个小故事或小变更。若 25–30 分钟内无法澄清，故事可能太大或缺少研究。
- 尽量在开发前“尽可能晚”举行 discovery，避免细节丢失，也允许计划根据新事实调整。
- 至少覆盖 Three Amigos 视角：产品/业务、开发、测试/质量。
- 先问例子，不要先问技术实现。
- 对未知问题显式记录，而不是猜。

AI agent 在没有真实三方会议时，应模拟三种视角，但必须标注哪些是推断、哪些需要用户确认。

### 4.2 Three Amigos：三种必要声音

- **Product owner / business representative**：决定范围、价值、哪些边界属于当前故事。
- **Tester / quality voice**：提出边界、失败路径、遗漏故事、系统如何破坏。
- **Developer / technical voice**：识别实现约束、依赖、隐藏复杂度和自动化可行性。

重要：场景语言初期应由全队一起建立；成熟后可以由开发+测试成对写 Gherkin，但需要产品/业务代表主动 review。

### 4.3 Example Mapping：把故事、规则、例子、问题分开

在进入开发前，用 Example Mapping 快速澄清 acceptance criteria：

- **Story（黄卡）**：当前用户故事。
- **Rules / acceptance criteria（蓝卡）**：约束、规则、验收标准。
- **Examples（绿卡）**：说明规则的具体例子。
- **Questions（红卡）**：当前无法回答的问题或假设。
- **New stories（另行记录）**：发现但延后出范围的新故事。

保持对话直到团队认为当前故事范围清晰，或时间到。未回答问题不要硬编码进规格。

### 4.4 User Story 与 Acceptance Criteria

User Story 是用于计划和优先级的小块价值功能。好故事通常满足 INVEST：Independent、Negotiable、Valuable、Estimable、Small、Testable。

常见故事格式：

```text
As an <actor>
I want a <feature>
So that <benefit>
```

BDD 不要求每个 feature 文件都使用这种格式，但需要能回答：

- Who：谁受益？
- What：需要什么能力？
- Why：为什么有价值？
- Acceptance：什么具体行为证明它完成？

### 4.5 Formulation：把例子写成可读、可自动化规格

目标：把已讨论清楚的例子写成人类和工具都能理解的形式。Cucumber 生态里通常是 Gherkin。

Formulation 要求：

- 使用领域语言。
- 具体但不技术化。
- 描述行为（what），不描述实现（how）。
- 每个场景聚焦一个行为/规则。
- 场景独立，可任意顺序运行。
- `Then` 只验证可观察结果。

### 4.6 Automation：把规格连接到系统

目标：一次自动化一个例子，用失败反馈驱动最小实现。

标准节奏：

1. 先写 scenario，运行 Cucumber，看到 `undefined`。
2. 添加 step definitions，运行，看到 `pending` 或 failing。
3. 让 step definition 调用系统行为，并在 `Then` 中断言。
4. 先看到失败（red），证明例子能捕获缺失行为。
5. 做最小实现使其通过（green）。
6. 重构实现和 step definitions，保持场景语言稳定。
7. 添加下一个例子或 `Scenario Outline`，继续循环。

如果用户只要求“写 Gherkin”，不要擅自实现生产代码；如果用户要求“用 BDD 实现”，才进入完整自动化和 red/green。

## 5. Cucumber 在本技能里的位置

Cucumber 是把 Gherkin 可执行规格连接到代码的工具。它读取 `.feature` 文件，匹配 step definitions，执行系统行为并报告结果。它是 BDD 自动化的经典实现，但不是唯一实现。

使用 Cucumber 时，仍然遵守 BDD 顺序：

1. 先对话形成例子。
2. 再写 Gherkin。
3. 最后写 step definitions 和实现。

不要因为项目已经装了 Cucumber，就跳过 Discovery；也不要因为 skill 内置 Cucumber.js 示例，就把所有 BDD 任务都假定为 JavaScript 项目。若项目使用其他语言/框架，迁移原则和 Gherkin 语言，替换自动化层。

## 6. Gherkin 预编译快速手册

### 6.1 文件和顶层结构

一个 `.feature` 文件只能有一个 `Feature`。

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

建议缩进两个空格。注释只能是新行开头的 `#`；Gherkin 不支持块注释。

### 6.2 Feature

`Feature:` 给出高层能力和场景分组。标题简短；下面的自由描述用于说明业务上下文、价值、规则列表。自由描述不会影响执行，但会进入报告。

好 Feature 描述能回答 Why / Who / What：

```gherkin
Feature: Account balance
  As a mobile bank customer
  I want to see balances for my accounts
  So that I can make informed spending decisions
```

不要把 Feature 写成技术模块名：

```gherkin
Feature: AccountController GET /api/v1/accounts JSON serializer
```

除非你的产品就是 API contract，否则这不是业务语言。

### 6.3 Rule

`Rule:` 表示一个业务规则，并把说明该规则的多个 scenarios 归组。一个 rule 应有一个或多个例子。

```gherkin
Feature: Transfer limits

  Rule: Transfers above the daily limit are rejected

    Scenario: Alice exceeds her daily limit
      Given Alice has already transferred $900 today
      When Alice tries to transfer $200 to Bob
      Then the transfer is rejected
      And Alice is told her remaining daily limit is $100
```

使用 `Rule` 可以避免 feature 文件变成无结构的 scenario 列表。

### 6.4 Scenario / Example

`Scenario` 和 `Example` 在 Gherkin 中同义。一个 scenario 是说明业务规则的具体例子，也是一条可执行测试。

官方建议每个 example 约 3–5 步；太多步骤会削弱规格/文档表达力。若一句话无法说明 scenario 目的，通常需要拆分。

### 6.5 Given / When / Then

- `Given`：初始上下文，使系统处于已知状态。避免用户交互细节。
- `When`：事件或动作，由用户或外部系统触发。
- `Then`：预期结果，必须用断言验证实际结果。
- `And` / `But`：延续前一个步骤类型，用于可读性。
- `*`：可把同类步骤写成项目列表。

```gherkin
Scenario: Transfer within the daily limit
  Given Alice has $430 in her checking account
  And Alice has not transferred money today
  When Alice transfers $125 to Bob
  Then Alice's checking balance is $305
  And Bob receives a $125 transfer notification
```

### 6.6 Step 匹配的重要限制

Cucumber 匹配 step definition 时不看 `Given` / `When` / `Then` 关键字，只匹配后面的文本。因此这些会冲突：

```gherkin
Given there is money in my account
Then there is money in my account
```

改成明确领域语言：

```gherkin
Given my account has a balance of £430
Then my account should have a balance of £430
```

### 6.7 Background

`Background` 用于所有场景都需要读者知道的共同上下文。它在每个 scenario 前执行，并且在 Before hooks 之后执行。

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

使用规则：

- 如果 setup 对业务读者重要，用 `Background` 或 `Given`。
- 如果 setup 只是启动浏览器、清理数据库，用 hooks。
- Background 保持短；超过约 4 行时考虑提高抽象或拆 Rule/Feature。
- Background 中的人名/状态应 vivid，避免 `User A` / `Site 1`。

### 6.8 Scenario Outline / Examples

当同一行为需要多组输入/输出时，用 `Scenario Outline` + `Examples`，不要复制粘贴多个几乎相同的 scenario。

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

`<day>` / `<answer>` 会在匹配 step definition 前替换为表格值。Outline 本身不直接运行；每个 Examples 行运行一次。

### 6.9 Doc Strings

Doc Strings 用于传递多行文本给 step definition。它会作为最后一个参数传入。

```gherkin
Given a blog post named "Random" with Markdown body
  """markdown
  # Some Title

  Here is the first paragraph.
  """
```

可以使用 `"""` 或反引号三连；很多编辑器对 `"""` 支持更稳定。Doc String 可标注内容类型，如 `"""markdown`。

### 6.10 Data Tables

Data Tables 用于传递结构化列表/表格，作为最后一个参数传入 step definition。

```gherkin
Given the following users exist:
  | name   | email             | role  |
  | Alice  | alice@example.com | admin |
  | Bob    | bob@example.com   | user  |
```

不要把 Data Table 当成 Excel/CSV 测试矩阵的替代品；feature 文件应保留关键例子，而不是海量测试数据。

### 6.11 Tags

Tags 用 `@` 标注 Feature、Rule、Scenario 或 Examples，用于分组、过滤、条件 hooks、报告。示例：

```gherkin
@billing @smoke
Scenario: Paid subscriber keeps access
  ...
```

常用用途：

- `@smoke` / `@critical`：快速反馈子集。
- `@wip`：临时工作标记，提交前应清理或明确策略。
- `@browser` / `@api`：执行环境分组。
- 条件 hooks：只对某些 tagged scenarios 启动浏览器或清理外部资源。

不要用 tags 掩盖场景混乱；tags 不是分类体系的替代品。

### 6.12 语言本地化

Gherkin 支持多种自然语言。语言应与用户和领域专家讨论领域时使用的语言一致，避免翻译损失。

可在 feature 文件第一行写：

```gherkin
# language: zh-CN
```

本技能示例默认用英文 Gherkin 关键字，因为 Cucumber.js tutorial 和多数项目默认英文；具体项目可按团队语言决定。

## 7. 好的 BDD/Gherkin 写作标准

### 7.0 Gherkin 质量门槛：先过场景，再写 glue code

写/审 `.feature` 时，先把 Gherkin 当作产品规格检查，而不是把它当成 runner 输入文件。任何 scenario 进入 step definitions 或实现前，至少先过这些门槛：

1. **一个可观察业务行为**：场景说明一个规则/边界/结果，不是一个笼统测试用例。
2. **领域语言优先**：读者能用业务词汇理解；没有无必要的 URL、CSS selector、数据库列、类名、HTTP 细节。
3. **具体而不技术化**：有真实角色、金额、日期、状态或对象；不用 `user1`、`foo`、`result is correct` 这类占位。
4. **Given/When/Then 语义清楚**：`Given` 建立业务上下文，`When` 触发事件，`Then` 断言外部可观察结果。
5. **短、独立、可复核**：通常 3–5 步；不依赖其他 scenario；`Background`、`Examples`、Data Table 都只承载必要语义。
6. **失败先修文字**：如果场景需要靠解释才能懂，或只能通过实现细节表达，先回到 Discovery/Formulation，而不是继续写 glue code。

### 7.1 具体，但不技术化

好例子使用具体人名、地点、日期、金额、角色和领域事实：

```gherkin
Scenario: Discount expires after campaign end date
  Given Carla has a 20% summer discount expiring on 2026-08-31
  When Carla checks out on 2026-09-01
  Then the summer discount is not applied
```

坏例子过于抽象：

```gherkin
Scenario: Discount works
  Given a user has a discount
  When the user checks out
  Then the result is correct
```

也不要技术化：

```gherkin
Scenario: Discount expires after campaign end date
  Given row id 42 exists in discounts table
  When POST /api/v1/checkout returns 200
  Then order_discounts.applied equals false
```

Cucumber 的 “Imagine it’s 1922” 启发：尽量写成没有计算机也能理解的行为；技术细节藏在 step definitions。

### 7.2 What not how

好：

```gherkin
Scenario: Subscriber can access paid content
  Given Paid Patty has a basic-level paid subscription
  When Paid Patty logs in
  Then she can read the paid article "Building Reliable Systems"
```

坏：

```gherkin
Scenario: Subscriber can access paid content
  Given I am on the login page
  When I type "paid@example.com" in the email field
  And I type "validPassword123" in the password field
  And I press the "Submit" button
  Then I see "Building Reliable Systems" inside div.article-title
```

UI 操作可在 helper 里实现；scenario 保留业务意图。

### 7.3 每个 step 表达一件事

坏 conjunction step：

```gherkin
Given I have shades and a brand new Mustang
```

好：

```gherkin
Given I have shades
And I have a brand new Mustang
```

如果多个底层动作需要合成一个高层动作，组合 helper methods，不要把 Gherkin step 文本写成复合句。

### 7.4 保持语言一致

不要在不同场景里用多种句子表达同一个状态：

```gherkin
Given I am logged in
Given I have logged in to the site
Given my session is authenticated
```

选一个领域表达并复用。语言不一致会导致 step definitions 膨胀、匹配歧义和维护成本上升。

### 7.5 每个 scenario 独立

Scenario 必须可单独运行、任意顺序运行、并行运行。不要让一个 scenario 依赖另一个 scenario 先创建数据。

- 业务可读上下文：`Given` / `Background`。
- 技术环境：hooks / fixtures / builders。
- 外部服务：测试替身或可控测试环境。
- 跨场景共享状态：不要做。

## 8. Cucumber.js 预编译快速手册

### 8.1 最小项目形态

```shell
mkdir hellocucumber
cd hellocucumber
npm init --yes
npm install --save-dev @cucumber/cucumber
mkdir -p features/step_definitions features/support
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

Node.js 版本注意：`@cucumber/cucumber@13` 要求较新的 Node.js（当前 npm 元数据为 Node `22 || 24 || >=26`）。若项目仍在 Node 20 或更旧版本，先运行：

```shell
npm view @cucumber/cucumber engines
```

选择兼容版本，不要盲目复制最新版本号。

### 8.2 常见目录

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

Cucumber.js 默认查找：

- features：`features/**/*.{feature,feature.md}`。
- support code：若 features 位于 `features/`，默认找 `features/**/*.@(js|cjs|mjs)`。

如果手动配置 `import` 或 `require`，默认 support code 查找会被替换，需要显式列全。

### 8.3 配置文件

Cucumber.js 会在项目根目录按顺序寻找：

- `cucumber.json`
- `cucumber.yaml`
- `cucumber.yml`
- `cucumber.js`
- `cucumber.cjs`
- `cucumber.mjs`

也可用 `--config` 指定。

CommonJS 示例：

```javascript
module.exports = {
  default: {
    format: ['progress-bar', 'html:cucumber-report.html'],
    require: ['features/**/*.js']
  }
};
```

ESM 示例：

```javascript
export default {
  format: ['progress-bar', 'html:cucumber-report.html'],
  import: ['features/**/*.mjs']
};
```

Tutorial 为了让 snippets 用同步函数，使用过：

```json
{
  "default": {
    "formatOptions": {
      "snippetInterface": "synchronous"
    }
  }
}
```

这是学习便利设置，不是所有项目的默认最佳实践。

### 8.4 Profiles

Profiles 用于把不同运行配置打包成命令别名。

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

运行：

```shell
cucumber-js --profile ci
# 或
cucumber-js -p ci
```

Profiles 可重复应用；CLI 上显式传入的选项仍可覆盖或追加。

### 8.5 官方 JavaScript tutorial 闭环：Is it Friday yet?

先写 `features/is_it_friday_yet.feature`：

```gherkin
Feature: Is it Friday yet?
  Everybody wants to know when it's Friday

  Scenario: Sunday isn't Friday
    Given today is Sunday
    When I ask whether it's Friday yet
    Then I should be told "Nope"
```

运行 `npm test`，先看到 undefined steps。然后写 step definitions。

`features/step_definitions/stepdefs.js`：

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

此时应失败，因为 `actualAnswer` 是 `undefined`。然后做最小实现：

```javascript
function isItFriday(today) {
  return 'Nope';
}
```

再加 Friday 例子并看到失败：

```gherkin
Scenario: Friday is Friday
  Given today is Friday
  When I ask whether it's Friday yet
  Then I should be told "TGIF"
```

收敛为 `Scenario Outline`：

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

最终 step definitions：

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

这个例子体现的是 BDD/TDD 小步反馈，不是业务复杂度本身。

## 9. Step definitions 手册

### 9.1 Step definition 是 glue code

Step definition 用表达式把 Gherkin step 文本连接到代码。当 Cucumber 执行 step 时，会寻找匹配的 step definition。

```javascript
const { Given } = require('@cucumber/cucumber');

Given('I have {int} cucumbers', function (count) {
  this.cucumbers = count;
});
```

优先使用 Cucumber Expressions：

- `{string}`：带引号字符串。
- `{int}`：整数。
- `{float}`：浮点数。
- `{word}`：单词。

需要复杂匹配时再用 RegExp：

```javascript
Given(/^I have (\d+) cucumbers$/, function (count) {
  this.cucumbers = Number(count);
});
```

不要让一个 step 能被多个 definitions 匹配；这会 ambiguous。

### 9.2 只实现真实场景需要的 steps

不要预先写“可能以后会用”的 step definitions。只实现当前 `.feature` 中已经出现的 steps；需要复用时再重构。

### 9.3 按领域概念组织 step 文件

推荐按领域对象/概念分组：

```text
features/step_definitions/
  employee_steps.js
  education_steps.js
  experience_steps.js
  authentication_steps.js
```

不推荐按 feature 文件机械绑定：

```text
features/step_definitions/
  edit_work_experience_steps.js
  edit_languages_steps.js
  edit_education_steps.js
```

后一种容易形成 feature-coupled step definitions：不可复用、重复多、维护成本高。

### 9.4 用 helper methods 复用，不要 steps 调 steps

好：

```javascript
function logInAs(world, userName) {
  world.currentUser = findUser(userName);
  world.session = createSession(world.currentUser);
}

Given('{word} is logged in', function (name) {
  logInAs(this, name);
});
```

不要在 step definition 中调用另一个 Gherkin step 文本来复用逻辑。组合和复用属于编程语言层，使用 helper、builder、fixture、domain service。

### 9.5 Step results 语义

Cucumber step 结果：

- **Success**：找到匹配 step definition，执行且没有抛错/reject。
- **Undefined**：找不到匹配 step definition；后续步骤 skipped。
- **Pending**：step definition 明确标记 pending；表示还有工作。
- **Failed**：执行时抛错/reject。
- **Skipped**：跟在 undefined/pending/failed 后，未执行。
- **Ambiguous**：多个 definitions 匹配同一步骤。

重要：返回值没有通过/失败意义；`return false`、`return null` 不会失败。

正确：

```javascript
Then('the balance should be {int}', function (expectedBalance) {
  assert.strictEqual(this.account.balance, expectedBalance);
});
```

错误：

```javascript
Then('the balance should be {int}', function (expectedBalance) {
  return this.account.balance === expectedBalance;
});
```

### 9.6 Async step definitions

Cucumber.js 支持 async/promise：

```javascript
When('Alice transfers ${int} to Bob', async function (amount) {
  this.response = await this.api.transfer({ from: 'Alice', to: 'Bob', amount });
});
```

失败应通过 assertion error、throw、或 rejected promise 表达。

## 10. State / World 手册

### 10.1 不要跨 scenario 共享状态

Cucumber state 文档的核心规则：不要在 scenarios 之间共享状态。跨场景状态泄漏会让测试脆弱，无法单独运行。

避免：

- global/static 变量保存业务状态。
- scenario 之间复用数据库记录且不清理。
- browser session/cookies 泄漏。

可做：

- `Before` hook 清理数据库。
- `Before` hook 清理 cookies。
- 每个 scenario 构建自己的测试数据。

### 10.2 Cucumber.js World

Cucumber-JS 为每个 scenario 创建隔离的 World。普通 `function () {}` step/hook 中的 `this` 指向当前 World，可在同一 scenario 的 steps 之间共享状态。

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

不要在需要 `this` 的 step/hook 中使用箭头函数：

```javascript
// 错误：箭头函数绑定词法 this，无法使用 Cucumber World。
Given('Alice has $430', () => {
  this.account = new Account('Alice', 430);
});
```

本技能默认建议 Cucumber.js step definitions 和 hooks 使用普通函数，除非明确不需要 World 且团队已有约定。

### 10.3 World 参数

Cucumber.js 可通过 `worldParameters` 把环境参数传给 World，例如 app URL、浏览器类型、测试租户等。适合环境配置，不适合业务规则决策。

```javascript
module.exports = {
  default: {
    worldParameters: {
      appUrl: process.env.APP_URL || 'http://localhost:3000/'
    }
  }
};
```

不要把 secret 写进 feature 文件或提交到配置。

## 11. Hooks 手册

Hooks 是在 Cucumber 执行周期中运行的代码块，通常用于环境 setup/teardown。

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

Cucumber 明确提醒：Before hook 里的事情对只读 feature 的人不可见。如果 setup 对业务理解重要，用 `Background` 或 `Given`；hook 只放低层逻辑，如启动浏览器、删除数据库数据、重置测试环境。

### 11.2 Conditional hooks

可以用 tags 限定 hooks：

```javascript
Before({ tags: '@browser' }, async function () {
  this.browser = await startBrowser();
});
```

适合只对 UI scenarios 启动浏览器，或只对某类外部资源做清理。

### 11.3 BeforeStep / AfterStep

用于每一步前后插入逻辑，例如调试、截图、日志。不要滥用；如果每步都在做复杂工作，可能说明测试架构需要重构。

```javascript
const { AfterStep } = require('@cucumber/cucumber');

AfterStep(async function ({ pickleStep }) {
  if (this.debug) {
    this.log(`finished step: ${pickleStep.text}`);
  }
});
```

失败截图常放在 `After` hook 中根据 scenario 状态处理，而不是污染业务场景。

## 12. 反模式与修正

### 12.1 “用 Cucumber 就是 BDD”

错误：装了 Cucumber，写了 feature 文件，但没有协作、没有例子讨论、没有业务反馈。

修正：恢复 Discovery → Formulation → Automation。至少让下一个故事从具体例子开始。

### 12.2 代码写完后补场景却称为 BDD

错误：实现完成后，为了测试覆盖率补 `.feature`。

修正：称为 acceptance automation / characterization；对未来变更重新采用 BDD 流程。

### 12.3 过程化 UI 脚本

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

### 12.4 Feature-coupled step definitions

错误：每个 feature 文件一个同名 steps 文件，里面写只服务该 feature 的句子。

修正：按领域概念分组 step definitions，用 domain-related names。

### 12.5 Conjunction steps

错误：一个 step 同时做多件事。

修正：拆成多个 steps，或在 step definition 中调用 helper methods 组合底层动作。

### 12.6 Steps 调 steps

错误：在 step definition 里用 Gherkin step 文本调用另一个 step 来复用。

修正：抽普通 JavaScript 函数、domain helper、builder。

### 12.7 条件跳过 scenario 或 step

如果场景运行时根据条件跳过，多半说明一个 scenario 覆盖太多行为，或数据/环境不可控。拆场景并修复根因。

### 12.8 Excel/CSV 测试用例替代 feature 文件

Cucumber FAQ 不建议把测试用例保存在 Excel/CSV 中再由 Cucumber 读取。Feature 文件本身应该是可读的 executable specifications。若数据太多，通常表示场景抽象层级错误。

### 12.9 验证深层实现细节

错误：`Then` 检查数据库内部列、私有对象字段、日志实现细节。

修正：验证用户或外部系统可观察输出：UI、API 响应、消息、报告、通知、状态变化的公开表现。

## 13. AI agent 操作协议

当用户要求“用 BDD 开发/设计/验收”时：

1. **先按 BDD 定义定位任务**：这是协作/规格问题，还是只是 Cucumber 自动化问题？不要直接跳到工具。
2. **读取证据**：需求、issue、代码、现有测试、领域词汇、产品文档。
3. **切小故事**：把大需求切成可在一次 discovery 中澄清的小行为。
4. **发现例子**：列正常例子、边界例子、拒绝/失败例子、未回答问题。
5. **模拟 Three Amigos**：分别列产品范围、测试边界、开发约束；需要用户决策时问最小问题。
6. **写 Gherkin 草案并先过质量门槛**：业务语言、具体数据、what not how；在写 step definitions 前先按第 7 节检查场景语义与写作质量。
7. **确认产品语义**：涉及规则/范围/边界时先确认；不要把猜测写进代码。
8. **自动化**：若用户要求实现，添加/更新 `.feature` 和 step definitions，先看到 undefined/pending/failing。
9. **最小实现**：只写让当前例子通过的代码。
10. **重构**：按领域组织 steps，抽 helpers，去重语言。
11. **报告证据**：列 scenarios、运行命令、红绿过程、残留问题。

如果用户只要求“review BDD”，不要擅自修改；输出具体发现和最小修正建议。

## 14. BDD/Gherkin 评审清单

### BDD 层

- [ ] 是否以共享理解为目标，而不是只追测试覆盖率？
- [ ] 是否先讨论具体例子，再写实现？
- [ ] 是否明确 Who / What / Why？
- [ ] 是否标出未回答问题和假设？
- [ ] 是否避免把 Cucumber 使用本身等同于 BDD？

### Scenario 层

- [ ] 每个 scenario 是否说明一个具体业务规则/行为？
- [ ] 是否使用具体真实数据，而非抽象占位？
- [ ] 是否描述 what，而不是 how？
- [ ] 是否避免 URL、按钮、CSS、数据库列等实现细节？
- [ ] 步骤是否大致 3–5 个？
- [ ] scenario 是否独立、可任意顺序运行？
- [ ] `Then` 是否验证可观察结果？
- [ ] Background 是否短且业务可读？
- [ ] 是否用 Scenario Outline 消除重复例子？
- [ ] 是否避免把海量数据塞进 Examples/Data Tables？

### Step/code 层

- [ ] 是否只实现已有 scenario 中出现的 steps？
- [ ] step definitions 是否按领域概念组织？
- [ ] 是否避免 feature-coupled steps？
- [ ] 是否用 helper methods 复用，而不是 steps 调 steps？
- [ ] Cucumber.js 中需要 World 的 steps/hooks 是否使用 `function () {}`？
- [ ] `Then` 是否使用 assertion/throw/reject，而不是返回 false？
- [ ] hooks 是否只放低层技术准备/清理？
- [ ] 是否避免跨 scenario 共享状态？
- [ ] 是否记录了至少一次失败反馈？

## 15. 快速模板

### 15.1 Discovery 输出模板

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

### 15.2 Feature 模板

```gherkin
Feature: <business capability>
  <why this matters>

  Rule: <business rule>

    Scenario: <concrete example title>
      Given <known business context>
      When <observable event/action>
      Then <observable expected outcome>
```

### 15.3 Step definition 模板

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

## 16. 何时回查官方文档

本技能已经内置大部分常用标准。只有在以下情况回查官方文档：

- 需要精确 CLI/config option、formatter、plugin、parallel/retry/sharding 行为。
- 项目使用非 JavaScript Cucumber 实现，需要语言特定 API。
- Cucumber.js 版本与本技能示例不同，需要确认 Node engines 或 breaking changes。
- 需要完整 DataTable/DocString API 或 custom parameter types。
- 需要 debug formatter/reporting/publish 细节。

默认情况下，写/审 BDD 场景时直接使用本手册，不要把“去看链接”作为替代工作。

## 17. 参考资料

### 17.1 本地参考（优先）

用于未来 AI agent 的默认阅读顺序：

- [official-reference-map.md](references/official-reference-map.md)
  - 先判断当前问题是“实践问题 / 场景写作 / 执行问题”，再选择下一步。
- [bdd-practice-reference.md](references/bdd-practice-reference.md)
  - Discovery / Formulation / Automation、Example Mapping、Three Amigos、Story 与 AC。
- [gherkin-cucumber-reference.md](references/gherkin-cucumber-reference.md)
  - Gherkin 语法结构、场景可维护性、常见反模式修正。
- [cucumber-js-reference.md](references/cucumber-js-reference.md)
  - Cucumber.js 运行侧（Step definitions、World、Hooks、配置、排障）。
### 17.2 外部官方入口（按需）

- 定义与实践：
  - Behavior-driven development — Wikipedia: <https://en.wikipedia.org/wiki/Behavior-driven_development>
  - Cucumber BDD Guide: <https://cucumber.io/docs/bdd/>
  - Cucumber Discovery Workshop: <https://cucumber.io/docs/bdd/discovery-workshop/>
  - Cucumber Example Mapping: <https://cucumber.io/docs/bdd/example-mapping/>
  - Cucumber Who does what / Three Amigos: <https://cucumber.io/docs/bdd/who-does-what/>
  - Cucumber Myths: <https://cucumber.io/docs/bdd/myths/>
- Gherkin 与写法：
  - Gherkin reference: <https://cucumber.io/docs/gherkin/reference/>
  - Step organization: <https://cucumber.io/docs/gherkin/step-organization/>
  - Writing better Gherkin: <https://cucumber.io/docs/bdd/better-gherkin/>
  - Cucumber Anti-patterns: <https://cucumber.io/docs/guides/anti-patterns/>
  - Step definitions: <https://cucumber.io/docs/cucumber/step-definitions/>
  - Cucumber API/reference: <https://cucumber.io/docs/cucumber/api/>
- Cucumber.js（JS 执行）：
  - Cucumber state / World: <https://cucumber.io/docs/cucumber/state/>
  - Cucumber.js configuration: <https://github.com/cucumber/cucumber-js/blob/main/docs/configuration.md>
  - Cucumber.js profiles: <https://github.com/cucumber/cucumber-js/blob/main/docs/profiles.md>
  - Cucumber.js hooks: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/hooks.md>
  - Cucumber.js world: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/world.md>
  - plugins/formatter/parallel/retry/sharding 等按需查 Cucumber.js docs: <https://github.com/cucumber/cucumber-js/tree/main/docs>
- 教程与扩展：
  - Cucumber 10-minute tutorial（JavaScript）: <https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript>

### 17.3 使用建议

- 默认不先读外链。除非本地文档无法快速回答，或需要精确版本参数（CLI、formatter、parallel/retry 等）。
- 任何时候先确认：行为协作问题是否先于工具。
- 若出现细节分歧，结合本地参考与官方文档逐步补齐。
