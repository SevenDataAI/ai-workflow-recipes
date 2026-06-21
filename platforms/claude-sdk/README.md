# Claude SDK 落地方式

Claude SDK 更适合做深度工具调用和复杂任务执行。

适合场景：

- 读取多个文件
- 生成和修改代码
- 调用本地脚本
- 执行多步分析
- 生成可复查的中间产物
- 把本地资料整理成知识资产

不适合场景：

- 只做简单问答
- 只生成一次性文案
- 不需要工具调用的轻量任务

## 推荐结构

```text
Task
  -> Read files
  -> Build context
  -> Plan steps
  -> Execute tools
  -> Verify output
  -> Write artifact
```

## 示例：本地文件到知识资产

Claude SDK 负责：

1. 扫描指定目录。
2. 读取文档和代码。
3. 按主题聚类。
4. 提取素材卡片。
5. 标记敏感内容。
6. 生成知识库章节建议。

规则负责：

1. 大文件跳过或分块。
2. 密钥、手机号、客户名脱敏。
3. 每张卡片保留来源路径。
4. 输出前人工确认。

## 输出建议

```text
knowledge_assets/
  index.md
  cards/
    ai-workflow.md
    data-agent.md
    content-system.md
  sensitive_review.md
```

## 常见错误

1. 不保留来源路径，后续无法复核。
2. 没有脱敏，直接写进公开文章。
3. 只生成摘要，没有形成可复用观点。
4. 没有输出结构化索引。

## Checklist

- [ ] 是否限定扫描目录
- [ ] 是否过滤敏感信息
- [ ] 是否保留来源路径
- [ ] 是否输出知识卡片
- [ ] 是否需要人工确认

