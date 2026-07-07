# 2026-07-06 Daily AI PM Log

## 1. 今天学习了什么

主题：Agent Series 1。从理论到代码，从 Tool Calling 到 OpenClaw，理解 Agent 是如何搭建起来的。

参考视频：

- https://www.bilibili.com/video/BV1dw526tEMA/

今天主要学习了：

- LangChain / LangGraph 的基础概念
- Tool Calling 的本质
- Agent 的基本组成方式
- ReAct、Reflection、Replan and Execute 等运行模式
- 从代码视角理解 Agent 如何把模型、工具、Prompt 和流程控制拼起来

## 2. LangChain 的体系概念

今天对 LangChain 的理解是：它是一个做大模型应用的组件工具箱，用来把 LLM、Prompt、Message、Tool、Tool Calling、Agent 等组件拼接起来。

核心概念：

- Model：接入的 LLM。
- Prompt：给模型的任务说明、角色约束和输出格式要求。
- Message：多轮对话中的消息结构。
- Tool：可被模型选择调用的外部函数或能力。
- Tool Calling：让模型不仅输出文本，还能输出“要调用什么工具、传什么参数”。
- Agent：围绕模型和工具组织任务执行流程的主程序或框架。

我的理解：

LangChain 的价值不只是“调用模型”，而是把大模型应用开发里常见的组件标准化，例如多轮对话管理、工具声明、工具调用解析、Agent 流程组织等。

## 3. LangGraph 的体系概念

今天对 LangGraph 的理解是：它更偏 Agent 工作流程编排。

核心概念：

- State：流程里的状态信息。
- Node：某个执行步骤。
- Edge：节点之间的顺序关系。
- Conditional Edge：带条件判断的连接关系。
- Graph：由 node、edge、conditional edge 组成的完整工作流程图。
- Compile：编译并检查流程是否可执行。

我的理解：

如果说 LangChain 更像组件工具箱，那么 LangGraph 更像 Agent 工作流编排框架。它适合表达更复杂的 Agent 流程，例如规划、执行、反思、重新规划、多节点协作等。

## 4. Tool Calling 的本质

今天对 Tool Calling 的理解有明显加深。

最初的模型只支持文本输入和文本输出，本身并不能直接和外部真实接口交互。Function Calling / Tool Calling 的本质，是让模型输出结构化内容，本地程序再解析这些结构化内容并执行对应函数。

示例：

用户输入：

```text
帮我查询北京的天气
```

模型输出工具调用意图：

```text
<Tool>Get_weather</Tool>
<Args>["city:Beijing","date:2020/02/02"]</Args>
```

本地 Agent 解析后：

```text
Toolname = Get_weather
Toolargs = {"city": "Beijing", "date": "2020/02/02"}
```

工具执行结果：

```text
北京的天气：25度，晴
```

关键理解：

- LLM 本身仍然只是输入输出文本或结构化消息。
- 真正执行工具的是本地 Agent 程序，不是模型本身。
- 只靠 Prompt 约束模型输出格式不够稳定，因为模型可能幻觉或不遵守格式。
- 工程化解法之一，是通过标准格式训练和模型原生 Tool Calling 能力，让模型更稳定地输出可解析结构。

## 5. Agent 的运行模式

今天继续学习了几种 Agent 运行模式。

### ReAct

ReAct 的本质可以理解为一个工具调用的 `while` 循环：

```text
do tools until LLM_output = problem solved
```

它的过程是：

- 模型先思考下一步。
- 如果需要外部能力，就输出工具调用。
- Agent 执行工具。
- 工具结果再返回给模型。
- 模型继续判断是否完成任务。

直到模型认为问题已经解决，循环结束，不再调用工具。

### Reflection

Reflection 可以理解为在 ReAct 的单步动作执行基础上增加“负反馈”。

也就是：

- 工具调用之后，不是直接进入下一步。
- 而是把执行结果再交给 LLM 检查：是否满足最初任务？是否有问题？是否需要修正？
- 如果不满足，就继续循环和改进。

我的理解是：Reflection 让 Agent 多了一层自我检查机制，有助于提升复杂任务的质量，但也会增加成本、耗时和上下文复杂度。

### Replan and Execute

Replan and Execute 更强调：

- 先规划。
- 再执行。
- 执行过程中根据结果重新规划。

它适合更复杂的任务，因为复杂任务通常不能只靠局部下一步判断完成。

## 6. 对 AI 产品经理岗位的新理解

今天的学习让我意识到，AI 产品经理理解 Agent 时不能只停留在“模型很聪明，会自动完成任务”。

更准确的理解应该是：

- 模型负责推理和生成工具调用意图。
- Agent 框架负责解析、执行、状态管理和流程控制。
- Tool Calling 设计影响 Agent 能否稳定工作。
- 工作流模式影响任务成功率、可解释性、成本和用户信任。

从产品视角看，Agent 产品的关键问题包括：

- 用户是否能理解 Agent 正在做什么？
- 工具调用是否可见、可控、可中断？
- 工具参数是否清晰、结构化、低歧义？
- 出错后 Agent 是否能反思、重试或重新规划？
- 什么时候应该使用 ReAct，什么时候应该使用 Plan/Replan 类模式？

## 7. 可沉淀到作品集的内容

- Agent 基础概念体系：LangChain / LangGraph / Tool Calling / Agent。
- Tool Calling 的产品解释：模型不执行工具，本地 Agent 才执行工具。
- ReAct、Reflection、Replan and Execute 的对比。
- 对 Agent 产品体验的判断框架：可见、可控、可恢复、可解释。

## 8. 明天计划

- 继续结合代码理解 Tool Calling 的实现方式。
- 尝试用现有 ReAct Agent 样例补充一个 Tool Calling 示例。
- 总结“Agent Friendly Tool 设计原则”。

