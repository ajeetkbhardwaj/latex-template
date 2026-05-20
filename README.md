# Automated LaTeX Research Docs Writing Environment

A professional-grade, containerized LaTeX environment for writing academic papers (arXiv style) with **automated dependency management**, **modular architecture**, and **zero setup friction** for collaborators.

> **Write-Once, Compile-Anywhere** — No more "it works on my machine" problems with LaTeX distributions.

***

## ✨ Key Features

| Feature | Benefit |
|---------|---------|
| 🐳 **Docker Isolation** | Full TeX Live 2026 engine inside container — no local LaTeX installation needed |
| 💻 **VS Code Dev Containers** | Seamless editor experience inside Docker (no terminal hell) |
| 📑 **Modular Architecture** | Write sections separately; avoid merge conflicts with co-authors |
| 📦 **Auto Package Management** | Missing packages? Add to `tex-packages.txt` and rebuild — automatic installation |
| 🧹 **Clean Project Directory** | Auxiliary files (`.aux`, `.log`) auto-moved to hidden `.tmp/` folder |
| 📚 **arXiv Style** | Professional formatting ready for preprint submission |
| 🔄 **Git-Ready** | Version control optimized for text-based collaboration |

***

## 🏗️ System Architecture

This environment solves the problem of massive, conflicting local LaTeX installations by isolating the entire **TeX Live engine** inside a Docker container.

| Component | Role |
|-----------|------|
| **Docker** | Lightweight, consistent LaTeX engine (TeX Live 2026) |
| **VS Code Dev Containers** | Connects your local editor into the running Docker container seamlessly |
| **LaTeX Workshop Extension** | Handles manual compilation and PDF syncing |
| **Git/GitHub** | Version control for text and collaboration with co-authors |
| **`tlmgr`** | Automates installation of missing LaTeX packages via `tex-packages.txt` |

***

## 📁 Project Structure

The project uses a **Modular Architecture**. Never write your actual paper content inside `main.tex` — use the `sections/` folder to prevent merge conflicts.

```
research-paper/
├── .devcontainer/
│   └── devcontainer.json   # Docker & VS Code configuration
├── bib/
│   └── references.bib      # Bibliography (BibTeX format)
├── figures/                # Place all images/charts here
├── sections/               # Modular .tex files for your paper
│   ├── 00-abstract.tex
│   ├── 01-introduction.tex
│   ├── 02-methodology.tex
│   ├── 03-results.tex
│   ├── 04-discussion.tex
│   └── 05-conclusion.tex
├── tex-packages.txt        # List of required LaTeX packages
├── main.tex                # Root file (configuration & layout only)
├── arxiv.sty               # Custom arXiv-style formatting
├── .gitignore              # Prevents junk files from entering GitHub
└── README.md
```

***

## 🛠️ Local Setup Guide

### 1. Prerequisites

Before starting, ensure you have the following installed on your machine:

| Requirement | Download Link |
|-------------|---------------|
| **Docker Desktop** | [Download](https://www.docker.com/products/docker-desktop/) (Must be running in background) |
| **VS Code** | [Download](https://code.visualstudio.com/) |
| **Remote - Containers Extension** | Install inside VS Code (search "Dev Containers") |

***

### 2. Initialization
**Fork with your title**
First Visit the our repos : [https://](https://github.com/ajeetkbhardwaj/latex-template/) and click onto the up right side to fork the repository.

**Clone the Repository:**
```bash
git clone https://github.com/your-username/latex-template.git
cd latex-template
```

**Open in VS Code:**
```bash
code .
```

**Enter the Container:**
1. A notification will appear: *"Folder contains a Dev Container configuration file"*
2. Click **"Reopen in Container"**
3. VS Code will pull the `qmcgaw/latexdevcontainer` image and configure your environment (first time: ~2 minutes)

**Verify Setup:**
- VS Code terminal should show `(latex)` prefix
- Open `main.tex` — LaTeX Workshop extension should be active
- Press `Ctrl+Alt+B` (or `Cmd+Opt+B` on Mac) — PDF should compile

***

## ✍️ Writing & Compiling Workflow

### How to Write

| Task | File to Edit |
|------|--------------|
| **Abstract** | `sections/00-abstract.tex` |
| **Introduction** | `sections/01-introduction.tex` |
| **Methodology** | `sections/02-methodology.tex` |
| **Results** | `sections/03-results.tex` |
| **Discussion** | `sections/04-discussion.tex` |
| **Conclusion** | `sections/05-conclusion.tex` |
| **Bibliography** | `bib/references.bib` |
| **Images/Charts** | `figures/` folder |
| **Title/Authors/Metadata** | `main.tex` (only for metadata, not content) |

***

### Manual Compilation

To keep your computer fast, this environment uses **Manual Compilation** (not auto-compile on every keystroke).

| Action | Mac Shortcut | Windows/Linux Shortcut |
|--------|--------------|------------------------|
| **Compile PDF** | `Cmd + Opt + B` | `Ctrl + Alt + B` |
| **View PDF** | `Cmd + Opt + V` | `Ctrl + Alt + V` |

> 💡 **Note:** All messy auxiliary files (`.aux`, `.log`, `.out`) are automatically moved to a hidden `.tmp/` folder to keep your project clean. The final PDF is copied back to your main folder.

***

## 📦 Dependency Management

If you need a new LaTeX package (e.g., `tikz`, `cleveref`, `algorithm2e`):

1. **Add the package name to `tex-packages.txt`:**
   ```text
   tikz
   cleveref
   algorithm2e
   ```

2. **Rebuild the container:**
   - Press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows/Linux)
   - Type: **"Dev Containers: Rebuild Container"**
   - Press Enter

3. **The environment will automatically use `tlmgr` to install the package** for the whole team.

***

## 🔄 Collaborating with Co-Authors

### Standard Workflow

**At the end of each writing session:**

```bash
# 1. Stage your changes
git add .

# 2. Commit with a clear message
git commit -m "Drafted the Methodology section"

# 3. Push to GitHub
git push origin main
```

**Co-authors pull latest changes:**
```bash
git pull origin main
```

### Handling Merge Conflicts

Since each section is in a separate `.tex` file, merge conflicts are **rare**. If they occur:

1. Open the conflicted file in VS Code
2. Use VS Code's built-in merge tool (shows `<<<<<<<`, `=======`, `>>>>>>>`)
3. Choose which changes to keep
4. `git add <file>` and `git commit`

***

## 🔧 Advanced Tips

### 1. Adding New Sections

**Create a new section file:**
```bash
# In sections/ folder
touch sections/06-future-work.tex
```

**Add to `main.tex`:**
```latex
\input{sections/06-future-work}
```

***

### 2. Adding Figures

**Place image in `figures/`:**
```
figures/
├── architecture-diagram.png
├── results-plot.pdf
└── table-comparison.svg
```

**Reference in LaTeX:**
```latex
\begin{figure}[h]
  \centering
  \includegraphics[width=0.8\textwidth]{figures/architecture-diagram.png}
  \caption{System architecture diagram}
  \label{fig:architecture}
\end{figure}
```

***

### 3. Customizing arXiv Style

**Modify `arxiv.sty` for custom formatting:**
```latex
% Example: Add custom command
\newcommand{\rael}[1]{\textcolor{blue}{#1}}
```

**Use in sections:**
```latex
This is a highlighted result \rael{very important}.
```

***

### 4. Offline Mode

If you're working without internet:

1. Container already has **all TeX Live packages** installed
2. You can still write and compile offline
3. `tlmgr` won't work offline (package installation requires internet)
4. Push changes when you're back online

***

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| **Container not starting** | Check Docker Desktop is running; restart VS Code |
| **"TeX Live not found"** | Rebuild container: `Cmd+Shift+P` → "Rebuild Container" |
| **Missing package error** | Add package to `tex-packages.txt` and rebuild |
| **PDF not updating** | Manually compile: `Ctrl+Alt+B` |
| **VS Code extensions not loading** | Rebuild container or reinstall "Remote - Containers" extension |
| **File permission errors** | Add your user to Docker group (Linux): `sudo usermod -aG docker $USER` |

***

## 📚 Resources

### Official Documentation
- [TeX Live Documentation](https://www.tug.org/texlive/doc.html)
- [LaTeX Project](https://www.latex-project.org/help/)
- [arXiv Submission Guide](https://arxiv.org/help/submit)

### VS Code Extensions
- [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
- [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

### Learning LaTeX
- [Overleaf Learn LaTeX](https://www.overleaf.com/learn/latex/Learn_LaTeX)
- [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX)

***

## 🎯 When to Use This Template

### ✅ Perfect For:
- PhD thesis chapters
- Research papers (arXiv, IEEE, ACM)
- Collaborative writing with co-authors
- Reproducible research (freeze LaTeX version)
- Teaching writing courses
- Portfolio documentation

### ❌ Skip When:
- Writing a one-page document (use Overleaf instead)
- Need real-time collaboration (use Overleaf's live editor)
- Working on a low-disk machine (<10 GB free)
- Just learning LaTeX (start with Overleaf tutorials)

***

## 📄 License

**MIT License** — See [LICENSE](LICENSE) for details.

You are free to:
- ✅ Use this template for personal or commercial projects
- ✅ Modify the template
- ✅ Distribute copies

***

## 🙏 Acknowledgments

- **TeX Live** for the LaTeX engine
- **VS Code Dev Containers** for seamless Docker integration
- **LaTeX Workshop** extension team
- **arXiv** for the professional formatting style

***

## Support the Project

If you find this `latex-template` valuable:

1. **Hit the ⭐ star button** on GitHub
2. **Cite it in your work:**
   ```bibtex
   @misc{latex-template,
     author = {Ajeet Kumar},
     title = {Automated LaTeX Research Docs Writing Environment},
     year = {2026},
     website = {\url{https://ajeetkbhardwaj.github.io}},
     howpublished = {\url{https://github.com/ajeetkbhardwaj/latex-template}}
   }
   ```
3. **Share with your research group**

***

## 📬 Contact

**Ajeet Kumar**  
📧 ajeetkamla7897@gmail.com  
🔗 [GitHub](https://github.com/ajeetkbhardwaj) | [Website](https://ajeetkbhardwaj.github.io/)

***

> **Isolated, reproducible, professional LaTeX writing — ready to share with the world.**
