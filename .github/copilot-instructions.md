# GitHub Copilot Instructions for Psychology Research Methods Course Notes

## Repository Overview

This repository contains course notes for PSY 310: Research Methods for Psychology Minors at Wake Forest University. The course materials are built using R's [bookdown](https://bookdown.org/) package to create an interactive online textbook.

**Repository Structure:**
- Course content is written in R Markdown (`.Rmd`) and placeholder files (`.Xmd`)
- Files are numbered sequentially (e.g., `0000_front.Rmd`, `0401_univariate.Rmd`)
- The book is rendered to the `docs/` directory for GitHub Pages hosting
- Source code and data files are stored in `code/` and `data/` directories

## File Naming Conventions

Files follow a strict naming pattern:
- **Format**: `XXYY_description.Rmd` or `XXYY_description.Xmd`
- **XX**: Module number (00-15 typically, but can go up to 99)
- **YY**: Section within module (00-02 typically, but can go higher)
- **Extension**: 
  - `.Rmd` for completed R Markdown files with content
  - `.Xmd` for placeholder/template files that need content
- Numbers use zero-padding (e.g., `01` not `1`)

**Example**: `0401_univariate.Rmd` = Module 04, Section 01, topic is univariate statistics

## R and Bookdown Best Practices

### R Markdown Structure

Each content file should:
1. Start with a module header: `# (PART) Module XX {-}`
2. Include a setup chunk that sources `code/common.R`
3. Load required libraries in the setup chunk
4. Include a links child document with: `` ```{r links, child="admin/md/links.md"} ``` ``
5. Use meaningful section headers (`#`, `##`, `###`)

**Standard setup chunk pattern:**
```r
```{r include = FALSE}
source("code/common.R")

# install.packages("devtools")

if (!require("tweetrmd"))  devtools::install_github("gadenbuie/tweetrmd")
library(tweetrmd) #... embedding tweets
class_urls <- read.csv("./data/class_urls.csv")
```

```{r links, child="admin/md/links.md"}
```
```

### Code Style

- Follow the [tidyverse style guide](https://style.tidyverse.org)
- Use tidyverse packages for data manipulation and visualization
- Prefer `library()` calls in setup chunks rather than `package::function()` for commonly used functions
- Use meaningful variable names that reflect statistical concepts
- Comment complex statistical calculations

### Dependencies

The project uses packages listed in `DESCRIPTION`. Core packages include:
- `bookdown` - for building the book
- `tidyverse` - for data manipulation and visualization
- `knitr`, `rmarkdown` - for document generation
- `DT` - for interactive tables
- `gt` - for formatted tables (installed from GitHub via Remotes)

**Note**: Some packages like `vembedr` (for embedding videos) and `tweetrmd` (for embedding tweets) are loaded with `library()` calls in files but not listed in DESCRIPTION. For GitHub-sourced packages, use the conditional install pattern: `if (!require("pkg")) devtools::install_github("source/pkg")`.

**Do not add new dependencies** without strong justification. Use existing packages when possible.

## Content Guidelines

### Educational Content

- Write for undergraduate psychology students with varying statistical backgrounds
- Include learning goals at the start of each module
- Provide clear explanations before introducing R code
- Use real-world psychology examples
- Include both conceptual explanations and practical R demonstrations

### Mathematical Notation

- Use LaTeX for mathematical formulas (inline: `$x$`, display: `$$x$$`)
- Define variables and symbols clearly
- Show both formulas and R implementations

### Code Examples

- Include reproducible examples with sample data
- Show both input and expected output
- Comment code to explain what it does, not just how
- Use the tidyverse approach for data manipulation when appropriate

## Attribution and Licensing

This work is licensed under [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

**When incorporating content:**
- Properly attribute all external sources
- Maintain existing attribution comments
- Major attributions go in `0000_front.Rmd`
- Use the existing citation style from `book.bib`

## Building and Testing

### Building the Book

```r
# In R console or RStudio
bookdown::render_book("index.Rmd")
```

This generates HTML output in the `docs/` directory.

### Development Workflow

1. Make changes to `.Rmd` files
2. Build the book to test changes
3. Check that links, images, and code chunks work correctly
4. Verify mathematical notation renders properly
5. Review the generated HTML in `docs/`

## Common Patterns

### Creating a New Module

1. Copy a template `.Xmd` file or an existing `.Rmd`
2. Follow the numbering convention (XXYY)
3. Update the module header
4. Include standard setup chunks
5. Add learning goals
6. Develop content with theory, examples, and R code

### Embedding Resources

- **Videos**: Use `vembedr::embed_url()` with YouTube URLs
- **Interactive tables**: Use `DT::datatable()`
- **Formatted tables**: Use `gt::gt()`
- **External links**: Define in `admin/md/links.md` for consistency

## Things to Avoid

- ❌ Do not modify the build configuration (`_bookdown.yml`, `_output.yml`) without discussion
- ❌ Do not remove or modify working R Markdown files without clear justification
- ❌ Do not add binary files or large datasets directly to the repository
- ❌ Do not change the file numbering scheme
- ❌ Do not introduce dependencies on non-CRAN packages without justification
- ❌ Do not remove existing attributions or license information

## Getting Help

- Check existing modules for patterns and examples
- Refer to [bookdown documentation](https://bookdown.org/yihui/bookdown/)
- Follow tidyverse style guides for R code
- File issues for questions or suggestions
