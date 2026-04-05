# Claude Code Best V5 (CCB)

[![GitHub Stars](https://img.shields.io/github/stars/claude-code-best/claude-code?style=flat-square&logo=github&color=yellow)](https://github.com/claude-code-best/claude-code/stargazers)
[![GitHub Contributors](https://img.shields.io/github/contributors/claude-code-best/claude-code?style=flat-square&color=green)](https://github.com/claude-code-best/claude-code/graphs/contributors)
[![GitHub Issues](https://img.shields.io/github/issues/claude-code-best/claude-code?style=flat-square&color=orange)](https://github.com/claude-code-best/claude-code/issues)
[![GitHub License](https://img.shields.io/github/license/claude-code-best/claude-code?style=flat-square)](https://github.com/claude-code-best/claude-code/blob/main/LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/claude-code-best/claude-code?style=flat-square&color=blue)](https://github.com/claude-code-best/claude-code/commits/main)
[![Bun](https://img.shields.io/badge/runtime-Bun-black?style=flat-square&logo=bun)](https://bun.sh/)

> Which Claude do you like? The open source one is the best.

A decompiled/reverse-engineered version of the official Anthropic [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI tool. The goal is to restore most of Claude Code's functionality and engineering capabilities (well, we've already paid for it anyway). It's hard not to laugh, but it's called CCB...

[Documentation is here, PRs welcome](https://ccb.agent-aura.top/)

Sponsorship placeholder

- [x] v1 will complete functional testing and basic type checking;
- [x] V2 will fully implement engineering infrastructure;
  - [ ] Biome formatting may not be implemented first to avoid code conflicts
  - [x] Build pipeline complete, artifacts can run on both Node and Bun
- [x] V3 will write extensive documentation and improve the documentation site
- [x] V4 will complete extensive test files to improve stability
  - [x] Buddy pet is back [Documentation](https://ccb.agent-aura.top/docs/features/buddy)
  - [x] Auto Mode restored [Documentation](https://ccb.agent-aura.top/docs/safety/auto-mode)
  - [x] All Features can now be configured via environment variables, no more `bun --feature`
- [x] V5 supports enterprise-grade monitoring and reporting, completes missing tools, lifts restrictions
  - [x] Remove anti-distillation code!!!
  - [x] Complete web search capability (using Bing search)!!! [Documentation](https://ccb.agent-aura.top/docs/features/web-browser-tool)
  - [x] Support Debug [Documentation](https://ccb.agent-aura.top/docs/features/debug-mode)
  - [x] Disable auto-updates;
  - [x] Add custom Sentry error reporting support [Documentation](https://ccb.agent-aura.top/docs/internals/sentry-setup)
  - [x] Add custom GrowthBook support (GB is also open source, now you can configure a custom control platform) [Documentation](https://ccb.agent-aura.top/docs/internals/growthbook-adapter)
  - [x] Custom login mode, everyone can configure Claude models this way!
- [ ] V6 massive refactoring and modularization
  - [ ] V6 will be on a new branch, at which time the main branch will be archived as historical version

> I don't know how long this project will survive. Star + Fork + git clone + .zip download is most reliable; in short, it's a flagship project, let's see how far it goes
>
> This project updates very quickly, with Opus continuously optimizing in the background, changes almost every few hours;
>
> Claude has already burned over $1000, ran out of money, switched to GLM to continue; @zai-org GLM 5.1 is very good;
>

## Quick Start

### Environment Requirements

Must use the latest version of bun, otherwise you'll encounter all sorts of weird bugs!!! `bun upgrade`!!!

- [Bun](https://bun.sh/) >= 1.3.11
- Standard Claude Code configuration, each provider has their own configuration method

### Installation

```bash
bun install
```

### Running

```bash
# Development mode, if you see version 888 then it's correct
bun run dev

# Build
bun run build
```

The build uses code splitting with multiple file bundling (`build.ts`), with artifacts output to the `dist/` directory (entry point `dist/cli.js` + approximately 450 chunk files).

The built version can be started with both bun and node. You can publish it to a private registry and run it directly.

If you encounter bugs, please open an issue directly, we prioritize fixing them.

### New User Configuration /login

After the first run, enter the `/login` command in the REPL to access the login configuration screen. Select **Custom Platform** to connect to third-party API-compatible services (no official Anthropic account required).

Fields to fill in:

| Field | Description | Example |
|-------|-------------|----------|
| Base URL | API service address | `https://api.example.com/v1` |
| API Key | Authentication key | `sk-xxx` |
| Haiku Model | Fast model ID | `claude-haiku-4-5-20251001` |
| Sonnet Model | Balanced model ID | `claude-sonnet-4-6` |
| Opus Model | High-performance model ID | `claude-opus-4-6` |

- **Tab / Shift+Tab** to switch fields, **Enter** to confirm and move to the next field, press Enter on the last field to save
- Model fields will automatically read and prefill from current environment variables
- Configuration is saved to the `env` field in `~/.claude/settings.json`, takes effect immediately after saving

You can also directly edit `~/.claude/settings.json`:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://api.example.com/v1",
    "ANTHROPIC_AUTH_TOKEN": "sk-xxx",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude-haiku-4-5-20251001",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude-sonnet-4-6",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude-opus-4-6"
  }
}
```

> Supports all Anthropic API-compatible services (such as OpenRouter, AWS Bedrock proxies, etc.), as long as the interface is compatible with the Messages API.

## Feature Flags

All feature flags are enabled via the `FEATURE_<FLAG_NAME>=1` environment variable, for example:

```bash
FEATURE_BUDDY=1 FEATURE_FORK_SUBAGENT=1 bun run dev
```

Detailed descriptions of each Feature can be found in the [`docs/features/`](docs/features/) directory, contributions are welcome.

## VS Code Debugging

TUI (REPL) mode requires a real terminal and cannot be debugged directly via VS Code launch. Use **attach mode**:

### Steps

1. **Start the inspect service in terminal**:
   ```bash
   bun run dev:inspect
   ```
   It will output an address similar to `ws://localhost:8888/xxxxxxxx`.

2. **Attach debugger in VS Code**:
   - Set breakpoints in `src/` files
   - Press F5 → Select **"Attach to Bun (TUI debug)"**


## Related Documentation and Websites

- **Online Documentation (Mintlify)**: [ccb.agent-aura.top](https://ccb.agent-aura.top/) — documentation source code is in the [`docs/`](docs/) directory, PRs are welcome
- **DeepWiki**: <https://deepwiki.com/claude-code-best/claude-code>

## Contributors

<a href="https://github.com/claude-code-best/claude-code/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=claude-code-best/claude-code" />
</a>

## Star History

<a href="https://www.star-history.com/?repos=claude-code-best%2Fclaude-code&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/image?repos=claude-code-best/claude-code&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/image?repos=claude-code-best/claude-code&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/image?repos=claude-code-best/claude-code&type=date&legend=top-left" />
 </picture>
</a>

## License

This project is for learning and research purposes only. All rights to Claude Code belong to [Anthropic](https://www.anthropic.com/).
