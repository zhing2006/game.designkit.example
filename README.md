# Game Design Kit 示例项目

本项目展示如何使用 [Game Design Kit](https://github.com/zhing2006/game.designkit.git) 工具包来辅助游戏设计和开发工作。

## 克隆仓库并支持符号链接

### 首次克隆仓库

本项目使用符号链接（symlinks）来共享 Game Design Kit 的配置文件。为了正确克隆仓库，请按照以下步骤操作：

#### Linux / macOS

```bash
# 克隆仓库并递归更新子模块
git clone <repository-url>
cd game.designkit.example
git submodule update --init --recursive
```

符号链接在 Linux 和 macOS 上默认支持，无需额外配置。

#### Windows

在 Windows 上使用符号链接需要满足以下条件之一：

**选项 1：启用开发者模式（推荐）**

1. 打开 Windows 设置
2. 进入"更新和安全" > "开发者选项"
3. 启用"开发人员模式"
4. 重启终端后执行：

```powershell
# 克隆仓库并递归更新子模块
git clone <repository-url>
cd game.designkit.example
git submodule update --init --recursive
```

**选项 2：使用管理员权限**

以管理员身份运行 PowerShell 或 Git Bash，然后执行克隆命令。

**配置 Git 支持符号链接**

```bash
# 全局启用符号链接支持（推荐）
git config --global core.symlinks true

# 或仅为当前仓库启用
git config core.symlinks true
```

**验证符号链接是否正常工作**

```bash
# Linux / macOS
ls -la .claude/commands  # 应显示 -> ../designkit/.claude/commands

# Windows (PowerShell)
Get-Item .claude\commands | Select-Object LinkType, Target
# 应显示 LinkType: SymbolicLink
```

### 如果已经克隆但符号链接未生效

如果你已经克隆了仓库但符号链接显示为普通文件，请执行以下步骤：

```bash
# 1. 启用符号链接支持
git config core.symlinks true

# 2. 重置工作区以重新创建符号链接
git reset --hard HEAD

# 3. 更新子模块
git submodule update --init --recursive
```

## 环境准备（新项目初始化）

如果你要创建一个新项目并使用 Game Design Kit，请按照以下步骤操作：

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
ln -s ../designkit/.claude/commands .codex/prompts
```

#### 使用 Cursor

```bash
mkdir -p .cursor
ln -s ../designkit/.claude/commands .cursor/commands
```

#### 使用 Kilo Code

```bash
mkdir -p .kilocode
ln -s ../designkit/.claude/commands .kilocode/workflows
```

#### 使用 Gemini CLI

```bash
mkdir -p .gemini
ln -s ../designkit/.claude/commands .gemini/commands
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

# Exclude everything in .kilocode except workflows
.kilocode/*
!.kilocode/workflows

# Exclude everything in .gemini except commands
.gemini/*
!.gemini/commands

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
git add .claude/commands     # Claude Code
# git add .codex/prompts     # Codex
# git add .cursor/commands   # Cursor
# git add .kilocode/workflows # Kilo Code
# git add .gemini/commands   # Gemini CLI
git commit -m "Initialize project with Game Design Kit"
```
