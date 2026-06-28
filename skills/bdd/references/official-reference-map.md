# 官方参考资料导航（本地索引）

本文件是该技能的**入口索引**：先决定你要解决的是 BDD 行为建模问题、Gherkin 场景写法问题，还是 Cucumber.js 执行问题，再选择对应的本地参考。

## 什么时候先读哪份？

- **先要明确需求行为、边界与协作口径**：读 `bdd-practice-reference.md`
- **要写/修 `.feature`、讨论场景质量与反模式**：读 `gherkin-cucumber-reference.md`
- **要把场景跑起来、排查配置或 hooks/结果语义**：读 `cucumber-js-reference.md`
- **要给团队说明“为什么这样写”**：先引用 `SKILL.md` 的 source-fidelity/写作标准章节，再按需补外部官方链接。
- **不确定先从哪儿看**：先读本文件，按下方职责边界选择本地参考；只有本地参考不足时，再按“外部官方文档路径”打开官网细节。

## 本地参考文件职责边界

### `bdd-practice-reference.md`
- 关注：BDD 作为协作/需求澄清方法（Discovery / Formulation / Automation）
- 关注问题：
  - 什么是该场景要验证的真实业务行为？
  - 需求与边界是否已经澄清？
  - 反例/未决问题是否被记录？
- 适用阶段：需求澄清、review 审核、Story 切分

### `gherkin-cucumber-reference.md`
- 关注：可维护的 Gherkin 写法（Feature/Rule/Scenario/Scenario Outline、Given/When/Then、Tags、Data Table）
- 关注问题：
  - 语句是否业务语言而非 UI/API 实现细节？
  - 场景是否可独立运行？
  - 是否出现了高频的 step 文案重复或技术化写法？
- 适用阶段：写场景、写评审、重构测试语言

### `cucumber-js-reference.md`
- 关注：Cucumber.js 的执行侧（项目结构、step definitions、World、hooks、配置/Profiles）
- 关注问题：
  - 运行是 `undefined/pending/failing` 还是 `passed`？
  - Hook/timeout/filter/tag 的顺序和语义？
  - 需要定位哪类 runner 配置？
- 适用阶段：自动化落地、故障排查、CI 集成前准备

## 外部官方文档路径（本地参考不足时）

当本地参考回答不够，优先按路径查外部：

1. **定义与实践优先**
   - Behavior-driven development — Wikipedia: <https://en.wikipedia.org/wiki/Behavior-driven_development>
   - Cucumber BDD Guide: <https://cucumber.io/docs/bdd/>
   - Discovery Workshop: <https://cucumber.io/docs/bdd/discovery-workshop/>
   - Example Mapping: <https://cucumber.io/docs/bdd/example-mapping/>
   - Who does what / Three Amigos: <https://cucumber.io/docs/bdd/who-does-what/>
   - Myths about BDD: <https://cucumber.io/docs/bdd/myths/>
2. **Gherkin 语义与写作质量**
   - Gherkin Reference: <https://cucumber.io/docs/gherkin/reference/>
   - Step Organization: <https://cucumber.io/docs/gherkin/step-organization/>
   - Writing better Gherkin: <https://cucumber.io/docs/bdd/better-gherkin/>
   - Anti-patterns: <https://cucumber.io/docs/guides/anti-patterns/>
   - Step Definitions: <https://cucumber.io/docs/cucumber/step-definitions/>
   - Cucumber API/reference: <https://cucumber.io/docs/cucumber/api/>
3. **Cucumber.js 配置与行为**
   - Cucumber state / World: <https://cucumber.io/docs/cucumber/state/>
   - Cucumber.js docs index: <https://github.com/cucumber/cucumber-js/tree/main/docs>
   - Configuration: <https://github.com/cucumber/cucumber-js/blob/main/docs/configuration.md>
   - Profiles: <https://github.com/cucumber/cucumber-js/blob/main/docs/profiles.md>
   - Hooks: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/hooks.md>
   - World: <https://github.com/cucumber/cucumber-js/blob/main/docs/support_files/world.md>
   - JavaScript 10-minute tutorial: <https://cucumber.io/docs/guides/10-minute-tutorial?lang=javascript>

## 快速决策规则

1. 能在本地文件里确认的，不要先打开外链。
2. 只在以下情况下回看官网：
   - 需要精确 CLI/formatter/plugin/reporter/并发/重试/分片行为
   - 版本升级后行为差异不确定（Node / Cucumber / Cucumber.js）
   - 需要精确断言某一官方参数边界
3. 任何时候先确认：**BDD 的问题是否先于工具**。
