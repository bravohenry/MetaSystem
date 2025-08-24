---
description: MCP服务器配置指导和建议
allowed-tools: Read
---

# 🔧 MCP服务器配置指导

提供针对当前团队特点的MCP服务器配置建议，增强AI团队的专业能力。

## 功能说明

基于团队的专业领域和工作需求，推荐最适合的MCP服务器配置方案。

## 配置建议逻辑

### 基于项目领域的推荐

#### 🛠️ 产品开发团队
- **filesystem**: 高效文件操作和代码管理
- **github**: 版本控制和协作开发
- **postgres**: 数据库设计和管理

#### ✍️ 内容创作团队
- **brave-search**: 实时信息获取和研究
- **filesystem**: 文档管理和文件组织
- **github**: 内容版本控制

#### 📈 市场营销团队
- **brave-search**: 市场趋势研究
- **google-analytics**: 数据分析增强
- **social-media**: 社交媒体集成

#### 🔍 SEO优化团队
- **brave-search**: 竞争对手分析
- **google-search-console**: SEO数据集成
- **analytics**: 流量分析增强

#### 📊 数据分析团队
- **postgres**: 数据库连接
- **sqlite**: 轻量级数据处理
- **python-execution**: 代码执行环境

## 通用推荐配置

### 基础配置包
- **filesystem**: 文件系统操作（所有团队必备）
- **brave-search**: 网络搜索和信息获取
- **github**: 版本控制和协作

### 增强配置包
根据具体需求添加：
- **postgres/sqlite**: 数据库操作
- **python-execution**: 代码执行
- **google-drive**: 云端文件管理
- **slack**: 团队通信集成

## 配置方法

### 安装MCP服务器
```bash
# 安装推荐的MCP服务器
npm install -g @mcp/server-filesystem
npm install -g @mcp/server-brave-search
npm install -g @mcp/server-github
```

### Claude Code配置
```json
// 在 claude_desktop_config.json 中添加
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["@mcp/server-filesystem", "/path/to/workspace"]
    },
    "brave-search": {
      "command": "npx", 
      "args": ["@mcp/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "your_api_key"
      }
    }
  }
}
```

## 使用建议

1. **从基础配置开始**: 先配置filesystem和brave-search
2. **根据需求扩展**: 基于团队工作模式添加专用服务器
3. **测试验证**: 确保所有MCP服务器正常工作
4. **团队培训**: 让团队成员了解如何利用增强功能

## 获取更多帮助

- Claude Code官方文档：MCP服务器配置指南
- 各MCP服务器的GitHub仓库：详细配置说明
- 社区论坛：实际使用经验分享

## 使用方式

直接输入 `/mcp` 即可获得针对当前团队的配置建议。
