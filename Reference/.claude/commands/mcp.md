---
description: MCP服务器配置指导和建议
allowed-tools: Read
---

# 🔧 {{TEAM_NAME}} MCP服务器配置指导

## 功能描述

基于{{TEAM_NAME}}团队的专业领域({{PROJECT_DOMAIN}})和工作需求，提供量身定制的MCP服务器配置建议，显著增强AI团队的专业能力和工作效率。

## 🎯 针对性配置建议

### 基于 {{PROJECT_DOMAIN}} 领域的专用配置

{{#if_domain "产品开发"}}
#### 🛠️ 产品开发专用配置
**核心服务器包**:
- **filesystem**: 高效文件操作和代码管理
- **github**: 版本控制和协作开发 
- **postgres**: 数据库设计和管理
- **figma**: 设计协作和原型管理

**增强服务器包**:
- **jira**: 项目管理和任务跟踪
- **slack**: 团队沟通协作
- **docker**: 容器化开发环境
{{/if_domain}}

{{#if_domain "内容创作"}}
#### ✍️ 内容创作专用配置
**核心服务器包**:
- **brave-search**: 实时信息获取和研究
- **filesystem**: 文档管理和文件组织
- **github**: 内容版本控制
- **google-drive**: 云端协作和存储

**增强服务器包**:
- **wordpress**: 内容发布管理
- **social-media**: 社交媒体集成
- **analytics**: 内容效果分析
{{/if_domain}}

{{#if_domain "市场营销"}}
#### 📈 市场营销专用配置
**核心服务器包**:
- **brave-search**: 市场趋势研究
- **google-analytics**: 数据分析增强
- **social-media**: 社交媒体管理
- **mailchimp**: 邮件营销自动化

**增强服务器包**:
- **facebook-ads**: 广告投放管理
- **google-ads**: 搜索广告优化
- **crm**: 客户关系管理
{{/if_domain}}

{{#if_domain "SEO优化"}}
#### 🔍 SEO优化专用配置
**核心服务器包**:
- **brave-search**: 关键词和竞争对手研究
- **google-search-console**: SEO数据集成
- **analytics**: 流量分析增强
- **screaming-frog**: 网站爬取分析

**增强服务器包**:
- **semrush**: 专业SEO工具集成
- **ahrefs**: 外链分析工具
- **gtmetrix**: 性能监控
{{/if_domain}}

{{#if_domain "数据分析"}}
#### 📊 数据分析专用配置
**核心服务器包**:
- **postgres**: 数据库连接和查询
- **sqlite**: 轻量级数据处理
- **python-execution**: 代码执行环境
- **jupyter**: 数据科学工作环境

**增强服务器包**:
- **bigquery**: 大数据查询分析
- **tableau**: 数据可视化
- **aws-s3**: 云端数据存储
{{/if_domain}}

## 🔧 通用基础配置

### 所有团队必备
```json
"基础服务器包": {
  "filesystem": "文件系统操作和管理",
  "brave-search": "网络搜索和信息获取", 
  "github": "版本控制和代码协作"
}
```

### 推荐增强配置
```json
"增强服务器包": {
  "google-drive": "云端文件协作",
  "slack": "团队沟通集成",
  "notion": "知识管理和文档协作",
  "calendar": "日程管理和提醒"
}
```

## 📋 配置实施指南

### 第一步：安装MCP服务器
```bash
# 安装核心服务器包
npm install -g @mcp/server-filesystem
npm install -g @mcp/server-brave-search  
npm install -g @mcp/server-github

# 安装领域专用服务器
{{#each domain_specific_servers}}
npm install -g {{package_name}}  # {{description}}
{{/each}}
```

### 第二步：Claude Code配置
在 `claude_desktop_config.json` 中添加：
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["@mcp/server-filesystem", "{{PROJECT_PATH}}"]
    },
    "brave-search": {
      "command": "npx", 
      "args": ["@mcp/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "{{BRAVE_API_KEY}}"
      }
    },
    "github": {
      "command": "npx",
      "args": ["@mcp/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "{{GITHUB_TOKEN}}"
      }
    }{{#each additional_servers}},
    "{{server_name}}": {
      "command": "{{command}}",
      "args": {{args}},
      "env": {{env_vars}}
    }{{/each}}
  }
}
```

### 第三步：权限配置
更新 `.claude/settings.local.json`：
```json
{
  "permissions": {
    "allow": [
      "Read", "Write", "Edit", "MultiEdit",
      "Bash(mkdir:*)", "Bash(ls:*)", "Bash(find:*)",
      "MCP(*)"
    ],
    "ask": ["Bash"],
    "mcp": {
      "allowed_servers": [
        {{#each allowed_mcp_servers}}"{{server_name}}"{{#unless @last}},{{/unless}}{{/each}}
      ]
    }
  }
}
```

## 🚀 配置验证和测试

### 验证安装
```bash
# 检查MCP服务器状态
claude mcp list

# 测试服务器连接
claude mcp test filesystem
claude mcp test brave-search
```

### 功能测试
在Claude Code中测试MCP功能：
```bash
# 测试文件操作
/mcp__filesystem__list_files

# 测试搜索功能  
/mcp__brave_search__search "{{PROJECT_DOMAIN}} latest trends"

# 测试GitHub集成
/mcp__github__list_repos
```

## 💡 使用建议和最佳实践

### 🎯 渐进式配置
1. **第一阶段**: 配置基础服务器包（filesystem, brave-search, github）
2. **第二阶段**: 根据团队需求添加领域专用服务器
3. **第三阶段**: 基于使用情况优化和扩展配置

### 🔒 安全注意事项
- **API密钥管理**: 使用环境变量安全存储敏感信息
- **权限控制**: 严格控制MCP服务器的访问权限
- **定期更新**: 保持MCP服务器版本更新

### ⚡ 性能优化
- **按需启用**: 只启用当前项目需要的服务器
- **资源监控**: 监控MCP服务器的资源使用情况
- **缓存配置**: 合理配置缓存机制提升响应速度

## 🎨 个性化定制建议

### 基于团队规模
- **小型团队** (1-3人): 基础配置 + 1-2个专用服务器
- **中型团队** (4-8人): 完整核心配置 + 领域专用包
- **大型团队** (8+人): 全套配置 + 企业级集成

### 基于项目复杂度
- **简单项目**: filesystem + brave-search
- **中等项目**: 核心包 + 2-3个专用服务器
- **复杂项目**: 完整配置 + 高级集成

## 📞 获取更多帮助

### 官方资源
- [Claude Code MCP文档](https://docs.anthropic.com/claude/docs/mcp)
- [MCP服务器GitHub仓库](https://github.com/anthropics/model-context-protocol)

### 社区支持
- MCP服务器社区论坛
- Claude Code用户社群
- 专业领域技术论坛

### 技术支持
- Claude Code官方技术支持
- MCP服务器开发者支持
- 企业级配置咨询服务

---

🔧 **配置提示**: 基于{{PROJECT_DOMAIN}}领域的特点，建议优先配置{{priority_servers}}，这将显著提升{{TEAM_NAME}}团队的工作效率和专业能力！
