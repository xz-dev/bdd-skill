# BDD 实践参考：BDD 的协作闭环

> 目的：回答“行为、需求、验收到底要讲清什么”，再决定是否走到 Cucumber.js 自动化。

## 1. 核心立场（先于工具）

- BDD 不是“特定测试框架”，而是以协作为核心的行为规格方法。
- 目标是让业务与开发形成**共享理解**：
  - 同一个目标
  - 明确的规则边界
  - 能被反例打破/更新的可执行示例
- 自动化是手段，不是定义。Cucumber/Gherkin 可以是实现方式，但不是 BDD 本身。

## 2. Discovery（发现）：先澄清行为，再谈实现

在 Discovery 中先解决：

- 我们到底要解决哪个业务问题？
- 哪些是规则、边界和异常？
- 还有哪些未回答问题？

建议产出：

- Story（故事）
- Rules（规则）
- Examples（示例）
- Questions（问题）

### 常见触发

- 团队对“同一个需求是否一致”有分歧
- 新故事反复修改但未稳定
- 场景写出来仍反复争论边界行为

### 快速判断

- 先问：Who / What / Why
- 先明确：什么算成功？失败案例如何定义？
- 先留：无法确认的假设，不要把它写进已确认规则

## 3. Formulation（表达）：把发现变成可沟通的规格

### Example Mapping 模型

- **Story（黄卡）**：叙述目标或故事
- **Rules（蓝卡）**：验收规则与边界条件
- **Examples（绿卡）**：可验证的正/反例
- **Questions（红卡）**：仍待确认的问题

### Three Amigos

- **产品/业务**：价值与范围
- **测试/质量**：边界与失败路径
- **开发**：实现约束与可行性

建议先输出最小结构：

```markdown
## Story
As a <actor>
I want <capability>
So that <benefit>

## Rules
- R1: ...
- R2: ...

## Examples
- Example: <具体可执行例子>
  - Given ...
  - When ...
  - Then ...

## Questions
- [ ] ...

## Out of scope
- ...
```

### User Story 与 Acceptance Criteria

- User Story 回答的是“谁 / 需要什么 / 为什么有价值”。
- AC 要可验证，至少能描述：
  - 可观察结果
  - 边界条件
  - 反例

## 4. Automation（自动化）：把闭环收口到反馈

典型节奏（适用于每个小行为）：

1. 写出场景或规则示例（不追求一上来全覆盖）
2. 运行并看到 `undefined`
3. 补 step definitions
4. 看到失败（assert/边界失败）
5. 做最小实现让它通过
6. 重构并补关键边界例子

自动化检查的是行为是否被正确执行，不是代替需求澄清。

## 5. 常见反模式

- 写了代码后再补场景（反向闭环）
- 用技术动作代替业务语言
- 场景之间存在运行顺序依赖
- 把未回答问题当成已确认规则
- 用大量数据表替代场景抽象

## 6. 何时回看官方来源

- `Discovery / Formulation / Automation` 及实践框架：Cucumber BDD 文档 / Three Amigos / Example Mapping。
- 反模式/写作风格：Cucumber Better Gherkin / Anti-patterns。
- 需要版本或实现细节：到对应官方文档再确认。

## 7. 精简外部入口清单

- Wikipedia: Behavior-driven development: https://en.wikipedia.org/wiki/Behavior-driven_development
- Cucumber BDD Guide: https://cucumber.io/docs/bdd/
- Cucumber Discovery Workshop: https://cucumber.io/docs/bdd/discovery-workshop/
- Cucumber Example Mapping: https://cucumber.io/docs/bdd/example-mapping/
- Cucumber Who does what: https://cucumber.io/docs/bdd/who-does-what/
- Cucumber Myths: https://cucumber.io/docs/bdd/myths/
- Cucumber Better Gherkin: https://cucumber.io/docs/bdd/better-gherkin/
- Cucumber Anti-patterns: https://cucumber.io/docs/guides/anti-patterns/
- User story: https://cucumber.io/docs/terms/user-story/
