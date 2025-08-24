---
description: 启动{{ROLE_TITLE}}工作流程（增强模式：包含状态管理和工作流控制）
allowed-tools: Read, Write, Edit
argument-hint: [可选参数]
---

# 🎯 {{ROLE_TITLE}} Subagent 启动（增强模式）

> **注意**: 您也可以直接使用 "使用{{AGENT_NAME}}处理{{SPECIFIC_TASK}}" 进行简单调用。
> 本命令提供完整的状态管理和工作流控制，适用于复杂的团队协作项目。

## 执行前置检查

### 1. 状态验证
检查当前项目状态是否允许启动{{ROLE_TITLE}}工作：
- **如果是第一个职位**: 需要 `PROJECT_IDLE` 或 `PROJECT_REVISING` 状态
- **如果是后续职位**: 需要前置职位的 `AGENT_{{PREVIOUS_ROLE}}_DONE` 状态

### 2. 前置产物检查
验证必要的前置产物文件是否存在：
- **检查文件**: `{{PREVIOUS_OUTPUT_FILE}}`（如果不是第一个职位）
- **验证内容**: 确保前置产物包含必要信息

## Subagent委托流程

如果前置检查通过，执行以下步骤：

### 1. 系统响应
```
🔥 正在委托 {{ROLE_TITLE}} Subagent...
```

### 2. 前置产物传递
如果有前置产物，显示：
```
📂 将向其提交 {{PREVIOUS_OUTPUT_NAME}}
```

### 3. Subagent委托
```
委托方式: 使用{{AGENT_NAME}}处理{{SPECIFIC_TASK}}
工作模式: 独立上下文窗口中进行专业化处理
专业领域: {{ROLE_TITLE}}专属任务
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
❌ 错误：找不到{{ROLE_TITLE}}的Subagent配置文件。
   缺失文件: .claude/agents/{{AGENT_FILE}}
   建议操作: 请检查Subagent配置文件是否存在。
```

## 模板变量说明

- `{{ROLE_TITLE}}`: Subagent角色名称（如：产品经理、设计师）
- `{{AGENT_FILE}}`: Subagent配置文件名（如：product_manager.md）
- `{{AGENT_NAME}}`: Subagent名称（如：product-manager）
- `{{SPECIFIC_TASK}}`: 具体委托任务描述
- `{{PREVIOUS_ROLE}}`: 前置职位名称
- `{{PREVIOUS_OUTPUT_FILE}}`: 前置产物文件路径
- `{{PREVIOUS_OUTPUT_NAME}}`: 前置产物友好名称
- `{{WORKFLOW_POSITION}}`: 当前工作流位置
- `{{TOTAL_WORKFLOW_STEPS}}`: 总工作流步数
- `{{CURRENT_STATUS}}`: 当前项目状态
- `{{REQUIRED_STATUS}}`: 所需项目状态
