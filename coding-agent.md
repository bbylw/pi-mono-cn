<p align="center">
  <a href="https://shittycodingagent.ai">
    <img src="https://shittycodingagent.ai/logo.svg" alt="pi logo" width="128">
  </a>
</p>
<p align="center">
  <a href="https://discord.com/invite/3cU7Bz4UPx"><img alt="Discord" src="https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white" /></a>
  <a href="https://www.npmjs.com/package/@mariozechner/pi-coding-agent"><img alt="npm" src="https://img.shields.io/npm/v/@mariozechner/pi-coding-agent?style=flat-square" /></a>
  <a href="https://github.com/badlogic/pi-mono/actions/workflows/ci.yml"><img alt="Build status" src="https://img.shields.io/github/actions/workflow/status/badlogic/pi-mono/ci.yml?style=flat-square&branch=main" /></a>
</p>
<p align="center">
  <a href="https://pi.dev">pi.dev</a> domain graciously donated by
  <br /><br />
  <a href="https://exe.dev"><img src="https://raw.githubusercontent.com/badlogic/pi-mono/main/packages/coding-agent/docs/images/exy.png" alt="Exy mascot" width="48" /><br />exe.dev</a>
</p>

> 新贡献者提交的 issue 和 PR 默认会自动关闭。维护者每天会审查自动关闭的 issue。请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md)。

---

Pi 是一个极简的终端编码工具。让 pi 适应你的工作流程，而不是反过来，无需 fork 和修改 pi 内部代码。通过 TypeScript [扩展](#extensions)、[技能](#skills)、[提示模板](#prompt-templates) 和 [主题](#themes) 来扩展它。将你的扩展、技能、提示模板和主题放入 [Pi 包](#pi-packages) 中，并通过 npm 或 git 与他人分享。

Pi 附带强大的默认设置，但跳过了子智能体和计划模式等功能。相反，你可以让 pi 构建你想要的功能，或安装符合你工作流程的第三方 pi 包。

Pi 以四种模式运行：交互式、打印或 JSON、用于进程集成的 RPC，以及用于嵌入你自己的应用程序的 SDK。请参阅 [openclaw/openclaw](https://github.com/openclaw/openclaw) 了解实际的 SDK 集成。

## 分享你的开源编码智能体会话

如果你使用 pi 进行开源工作，请分享你的编码智能体会话。

公开的开源会话数据有助于使用真实的开发工作流程来改进模型、提示、工具和评估。

完整的解释请参阅 [X 上的这篇帖子](https://x.com/badlogicgames/status/2037811643774652911)。

要发布会话，请使用 [`badlogic/pi-share-hf`](https://github.com/badlogic/pi-share-hf)。阅读其 README.md 了解设置说明。你只需要一个 Hugging Face 账户、Hugging Face CLI 和 `pi-share-hf`。

你也可以观看 [这个视频](https://x.com/badlogicgames/status/2041151967695634619)，我在其中展示了如何发布我的 `pi-mono` 会话。

我定期在这里发布我自己的 `pi-mono` 工作会话：

- [badlogicgames/pi-mono on Hugging Face](https://huggingface.co/datasets/badlogicgames/pi-mono)

## Table of Contents

- [快速开始](#quick-start)
- [提供商和模型](#providers--models)
- [交互模式](#interactive-mode)
  - [编辑器](#editor)
  - [命令](#commands)
  - [键盘快捷键](#keyboard-shortcuts)
  - [消息队列](#message-queue)
- [会话](#sessions)
  - [分支](#branching)
  - [压缩](#compaction)
- [设置](#settings)
- [上下文文件](#context-files)
- [自定义](#customization)
  - [提示模板](#prompt-templates)
  - [技能](#skills)
  - [扩展](#extensions)
  - [主题](#themes)
  - [Pi 包](#pi-packages)
- [编程用法](#programmatic-usage)
- [理念](#philosophy)
- [CLI 参考](#cli-reference)

---

## 快速开始

```bash
npm install -g @mariozechner/pi-coding-agent
```

使用 API 密钥进行身份验证：

```bash
export ANTHROPIC_API_KEY=sk-ant-...
pi
```

或使用你现有的订阅：

```bash
pi
/login  # 然后选择提供商
```

然后直接与 pi 对话。默认情况下，pi 为模型提供四个工具：`read`、`write`、`edit` 和 `bash`。模型使用这些工具来满足你的请求。通过 [技能](#skills)、[提示模板](#prompt-templates)、[扩展](#extensions) 或 [pi 包](#pi-packages) 添加功能。

**平台说明：** [Windows](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/windows.md) | [Termux (Android)](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/termux.md) | [tmux](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/tmux.md) | [终端设置](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/terminal-setup.md) | [Shell 别名](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/shell-aliases.md)

---

## 提供商和模型

对于每个内置提供商，pi 维护一个支持工具的模型列表，每次发布时更新。通过订阅（`/login`）或 API 密钥进行身份验证，然后通过 `/model`（或 Ctrl+L）选择该提供商的任何模型。

**订阅：**
- Anthropic Claude Pro/Max
- OpenAI ChatGPT Plus/Pro (Codex)
- GitHub Copilot
- Google Gemini CLI
- Google Antigravity

**API 密钥：**
- Anthropic
- OpenAI
- Azure OpenAI
- Google Gemini
- Google Vertex
- Amazon Bedrock
- Mistral
- Groq
- Cerebras
- xAI
- OpenRouter
- Vercel AI Gateway
- ZAI
- OpenCode Zen
- OpenCode Go
- Hugging Face
- Kimi For Coding
- MiniMax

详细的设置说明请参阅 [docs/providers.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/providers.md)。

**自定义提供商和模型：** 如果它们使用支持的 API（OpenAI、Anthropic、Google），可以通过 `~/.pi/agent/models.json` 添加提供商。对于自定义 API 或 OAuth，请使用扩展。请参阅 [docs/models.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/models.md) 和 [docs/custom-provider.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/custom-provider.md)。

---

## 交互模式

<p align="center"><img src="https://raw.githubusercontent.com/badlogic/pi-mono/main/packages/coding-agent/docs/images/interactive-mode.png" alt="Interactive Mode" width="600"></p>

界面从上到下：

- **启动头部** - 显示快捷键（`/hotkeys` 查看全部）、已加载的 AGENTS.md 文件、提示模板、技能和扩展
- **消息** - 你的消息、助手响应、工具调用和结果、通知、错误和扩展 UI
- **编辑器** - 你输入的地方；边框颜色表示思考级别
- **页脚** - 工作目录、会话名称、总令牌/缓存使用量、成本、上下文使用量、当前模型

编辑器可以被其他 UI 临时替换，例如内置的 `/settings` 或来自扩展的自定义 UI（例如，让用户以结构化格式回答模型问题的问答工具）。[扩展](#extensions) 还可以替换编辑器，在其上方/下方添加小部件、状态行、自定义页脚或覆盖层。

### 编辑器

| 功能 | 方法 |
|---------|-----|
| 文件引用 | 输入 `@` 模糊搜索项目文件 |
| 路径补全 | Tab 补全路径 |
| 多行 | Shift+Enter（或在 Windows Terminal 上使用 Ctrl+Enter）|
| 图片 | Ctrl+V 粘贴（在 Windows 上使用 Alt+V），或拖动到终端 |
| Bash 命令 | `!command` 运行并将输出发送到 LLM，`!!command` 运行但不发送 |

标准的编辑键绑定，用于删除单词、撤销等。请参阅 [docs/keybindings.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/keybindings.md)。

### 命令

在编辑器中输入 `/` 触发命令。[扩展](#extensions) 可以注册自定义命令，[技能](#skills) 可作为 `/skill:name` 使用，[提示模板](#prompt-templates) 通过 `/templatename` 展开。

| 命令 | 描述 |
|---------|-------------|
| `/login`, `/logout` | OAuth 身份验证 |
| `/model` | 切换模型 |
| `/scoped-models` | 启用/禁用 Ctrl+P 循环的模型 |
| `/settings` | 思考级别、主题、消息传递、传输方式 |
| `/resume` | 从以前的会话中选择 |
| `/new` | 开始新会话 |
| `/name <name>` | 设置会话显示名称 |
| `/session` | 显示会话信息（路径、令牌、成本）|
| `/tree` | 跳转到会话中的任何点并从那里继续 |
| `/fork` | 从当前分支创建新会话 |
| `/compact [prompt]` | 手动压缩上下文，可选自定义指令 |
| `/copy` | 将最后一条助手消息复制到剪贴板 |
| `/export [file]` | 将会话导出为 HTML 文件 |
| `/share` | 上传为私有 GitHub gist，带有可共享的 HTML 链接 |
| `/reload` | 重新加载键绑定、扩展、技能、提示和上下文文件（主题自动热重载）|
| `/hotkeys` | 显示所有键盘快捷键 |
| `/changelog` | 显示版本历史 |
| `/quit` | 退出 pi |

### 键盘快捷键

完整列表请参阅 `/hotkeys`。通过 `~/.pi/agent/keybindings.json` 自定义。请参阅 [docs/keybindings.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/keybindings.md)。

**常用：**

| 键 | 操作 |
|-----|--------|
| Ctrl+C | 清除编辑器 |
| Ctrl+C 两次 | 退出 |
| Escape | 取消/中止 |
| Escape 两次 | 打开 `/tree` |
| Ctrl+L | 打开模型选择器 |
| Ctrl+P / Shift+Ctrl+P | 向前/向后循环范围模型 |
| Shift+Tab | 循环思考级别 |
| Ctrl+O | 折叠/展开工具输出 |
| Ctrl+T | 折叠/展开思考块 |

### 消息队列

在智能体工作时提交消息：

- **Enter** 将 *引导* 消息排队，在当前助手回合完成执行其工具调用后传递
- **Alt+Enter** 将 *后续* 消息排队，仅在智能体完成所有工作后传递
- **Escape** 中止并将排队的消息恢复到编辑器
- **Alt+Up** 将排队的消息检索回编辑器

在 Windows Terminal 上，`Alt+Enter` 默认为全屏。在 [docs/terminal-setup.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/terminal-setup.md) 中重新映射它，以便 pi 可以接收后续快捷键。

在 [设置](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/settings.md) 中配置传递：`steeringMode` 和 `followUpMode` 可以是 `"one-at-a-time"`（默认，等待响应）或 `"all"`（一次传递所有排队消息）。`transport` 为支持多种传输的提供商选择提供商传输首选项（`"sse"`、`"websocket"` 或 `"auto"`）。

---

## 会话

会话以具有树结构的 JSONL 文件存储。每个条目都有一个 `id` 和 `parentId`，可以在不创建新文件的情况下进行就地分支。请参阅 [docs/session.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/session.md) 了解文件格式。

### 管理

会话自动保存到 `~/.pi/agent/sessions/`，按工作目录组织。

```bash
pi -c                  # 继续最近的会话
pi -r                  # 浏览并从过去的会话中选择
pi --no-session        # 临时模式（不保存）
pi --session <path>    # 使用特定的会话文件或 ID
pi --fork <path>       # 将特定的会话文件或 ID 分叉到新会话
```

### 分支

**`/tree`** - 就地导航会话树。选择任何以前的点，从那里继续，并在分支之间切换。所有历史记录保存在单个文件中。

<p align="center"><img src="https://raw.githubusercontent.com/badlogic/pi-mono/main/packages/coding-agent/docs/images/tree-view.png" alt="Tree View" width="600"></p>

- 通过输入搜索，使用 Ctrl+←/Ctrl+→ 或 Alt+←/Alt+→ 在分支之间折叠/展开和跳转，使用 ←/→ 翻页
- 过滤模式（Ctrl+O）：默认 → 无工具 → 仅用户 → 仅标签 → 全部
- 按 Shift+L 将条目标记为书签，按 Shift+T 切换标签时间戳

**`/fork`** - 从当前分支创建新的会话文件。打开选择器，复制历史记录直到选定点，并将该消息放在编辑器中进行修改。

**`--fork <path|id>`** - 直接从 CLI 分叉现有的会话文件或部分会话 UUID。这会将完整的源会话复制到当前项目中的新会话文件。

### 压缩

长会话可能会耗尽上下文窗口。压缩会总结较旧的消息，同时保留较新的消息。

**手动：** `/compact` 或 `/compact <自定义指令>`

**自动：** 默认启用。在上下文溢出时触发（恢复并重试）或在接近限制时触发（主动）。通过 `/settings` 或 `settings.json` 配置。

压缩是有损的。完整的历史记录保留在 JSONL 文件中；使用 `/tree` 重新访问。通过 [扩展](#extensions) 自定义压缩行为。请参阅 [docs/compaction.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/compaction.md) 了解内部原理。

---

## 设置

使用 `/settings` 修改常用选项，或直接编辑 JSON 文件：

| 位置 | 范围 |
|----------|-------|
| `~/.pi/agent/settings.json` | 全局（所有项目）|
| `.pi/settings.json` | 项目（覆盖全局）|

所有选项请参阅 [docs/settings.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/settings.md)。

要选择退出与变更日志检测相关的匿名安装/更新遥测，请在 `settings.json` 中将 `enableInstallTelemetry` 设置为 `false`，或设置 `PI_TELEMETRY=0`。

---

## 上下文文件

Pi 在启动时从以下位置加载 `AGENTS.md`（或 `CLAUDE.md`）：
- `~/.pi/agent/AGENTS.md`（全局）
- 父目录（从 cwd 向上遍历）
- 当前目录

用于项目指令、约定、常用命令。所有匹配的文件都会被连接。

### 系统提示

使用 `.pi/SYSTEM.md`（项目）或 `~/.pi/agent/SYSTEM.md`（全局）替换默认系统提示。通过 `APPEND_SYSTEM.md` 追加而不替换。

---

## 自定义

### 提示模板

可重用的提示作为 Markdown 文件。输入 `/name` 展开。

```markdown
<!-- ~/.pi/agent/prompts/review.md -->
审查此代码的错误、安全问题和性能问题。
重点关注：{{focus}}
```

放置在 `~/.pi/agent/prompts/`、`.pi/prompts/` 或 [pi 包](#pi-packages) 中与他人分享。请参阅 [docs/prompt-templates.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/prompt-templates.md)。

### 技能

按需功能包，遵循 [Agent Skills 标准](https://agentskills.io)。通过 `/skill:name` 调用或让智能体自动加载它们。

```markdown
<!-- ~/.pi/agent/skills/my-skill/SKILL.md -->
# 我的技能
当用户询问 X 时使用此技能。

## 步骤
1. 执行此操作
2. 然后执行那个操作
```

放置在 `~/.pi/agent/skills/`、`~/.agents/skills/`、`.pi/skills/` 或 `.agents/skills/`（从 `cwd` 向上通过父目录）或 [pi 包](#pi-packages) 中与他人分享。请参阅 [docs/skills.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/skills.md)。

### 扩展

<p align="center"><img src="https://raw.githubusercontent.com/badlogic/pi-mono/main/packages/coding-agent/docs/images/doom-extension.png" alt="Doom Extension" width="600"></p>

TypeScript 模块，通过自定义工具、命令、键盘快捷键、事件处理程序和 UI 组件来扩展 pi。

```typescript
export default function (pi: ExtensionAPI) {
  pi.registerTool({ name: "deploy", ... });
  pi.registerCommand("stats", { ... });
  pi.on("tool_call", async (event, ctx) => { ... });
}
```

**可以实现的功能：**
- 自定义工具（或完全替换内置工具）
- 子智能体和计划模式
- 自定义压缩和摘要
- 权限门控和路径保护
- 自定义编辑器和 UI 组件
- 状态行、头部、页脚
- Git 检查点和自动提交
- SSH 和沙箱执行
- MCP 服务器集成
- 让 pi 看起来像 Claude Code
- 等待时玩游戏（是的，Doom 可以运行）
- ...任何你能想到的功能

放置在 `~/.pi/agent/extensions/`、`.pi/extensions/` 或 [pi 包](#pi-packages) 中与他人分享。请参阅 [docs/extensions.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/extensions.md) 和 [examples/extensions/](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent/examples/extensions/)。

### 主题

内置：`dark`、`light`。主题热重载：修改活动主题文件，pi 立即应用更改。

放置在 `~/.pi/agent/themes/`、`.pi/themes/` 或 [pi 包](#pi-packages) 中与他人分享。请参阅 [docs/themes.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/themes.md)。

### Pi 包

通过 npm 或 git 打包和分享扩展、技能、提示和主题。在 [npmjs.com](https://www.npmjs.com/search?q=keywords%3Api-package) 或 [Discord](https://discord.com/channels/1456806362351669492/1457744485428629628) 上查找包。

> **安全：** Pi 包以完全系统访问权限运行。扩展执行任意代码，技能可以指示模型执行任何操作，包括运行可执行文件。在安装第三方包之前，请查看源代码。

```bash
pi install npm:@foo/pi-tools
pi install npm:@foo/pi-tools@1.2.3      # pinned version
pi install git:github.com/user/repo
pi install git:github.com/user/repo@v1  # tag or commit
pi install git:git@github.com:user/repo
pi install git:git@github.com:user/repo@v1  # tag or commit
pi install https://github.com/user/repo
pi install https://github.com/user/repo@v1      # tag or commit
pi install ssh://git@github.com/user/repo
pi install ssh://git@github.com/user/repo@v1    # tag or commit
pi remove npm:@foo/pi-tools
pi uninstall npm:@foo/pi-tools          # alias for remove
pi list
pi update                               # skips pinned packages
pi config                               # enable/disable extensions, skills, prompts, themes
```

包安装到 `~/.pi/agent/git/`（git）或全局 npm。使用 `-l` 进行项目本地安装（`.pi/git/`、`.pi/npm/`）。如果你使用 Node 版本管理器并希望包安装重用稳定的 npm 上下文，请在 `settings.json` 中设置 `npmCommand`，例如 `["mise", "exec", "node@20", "--", "npm"]`。

通过在 `package.json` 中添加 `pi` 键来创建包：

```json
{
  "name": "my-pi-package",
  "keywords": ["pi-package"],
  "pi": {
    "extensions": ["./extensions"],
    "skills": ["./skills"],
    "prompts": ["./prompts"],
    "themes": ["./themes"]
  }
}
```

如果没有 `pi` 清单，pi 会从常规目录（`extensions/`、`skills/`、`prompts/`、`themes/`）自动发现。

请参阅 [docs/packages.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/packages.md)。

---

## 编程用法

### SDK

```typescript
import { AuthStorage, createAgentSession, ModelRegistry, SessionManager } from "@mariozechner/pi-coding-agent";

const authStorage = AuthStorage.create();
const modelRegistry = ModelRegistry.create(authStorage);
const { session } = await createAgentSession({
  sessionManager: SessionManager.inMemory(),
  authStorage,
  modelRegistry,
});

await session.prompt("What files are in the current directory?");
```

对于高级多会话运行时替换，请使用 `createAgentSessionRuntime()` 和 `AgentSessionRuntime`。

请参阅 [docs/sdk.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/sdk.md) 和 [examples/sdk/](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent/examples/sdk/)。

### RPC 模式

对于非 Node.js 集成，请通过 stdin/stdout 使用 RPC 模式：

```bash
pi --mode rpc
```

RPC 模式使用严格的 LF 分隔 JSONL 帧格式。客户端必须仅在 `\n` 上拆分记录。不要使用通用的行读取器（如 Node `readline`），它们也会在 JSON 载荷内的 Unicode 分隔符上拆分。

协议请参阅 [docs/rpc.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/rpc.md)。

---

## 理念

Pi 具有极强的可扩展性，因此不必规定你的工作流程。其他工具内置的功能可以通过 [扩展](#extensions)、[技能](#skills) 构建，或从第三方 [pi 包](#pi-packages) 安装。这保持了核心的最小化，同时让你能够塑造 pi 以适应你的工作方式。

**没有 MCP。** 使用 README 构建 CLI 工具（请参阅 [技能](#skills)），或构建添加 MCP 支持的扩展。[为什么？](https://mariozechner.at/posts/2025-11-02-what-if-you-dont-need-mcp/)

**没有子智能体。** 有很多方法可以实现这一点。通过 tmux 生成 pi 实例，或使用 [扩展](#extensions) 构建自己的子智能体，或安装以你自己的方式执行此操作的包。

**没有权限弹出窗口。** 在容器中运行，或使用 [扩展](#extensions) 构建你自己的确认流程，与你的环境和安全要求内联。

**没有计划模式。** 将计划写入文件，或使用 [扩展](#extensions) 构建，或安装包。

**没有内置待办事项。** 它们会混淆模型。使用 TODO.md 文件，或使用 [扩展](#extensions) 构建自己的待办事项。

**没有后台 bash。** 使用 tmux。完全可观察性，直接交互。

完整的理由请阅读 [博客文章](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/)。

---

## CLI 参考

```bash
pi [options] [@files...] [messages...]
```

### 包命令

```bash
pi install <source> [-l]     # 安装包，-l 用于项目本地
pi remove <source> [-l]      # 移除包
pi uninstall <source> [-l]   # remove 的别名
pi update [source]           # 更新包（跳过固定版本）
pi list                      # 列出已安装的包
pi config                    # 启用/禁用包资源
```

### 模式

| 标志 | 描述 |
|------|-------------|
| (default) | 交互模式 |
| `-p`, `--print` | 打印响应并退出 |
| `--mode json` | 将所有事件输出为 JSON 行（请参阅 [docs/json.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/json.md)）|
| `--mode rpc` | 用于进程集成的 RPC 模式（请参阅 [docs/rpc.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/rpc.md)）|
| `--export <in> [out]` | 将会话导出为 HTML |

在打印模式下，pi 还会读取管道 stdin 并将其合并到初始提示中：

```bash
cat README.md | pi -p "Summarize this text"
```

### 模型选项

| 选项 | 描述 |
|--------|-------------|
| `--provider <name>` | 提供商（anthropic、openai、google 等）|
| `--model <pattern>` | 模型模式或 ID（支持 `provider/id` 和可选的 `:<thinking>`）|
| `--api-key <key>` | API 密钥（覆盖环境变量）|
| `--thinking <level>` | `off`、`minimal`、`low`、`medium`、`high`、`xhigh` |
| `--models <patterns>` | 用于 Ctrl+P 循环的逗号分隔模式 |
| `--list-models [search]` | 列出可用模型 |

### 会话选项

| 选项 | 描述 |
|--------|-------------|
| `-c`, `--continue` | 继续最近的会话 |
| `-r`, `--resume` | 浏览并选择会话 |
| `--session <path>` | 使用特定的会话文件或部分 UUID |
| `--fork <path>` | 将特定的会话文件或部分 UUID 分叉到新会话 |
| `--session-dir <dir>` | 自定义会话存储目录 |
| `--no-session` | 临时模式（不保存）|

### 工具选项

| 选项 | 描述 |
|--------|-------------|
| `--tools <list>` | 启用特定的内置工具（默认：`read,bash,edit,write`）|
| `--no-tools` | 禁用所有内置工具（扩展工具仍然有效）|

可用的内置工具：`read`、`bash`、`edit`、`write`、`grep`、`find`、`ls`

### 资源选项

| 选项 | 描述 |
|--------|-------------|
| `-e`, `--extension <source>` | 从路径、npm 或 git 加载扩展（可重复）|
| `--no-extensions` | 禁用扩展发现 |
| `--skill <path>` | 加载技能（可重复）|
| `--no-skills` | 禁用技能发现 |
| `--prompt-template <path>` | 加载提示模板（可重复）|
| `--no-prompt-templates` | 禁用提示模板发现 |
| `--theme <path>` | 加载主题（可重复）|
| `--no-themes` | 禁用主题发现 |

将 `--no-*` 与显式标志结合使用，以准确加载你需要的内容，忽略 settings.json（例如 `--no-extensions -e ./my-ext.ts`）。

### 其他选项

| 选项 | 描述 |
|--------|-------------|
| `--system-prompt <text>` | 替换默认提示（上下文文件和技能仍然追加）|
| `--append-system-prompt <text>` | 追加到系统提示 |
| `--verbose` | 强制详细启动 |
| `-h`, `--help` | 显示帮助 |
| `-v`, `--version` | 显示版本 |

### 文件参数

使用 `@` 前缀文件以包含在消息中：

```bash
pi @prompt.md "Answer this"
pi -p @screenshot.png "What's in this image?"
pi @code.ts @test.ts "Review these files"
```

### 示例

```bash
# 带有初始提示的交互模式
pi "列出 src/ 中的所有 .ts 文件"

# 非交互模式
pi -p "总结此代码库"

# 带有管道 stdin 的非交互模式
cat README.md | pi -p "总结此文本"

# 不同模型
pi --provider openai --model gpt-4o "帮我重构"

# 带有提供商前缀的模型（不需要 --provider）
pi --model openai/gpt-4o "帮我重构"

# 带有思考级别简写的模型
pi --model sonnet:high "解决这个复杂问题"

# 限制模型循环
pi --models "claude-*,gpt-4o"

# 只读模式
pi --tools read,grep,find,ls -p "审查代码"

# 高思考级别
pi --thinking high "解决这个复杂问题"
```

### 环境变量

| 变量 | 描述 |
|----------|-------------|
| `PI_CODING_AGENT_DIR` | 覆盖配置目录（默认：`~/.pi/agent`）|
| `PI_PACKAGE_DIR` | 覆盖包目录（对于存储路径标记不佳的 Nix/Guix 很有用）|
| `PI_SKIP_VERSION_CHECK` | 跳过启动时的版本检查 |
| `PI_TELEMETRY` | 覆盖安装遥测。使用 `1`/`true`/`yes` 启用或 `0`/`false`/`no` 禁用 |
| `PI_CACHE_RETENTION` | 设置为 `long` 以扩展提示缓存（Anthropic：1h，OpenAI：24h）|
| `VISUAL`, `EDITOR` | Ctrl+G 的外部编辑器 |

---

## 贡献和开发

请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md) 了解指南，参阅 [docs/development.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/development.md) 了解设置、分叉和调试。

---

## 许可证

MIT

## 另请参阅

- [@mariozechner/pi-ai](https://www.npmjs.com/package/@mariozechner/pi-ai): 核心 LLM 工具包
- [@mariozechner/pi-agent](https://www.npmjs.com/package/@mariozechner/pi-agent): 智能体框架
- [@mariozechner/pi-tui](https://www.npmjs.com/package/@mariozechner/pi-tui): 终端 UI 组件