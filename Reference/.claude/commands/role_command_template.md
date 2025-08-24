---
description: 启动{{ROLE_TITLE}}工作流程
allowed-tools: Read, Write, Edit
argument-hint: [可选参数]
---

# 🎯 {{ROLE_TITLE}} Agent 启动

## 执行前置检查

### 1. 状态验证
检查当前项目状态是否允许启动{{ROLE_TITLE}}工作：
- **如果是第一个职位**: 需要 `PROJECT_IDLE` 或 `PROJECT_REVISING` 状态
- **如果是后续职位**: 需要前置职位的 `AGENT_{{PREVIOUS_ROLE}}_DONE` 状态

### 2. 前置产物检查
验证必要的前置产物文件是否存在：
- **检查文件**: `{{PREVIOUS_OUTPUT_FILE}}`（如果不是第一个职位）
- **验证内容**: 确保前置产物包含必要信息

## Agent召唤流程

如果前置检查通过，执行以下步骤：

### 1. 系统响应
```
🔥 正在召唤 {{ROLE_TITLE}} Agent...
```

### 2. 前置产物传递
如果有前置产物，显示：
```
📂 将向其提交 {{PREVIOUS_OUTPUT_NAME}}
```

### 3. Agent激活
```
读取并执行: @.claude/prompts/{{PROMPT_FILE}}
角色身份: 完全切换到{{ROLE_TITLE}}身份  
工作模式: 按照Agent定义执行专业任务
```

### 4. 状态更新
```
项目状态: PROJECT_STATUS → AGENT_{{ROLE_TITLE}}_WORKING
工作阶段: {{WORKFLOW_POSITION}}/{{TOTAL_WORKFLOW_STEPS}}
```

## 错误处理

### 状态不匹配
```
❌ 错误：当前阶段不能启动{{ROLE_TITLE}}工作。
   当前状态: {{CURRENT_STATUS}}
   需要状态: {{REQUIRED_STATUS}}
   建议操作: 请先完成{{REQUIRED_PREVIOUS_STEPS}}。
```

### 产物缺失
```
❌ 错误：缺少必要的前置产物。
   缺失文件: {{PREVIOUS_OUTPUT_FILE}}
   前置职位: {{PREVIOUS_ROLE}}
   建议操作: 请先完成{{PREVIOUS_ROLE}}的工作。
```

### 文件缺失
```
❌ 错误：找不到{{ROLE_TITLE}}的Agent定义文件。
   缺失文件: .claude/prompts/{{PROMPT_FILE}}
   建议操作: 请检查Agent配置文件是否存在。
```

## 模板变量说明

- `{{ROLE_TITLE}}`: Agent角色名称（如：产品经理、设计师）
- `{{PROMPT_FILE}}`: Agent提示词文件名（如：product_manager.md）
- `{{PREVIOUS_ROLE}}`: 前置职位名称
- `{{PREVIOUS_OUTPUT_FILE}}`: 前置产物文件路径
- `{{PREVIOUS_OUTPUT_NAME}}`: 前置产物友好名称
- `{{WORKFLOW_POSITION}}`: 当前工作流位置
- `{{TOTAL_WORKFLOW_STEPS}}`: 总工作流步数
- `{{CURRENT_STATUS}}`: 当前项目状态
- `{{REQUIRED_STATUS}}`: 所需项目状态
