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
  <a href="https://exe.dev"><img src="https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/images/exy.png" alt="Exy mascot" width="48" /><br />exe.dev</a>
</p>

> New issues and PRs from new contributors are auto-closed by default. Maintainers review auto-closed issues daily. See [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md).

---

# Pi Monorepo

> **在寻找 pi 编码代理吗？** 请查看 **[packages/coding-agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)** 了解安装和使用方法。

用于构建 AI 代理和管理 LLM 部署的工具。

## 分享你的 OSS 编码代理会话

如果你在开源项目中使用 pi 或其他编码代理，请分享你的会话。

公开的 OSS 会话数据有助于使用真实世界的任务、工具使用、故障和修复来改进编码代理，而不是使用玩具基准测试。

完整说明请参见 [X 上的这篇帖子](https://x.com/badlogicgames/status/2037811643774652911)。

要发布会话，请使用 [`badlogic/pi-share-hf`](https://github.com/badlogic/pi-share-hf)。请阅读其 README.md 获取安装说明。你只需要一个 Hugging Face 账户、Hugging Face CLI 和 `pi-share-hf`。

你也可以观看 [这个视频](https://x.com/badlogicgames/status/2041151967695634619)，其中我展示如何发布我的 `pi-mono` 会话。

我定期在这里发布我自己的 `pi-mono` 工作会话：

- [badlogicgames/pi-mono on Hugging Face](https://huggingface.co/datasets/badlogicgames/pi-mono)

## Packages

| Package | Description |
|---------|-------------|
| **[@mariozechner/pi-ai](https://github.com/badlogic/pi-mono/tree/main/packages/ai)** | Unified multi-provider LLM API (OpenAI, Anthropic, Google, etc.) |
| **[@mariozechner/pi-agent-core](https://github.com/badlogic/pi-mono/tree/main/packages/agent)** | Agent runtime with tool calling and state management |
| **[@mariozechner/pi-coding-agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)** | Interactive coding agent CLI |
| **[@mariozechner/pi-mom](https://github.com/badlogic/pi-mono/tree/main/packages/mom)** | Slack bot that delegates messages to the pi coding agent |
| **[@mariozechner/pi-tui](https://github.com/badlogic/pi-mono/tree/main/packages/tui)** | Terminal UI library with differential rendering |
| **[@mariozechner/pi-web-ui](https://github.com/badlogic/pi-mono/tree/main/packages/web-ui)** | Web components for AI chat interfaces |
| **[@mariozechner/pi-pods](https://github.com/badlogic/pi-mono/tree/main/packages/pods)** | CLI for managing vLLM deployments on GPU pods |

## 贡献指南

请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md) 了解贡献指南，以及 [AGENTS.md](https://github.com/badlogic/pi-mono/blob/main/AGENTS.md) 了解项目特定规则（适用于人类和代理）。

## 开发

```bash
npm install          # 安装所有依赖项
npm run build        # 构建所有包
npm run check        # 代码检查、格式化和类型检查
./test.sh            # 运行测试（跳过不需要 API 键的 LLM 相关测试）
./pi-test.sh         # 从源代码运行 pi（可在任何目录执行）
```

> **注意：** `npm run check` 需要先运行 `npm run build`。web-ui 包使用 `tsc`，需要依赖项编译后的 `.d.ts` 文件。

## 许可证

MIT

## 定制

### Prompt Templates

可重用的提示作为 Markdown 文件。输入 `/name` 来展开。

```markdown
<!-- ~/.pi/agent/prompts/review.md -->
Review this code for bugs, security issues, and performance problems.
Focus on: {{focus}}
```

放置在 `~/.pi/agent/prompts/`、`.pi/prompts/`，或一个 [pi package](#pi-packages) 来与他人分享。请参阅 [docs/prompt-templates.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/prompt-templates.md)。

### Skills

按需能力包遵循 [Agent Skills standard](https://agentskills.io)。通过 `/skill:name` 调用或让代理自动加载。

```markdown
<!-- ~/.pi/agent/skills/my-skill/SKILL.md -->
# My Skill
使用此技能当用户询问关于 X。

## Steps
1. Do this
2. Then that
```

放置在 `~/.pi/agent/skills/`、`~/.agents/skills/`、`.pi/skills/`，或 `.agents/skills/`（从 `cwd` 向上遍历父级目录）或一个 [pi package](#pi-packages) 来与他人分享。请参阅 [docs/skills.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/skills.md)。

### Extensions

TypeScript 模块，用于扩展 pi 的自定义工具、命令、键盘快捷键、事件处理器和 UI 组件。

```typescript
export default function (pi: ExtensionAPI) {
  pi.registerTool({ name: "deploy", ... });
  pi.registerCommand("stats", { ... });
  pi.on("tool_call", async (event, ctx) => { ... });
}
```

**可能的扩展：**
- 自定义工具（或完全替换内置工具）
- 子代理和计划模式
- 自定义编译和摘要
- 权限门和路径保护
- 自定义编辑器和 UI 组件
- 状态行、页眉、页脚
- Git 检查点和自动提交
- SSH 和沙箱执行
- MCP 服务器集成
- 让 pi 看起来像 Claude Code
- 在等待时玩游戏（是的，Doom 可以运行）
- ...任何你能想到的

放置在 `~/.pi/agent/extensions/`、`.pi/extensions/`，或一个 [pi package](#pi-packages) 来与他人分享。请参阅 [docs/extensions.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/extensions.md) 和 [examples/extensions/](https://github.com/badlogic/pi-mono/tree/main/examples/extensions)。

### Themes

内置：`dark`、`light`。主题热重载：修改活动主题文件，pi 立即应用更改。

放置在 `~/.pi/agent/themes/`、`.pi/themes/`，或一个 [pi package](#pi-packages) 来与他人分享。请参阅 [docs/themes.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/themes.md)。

### Pi Packages

通过 npm 或 git 打包和共享扩展、技能、提示和主题。查找 npm 上的包：[npmjs.com](https://www.npmjs.com/search?q=keywords%3Api-package) 或 [Discord](https://discord.com/channels/1456806362351669492/1457744485428629628)。

> **安全性：** Pi 包以完全的系统权限运行。扩展执行任意代码，技能可以指导模型执行任何操作，包括运行可执行文件。在安装第三方包之前，请审查源代码。

```bash
pi install npm:@foo/pi-tools
pi install npm:@foo/pi-tools@1.2.3      # 固定版本
pi install git:github.com/user/repo
pi install git:github.com/user/repo@v1  # 标签或提交
pi install git:git@github.com:user/repo
pi install git:git@github.com:user/repo@v1  # 标签或提交
pi install https://github.com/user/repo
pi install https://github.com/user/repo@v1      # 标签或提交
pi install ssh://git@github.com/user/repo
pi install ssh://git@github.com/user/repo@v1    # 标签或提交
pi remove npm:@foo/pi-tools
pi uninstall npm:@foo/pi-tools          # 别名用于移除
pi list
pi update                               # 跳过固定包
pi config                               # 启用/禁用扩展、技能、提示、主题
```

包安装到 `~/.pi/agent/git/`（git）或全局 npm。使用 `-l` 进行项目本地安装（`.pi/git/`、`.pi/npm/`）。如果您使用 Node 版本管理器并希望包安装重用稳定的 npm 上下文，请在 `settings.json` 中设置 `npmCommand`，例如 `["mise", "exec", "node@20", "--", "npm"]`。

通过添加 `pi` 键到 `package.json` 创建包：

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

如果没有 `pi` 清单，pi 会自动从常规目录（`extensions/`、`skills/`、`prompts/`、`themes/`）中发现。

请参阅 [docs/packages.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/packages.md)。

---

## Programmatic Usage

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

await session.prompt("当前目录中有哪些文件？");
```

对于高级的多会话运行时替换，使用 `createAgentSessionRuntime()` 和 `AgentSessionRuntime`。

请参阅 [docs/sdk.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/sdk.md) 和 [examples/sdk/](examples/sdk/)。

### RPC Mode

对于非 Node.js 集成，使用 RPC 模式通过 stdin/stdout：

```bash
pi --mode rpc
```

RPC 模式使用严格的基于 LF 的 JSONL 帧格式。客户端必须仅按 `\n` 分割记录。不要使用通用的行读取器，比如 Node 的 `readline`，它也会在 JSON 有效负载内按 Unicode 分隔符分割。

请参阅 [docs/rpc.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/rpc.md) 了解协议。

---

## Philosophy

Pi 是高度可扩展的，因此它不需要指定你的工作流程。可以使用 [extensions](#extensions)、[skills](#skills) 或从第三方安装 [pi packages](#pi-packages) 来构建功能，而核心保持最小，让你能够按照自己的工作方式塑造 pi。

**没有 MCP。** 使用 README 构建 CLI 工具（请参阅 [Skills](#skills)），或构建一个扩展来添加 MCP 支持。[为什么？](https://mariozechner.at/posts/2025-11-02-what-if-you-dont-need-mcp/)

**没有子代理。** 有很多方法可以做到这一点。通过 tmux 启动 pi 实例，或者使用 [extensions](#extensions) 构建你自己的，或者安装一个按照你的方式工作的包。

**没有权限弹出窗口。** 在容器中运行，或使用 [extensions](#extensions) 构建自己的确认流程，以符合你的环境和安全要求。

**没有计划模式。** 将计划写入文件，或者使用 [extensions](#extensions) 构建它，或者安装一个包。

**没有内置的待办事项。** 它们会混淆模型。使用 TODO.md 文件，或者使用 [extensions](#extensions) 构建你自己的。

**没有后台 bash。** 使用 tmux。完全可观察，直接互动。

阅读 [博客文章](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/) 了解完整理由。

---

## CLI Reference

```bash
pi [options] [@files...] [messages...]
```

### Package Commands

```bash
pi install <source> [-l]     # 安装包，-l 表示项目本地
pi remove <source> [-l]      # 移除包
pi uninstall <source> [-l]   # 移除包的别名
pi update [source]           # 更新包（跳过固定包）
pi list                      # 列出已安装的包
pi config                    # 启用/禁用包资源
```

### 模式

| Flag | 描述 |
|------|-------------|
| (default) | 交互模式 |
| `-p`, `--print` | 打印响应并退出 |
| `--mode json` | 以 JSON 行输出所有事件（请参阅 [docs/json.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/json.md)） |
| `--mode rpc` | 用于进程集成的 RPC 模式（请参阅 [docs/rpc.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/rpc.md)） |
| `--export <in> [out]` | 导出会话为 HTML 文件 |

在打印模式下，pi 还会读取通过管道传入的 stdin 并将其合并到初始提示中：

```bash
cat README.md | pi -p "总结此文本"
```

### 模型选项

| 选项 | 描述 |
|------|-------------|
| `--provider <name>` | 提供者（anthropic、openai、google 等） |
| `--model <pattern>` | 模型模式或 ID（支持 `provider/id` 和可选的 `:<thinking>`） |
| `--api-key <key>` | API 密钥（覆盖环境变量） |
| `--thinking <level>` | `off`、`minimal`、`low`、`medium`、`high`、`xhigh` |
| `--models <patterns>` | 用于 Ctrl+P 循环的逗号分隔模式 |
| `--list-models [search]` | 列出可用的模型 |

### 会话选项

| 选项 | 描述 |
|------|-------------|
| `-c`, `--continue` | 继续最近一次会话 |
| `-r`, `--resume` | 浏览并选择会话 |
| `--session <path>` | 使用特定的会话文件或部分 UUID |
| `--fork <path>` | 从当前分支 Fork 一个特定的会话文件或部分 UUID 到一个新会话 |
| `--session-dir <dir>` | 自定义会话存储目录 |
| `--no-session` | 临时模式（不保存） |

### 工具选项

| 选项 | 描述 |
|------|-------------|
| `--tools <list>` | 启用特定的内置工具（默认：`read,bash,edit,write`） |
| `--no-tools` | 禁用所有内置工具（扩展工具仍有效） |

可用的内置工具：`read`、`bash`、`edit`、`write`、`grep`、`find`、`ls`

### 资源选项

| 选项 | 描述 |
|------|-------------|
| `-e`, `--extension <source>` | 从路径、npm 或 git 加载扩展（可重复） |
| `--no-extensions` | 禁用扩展发现 |
| `--skill <path>` | 加载技能（可重复） |
| `--no-skills` | 禁用技能发现 |
| `--prompt-template <path>` | 加载提示模板（可重复） |
| `--no-prompt-templates` | 禁用提示模板发现 |
| `--theme <path>` | 加载主题（可重复） |
| `--no-themes` | 禁用主题发现 |

将 `--no-*` 与显式标志结合以加载您需要的内容，忽略 settings.json（例如 `--no-extensions -e ./my-ext.ts`）。

### 其他选项

| 选项 | 描述 |
|------|-------------|
| `--system-prompt <text>` | 替换默认提示（上下文文件和技能仍会被追加） |
| `--append-system-prompt <text>` | 附加到系统提示 |
| `--verbose` | 强制详细启动 |
| `-h`, `--help` | 显示帮助 |
| `-v`, `--version` | 显示版本 |

### 文件参数

使用 `@` 前缀将文件包含在消息中：

```bash
pi @prompt.md "回答这个"
pi -p @screenshot.png "这张图片里有什么？"
pi @code.ts @test.ts "审查这些文件"
```

### 示例

```bash
# 带初始提示的交互模式
pi "列出 src/ 目录中所有的 .ts 文件"

# 非交互模式
pi -p "总结这个代码库"

# 通过管道输入的非交互模式
cat README.md | pi -p "总结此文本"

# 不同的模型
pi --provider openai --model gpt-4o "帮我重构代码"

# 带提供商标识符的模型（不需要 --provider）
pi --model openai/gpt-4o "帮我重构代码"

# 模型思维等级简写
pi --model sonnet:high "解决这个复杂问题"

# 限制模型循环
pi --models "claude-*,gpt-4o"

# 只读模式
pi --tools read,grep,find,ls -p "Review the code"

# 高思维等级
pi --thinking high "解决这个复杂问题"
```

### 环境变量

| 变量 | 描述 |
|------|-------------|
| `PI_CODING_AGENT_DIR` | 覆盖配置目录（默认：`~/.pi/agent`） |
| `PI_PACKAGE_DIR` | 覆盖包目录（对 Nix/Guix 有用，其中存储路径 token 化较差） |
| `PI_SKIP_VERSION_CHECK` | 启动时跳过版本检查 |
| `PI_TELEMETRY` | 覆盖安装遥测。使用 `1`/`true`/`yes` 启用或 `0`/`false`/`no` 禁用 |
| `PI_CACHE_RETENTION` | 设置为 `long` 以延长提示缓存（Anthropic: 1h，OpenAI: 24h） |
| `VISUAL`, `EDITOR` | 用于 Ctrl+G 的外部编辑器 |

---

## Contributing & Development

请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md) 了解指南，以及 [docs/development.md](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/development.md) 了解设置、Fork 和调试。

---

## License

MIT

## See Also

- [@mariozechner/pi-ai](https://www.npmjs.com/package/@mariozechner/pi-ai): Core LLM toolkit
- [@mariozechner/pi-agent](https://www.npmjs.com/package/@mariozechner/pi-agent): Agent framework
- [@mariozechner/pi-tui](https://www.npmjs.com/package/@mariozechner/pi-tui): Terminal UI components