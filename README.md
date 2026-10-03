# OpenClash 专家助手

用于 Codex 的中文 skill，帮助配置、排查和理解 OpenWrt 上的 OpenClash / Mihomo。

## 工作机制

本仓库提供指导 AI 行为的指令，使用时要求 AI 重新获取并完整阅读 [OpenClash 官方用户指南](https://raw.githubusercontent.com/vernesong/OpenClash/dev/.github/skills/openclash-user-guide/SKILL.md)，再依据指南回答。仓库不保存指南副本；无法获取或完整读取指南时，skill 要求停止给出实质性建议。

适用范围包括启停与运行模式、代理与 DNS、流量和访问控制、IPv6、规则与 GEO 更新、订阅、覆写模块、日志分析、LuCI 操作、UCI / CLI 命令，以及源码和 Issue 核验。

## 安装

在 Codex 中使用内置安装器，输入：

```text
使用 $skill-installer 安装 https://github.com/phoenixap/openclash-expert-skill 中仓库根目录的 skill，安装名称为 openclash-expert。
```

也可以将仓库克隆到个人 skill 目录。按[当前 Codex 官方文档](https://learn.chatgpt.com/docs/build-skills)，个人目录为 `~/.agents/skills`。

Windows PowerShell（需要 Git，目标目录须不存在）：

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.agents\skills" | Out-Null
git clone https://github.com/phoenixap/openclash-expert-skill.git "$HOME\.agents\skills\openclash-expert"
```

macOS / Linux：

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/phoenixap/openclash-expert-skill.git ~/.agents/skills/openclash-expert
```

部分现有安装使用 `~/.codex/skills`；请以本机实际配置和安装器结果为准，避免在多个目录重复安装同名 skill。安装后检查 skill 列表；未显示时重新启动 Codex。

## 使用示例

```text
使用 $openclash-expert 帮我配置或排查 OpenClash 问题。
```

```text
$openclash-expert OpenClash 启动失败，帮我按官方指南排查。
```

```text
$openclash-expert 解释这个覆写配置为什么没有生效，并核验相关源码。
```

## 使用要求与边界

- AI 需要能访问远程指南，并在需要时查阅官方文档、源码和 Issues。
- 配置问题优先提供 LuCI 路径；明确要求 CLI 或 LuCI 不可用时才提供命令。
- 故障排查先获取调试日志，再按证据分析；分享日志前应脱敏密码、订阅链接、节点凭据和令牌。
- 输出区分只读诊断、状态修改和高风险操作；实际修改路由器需要单独授权并验证。
- 本仓库没有执行脚本，也不会自行连接、修改或重启路由器。指令能约束回答流程，但不能保证模型每次都正确执行。

## 仓库结构

```text
openclash-expert-skill/
├── SKILL.md            # 触发描述、权威来源和回答工作流
├── LICENSE             # MIT 许可证和本仓库版权署名
├── agents/
│   └── openai.yaml     # 显示名称、简述和默认提示词
└── README.md
```

## 来源

- [OpenClash 项目](https://github.com/vernesong/OpenClash)
- [OpenClash 官方用户指南](https://raw.githubusercontent.com/vernesong/OpenClash/dev/.github/skills/openclash-user-guide/SKILL.md)
- [Codex skill 文档](https://learn.chatgpt.com/docs/build-skills)

本仓库是独立的 skill 包，未声明与 OpenClash、Mihomo 或 OpenAI 存在官方关联。上游内容及商标的权利归各自权利人所有。

## 许可证与署名

本仓库原创内容采用 [MIT 许可证](LICENSE)，版权署名为 `Copyright (c) 2026 phoenixap`。使用、修改或分发这些内容时，请保留许可证及版权声明。

本 skill 的设计参考了 OpenClash 项目的用户指南及其使用流程。[上游指南入口](https://github.com/vernesong/OpenClash/blob/dev/.github/skills/openclash-user-guide/SKILL.md)在 2026-10-03 核验时标注 `license: MIT`。本仓库通过链接引用该指南，不收录指南全文；上游内容的版权归其原作者所有，本仓库的署名不代表对上游内容主张版权。若后续收录或改编上游文字，应保留其适用的许可及版权声明。
