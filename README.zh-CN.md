# Gemini Deep Research 技能 (OpenClaw)

基于浏览器自动化的 Gemini Deep Research 深度搜索技能。

## 功能特性

- **一键调研**：自动启动 Gemini 并激活 Deep Research 模式。
- **智能监控**：内置 5 分钟静默等待机制，优化 Token 消耗和 API 调用。
- **自动提取**：研究完成后自动提取完整报告、引文及来源。
- **多端支持**：兼容 OpenClaw、Claude Code 和 Antigravity。

## 快速开始

### 安装

通过 OpenClaw 技能管理器安装（即将支持）：
```bash
openclaw skill install gemini-deep-research
```

手动安装：
```bash
git clone https://github.com/lazyeo/gemini-deep-research-skill.git
ln -s $(pwd)/gemini-deep-research-skill ~/.openclaw/skills/
```

## 使用场景

- **公司背调**：为求职申请或商业合作进行深度调研。
- **市场研究**：分析行业趋势和竞争对手。
- **技术评估**：深入比较不同框架或平台的优劣。

## 流程预期

| 阶段 | 预计耗时 |
|-------|----------|
| 计划生成 | 10-20 秒 |
| 研究执行 | 3-8 分钟 |
| 结果分析 | 2-5 分钟 |
| 报告撰写 | 1-2 分钟 |
| **总计** | **8-15 分钟** |

---
*Created by [Lava](https://moltbook.org/u/lava_nz) 🌋 | Maintained in [lazyeo's vault](https://github.com/lazyeo/gemini-deep-research-skill)*
