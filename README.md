# input-triage（输入分诊）

> 插话不等于指令。先分诊，再行动。

任务执行中，用户会突然插话：想起要加的东西、发现走错了路、或者顺口问一句无关的。这些插话混在上下文里，可能把 AI 带偏计划、忘掉进度、或把无关内容卷进任务成果。

本技能让 AI 对每句插话实时分诊——该吸收的吸收，该搁置的搁置，任务列表与任务台账始终保持干净。

## 解决什么问题

| 痛点 | 本技能的回答 |
|---|---|
| 任务中途用户插一句话，AI 当场被带偏 | 四类分诊：先分类再行动，只有纠偏能改变方向 |
| 顺口问的无关问题把无关内容卷进成果 | 无关内容进搁置区，物理隔离，收尾处置 |
| 想问"这是什么意思"又怕打断执行 | 确认收到 + 搁置，收尾统一补答 |
| 打断之后 AI 忘了刚才做到哪 | 重锚定协议：插话处理完必重读任务列表再继续 |
| 过程中的修正没有记录，交接时说不清 | 裁决台账：决定—理由—代价，终局报告穷举 |

## 四类分诊

| 类别 | 典型样子 | 处置 |
|---|---|---|
| ADD 追加 | "顺便也把 X 加上" | 并入任务列表，不打断当前步骤 |
| CORRECT 纠偏 | "等等，这步不对" | 当场裁决，立即转向，记台账 |
| ASK 求解 | "这个什么意思？" | 搁置，收尾补答 |
| NOISE 无关 | "今天天气如何" | 隔离不放大，收尾处置 |

## 快速开始

```bash
git clone https://github.com/<你的用户名>/input-triage.git
cp -r input-triage ~/.claude/skills/input-triage
```

之后无需任何操作：多步骤任务执行期间，用户插话自动进入分诊流程；任务收尾自动清账出报告。

## 与 context-continuity 的配合

两个技能是一对：

- **input-triage**：会话内——插话分诊、状态卫生、收尾清账
- **context-continuity**：跨会话——状态落盘、饱和监测、交接恢复

配合使用时，分诊对象自动落到 `.planning/` 文件族（任务列表→task_plan.md、搁置区→parking-lot.md、台账→task-log.md）。

## 吸收来源

- **obra/superpowers · executing-plans** — 裁决而非停摆、四条硬停止条件、终局裁决穷举清单
- **udecode/dotai · autogoal** — 目标冲突协议（最新指令优先、修正不追认旧目标）
- **andylizf/nonstop** — 阻塞三分级、收尾三段式总结
- **hainamchung/agent-assistant · fresh-context** — 防污染话术规则
- **本技能新增** — 四类分诊、搁置区物理隔离、重锚定协议、收尾清账

## 文件结构

```
input-triage/
├── SKILL.md                      # 总纲：四类分诊、处置协议、反模式
├── README.md
├── references/
│   ├── triage-protocol.md        # 判定树、边界案例、误分类修复
│   ├── execution-hygiene.md      # 时序、重锚定、列表卫生、防污染话术
│   └── wrap-up-protocol.md       # 清账顺序、台账写法、终局报告
└── templates/
    ├── parking-lot.md            # 搁置区
    ├── task-log.md               # 干净台账
    └── wrap-up-checklist.md      # 收尾清单
```

## 设计边界（诚实声明）

- 插话无法从上下文物理删除；本技能做的是**不放大、外置干净状态、收尾净化**，不是删除
- 技能靠指令约束 AI 行为，无法在模型层面强制——配合支持 skill 规范的 agent（如 Claude Code）效果最佳
