# 🚀 Automated LaTeX Research Docs Writing Environment
This latex-template system is designed to provide a "Write-Once, Compile-Anywhere" experience using Docker to eliminate the "it works on my machine" problem with LaTeX distributions.

### *VSCode + Docker + Git + GitHub + TeX Live*

This project provides a professional-grade, containerized environment for writing academic papers (arXiv style) with automated dependency management and a clean directory architecture.

## System Architecture
This environment solves the problem of massive, conflicting local LaTeX installations by isolating the entire TeX Live engine inside a **Docker Container**.

| Component | Role |
| :--- | :--- |
| **Docker** | [cite_start]Provides a lightweight, consistent LaTeX engine (`TeX Live 2026`)[cite: 5, 8]. |
| **VSCode Dev Containers** | Connects your local editor into the running Docker container seamlessly. |
| **LaTeX Workshop** | VSCode extension that handles manual compilation and PDF syncing. |
| **Git/GitHub** | Version control for text and collaboration with co-authors. |
| **tlmgr** | Automates the installation of missing LaTeX packages via `tex-packages.txt`. |

---

## Project Structure
The project uses a **Modular Architecture**. Never write your actual paper content inside `main.tex`; use the `sections/` folder to prevent merge conflicts.

```text
research-paper/
├── .devcontainer/
│   └── devcontainer.json   # Docker & VSCode configuration
├── bib/
│   └── references.bib      # Bibliography (BibTeX format)
├── figures/                # Place all images/charts here
├── sections/               # modular .tex files for your paper
│   ├── 00-abstract.tex
│   ├── 01-introduction.tex
│   └── 02-methodology.tex
├── tex-packages.txt        # List of required LaTeX packages
├── main.tex                # Root file (Configuration & Layout)
└── .gitignore              # Prevents junk files from entering GitHub
```

---

## Local Setup Guide

### 1. Prerequisites
Before starting, ensure you have the following installed on your machine:
* **Docker Desktop:** [Download here](https://www.docker.com/products/docker-desktop/). (Must be running in the background) [cite_start][cite: 8].
* **VSCode:** [Download here](https://code.visualstudio.com/).
* **Remote Development Extension Pack:** Install this inside VSCode.

### 2. Initialization
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/your-research-paper.git
   cd your-research-paper
   ```
2. **Open in VSCode:**
   ```bash
   code .
   ```
3. **Enter the Container:**
   * [cite_start]A notification will appear in the bottom right: *"Folder contains a Dev Container configuration file."*[cite: 8].
   * [cite_start]Click **Reopen in Container**[cite: 8].
   * [cite_start]VSCode will pull the `qmcgaw/latexdevcontainer` image and configure your environment[cite: 8].

---

## Writing & Compiling Workflow

### How to Write
* **Abstract:** Write in `sections/00-abstract.tex`.
* **Main Body:** Open the relevant section in the `sections/` folder.
* **Metadata:** Edit `main.tex` only to change the Title, Authors, or to add new `\input{}` commands.

### Manual Compilation
To keep your computer fast, this environment uses **Manual Compilation**.
* **Compile (Mac):** Press **`Cmd + Opt + B`**.
* **Compile (Windows/Linux):** Press **`Ctrl + Alt + B`**.
* **View PDF:** Press **`Cmd + Opt + V`** to see the live PDF preview.

> **Note:** All "messy" auxiliary files (`.aux`, `.log`, `.out`) are automatically moved to a hidden `.tmp/` folder to keep your project clean. The final PDF is then copied back to your main folder.

---

## Dependency Management
If you need a new LaTeX package (e.g., `tikz` or `cleveref`):
1. Add the package name to `tex-packages.txt`.
2. Rebuild the container (**Cmd+Shift+P** -> `Dev Containers: Rebuild Container`).
3. The environment will automatically use `tlmgr` to install the package for the whole team.

---

## Ending Your Session
Always push your work at the end of the day to ensure your co-authors have the latest version:
1. **Stage:** `git add .`
2. **Commit:** `git commit -m "Drafted the Methodology section"`
3. **Push:** `git push origin main`

---
## Summary
If you find the my project/latex-template valuable please hit a star to the repo and cite into your work.

```citation
ajeet

```
