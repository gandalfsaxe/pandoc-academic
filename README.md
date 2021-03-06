# pandoc-academic

## Introduction

This repository is meant to showcase capabilities of [pandoc](http://pandoc.org/) in an academic setting, in particularly technical writing. scientists engineers. I decided to write my MSc thesis in Markdown, using pandoc + pandoc filters + LaTeX template. This was time consuming to learn and set up, but the advantages are clear:

1. **Simplicity + Power:** GitHub Flavored Markdown (GFM) + extensions gives a source text format that is a lot simpler and nicer to read than LaTeX source code and still provides most of the power.
2. **Format flexibility:** Being markdown, the source text is more flexible since it can be converted into various document formats via pandoc (HTML, docx, latex, pdf)

What you need for this workflow to work:

1. pandoc
2. LaTeX distribution

And a bunch of pandoc filters:

1. `pandoc-citeproc` (for citing references using biblatex)
2. `pandoc-crossref` (for cross-referencing figures, equations and tables, can optionally use cref from `cleverref` latex package)
3. `pandoc-newpage` [OPTIONAL] (a non-essential filter that conveniently converts horizontal lines in markdown into `\cleardoublepage` in latex)
4. `pandoc-minted` [OPTIONAL] (if you wish to use latex package `minted` for source code syntax highlighting)

## Demos

The `demos` folder contains self-containing example documents that each showcase a certain feature one may wish to use in academic writing.

The pandoc commands to run on the various .md files are commented out in the YAML header of the demo documents.

### Other demo resources

pandoc-crossref have good [documentation](https://github.com/lierdakil/pandoc-crossref/blob/master/docs/index.md) and a [demo](https://github.com/lierdakil/pandoc-crossref/blob/master/docs/demo/demo.md) with corresponding [latex](https://github.com/lierdakil/pandoc-crossref/blob/master/docs/demo/output.latex) output and [pdf output](https://github.com/lierdakil/pandoc-crossref/blob/master/docs/demo/output.pdf), and finally an example [makefile](https://github.com/lierdakil/pandoc-crossref/blob/master/docs/demo/Makefile).

## Installation

### macOS

```bash
brew install pandoc
brew install pandoc-citeproc
brew install pandoc-crossref
```

### Windows

pandoc and pandoc-citeproc comes with Anaconda, but pandoc is not always up-to-date. For that you can install it from conda-forge:

`conda install -c conda-forge pandoc`

Then install pandoc-crossref:

1. Download windows-*.zip from [pandoc-crossref releases](https://github.com/lierdakil/pandoc-crossref/releases) (if necessary, newest committed but not released version of pandoc-crossref can be found [here](https://ci.appveyor.com/project/lierdakil/pandoc-crossref/build/artifacts)).
2. Extract and move pandoc-crossref.exe to a folder in PATH.

Or compile pandoc-crossref from source, similar procedure to alternative 2 below.

#### Alternative 1 - MSI installer

Alternatively both pandoc and pandoc-citeproc can be manually installed with the release MSI installer:

1. Download pandoc-*-windows-x86_64.zip from [pandoc releases](https://github.com/jgm/pandoc/releases).
2. Extract and add both pandoc.exe and pandoc-citeproc.exe to PATH.

The application will then be typically found in `C:\Users\[USER]\AppData\Local\Pandoc` and the path automatically added to PATH.

#### Alternative 2 - Compiling source

1. `git clone https://github.com/jgm/pandoc`
2. download / install the [Haskell tool stack](https://docs.haskellstack.org/en/stable/README/).
3. Go to the cloned pandoc repository and run:
    1. `stack update`
    2. `stack build` (can take a while)
    3. `stack install`

The binaries will then typically be put in `C:\Users\[USERS]\AppData\Roaming\local\bin\`

### Additional filters via pip (all platforms)

```bash
pip install pandoc-latex-newpage
pip install pandoc-minted
```

## Pandoc Templates

When pandoc converts document `document.format1` into `document.format2`, it will use a [default template](https://github.com/jgm/pandoc-templates) for the format `format2`. In the conversion, one can choose to include all of the template so that the document is a 'standalone' document by including the `--standalone` or `-s` option. For example. in LaTeX it would include `\documentclass{}` and all necessary packages in preamble, instead of just the content between `\begin{document}` and `\end{document}`. These templates can either be completely replaced via the `--template` option that points to a custom template, or amended with additional packages by using the `--header-includes` command. For more details see [general writer options](https://pandoc.org/MANUAL.html#general-writer-options) in the manual.

## YAML Header

This is sort of like the preamble in LaTeX. It contains data that act as options and settings for the current document.

* A YAML object is delimited by three `---` at the top and bottom.
* Denote items in a list by starting new liens with `-`.
* Write multi-line strings, preserving newlines with `|`
* It can either be included in the document (usually at the top) or in a separate file:
  `pandoc chap1.md chap2.md chap3.md metadata.yaml -s -o book.html`

Read more about the YAML syntax [here](https://en.wikipedia.org/wiki/YAML#Syntax) and supported YAML option in pandoc [here](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block).

### Example YAML header

All the variables that are being set in the following is variables from the appropriate pandoc template.

```yaml
---
title: My demonstration
author:
 - Kurt Gödel
 - Haskell Curry
version:
 - number: 1.0
   date: July 13, 1945
   log:  Initial commit
 - number: 1.1
   date: August 14,1946
   log:  Added some math
bibliography: sample2.bib
csl: chicago-fullnote-bibliography.csl
header-includes:
- \usepackage{xcolor}
- \usepackage{minted}
- \setminted{linenos=true}
---
```

## pandoc and LaTeX

* [Default loaded LaTeX packages](https://pandoc.org/MANUAL.html#creating-a-pdf)
* [Default LaTeX variables are listed here](https://pandoc.org/MANUAL.html#variables-for-latex)

## TODO

* Figure out way to make `.tex` conversion a little nicer with respect to line wrapping (see `subfig-demo.tex` for example)

### Maybe

* Add to README.md a single example that is a mixture of all the demos as a minimal example + TOC
