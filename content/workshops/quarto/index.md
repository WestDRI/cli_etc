---
title: Authoring scientific documents with Markdown & Quarto
topic: Markup
slug: quarto
weight: 10
execute:
  error: true
format: hugo
---

## Abstract

{{<def>}}
<br>This workshop will show you how to easily create beautiful scientific documents (html, pdf, websites, books...)---complete with formatted text, dynamic code, and figures with <a href="https://quarto.org/" target="_blank">Quarto</a>, an open-source tool combining the powers of Jupyter or knitr with Pandoc to turn your text and code blocks into fully dynamic and formatted documents.<br><br>
{{</def>}}

## Markup and Markdown

### Markup languages

Markup languages control the formatting of text documents. They are powerful but complex and the raw text (before it is rendered into its formatted version) is visually cluttered and hard to read.

Examples of markup languages include LaTeX and HTML.

-   Tex (often with the macro package LaTeX) is used to create pdf.

{{<ex>}}
Example LaTeX:
{{</ex>}}

``` latex
\documentclass{article}
\title{My title}
\author{My name}
\date{\today}
\begin{document}
 \maketitle
 \section{First section}
 Some text in the first section.
\end{document}
```

-   HTML (often with css or scss files to customize the format) is used to create webpages.

{{<ex>}}
Example HTML:
{{</ex>}}

``` html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>My title</title>
    <address class="author">My name</address>
    <input type="date" value="2022-11-24" />
  </head>
  <h1>First section</h1>
  <body>
    Some text in the first section.
  </body>
</html>
```

### Markdown

A number of minimalist markup languages intend to remove all the visual clutter and complexity to create raw texts that are readable prior to rendering. <a href="https://en.wikipedia.org/wiki/Markdown" target="_blank">Markdown</a> (note the pun with "markup"), created in 2004, is the most popular of them. Due to its simplicity, it has become quasi-ubiquitous. Many implementations exist which add a varying number of features (as you can imagine, a very simple markup language is also fairly limited).

Markdown files are simply text files and they use the `.md` extension.

### Basic Markdown syntax

In its <a href="https://daringfireball.net/projects/markdown/" target="_blank">basic form</a>, Markdown is mostly used to create webpages. Conveniently, raw HTML can be included whenever the limited markdown syntax isn't sufficient.

<a href="https://www.markdownguide.org/basic-syntax/" target="_blank">Here</a> is an overview of the Markdown syntax supported by many applications.

### Pandoc and its extended Markdown syntax

While the basic syntax is good enough for HTML outputs, it is very limited for other formats.

<a href="https://pandoc.org/" target="_blank">Pandoc</a> is a free and open-source markup format converter. Pandoc supports <a href="https://quarto.org/docs/authoring/markdown-basics.html" target="_blank">an extended Markdown syntax</a> with functionality for figures, tables, callout blocks, LaTeX mathematical equations, citations... in short, everything needed for the creation of scientific documents.

Such documents remain as readable as basic Markdown documents (thus respecting the Markdown philosophy), but they can now be rendered in sophisticated pdf, books, entire websites, Word documents, etc.

And of course, as such documents remain text files, you can put them under version control with <a href="https://git-scm.com/" target="_blank">Git</a>.

## Literate programming

<a href="https://en.wikipedia.org/wiki/Literate_programming" target="_blank">Literate programming</a> is a methodology that combines snippets of code in a written document. While first introduced in 1984, this approach to the creation of documents has only in recent years truly exploded in popularity, mostly thanks to the development of new tools such as <a href="https://r4ds.had.co.nz/r-markdown.html" target="_blank">R Markdown</a> and, later, <a href="https://jupyter.org/" target="_blank">Jupyter notebooks</a>.

## Quarto

### How it works

Quarto files are transformed into Pandoc's extended Markdown by Jupyter (when used with Python or Julia) or by knitr (when used with R), then pandoc turns the Markdown document into whatever output of your choice.

{{<ex>}}
Julia and Python make use of the Jupyter engine:
{{</ex>}}
{{<img src="/img/quarto/qmd_jupyter.png" title="" width="90%" line-height="1.0rem">}}
From <a href="https://quarto.org/" target="_blank">Quarto documentation</a>
{{</img>}}
{{<ex>}}
R uses the knitr engine:
{{</ex>}}
{{<img src="/img/quarto/qmd_knitr.png" title="" width="98%" line-height="0.2rem">}}
From <a href="https://quarto.org/" target="_blank">Quarto documentation</a>
{{</img>}}

Quarto files use the extension `.qmd`.

When using R, you can use Quarto directly from RStudio: if you are used to R Markdown, Quarto is the new and better R Markdown.

When using Python or Julia, you can use Quarto directly from a Jupyter notebook (with `.ipynb` extension).

{{<ex>}}
Using Quarto directly from a Jupyter notebook:
{{</ex>}}
{{<img src="/img/quarto/ipynb.png" title="" width="80%" line-height="1.7rem">}}
From <a href="https://quarto.org/" target="_blank">Quarto documentation</a>
{{</img>}}

In this workshop, we will see the most general workflow: simply using a text editor.

### Supported languages

<u>Supported languages:</u>

-   Python
-   R
-   Julia
-   Observable JS

<u>Supported outputs:</u>

-   HTML
-   PDF
-   MS Word
-   OpenOffice
-   ePub
-   Revealjs
-   PowerPoint
-   Beamer
-   GitHub Markdown
-   CommonMark
-   Hugo
-   Docusaurus
-   Markua
-   MediaWiki
-   DokuWiki
-   ZimWiki
-   Jira Wiki
-   XWiki
-   JATS
-   Jupyter
-   ConTeXt
-   RTF
-   reST
-   AsciiDoc
-   Org-Mode
-   Muse
-   GNU
-   Groff

### Installation

Download Quarto <a href="https://quarto.org/docs/get-started/" target="_blank">here</a>.

### Document structure and syntax

#### Front matter

Written in YAML. Sets the options for the document. Let's see a few examples.

{{<ex>}}
HTML output:
{{</ex>}}

``` yaml
---
title: "My title"
author: "My name"
format: html
---
```

{{<ex>}}
HTML output with a few options:
{{</ex>}}

``` yaml
---
title: "My title"
author: "My name"
format:
  html:
    toc: true
    css: <my_file>.css
---
```

The above examples would work if you don't use any code blocks or if you use R code blocks. If you use Python or Julia however, you need to add a `jupyter` entry with the name of the language that should run in Jupyter.

{{<ex>}}
MS Word output with Python code blocks:
{{</ex>}}

``` yaml
---
title: "My title"
author: "My name"
format: docx
jupyter: python3
---
```

{{<ex>}}
revealjs output with some options and Julia code blocks:
{{</ex>}}

``` yaml
---
title: "Some title"
subtitle: "Some subtitle"
institute: "Simon Fraser University"
date: "2022-11-24"
execute:
  error: true
  echo: true
format:
  revealjs:
    theme: [default, custom.scss]
    highlight-style: monokai
    code-line-numbers: false
    embed-resources: true
jupyter: julia-1.8
---
```

See <a href="https://quarto.org/docs/guide/" target="_blank">the Quarto documentation</a> for an exhaustive list of options for all formats.

#### Written sections

Written sections are written in <a href="https://quarto.org/docs/authoring/markdown-basics.html" target="_blank">Pandoc’s extended Markdown</a>.

#### Code blocks

Code blocks are written in the format:

If all you want is syntax highlighting of the code blocks, use:

    ```{.language}
    <some code>
    ```

If you want syntax highlighting of the blocks and for the code to run, use instead:

    ```{language}
    <some code>
    ```

In addition, options can be added to individual code blocks:

    ```{language}
    #| echo: true
    <some code>
    ```

### Rendering

Using Quarto is very simple: there are only two commands you need to know.

In a terminal, simply run either of:

``` bash
quarto render <file>.qmd     # this will render the document
quarto preview <file>.qmd    # this will display live preview as you work on your document
```

## Let's give all this a try

Create a file called `test.qmd` with the text editor of your choice.

{{<ex>}}
Example:
{{</ex>}}

``` bash
nano test.qmd
```

Then open a new terminal, `cd` to the location of the file and run the command:

``` bash
quarto preview test.qmd
```

## Comments & questions

<!-- https://www.lib.sfu.ca/about/branches-depts/rc/software-data-dh/software/37398 -->
<!-- https://libcal.library.ubc.ca/event/3683985 -->
