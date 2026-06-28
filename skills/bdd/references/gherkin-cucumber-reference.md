# Gherkin 与 Cucumber 快速参考：写高质量场景

> 目标：把“看起来能跑”变成“可读、可维护、可复用”的 `.feature` 实践指南。

## 1. 先写语法骨架，再填充行为细节

- `Feature`：一个业务能力。
- `Rule`：将同一规则下的场景归组。
- `Scenario`：一个具体可执行例子。
- `Scenario Outline + Examples`：同类场景的多组输入。
- `Background`：各场景共享的业务背景。
- `Tags`：按维度标注分类和执行策略。

## 2. 核心语义

- `Given`：建立前提上下文（可观测业务状态）。
- `When`：触发事件（行为动作）。
- `Then`：断言可观察结果。
- `And/But/*`：延续步类型，不是额外语法概念。

注意：`Given` 与 `Then` 并不表示业务上可互换，场景表达要保持语义一致。

## 3. 常用写作规则（高频修正项）

1. 统一语言，避免同一业务事实出现多个措辞。
2. 使用真实具体数据（时间、数量、金额、对象）。
3. **What not how**，保持行为语言。
4. 一个 step 一件事。
5. `Scenario` 可独立运行，不依赖顺序。
6. `Scenario Outline` 替代重复拷贝。
7. `Background` 保持短，避免承载实现细节。

## 4. 常见反模式

- 写成 UI 操作脚本：`点击按钮`、`填写字段`等细节直接进入主语句。
- 技术参数直接写入 `Given`。
- 复用/重复 step 文案失控（`Given`、`When` 重复但语义不同）。
- `Background` 承担测试环境搭建细节。
- 一条 step 包含多个业务动作（junction/conjunction）。

## 5. 当场改写示例

### 旧（技术化）

```gherkin
Scenario: Discount works
  Given a user has discount flag
  When the user enters "user1" into username field
  Then the discount should be shown
```

### 新（行为化）

```gherkin
Scenario: Discount expires after campaign
  Given Carla has a 20% summer discount
  And the campaign ends on 2026-08-31
  When Carla checks out on 2026-09-01
  Then the summer discount is not applied
```

## 6. 结构化排错路径

- 语句重复多：先检查同义表达。
- 规则边界不清：在 `Rule` 或 `Examples` 中补充 negative case。
- tags 泛化过度：拆分 tags 维度。
- 例子过长：考虑拆成多个场景。

## 7. 与外链衔接（要点优先）

- Gherkin reference：关键字、结构、案例规则。
- Step organization：step 组织和复用边界。
- Writing better Gherkin：语言质量指导。
- Step definitions：与 steps 的绑定关系。
- Anti-patterns：长期维护时的风险点。

## 8. 场景决策速记

- 优先回答：这个场景是否回答了一个可观察业务问题？
- 是否能被业务/测试/开发共同理解？
- 是否容易单独运行与调试？
- 是否有明确失败语义（not/反例）？

## 9. 目录与文件约定（默认）

```text
features/
  *.feature
  step_definitions/
  support/
    hooks.js
```

- 重点不是“文件名”，而是场景是否可读。
