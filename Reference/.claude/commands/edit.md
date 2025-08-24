---
description: 智能修改模式，允许重新执行任意已完成阶段
allowed-tools: Read, Write, Edit
---

# 🔄 智能修改模式

## 功能描述

检查当前项目状态，如果有已完成的工作阶段，则提供修改选项菜单，允许用户重新执行任意已完成的阶段。

## 执行前置检查

### 状态验证
- **适用状态**: 任何有已完成阶段的项目状态
- **最低要求**: 至少需要有一个 `AGENT_[职位]_DONE` 状态

### 产物扫描
扫描项目目录，识别已完成的产物文件：
```yaml
扫描逻辑:
  for each agent in TEAM_AGENTS:
    check_file: agent.output_artifact
    if exists: mark as "COMPLETED"
    else: determine status based on workflow
```

## 执行流程

### 1. 状态分析
```
📊 正在分析项目状态...
🔍 扫描已完成的工作阶段...
📋 生成修改选项菜单...
```

### 2. 动态菜单生成
```
📝 **修改选项菜单**

您可以选择修改以下任意阶段：
[根据 WORKFLOW_SEQUENCE 和产物文件动态生成]

✅ {{COMPLETED_ROLE_1}} - 输入 `/{{COMMAND_1}}` 重新开始该阶段
   📄 产物: {{OUTPUT_FILE_1}} ({{COMPLETION_TIME_1}})
   
✅ {{COMPLETED_ROLE_2}} - 输入 `/{{COMMAND_2}}` 重新开始该阶段  
   📄 产物: {{OUTPUT_FILE_2}} ({{COMPLETION_TIME_2}})

⏸️ {{CURRENT_ROLE}} - 当前可以继续，或输入 `/{{CURRENT_COMMAND}}` 重新开始
   📄 状态: 正在进行中

⏭️ {{PENDING_ROLE_1}} - 尚未开始，完成前置阶段后可启动
⏭️ {{PENDING_ROLE_2}} - 尚未开始，完成前置阶段后可启动

选择您要修改的阶段，系统将从该阶段重新开始。
```

### 3. 状态更新
选择修改阶段后：
```
🔄 项目状态更新: {{CURRENT_STATUS}} → PROJECT_REVISING
📍 修改目标: {{SELECTED_ROLE}}
⚠️  注意: 从该阶段开始的所有后续工作将被重置
```

## 错误处理

### 项目尚未开始
```
❌ 错误：项目尚未开始，暂无内容可供修改。
   当前状态: PROJECT_IDLE
   建议操作: 
   • 输入 `/{{FIRST_COMMAND}}` 开始{{FIRST_ROLE}}工作
   • 输入 `/help` 查看所有可用指令
```

### 无已完成阶段
```
❌ 错误：当前没有已完成的工作阶段。
   项目进度: {{CURRENT_PROGRESS}}
   建议操作: 
   • 继续当前工作或启动下一阶段
   • 使用 `/status` 查看详细进度
```

## 使用场景

1. **内容优化**: 基于新需求重新优化某个阶段的产物
2. **质量提升**: 发现问题后重做特定阶段
3. **需求变更**: 适应新的项目要求重新执行
4. **迭代改进**: 基于反馈进行迭代式改进

## 注意事项

- 重新执行某阶段会重置该阶段及之后的所有工作
- 建议在重新执行前备份重要产物
- 可以多次使用edit功能进行迭代改进

## 使用方式

```bash
/edit    # 显示修改选项菜单
```
