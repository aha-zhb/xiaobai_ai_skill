# 小白 AI 需求表达助手

一个帮助 AI 使用小白表达需求的 Skill。用户可以从一句模糊的话、几条消息或部分材料开始，通过具体选择、短对比和局部小样，逐步形成自己认可、Agent 能够使用的任务说明。

核心目标：让 Agent 承担一部分需求澄清工作，帮助用户把模糊诉求变成明确任务。

## 使用入口

Skill 源文件位于 [skills/clarify-intent](skills/clarify-intent/SKILL.md)。将该目录按使用中的 Agent 所支持的方式加载；如果 Agent 可以读取项目文件，也可以先明确要求它读取入口：

```text
请读取 skills/clarify-intent/SKILL.md，并按其中的规则帮我澄清需求。
我现在的想法是：这些项目记录太乱了，想整理一下，但还不知道怎么说。
```

已加载 Skill 的环境中，可以直接使用宿主提供的技能调用入口。不同 Agent 的导入和发现方式以各自实际能力为准；仅复制文件不代表当前会话已自动加载。

## 交互规则

- 优先实际调用宿主原生提问工具，以问题卡片或选择按钮收集回答。
- 遵守当前工具的参数、长度、数量及单选或多选规则，不硬编码平台接口。
- 原生工具不可用、不适用或调用失败时，退回文字选择题。
- 问会影响下一步做法的问题，不要求用户填写固定问卷。
- 接受自由补充、全部否定和部分纠正，不把 AI 推测当作用户认可。
- 已经清楚的需求直接收敛；用户答不上来时换成实例、对比或短小样。
- 保留暂定安排和未决事项，不自动扩展成完整方案或外部执行。

## 文件结构

```text
skills/clarify-intent/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── interaction-patterns.md
    └── evaluation-cases.md

workfile/
├── 需求澄清Skill产品方案.md
└── clarify-intent开发验收记录.md
```

- [产品方案](workfile/需求澄清Skill产品方案.md)：定位、澄清机制、交互设计、实现与评估安排。
- [引导示例](skills/clarify-intent/references/interaction-patterns.md)：复杂引导场景按需读取。
- [验收案例](skills/clarify-intent/references/evaluation-cases.md)：20个行为验收场景，供开发与后续验证使用。
- [开发验收记录](workfile/clarify-intent开发验收记录.md)：实际检查结果与待验证事项。

## 当前验证状态

首版源文件已完成，Skill 格式、引用路径和静态内容检查通过，完成了六条纸面交互演练。20个案例尚未执行完整模型行为测试，WorkBuddy 等真实宿主的问题卡片显示、答案回传和用户体验尚未实测。

本 Skill 提供通用行为规则。原生卡片由宿主的工具和界面实现，源文件可读不等于所有平台已经完成适配。
