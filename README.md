# credit-spread-db 技术架构手册

> 信用利差数据库（credit-spread-db）的解耦架构文档 —— 11 视角 × 5 数据源 × 4 取数引擎，面向集成者与二次开发者。

**作者：叶青** · fioutput Report Design System · Navy

> 📌 本仓库开源**文档**（架构手册 HTML），Skill 源码（SKILL.md / scripts / knowledge_base 等）**不开源**。

---

## 🚀 一句 Prompt 获取 Skill

在 AI Agent 对话框中输入：

```
"安装 credit-spread-db skill"
```

或：

```
"安装信用利差数据库 skill，配置 DM Quant API 凭证"
```

Agent 会自动完成下载、安装、依赖配置。

**Skill Installer API**：

```
GET https://kmrhoavgygtv.sealosbja.site/api/skill-installer
```

**商店直链**：https://kmrhoavgygtv.sealosbja.site

---

## 文档清单

| 文件 | 说明 |
|------|------|
| `architecture.html` | 技术架构手册（自包含 HTML，可直接浏览器打开） |
| `README.md` | 本文件 |
| `LICENSE` | CC BY-NC 4.0 |

---

## 架构概览

```
┌─────────────────────────────────────────────────────┐
│  L4 输出层   chart_credit_spread.py / commentary /  │
│              dashboard_template.html                │
├─────────────────────────────────────────────────────┤
│  L3 计算层   CS/TS/RS/PS 利差引擎 + 分位数 + 评分卡  │
├─────────────────────────────────────────────────────┤
│  L2 知识层   data_contract.yaml / edb_codes /       │
│              thresholds.md / data_snapshot.json     │
├─────────────────────────────────────────────────────┤
│  L1 取数层   dm_fetcher / ifind_fetcher /           │
│              akshare_fetcher / unified_fetcher      │
├─────────────────────────────────────────────────────┤
│  L0 数据源   DM Quant · iFinD HTTP · AKShare ·      │
│              Wind MCP · iFinD MCP                   │
└─────────────────────────────────────────────────────┘
```

每一层可独立使用、可等价替换。取数层全部失效时，知识层离线快照仍可支撑计算与演示。

---

## 集成模式

| 模式 | 涉及层 | 典型场景 |
|------|--------|---------|
| ① 全流程集成 | L0–L4 | 周报组装器 / 信用策略专题 |
| ② 只取数 | L0–L1 | 其他 Skill 需要 YTM / 利差原始数据 |
| ③ 只查知识 | L2 | 人工查阈值 / 查 M码 / 离线回测 |
| ④ 只复用图表 | L4 | 已有数据管线，只缺周报级图表 |

---

## 在线阅读

https://kmrhoavgygtv.sealosbja.site/pages/tutorial-credit-spread-db-architecture/

---

## License

[CC BY-NC 4.0](LICENSE) — 文档开源，Skill 源码不开源。
