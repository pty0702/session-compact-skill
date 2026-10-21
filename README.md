# session-compact skill

会话信息沉淀（compact）技能：把当前对话窗口的全部有效信息提炼为项目根目录的 `COMPACT.md`，让下一个大模型**不回看原对话**即可快速接手。

完整规范见 [`SKILL.md`](./SKILL.md)，文档骨架见 [`templates/COMPACT.md`](./templates/COMPACT.md)。

## 核心特点

- **纯客观**：只保留可验证的技术发现——文件路径（含行号）、命令原文、报错原文、实测结论、信息出处；主观判断、计划建议、安全声明一律不写。文档本质是会话压缩**数据**，不是给模型的行为指令。
- **实体强制**：每条发现必须带可定位的证据（路径/行号/命令/报错/数值/URL），泛泛概括全部禁止。
- **阅读指引内建**：文档第一节就是给接手模型的读法说明与"接手入口"（上次工作中止点的客观描述）。
- **返回接手 Prompt**：执行完成后在对话里直接返回一段可直接粘贴的接手 Prompt（同时存于文档第 7 节），下一个模型贴上即可开工。
- **CLI 无关**：只用文件读写，Claude Code / Codex / ZCode / WorkBuddy / opencode / mimo 均可执行。

## 安装

```bash
git clone https://github.com/pty0702/session-compact-skill.git \
  "$HOME/.agents/skills/session-compact"
```

（各 agent 按自己的 skill 目录约定 clone 到对应位置即可。）

## 使用

对 AI 说一句：

```
compact
```

或「压缩会话」「沉淀会话」「会话快照」「给下一个模型留档」。

执行后得到：

1. `<项目根>/COMPACT.md` —— 七节结构的客观信息沉淀；
2. 对话里返回的**接手 Prompt** —— 复制给下一个模型，贴上即接手。

## 与 project-handoff skill 的分工

| | session-compact | project-handoff |
|---|---|---|
| 范围 | 当前对话窗口 | 项目全周期 |
| 内容 | 纯客观事实，无计划无建议 | 含下一步计划、Resume Prompt、TODO 联动 |
| 联动 | 无（只写一个文件） | README、git push、TODO.md |
| 更新方式 | 每次整体覆盖（最新快照） | 活文档增量更新 |

## License

MIT
