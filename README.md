<p align="center">
  <a href="https://shittycodingagent.ai">
    <img src="https://shittycodingagent.ai/logo.svg" alt="pi logo" width="128">
  </a>
</p>
<p align="center">
  <a href="https://discord.com/invite/3cU7Bz4UPx"><img alt="Discord" src="https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white" /></a>
  <a href="https://github.com/badlogic/pi-mono/actions/workflows/ci.yml"><img alt="Build status" src="https://img.shields.io/github/actions/workflow/status/badlogic/pi-mono/ci.yml?style=flat-square&branch=main" /></a>
</p>
<p align="center">
  <a href="https://pi.dev">pi.dev</a> 域名由以下机构慷慨捐赠
  <br /><br />
  <a href="https://exe.dev"><img src="https://raw.githubusercontent.com/badlogic/pi-mono/main/packages/coding-agent/docs/images/exy.png" alt="Exy mascot" width="48" /><br />exe.dev</a>
</p>

> 新贡献者提交的 issue 和 PR 默认会自动关闭。维护者每天会审查自动关闭的 issue。请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md)。

---

# Pi Monorepo

> **寻找 pi 编码智能体？** 请参阅 **[packages/coding-agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)** 了解安装和使用方法。

用于构建 AI 智能体和管理 LLM 部署的工具。

## 分享你的开源编码智能体会话

如果你使用 pi 或其他编码智能体进行开源工作，请分享你的会话。

公开的开源会话数据有助于通过真实世界的任务、工具使用、失败和修复来改进编码智能体，而不是使用玩具基准测试。

完整的解释请参阅 [X 上的这篇帖子](https://x.com/badlogicgames/status/2037811643774652911)。

要发布会话，请使用 [`badlogic/pi-share-hf`](https://github.com/badlogic/pi-share-hf)。阅读其 README.md 了解设置说明。你只需要一个 Hugging Face 账户、Hugging Face CLI 和 `pi-share-hf`。

你也可以观看 [这个视频](https://x.com/badlogicgames/status/2041151967695634619)，我在其中展示了如何发布我的 `pi-mono` 会话。

我定期在这里发布我自己的 `pi-mono` 工作会话：

- [badlogicgames/pi-mono on Hugging Face](https://huggingface.co/datasets/badlogicgames/pi-mono)

## 包

| 包 | 描述 |
|---------|-------------|
| **[@mariozechner/pi-ai](https://github.com/badlogic/pi-mono/tree/main/packages/ai)** | 统一的多提供商 LLM API（OpenAI、Anthropic、Google 等） |
| **[@mariozechner/pi-agent-core](https://github.com/badlogic/pi-mono/tree/main/packages/agent)** | 具有工具调用和状态管理的智能体运行时 |
| **[@mariozechner/pi-coding-agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)** | 交互式编码智能体 CLI |
| **[@mariozechner/pi-mom](https://github.com/badlogic/pi-mono/tree/main/packages/mom)** | 将消息委托给 pi 编码智能体的 Slack 机器人 |
| **[@mariozechner/pi-tui](https://github.com/badlogic/pi-mono/tree/main/packages/tui)** | 具有差异渲染的终端 UI 库 |
| **[@mariozechner/pi-web-ui](https://github.com/badlogic/pi-mono/tree/main/packages/web-ui)** | 用于 AI 聊天界面的 Web 组件 |
| **[@mariozechner/pi-pods](https://github.com/badlogic/pi-mono/tree/main/packages/pods)** | 用于在 GPU pod 上管理 vLLM 部署的 CLI |

## 贡献

请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md) 了解贡献指南，参阅 [AGENTS.md](https://github.com/badlogic/pi-mono/blob/main/AGENTS.md) 了解项目特定规则（适用于人类和智能体）。

## 开发

```bash
npm install          # 安装所有依赖
npm run build        # 构建所有包
npm run check        # Lint、格式化和类型检查
./test.sh            # 运行测试（没有 API 密钥时跳过 LLM 依赖的测试）
./pi-test.sh         # 从源代码运行 pi（可以从任何目录运行）
```

> **注意：** `npm run check` 需要先运行 `npm run build`。web-ui 包使用 `tsc`，它需要来自依赖项的已编译 `.d.ts` 文件。

## 许可证

MIT