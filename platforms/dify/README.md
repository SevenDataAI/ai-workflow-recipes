# Dify 落地方式

Dify 适合把一个 AI 能力包装成可用应用。

适合放进 Dify 的部分：

- 用户输入
- 意图识别
- 文档问答
- 文案生成
- SQL 草稿生成
- 结果解释
- 简单条件分支

不建议完全放进 Dify 的部分：

- 高风险 SQL 执行
- 权限审批
- 复杂定时任务
- 大规模文件扫描
- 多系统数据同步
- 生产级日志和审计

## 推荐结构

```text
Dify
  -> 收集用户输入
  -> 调用知识库 / Prompt / LLM
  -> 生成结构化输出
  -> 交给外部系统执行
```

外部系统可以是：

- n8n
- 后端 API
- 数据平台网关
- 飞书审批
- Codex / Claude SDK 本地任务

## 示例：AI 生成 SQL 审查

Dify 负责：

1. 接收用户问题和 AI 生成 SQL。
2. 调用提示词解释 SQL 意图。
3. 输出结构化审查结果。

外部规则负责：

1. 解析 SQL。
2. 检查分区。
3. 检查敏感字段。
4. 检查指标口径。
5. 决定 allow / deny / review。

推荐输出格式：

```json
{
  "decision": "review",
  "risk_level": "P1",
  "blocked_rules": [],
  "warnings": ["missing_partition_filter"],
  "review_reason": "查询 DWD 明细表时没有明确 dt 分区，可能导致大表扫描。",
  "next_action": "补充分区条件后再执行"
}
```

## 常见错误

1. 把所有节点都交给 LLM。
2. 让 Dify 直接执行生产 SQL。
3. 没有结构化输出。
4. 没有失败分支。
5. 没有人工确认节点。

## Checklist

- [ ] 输入变量是否清楚
- [ ] 输出是否结构化
- [ ] 高风险动作是否外置
- [ ] 是否有人工确认
- [ ] 是否能记录 Bad Case

