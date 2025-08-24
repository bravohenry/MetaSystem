---
description: 显示当前项目的详细状态报告和进度
allowed-tools: Read
---

# 📊 智能项目状态报告

## 功能描述

扫描项目状态，生成包含当前进度、已完成产物和下一步建议的状态报告，为用户提供清晰的项目全景视图。

## 智能扫描机制

### 状态识别流程
```yaml
扫描步骤:
  1. 配置读取: 
     - 读取 COORDINATOR_CONFIG 获取团队配置
     - 解析 WORKFLOW_SEQUENCE 工作流程
     - 识别 TEAM_AGENTS 角色定义
     
  2. 文件扫描:
     - 检查所有Agent的预期产物文件
     - 获取文件创建/修改时间
     - 分析文件大小和内容完整性
     
  3. 位置确定:
     - 根据工作流程确定当前进度位置
     - 识别下一个可执行的阶段
     - 判断是否存在阻塞问题
     
  4. 报告生成:
     - 生成个性化状态报告
     - 提供具体操作建议
     - 展示项目健康度指标
```

### 文件扫描逻辑
```yaml
for each agent in TEAM_AGENTS:
  target_file: agent.output_artifact
  
  if file_exists(target_file):
    status: "COMPLETED"
    completion_time: file.modified_time
    file_size: file.size
  elif is_current_agent(agent):
    status: "IN_PROGRESS" 
  else:
    status: "PENDING"
    blocking_factor: get_blocking_reason(agent)
```

## 状态报告模板

### 基础信息段
```
📊 **{{TEAM_NAME}} 项目状态报告**

🎯 **项目概览**
• 项目领域: {{PROJECT_DOMAIN}}
• 团队规模: {{TEAM_SIZE}}个专业角色
• 当前状态: `{{CURRENT_PROJECT_STATUS}}`
• 最后更新: {{LAST_UPDATE_TIME}}

🔄 **工作流程**
{{WORKFLOW_SEQUENCE_VISUAL}}
```

### 进度详情段
```
📈 **项目进度** ({{COMPLETED_COUNT}}/{{TOTAL_COUNT}})

**✅ 已完成阶段:**
{{#each completed_agents}}
✅ {{role_name}} ({{completion_time}})
   📄 产物: {{output_file}} ({{file_size}})
   🎯 质量: {{quality_indicator}}
{{/each}}

{{#if current_agent}}
**⏸️ 进行中:**
⏸️ {{current_agent.role_name}} - {{current_agent.description}}
   📍 状态: AGENT_{{current_agent.role_title}}_WORKING
   ⏱️  开始: {{current_agent.start_time}}
   📋 任务: {{current_agent.current_task}}
{{/if}}

**⏭️ 待完成阶段:**
{{#each pending_agents}}
⏭️ {{role_name}} - {{description}}
   📊 依赖: {{dependency_info}}
   🔓 解锁条件: {{unlock_condition}}
{{/each}}
```

### 操作建议段
```
🚀 **下一步操作建议**

{{#if next_available_action}}
**🎯 推荐操作:**
• 输入 `/{{next_command}}` - 开始{{next_role}}工作
  📝 任务描述: {{next_task_description}}
  ⏱️  预计耗时: {{estimated_time}}
{{/if}}

**🔧 管理操作:**
• 输入 `/edit` - 修改已完成的阶段 ({{completed_count}}个可选)
• 输入 `/help` - 查看所有可用指令
• 输入 `/mcp` - 配置MCP服务器增强功能

{{#if has_issues}}
**⚠️  注意事项:**
{{#each issues}}
• {{issue_description}} - {{suggested_solution}}
{{/each}}
{{/if}}
```

### 健康度指标段
```
📊 **项目健康度**

🎯 **完成率**: {{completion_percentage}}% ({{completed_count}}/{{total_count}})
⚡ **活跃度**: {{activity_status}} (最后活动: {{last_activity}})
🔧 **配置完整性**: {{config_completeness}}%
📁 **文件完整性**: {{file_integrity}}%

{{#if performance_metrics}}
📈 **效率指标**:
• 平均阶段用时: {{avg_stage_time}}
• 产物质量评分: {{quality_score}}/10
• 工作流顺畅度: {{workflow_smoothness}}%
{{/if}}
```

## 适用状态

- **任何项目状态**: 都可以查看状态报告
- **实时更新**: 提供最新的准确状态信息
- **智能分析**: 自动识别问题和优化机会

## 执行示例

```bash
用户输入: /status

系统输出:
📊 正在分析项目状态...
🔍 扫描工作流程和产物文件...
📋 生成状态报告...

[详细状态报告内容]

✅ 状态报告生成完成！
```

## 使用方式

```bash
/status    # 获得完整的项目状态报告
```

## 高级功能

### 状态历史
- 跟踪项目状态变化历史
- 分析团队工作效率趋势
- 识别瓶颈和优化机会

### 智能建议
- 基于当前状态提供个性化建议
- 预测下一步操作的时间需求
- 提供质量改进建议
