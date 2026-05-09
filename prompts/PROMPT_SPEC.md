# Prompt Spec - 企业级 Prompt 治理规范

## 1. 目标

Prompt 是 AI 研发平台的重要工程资产，必须像代码一样被设计、评审、版本化、测试、发布和审计。

本规范用于约束：

- 研发类 Prompt。
- Review 类 Prompt。
- 评测类 Prompt。
- 工作流编排 Prompt。
- 业务 Agent Prompt。

## 2. Prompt 元数据

每个 Prompt 文件必须包含以下元数据：

```yaml
id: user-center.create-user.v1
name: 创建用户用例代码生成 Prompt
version: 1.0.0
owner: user-center-team
status: draft | active | deprecated
scenario: code-generation | code-review | evaluation | workflow
model_scope: gpt-family
created_at: 2026-05-09
updated_at: 2026-05-09
```

## 3. Prompt 必备结构

Prompt 必须包含：

1. 背景上下文：业务背景、系统边界、已有模块。
2. 任务目标：要解决的问题和交付物。
3. 输入约束：可用信息、禁止事项、依赖限制。
4. 架构约束：DDD 分层、接口边界、事务边界。
5. 安全约束：鉴权、审计、敏感信息、注入防护。
6. 质量约束：测试、性能、日志、异常、可维护性。
7. 输出格式：代码、文档、Review 结论或评测报告格式。
8. 验收标准：自动化检查、人工 Review 标准、风险确认。

## 4. Prompt 版本规范

版本号采用语义化版本：

- `MAJOR`：改变 Prompt 目标、输出协议或关键约束。
- `MINOR`：新增约束、场景或输出字段，保持兼容。
- `PATCH`：修正文案、示例或非关键说明。

变更必须记录：

- 变更原因。
- 影响范围。
- 回滚方式。
- 评测结果。

## 5. Prompt 评测规范

Prompt 发布前必须至少完成以下评测：

- 正常任务完成度。
- 边界条件遵循度。
- 安全限制遵循度。
- DDD 分层遵循度。
- 输出格式稳定性。
- 幻觉与越权行为检查。

评测结果建议记录在 `evaluation-center/` 或对应模块的评测目录中。

## 6. Prompt AB Test 规范

适合 AB Test 的变更包括：

- 提升代码质量的结构化提示。
- 不同 Review 维度顺序。
- 不同输出格式。
- 不同上下文压缩策略。

AB Test 必须定义：

- 对照组与实验组。
- 样本任务。
- 质量指标。
- 失败回滚标准。

## 7. Prompt 安全规范

Prompt 禁止包含：

- 明文密钥、Token、密码。
- 真实生产用户隐私数据。
- 绕过安全审计或权限控制的指令。
- 要求 AI 忽略项目规范的指令。

Prompt 必须明确：

- 不输出敏感信息。
- 不修改未经授权的基础设施和数据库结构。
- 不生成 Demo 级代码。

## 8. Prompt 模板

```markdown
---
id: <domain>.<scenario>.v1
name: <Prompt 名称>
version: 1.0.0
owner: <团队或负责人>
status: draft
scenario: code-generation
---

# 背景

<说明业务背景、模块边界、已有约束。>

# 目标

<说明需要完成的交付物。>

# 输入

<列出输入信息和可引用上下文。>

# 约束

- 遵循 DDD 分层。
- 不新增未经确认的依赖。
- 不修改公共协议或数据库结构，除非需求明确授权。
- 必须包含测试与验证方案。

# 输出格式

<说明期望输出结构。>

# 验收标准

- 架构边界正确。
- 安全风险已处理。
- 测试通过。
- 文档更新完整。
```
