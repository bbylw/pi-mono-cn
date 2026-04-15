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
  <a href="https://pi.dev">pi.dev</a> 域名由以下方慷慨捐赠
  <br /><br />
  <a href="https://exe.dev"><img src="packages/coding-agent/docs/images/exy.png" alt="Exy mascot" width="48" /><br />exe.dev</a>
</p>

>> 默认情况下，来自新贡献者的新问题和拉取请求会被自动关闭。维护者会每天审查自动关闭的问题。请参阅 [CONTRIBUTING.md](https://github.com/badlogic/pi-mono/blob/main/CONTRIBUTING.md)。

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
