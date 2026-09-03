# Setup Guide

For Git workflow (branching, committing, merge requests), see [working_with_git.md](working_with_git.md).

## Prerequisites

Install the following tools before getting started:

1. **R** - Download and install from [https://cran.r-project.org](https://cran.r-project.org)
2. **Quarto** - Download and install from [https://quarto.org/docs/get-started/](https://quarto.org/docs/get-started/)
3. **VS Code** - Download and install from [https://code.visualstudio.com](https://code.visualstudio.com)

## VS Code Extensions

Install the following extensions from the VS Code Extensions marketplace:

- **R** (`REditorSupport.r`) - R language support
- **R Syntax** (`REditorSupport.r-syntax`) - Enhanced R syntax highlighting
- **Quarto** (`quarto.quarto`) - Quarto document support


## Getting Started

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd <repository_path_on_local_machine>
   ```

2. **Open in VS Code**
   ```bash
   code .
   ```

3. **Install required R packages**

   Open a terminal and launch R, then run:
   ```r
   install.packages(c(
     "tidyverse", "patchwork", "corrplot", "GGally",
     "tidymodels", "ranger", "xgboost", "vip", "DALEXtra", "themis", "doParallel",
     "rpart", "rpart.plot", "ggrepel"
   ))
   ```

4. **Run notebook files**

   Open any `.qmd` file in VS Code and use the Quarto extension to run or preview it, or render from the terminal:
   ```bash
   quarto render filename.qmd
   ```
