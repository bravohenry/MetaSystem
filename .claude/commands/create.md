---
description: 启动引导式AI团队创建流程，通过5步对话构建定制化的专业AI协作团队
category: meta-system
argument-hint: [可选：团队类型或领域]
allowed-tools: Read, Write, Edit, MultiEdit, Bash
---

# 🚀 创建AI团队系统

## 核心功能
启动Bravo MetaSystem的引导式创建流程，通过结构化对话帮助用户从模糊想法转化为完整的AI专业团队系统。

## 执行流程

### 🎯 激活元系统架构师
1. **读取元系统配置**: 加载 @CLAUDE.md 中的系统架构师身份
2. **初始化创建状态**: 设置状态为 `META_WELCOME`
3. **启动引导流程**: 开始五步引导式创建对话

### 📋 五步创建流程
1. **欢迎与愿景探索**: 展示ASCII Logo，了解用户需求和项目领域
2. **角色定义与团队组建**: 基于领域推荐专业职位，确认团队配置
3. **工作流编排**: 设计角色间的协作顺序和产物交接流程
4. **系统创建与最终确认**: 生成系统蓝图，请求用户最终确认
5. **完成与后续步骤**: 基于Reference/蓝图创建完整AI团队系统

### 🔧 智能系统生成
基于用户配置和Reference/模板，自动生成：
- 团队根目录和系统文件结构
- 协调者CLAUDE.md（定制化团队管理逻辑）
- .claude/commands/目录（职位专用斜杠命令）
- .claude/agents/目录（专业Subagent配置）
- 权限配置和Hook机制

## 使用示例

```bash
# 基础创建
/create

# 带领域提示
/create 产品开发
/create 内容创作  
/create SEO优化
```

## 预期输出
- 完整的AI团队系统目录
- 可直接使用的专业Subagent
- 结构化的工作流程
- Claude Code完整集成

## 系统要求
- 需要访问Reference/目录下的蓝图模板
- 需要Write权限创建新系统目录
- 需要读取role_configs.yaml配置库

---
*这是Bravo MetaSystem的核心创建命令，将引导您构建专属的AI专业团队*