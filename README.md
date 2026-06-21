# AI Workflow Recipes

把重复工作变成可复用 AI 工作流。

这个仓库不讨论“AI 会不会取代人”，只讨论一个更实际的问题：

**一件每天重复做、流程相对固定、但中间又需要一点判断的工作，怎么拆成稳定可执行的 workflow。**

适合人群：

- 自媒体人：选题、脚本、封面、评论回复、素材入库
- 职场人：会议纪要、周报、资料整理、邮件回复
- 数据分析师：Excel / CSV 分析、经营日报、指标异常归因
- 数据开发：AI 问数、SQL Review、取数需求澄清
- AI 工具用户：想把 Dify、n8n、Claude SDK、Codex 用到真实工作里

## Core Idea

很多人用 AI 没效果，不是模型不行，而是把所有步骤都丢给模型猜。

一个可落地的 workflow 应该分清楚：

| 类型 | 应该交给谁 | 例子 |
| --- | --- | --- |
| 理解和生成 | AI | 总结会议、生成脚本、解释数据 |
| 格式和校验 | 规则 | 字段必填、SQL 禁止敏感字段、输出结构检查 |
| 外部执行 | 工具 | 读文件、查数据库、发飞书、写文档 |
| 风险控制 | 人工确认 | 发给客户、发布内容、生产查询、批量修改 |
| 经验沉淀 | 知识库 / 日志 | Bad Case、用户反馈、常见问题、版本记录 |

核心原则：

```text
AI 负责判断、生成和解释。
确定性流程交给代码、规则、模板、工作流引擎和自动化工具。
```

## Recipe Structure

每个 recipe 都包含：

- `workflow.yaml`：标准化流程定义
- `README.md`：场景说明、步骤拆解、落地建议
- `inputs`：需要准备什么
- `steps`：流程节点
- `ai_tasks`：哪些节点由 AI 完成
- `rules`：哪些地方必须规则化
- `human_review`：哪些地方需要人工确认
- `outputs`：最终交付物

## Recipes

### 1. Content Creator

[`video-script-to-publish-plan`](./recipes/content_creator/video-script-to-publish-plan/)

把一个选题变成视频脚本、封面标题、平台文案和私信引导话术。

适合：

- 短视频创作者
- 小红书博主
- 知识付费产品
- B 站技术内容

### 2. Office Worker

[`meeting-summary-to-actions`](./recipes/office_worker/meeting-summary-to-actions/)

把会议纪要变成行动计划、责任人、风险点和后续沟通话术。

适合：

- 项目经理
- 产品经理
- 业务负责人
- 一线管理者

### 3. Data Analyst

[`csv-insight-report`](./recipes/data_analyst/csv-insight-report/)

把 CSV / Excel 明细变成可复核的数据分析报告。

适合：

- 数据分析师
- 运营分析
- 业务分析
- 增长分析

### 4. Data Agent

[`sql-review-gate`](./recipes/data_agent/sql-review-gate/)

对 AI 生成 SQL 做上线前审查，避免缺分区、口径错误、敏感字段、全表扫描和 join 放大。

适合：

- 数据开发
- 数仓工程师
- AI 问数 / NL2SQL 项目
- 企业 Data Agent 团队

## Platform Mapping

同一个 workflow 可以映射到不同工具：

| 平台 | 适合做什么 |
| --- | --- |
| Dify | AI 应用、问答、轻量 workflow、知识库增强 |
| n8n | 自动化集成、通知、审批、定时任务、跨系统串联 |
| Claude SDK | 深度工具调用、复杂任务执行、代码和文件操作 |
| Codex | 本地项目处理、代码修改、文档生成、数据文件分析 |
| LangGraph | 有状态、多节点、可恢复的 Agent 编排 |
| 飞书 / 企业微信 | 消息触达、审批、文档沉淀、团队协同 |

## How to Use

1. 选择一个接近你场景的 recipe。
2. 复制 `workflow.yaml`。
3. 改成你的输入、工具和输出。
4. 先人工跑一遍，确认流程没有漏环节。
5. 再接入 Dify / n8n / Claude SDK / Codex。
6. 把失败案例写回 `bad_cases`。
7. 每周优化一次规则和提示词。

## Roadmap

- [ ] Dify DSL generator
- [ ] n8n workflow JSON generator
- [ ] Claude SDK Python scaffold
- [ ] LangGraph scaffold
- [ ] Mermaid architecture diagram generator
- [ ] Workflow quality checklist
- [ ] Bad Case template
- [ ] Chinese documentation examples

## Why This Exists

Prompt 不是产品。

一次性的 AI 问答，也不是真正的自动化。

能长期产生价值的是：

- 可复用的流程
- 可校验的规则
- 可追溯的日志
- 可沉淀的经验
- 可持续迭代的系统

这个仓库会持续沉淀真实场景下的 AI workflow 模板。

