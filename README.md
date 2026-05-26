# NumPDE Study Vault (Obsidian)

Structured study notes for **401-0674-00L Numerical Methods for Partial Differential Equations** (ETH Zurich). The vault is organized by week, with linked concept cards, homework problem maps, LehrFEM++ code patterns, and formula sheets.

**Start here:** open this folder as an Obsidian vault, then open the home note [`NumPDE — Numerical Methods for Partial Differential Equations.md`](NumPDE%20—%20Numerical%20Methods%20for%20Partial%20Differential%20Equations.md) (master index with links to all weeks).

---

## What is inside

| Folder | Contents |
|--------|----------|
| `weeks/` | Weekly handouts (Week 1–13): theory gist, recipes, homework, exam links |
| `concepts/` | Short concept cards (definitions, links, exam notes) |
| `problems/` | Homework problems by theme, with code-folder names and solution gists |
| `code/` | LehrFEM++ assembly / solver / mesh patterns (C++ snippets) |
| `formulas/` | Quick formula reference sheets |
| `endterm/` | **Endterm prep** (Ch.9 + Ch.12): handouts, exam compendiums, practice set — start at [[Endterm-Prep-Ch9-Ch12]] |
| `exams/` | **Full-course exam prep**: master bank, midterm/finals compendiums, theme deep dives — start at [[Exam-Prep-Index]] |

Wikilinks like `[[Week-03-FEM-I]]` connect notes inside Obsidian. For exams: open [[Exam-Prep-Index]] (full course) or [[Endterm-Prep-Ch9-Ch12]] (endterm scope).

---

## Get the vault

### Option A — GitHub (recommended)

```bash
git clone https://github.com/ansh-jainx/NumPDE-Study-Vault.git
cd NumPDE-Study-Vault
```

> **Access:** this repository is **private**. Your instructor must add your GitHub username under **Settings → Collaborators** (or via a GitHub team) before `git clone` works.

Then open that folder in Obsidian (see below).

To update later:

```bash
git pull
```

### Option B — Download ZIP (no Git)

1. On GitHub: **Code → Download ZIP**
2. Unzip anywhere (e.g. `~/Documents/NumPDE-Vault`)
3. Open the unzipped folder in Obsidian

Pin the release tag your instructor gives you (e.g. `v2026.1`) so everyone uses the same version.

---

## Install Obsidian

1. Download **Obsidian** from [https://obsidian.md](https://obsidian.md) (macOS, Windows, Linux).
2. Launch Obsidian and choose **Open folder as vault**.
3. Select this repository root (the folder that contains `README.md` and `weeks/`).
4. Optional: enable **Settings → Files & links → Automatically update internal links** if you rename files.

No paid Obsidian account or sync is required. The vault works fully offline.

---

## Suggested workflow

1. Each week: read the matching `weeks/Week-XX-....md` handout.
2. For homework: use the week’s problem list → open the linked `problems/...` card for **code folder** names and gists.
3. Implement code in the official course repo **[NPDERepo](https://gitlab.math.ethz.ch/ralfh/NPDERepo)** (`homeworks/<ProblemName>/mysolution/`).
4. Before coding: skim the relevant `code/LehrFEM-....md` pattern card.
5. Use **Graph view** or **Backlinks** in Obsidian to see how concepts connect across weeks.

---

## Course materials (not in this repo)

This vault is **notes and maps**, not a replacement for official course assets:

| Resource | Where |
|----------|--------|
| Lecture notes | [NUMPDE.pdf](https://www.sam.math.ethz.ch/~grsam/NUMPDEFL/NUMPDE.pdf) |
| Homework statements | [NPDEFL_Problems.pdf](https://www.sam.math.ethz.ch/~grsam/NUMPDEFL/HOMEWORK/NPDEFL_Problems.pdf) |
| C++ homework code | [NPDERepo](https://gitlab.math.ethz.ch/ralfh/NPDERepo) |
| LehrFEM++ API docs | [LehrFEM++ documentation](https://craffael.github.io/lehrfempp/) |

Keep PDFs and cloned `NPDERepo` on your machine; link paths in your own notes if needed.

---

## LehrFEM++ namespaces (edge providers)

Some providers exist in both `lf::fe::` and `lf::uscalfe::` (documented in LehrFEM++). Course **master solutions** in NPDERepo often use `lf::uscalfe::` (e.g. `MassEdgeMatrixProvider`, `ScalarLoadEdgeVectorProvider`). Either namespace can be valid depending on FE space type; follow the pattern in the homework folder you are solving.

---

## Vault layout (quick map)

```
.
├── NumPDE — … .md              # Master index (home note)
├── weeks/                      # Week 01–13 handouts
├── concepts/                   # Concept cards
├── problems/                   # Problem theme files
├── code/                       # LehrFEM++ patterns
├── formulas/                   # Formula cheat sheets
├── endterm/                    # Endterm prep (Ch.9 & Ch.12)
├── exams/                      # Full-course exam prep
└── README.md                   # This file
```

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Wikilinks don't open | Ensure you opened the **vault root** (folder with `README.md` and `weeks/`), not a subfolder |
| Broken link after rename | Use Obsidian’s rename feature so links update, or fix the wikilink target name |
| Code won’t compile | Use **NPDERepo** mastersolution/templates as ground truth; compare with the pattern card for structure |
| Graph is empty | Open a few week notes first; graph fills as you browse linked notes |

---

## Contributing / issues

If you find a broken wikilink or a mismatch with NPDERepo folder names, tell your instructor. Cite **week + problem id** (e.g. Week 8, Problem 10-8).

---

## License and use

For **course study** by enrolled students. Lecture content © course authors. Do not redistribute official PDFs via this repository.
