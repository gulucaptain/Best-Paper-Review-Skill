<div align="center">

# <img src="assets/logo-violet.svg" height="44" align="top" alt="logo"> Best-Paper-Review-Skill

**可校验、可复核、不被预设结论左右的 AI 论文审稿 Skill**

📌 每条意见都有原文页码证据 · 🧩 逐条贡献并行查新 · 🧑‍⚖️ 独立子代理复核<br>
一个 Skill，同时支持 Claude 与 Codex

[![project page](https://img.shields.io/badge/Project%20Page-online-6D4EE0?logo=googlechrome&logoColor=white)](https://gulucaptain.github.io/Best-Paper-Review-Skill/) ![version](https://img.shields.io/badge/version-v1.5.1-6D4EE0) ![Claude](https://img.shields.io/badge/Claude-Skill-8A63D2) ![Codex](https://img.shields.io/badge/Codex-Skill-10A37F) ![license](https://img.shields.io/badge/license-MIT-lightgrey)

[🌐 项目主页](https://gulucaptain.github.io/Best-Paper-Review-Skill/) · [中文](README.md) · [English](README_en.md) · [更新日志](CHANGELOG.md)

</div>

---

## ✨ 它能做什么

给它一篇论文 PDF，得到一份能逐条核对的审稿：

- 📌 **证据可校验**：引文只来自 PDF 快照，脚本核对原句与页码，数字由脚本复算
- 🧩 **逐贡献并行查新**：每个贡献派一个子代理检索、读前作，截止日期之后的不算
- 🛡️ **反证与独立复核**：每条批评先替作者辩护，伪问题主动撤销；独立子代理再逐条复核
- 🎯 **按核心主张出分**：分数由核心主张是否成立决定，不按问题数量扣分
- ⚖️ **中立、防篡改**：使用者表态只记录、不执行；规则文件有指纹，改动可被发现

交付一份中文审稿、PDF 阅读器（意见高亮在原句上）与英文提交稿。

### 为什么不直接让 AI 审？

通用 AI 审稿的常见问题：编造引文和页码、把附录里已有的实验说成“缺失”、拿截止日之后的工作批评创新性、使用者一表态就跟着改分。

| 方面 | 直接让 AI 审 | 本 Skill |
|---|---|---|
| 引文 | 可能凭记忆改写或编造 | 只能来自 PDF 快照，脚本校验原文与页码 |
| 创新性 | 一次检索，凭印象说“已有类似工作” | 每个贡献并行检索，读过双方原文才能确认“不够新” |
| 前作日期 | 不核对 | 按 arXiv 版本历史 / Crossref 核对，截止日之后的工作不算 |
| 伪问题 | “未报告方差”“参数量不公平”…… | 先全文与附录搜索作者是否已回应，再定级 |
| 覆盖面 | 想到哪写到哪 | 九个维度逐项给结论 |
| 使用者施压 | 容易顺着改分 | 表态只记录；对称自检；没有新证据不改分 |
| 交付 | 一段文字 | 中文审稿 + 会议表单 + PDF 阅读器 + 英文提交稿页面 |

科学判断由加载 Skill 的模型完成；脚本负责抽取、检索、溯源和确定性检查。**脚本校验通过只说明记录自洽、引文真实存在，不说明结论正确。**

---

## 🚀 使用方式

**📄 论文 PDF**　→　🧭 理解与拆贡献　→　🔎 并行查新　→　✅ 九维度检查　→　🛡️ 反证定级　→　🧑‍⚖️ 独立复核　→　⚖️ 总评与对称自检　→　📦 阅读器 + 英文提交稿

装好后，直接对 agent 说：

> 用 best-paper-review 审这篇论文：`paper.pdf`

| 模式 | 适用 | 交付 |
|---|---|---|
| `quick` 快速预审 | 半小时内判断大方向 | `review.md` |
| `full` 完整审稿（默认） | 想看审稿人会怎么说 | 英文提交稿页面 + PDF 阅读器 + 源数据 |
| `self` 投稿前自查 | 作者本人，想知道怎么改 | 同上，另附被拒风险排序与修改方案 |
| `rebuttal` 答辩评估 | 已有评审与作者回复 | 逐条 已解决 / 部分解决 / 未解决 |
| `revise` 修改闭环 | 收到审稿意见后修改论文 | 问题看板、修改核验、回复信 |

### 📦 输出目录

```
reviews/20261101_Paper_Title/
├── comments_submission.html   # 英文提交稿：详略切换、可编辑、复制为 Markdown
├── review-viewer.html         # PDF 阅读器：意见高亮在原句上、论文速览
├── source/                    # review.json · review.md · form.md · submission_en.json
└── review_process_files/      # 前作快照、创新性比较、复核记录
```

---

## 📦 安装

```bash
git clone https://github.com/gulucaptain/Best-Paper-Review-Skill.git
cd Best-Paper-Review-Skill

./install.sh claude     # Claude Code → ~/.claude/skills/
./install.sh codex      # Codex       → ~/.agents/skills/
./install.sh all        # 两个都装；加 --project 则装到当前项目目录
```

| 平台 | 方式 |
|---|---|
| 🟣 **Claude Code** | `./install.sh claude`，或手动复制 `skills/best-paper-review/` 到 `~/.claude/skills/` |
| 🟣 **Claude.ai / Cowork** | 把 `best-paper-review` 文件夹打成 zip，在 Skills 页面上传 |
| 🟢 **Codex** | `./install.sh codex`，或手动复制到 `~/.agents/skills/`；用 `$best-paper-review` 显式调用 |

依赖：Python 3.9+（只用标准库）；`pdftotext`（poppler，没有时自动改用 `pypdf`）。阅读器所需的 PDF.js、KaTeX 已内置，离线可用。浏览器回归测试需要 Node.js + Playwright。

试一下合成示例：

```bash
cd skills/best-paper-review
python3 scripts/package_viewer.py examples/demo/paper.pdf examples/demo/review.json /tmp/demo-viewer.html
python3 scripts/serve.py --demo                 # 可编辑的批注查看器 http://127.0.0.1:8768
python3 -B -m unittest discover -s tests -v     # 78 个离线单元测试
```

---

## 🗂️ 目录结构

```
Best-Paper-Review-Skill/
├── README.md / README_en.md / CHANGELOG.md / LICENSE
├── assets/logo-violet.svg
├── install.sh                 # 一键安装
└── skills/best-paper-review/
    ├── SKILL.md               # 入口：不可协商的规则、五种模式、十一步流程
    ├── references/            # 必查清单、论文类型、创新性与多代理协议、反证、标定与写作、
    │                          # 中立性、伦理、复核、修改闭环、英文提交稿、会议、schema、阅读器
    ├── scripts/               # init_review · extract_pdf · find_quote · sources · fetch_arxiv · verify_dates
    │                          # novelty · evidence · critique · neutrality · integrity · stance_eval
    │                          # render · revision · submission · finalize · package_viewer · serve
    ├── assets/                # venues.json（CCF-A 95 个会议/期刊 + 表单）· integrity.json · templates/ · vendor/katex
    ├── examples/
    │   └── demo/              # 合成论文（测试用）：植入 6 个缺陷与 5 个“伪问题”
    └── tests/                 # 单元测试、浏览器测试、合成论文评测
```

---

## 🔏 官方规则指纹

开源意味着任何人都能修改规则；`integrity.py` 让修改可被发现。每份 `review.json` 的 `provenance.rules_sha256` 记录生成时的规则指纹，与下表对照即可判断是否在未修改的规则下生成：

| 版本 | 规则指纹（`python3 scripts/integrity.py fingerprint`） |
|---|---|
| v1.2.0 | `cb39682d14a0c33dbf841303fd0cda07c6bf1601da8725c1d26b0436b0b1ddbd` |
| v1.3.0 | `e7eb73011829dddc10a889b1549b9fde1ac5853e6d4f78364062b550ad73a848` |
| v1.4.0 | `3142cfa93dfc012eb8626e8ca705f73f44b632048c193e6cef779112e8b57217` |
| v1.5.0 | `02e56ae42041e2fb5d3752f3b86ac0d3ce1dda796a4203679bcce14b8065a4e5` |
| v1.5.1 | `a4465b789e4e8c9fe16abbffed2b93144422283d5dec31a8ea50748c7aaead5b` |

---

## ⚠️ 负责任地使用

- **正式审稿人请先查会议政策。** 多数会议限制在审稿中使用 LLM，未公开稿件不得发给外部服务。会议禁止时，本 Skill 只提供理解辅助，不代写意见（见 `references/ethics.md`）。
- 有利益冲突（如竞争对手的论文）时，请声明或回避；Skill 不会为此生成可提交的意见与评分。
- 审稿结论需要你亲自核对。它是助手，不是审稿人。

## 🚧 已知局限

- 扫描版 PDF 需先 OCR；跨栏长引文的区域框可能偏大。
- 除 ICML 2026 外，会议表单为近年常见形式，使用前请核对当年审稿指南。
- Semantic Scholar / OpenAlex 无 API Key 时容易限流，可设置 `SEMANTIC_SCHOLAR_API_KEY`、`OPENALEX_API_KEY`。
- 审稿内容默认用简体中文撰写，英文提交稿另行生成。

## 📄 版权与许可

- 代码与文档采用 [MIT](LICENSE)。PDF.js（Apache-2.0）、pdf-lib（MIT）、KaTeX（MIT）保留各自许可。
- 本仓库**不含第三方论文的 PDF 或全文**：`examples/demo/` 中是自行生成的合成论文。
- 

## 🔗 姊妹项目

- [Best-Paper-Writing-Skill](https://github.com/gulucaptain/Best-Paper-Writing-Skill)：从 60 篇获奖论文提炼写作规律，生成论文底稿。写完用它，审稿用本项目。

## 🤝 参与

欢迎通过 Issue 反馈误报与漏报、补充会议表单与量表、或分享你的使用记录（请勿上传未公开稿件）。如果它对你有帮助，欢迎点一个 ⭐ Star。
