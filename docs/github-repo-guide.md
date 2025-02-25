# GitHub Repository Guidelines

In order to facilitate rapid collaboration across many different projects, we have adapted guidelines for our analysis projects, including the repository structure, docker image principles, a pull request model, and code review. 

## Repository guidelines (see [OpenPedCan documentation](https://github.com/rokitalab/OpenPedCan-Project-CNH/#how-to-add-an-analysis))

**Repository Docker Image**

- We set up all of our repositories to use project-specific Docker images containing an instance of RStudio and tidyverse (R > 4.4) from the [Rocker project](https://rocker-project.org/).
    - `rocker/tidyverse` has already installed many R packages and their dependencies’ apt packages. e.g. [the `tidyverse` package](https://www.tidyverse.org/), [the `devtools` package](https://devtools.r-lib.org/), [the `rmarkdown` package](https://rmarkdown.rstudio.com/), some [R Database Interface](https://dbi.r-dbi.org/) packages, [the `data.table` package](https://rdatatable.gitlab.io/data.table/), [the `fst` package](https://www.fstpackage.org/), and [the Apache Arrow R package](https://arrow.apache.org/docs/r/).
- More on docker [here](https://www.notion.so/Docker-b5eb9d8caea84748b8babba71fe8fc65?pvs=21).

**Repository folder structure**

- Users performing analyses should **always** refer to the symlinks in the `data/` directory and not files within the release folder, as an updated release may be produced before a publication is prepared.
- The repository folder structure is designed to separate each analysis into its own set of notebooks that are independent of other analyses. Within the `analyses` directory, create a folder for your analysis. Choose a name that is unique from other analyses and somewhat detailed. For example, instead of `gene-expression`, choose `gene-expression-clustering` if you are clustering samples by their gene expression values. You should assume that any data files are in the `../../data` directory and that their file names match what the `download-data.sh` script produces. These files should be read in at their relative path, so that we can re-run analyses if the underlying data change. Files that are primarily graphic should be placed in a `plots` subdirectory and should adhere to a [color palette guide](https://github.com/d3b-center/OpenPedCan-analysis/blob/dev/figures/README.md#color-palette-usage) for your project. Files that are primarily tabular results files should be placed in a `results` subdirectory. Intermediate files that are useful within the processing steps but that do not represent final results should be placed in `../../scratch/`. It is safe to assume that files placed in `../../scratch` will be available to all analyses within the same folder. It is not safe to assume that files placed in `../../scratch` will be available from analyses in a different folder.
- An example highlighting a `new-analysis` directory is shown below. The directory is placed alongside existing analyses within the `analyses` directory. In this case, the author of the analysis has run their workflows in R Markdown notebooks. This is denoted with the `.Rmd` suffix. However, the author could have used Jupyter notebooks, R scripts, or another scriptable solution. The author has created a new function or set of functions and placed those into `new-function.R` which lives in the `util` folder of the `new-analysis` folder. The author has produced their output figures as `.pdf` files. We have a preference for vector graphics as PDF files, though other forms of vector graphics are also appropriate. The results folder contains a tabular summary as a comma separated values file. We expect that the file suffix (`.csv`, `.tsv`) accurately denotes the format of the added files.
- The author has also included a `README.md` ([see Documenting Your Analysis](https://github.com/d3b-center/OpenPedCan-analysis#documenting-your-analysis)).

```bash
OpenPedCan-analysis
├── README.md
├── analyses
│  ├── existing-analysis-1
│  └── new-analysis
│      ├── 01-preprocess-data.Rmd
│      ├── 02-run-analyses.Rmd
│      ├── 03-make-figures.Rmd
│      ├── README.md
│      ├── plots
│      │  ├── figure1.pdf
│      │  └── figure2.pdf
│      ├── util
│      │   └── new-function.R
│      ├── results
│      │   └── tabular_summary.csv
│      └── run-new-analysis.sh
├── data
├── download-data.sh
├── figures
└── scratch
```