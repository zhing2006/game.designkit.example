# Game Design Kit 示例项目

本项目展示如何使用 [Game Design Kit](https://github.com/zhing2006/game.designkit.git) 工具包来辅助游戏设计和开发工作。

## 环境准备

### 1. 添加 Game Design Kit 作为 Submodule

将 Game Design Kit 添加到项目中：

```bash
git submodule add https://github.com/zhing2006/game.designkit.git designkit
```

### 2. 配置 Git 支持符号链接

启用 Git 对符号链接的支持：

```bash
git config core.symlinks true
```

### 3. 根据使用的 AI 工具创建符号链接

根据你使用的 AI 编程工具，选择创建对应的符号链接：

#### 使用 Claude Code

```bash
mkdir -p .claude
ln -s ../designkit/.claude/commands .claude/commands
```

#### 使用 Codex

```bash
mkdir -p .codex
ln -s ../designkit/.codex/prompts .codex/prompts
```

#### 使用 Cursor

```bash
mkdir -p .cursor
ln -s ../designkit/.cursor/commands .cursor/commands
```

**注意**：只需要根据你实际使用的 AI 工具创建对应的符号链接，无需全部创建。

### 4. 创建游戏设计工作目录

创建 `.game.design` 目录并链接到设计工具的脚本和模板：

```bash
mkdir -p .game.design
ln -s ../designkit/.game.design/scripts .game.design/scripts
ln -s ../designkit/.game.design/templates .game.design/templates
```

这个目录提供：
- `scripts/` - 游戏设计辅助脚本（bash 和 powershell）
- `templates/` - 设计文档模板（规范、计划、任务等）

### 5. 配置 .gitignore

在项目根目录创建 `.gitignore` 文件，添加以下内容：

```gitignore
# Exclude everything in .claude except commands
.claude/*
!.claude/commands

# Exclude everything in .codex except prompts
.codex/*
!.codex/prompts

# Exclude everything in .cursor except commands
.cursor/*
!.cursor/commands

# MCP files
.mcp.json
```

这个配置确保：
- 只保留符号链接本身到版本控制
- 排除 AI 工具生成的配置文件和历史记录
- 保持仓库整洁

### 6. 提交初始化更改

完成以上配置后，提交更改：

```bash
git add .gitmodules designkit .gitignore .game.design/
# 根据你使用的 AI 工具添加对应的符号链接
git add .claude/commands  # 或 .codex/prompts 或 .cursor/commands
git commit -m "Initialize project with Game Design Kit"
```
