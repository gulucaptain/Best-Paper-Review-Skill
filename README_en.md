<div align="center">

# <img src="assets/logo-violet.svg" height="44" align="top" alt="logo"> Best-Paper-Review-Skill

**An AI paper-review skill whose every comment can be checked, critiqued, and is immune to the user's preferred verdict**

📌 Page-anchored evidence · 🧩 Parallel novelty search per contribution · 🧑‍⚖️ Independent critic<br>
One skill for both Claude and Codex

[![project page](https://img.shields.io/badge/Project%20Page-online-6D4EE0?logo=googlechrome&logoColor=white)](https://gulucaptain.github.io/Best-Paper-Review-Skill/) ![version](https://img.shields.io/badge/version-v1.5.1-6D4EE0) ![Claude](https://img.shields.io/badge/Claude-Skill-8A63D2) ![Codex](https://img.shields.io/badge/Codex-Skill-10A37F) ![license](https://img.shields.io/badge/license-MIT-lightgrey)

[🌐 Project Page](https://gulucaptain.github.io/Best-Paper-Review-Skill/) · [中文](README.md) · [English](README_en.md) · [Changelog](CHANGELOG.md)

</div>

---

## ✨ What it does

Give it a paper PDF; get a review you can check line by line:

- 📌 **Verifiable evidence**: quotes come only from PDF snapshots, checked by text and page; numbers are recomputed by script
- 🧩 **Parallel novelty search**: one sub-agent per contribution searches and reads prior work; anything after the cutoff does not count
- 🛡️ **Counter-evidence & independent critic**: each criticism first states the authors' best defence, false issues are withdrawn, then a fresh critic re-checks every comment
- 🎯 **Scored by core claims**: the score follows whether the core claims hold, not how many issues were found
- ⚖️ **Neutral & tamper-evident**: user stances are recorded, never obeyed; rule files are fingerprinted

Delivers a Chinese review, a PDF reader with comments on the original sentences, and an English submission draft.

### Why not just ask an LLM?

| Aspect | Plain LLM review | This skill |
|---|---|---|
| Quotes | paraphrased or invented | only from PDF snapshots; text and page verified |
| Novelty | one search, "similar work exists" | parallel search per contribution; both texts read |
| Prior-work dates | unchecked | arXiv history / Crossref; post-cutoff work excluded |
| False positives | "no variance reported", "unfair params"… | search paper + appendix for the authors' answer first |
| Coverage | ad hoc | nine dimensions, each with a verdict |
| User pressure | drifts toward the user's wish | recorded only; symmetry check; no score change without evidence |
| Output | a block of text | Chinese review + venue form + PDF reader + English submission page |

The host model makes the scientific judgements; scripts handle extraction, retrieval, provenance and deterministic checks. **Passing validation means the record is consistent and the quotes exist, not that the conclusions are correct.**

---

## 🚀 Usage

**📄 PDF** → 🧭 understand & split contributions → 🔎 parallel novelty search → ✅ nine-dimension check → 🛡️ counter-evidence & grading → 🧑‍⚖️ independent critique → ⚖️ verdict & symmetry check → 📦 reader + English draft

> Use best-paper-review to review `paper.pdf`

| Mode | When | Output |
|---|---|---|
| `quick` | a 30-minute sanity check | `review.md` |
| `full` (default) | what would reviewers say? | English submission page + PDF reader + source data |
| `self` | authors before submission | same, plus rejection-risk ranking and fix plan |
| `rebuttal` | reviews + author response exist | resolved / partly / unresolved per point |
| `revise` | revising after reviews | issue board, fix verification, response letter |

Review text is written in Simplified Chinese by default; the English submission draft is generated separately.

---

## 📦 Install

```bash
git clone https://github.com/gulucaptain/Best-Paper-Review-Skill.git
cd Best-Paper-Review-Skill
./install.sh claude     # Claude Code → ~/.claude/skills/
./install.sh codex      # Codex       → ~/.agents/skills/
./install.sh all        # both; add --project to install into the current project
```

Claude.ai / Cowork: zip the `best-paper-review` folder and upload it on the Skills page. Codex: invoke with `$best-paper-review`.

Requirements: Python 3.9+ (standard library only); `pdftotext` (poppler, falls back to `pypdf`). PDF.js and KaTeX are bundled. Browser tests need Node.js + Playwright.

```bash
cd skills/best-paper-review
python3 scripts/package_viewer.py examples/demo/paper.pdf examples/demo/review.json /tmp/demo-viewer.html
python3 scripts/serve.py --demo                 # editable annotator at http://127.0.0.1:8768
python3 -B -m unittest discover -s tests -v     # 78 offline unit tests
```

---

## 🔏 Official rule fingerprints

Compare with `provenance.rules_sha256` in any `review.json` (`python3 scripts/integrity.py fingerprint`):

| Version | Fingerprint |
|---|---|
| v1.2.0 | `cb39682d14a0c33dbf841303fd0cda07c6bf1601da8725c1d26b0436b0b1ddbd` |
| v1.3.0 | `e7eb73011829dddc10a889b1549b9fde1ac5853e6d4f78364062b550ad73a848` |
| v1.4.0 | `3142cfa93dfc012eb8626e8ca705f73f44b632048c193e6cef779112e8b57217` |
| v1.5.0 | `02e56ae42041e2fb5d3752f3b86ac0d3ce1dda796a4203679bcce14b8065a4e5` |
| v1.5.1 | `a4465b789e4e8c9fe16abbffed2b93144422283d5dec31a8ea50748c7aaead5b` |

---

## ⚠️ Responsible use

- **Official reviewers: check your venue's LLM policy first.** Many venues restrict LLM use and forbid sending unpublished submissions to external services. Where prohibited, the skill only offers comprehension help and will not draft review text (`references/ethics.md`).
- With a conflict of interest, disclose or recuse; the skill will not produce a submittable review in that case.
- You remain responsible for every conclusion.

## 📄 License

Code and docs: [MIT](LICENSE). PDF.js (Apache-2.0), pdf-lib (MIT) and KaTeX (MIT) keep their licences. The repo **contains no third-party paper PDFs or full texts**: `examples/demo/` is a synthetic paper.

## 🏆 The Best-Paper series

| | Project | Purpose |
|---|---|---|
| ✍️ | [Best-Paper-Writing-Skill](https://github.com/gulucaptain/Best-Paper-Writing-Skill) | Write: best-paper-style drafts |
| 🔍 | **Best-Paper-Review-Skill** (this repo) | Review: verifiable, cross-checked reviews |

## 🤝 Contributing

Issues on false positives/negatives, venue forms and scales, or usage reports are welcome (never upload unpublished manuscripts). If it helps you, a ⭐ is appreciated.
