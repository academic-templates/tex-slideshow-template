<h1 align="center">LaTeX Slideshow Template <a href="https://twitter.com/intent/tweet?text=LaTeX%20Slideshow%20Template.%0D%0ALaTeX%20template%20for%20creating%20your%20beautiful%20slideshow%20with%20Beamer%2e%0D%0A&hashtags=TeXLaTeX,LaTeXbeamer"><img src="https://img.shields.io/badge/Tweet--lightgrey?logo=twitter&style=social" alt="Tweet" height="20"/></a></h1>

## :information_source: Introduction

The goal of this template is to provide a nice-looking slideshow layout, easy to configure and fill in.

Here is an example preview of the heading page and outline:

<p align="center"><img src="https://raw.githubusercontent.com/academic-templates/tex-slideshow-template/main/doc/preview-heading-outline.png" width="66%"><br>
<sub><sup>Preview image generated with <a href="https://gist.github.com/dhondta/f57dfde304905644ca5c43e48c249125">this tool</a></sup></sub></p>

Here is an example preview of some content slides:

<p align="center"><img src="https://raw.githubusercontent.com/academic-templates/tex-slideshow-template/main/doc/preview-slides.png" width="66%"><br>
<sub><sup>Preview image generated with <a href="https://gist.github.com/dhondta/f57dfde304905644ca5c43e48c249125">this tool</a></sup></sub></p>

Here is an example preview of some reference and appendix slides:

<p align="center"><img src="https://raw.githubusercontent.com/academic-templates/tex-slideshow-template/main/doc/preview-ref-app.png"><br>
<sub><sup>Preview image generated with <a href="https://gist.github.com/dhondta/f57dfde304905644ca5c43e48c249125">this tool</a></sup></sub></p>


## :card_file_box: Structure

The template is structured in the following way:

- `main.tex`: This is the main TeX file to be compiled. Here you can include sections, parts and appendices and also configure some settings (i.e. title, author and so forth).
- `figures`: This folder is aimed to contain the figures (that is, the pictures to be captioned that are included in the list of figures).
- `icons`: This folder is aimed to contain icons that are used without captions, e.g. these included in slide objects.
- `logos`: This folder is aimed to contain logos from the university, e.g. for use on the heading slide.
- `parts`: This folder contains every part other than sections (i.e. appendix and reference slides), one TeX file for each of them, to be included in `main.tex`. It also contains `bibliography.bib` (in BibTeX format) to be used in `references.tex` of this folder.
- `sections`: This folder contains the sections, one TeX file for each of them, to be included in `main.tex`.
- `styles`: This folder contains the styles for defining the layout (imported in `presentation.sty` of this folder). Most of the included one should not be edited.

## :gear: Compilation

The compilation can easilly be configured in [Texmaker](https://en.wikipedia.org/wiki/Texmaker) by defining a *Quick Build Command*:

1. Go to the menu *Options*
2. Select *Configure Texmaker*
3. Go to tab *Quick Build*
4. In the field *User : (...)*, replace the command with:

        pdflatex -synctex=1 -interaction=nonstopmode %.tex|bibtex %.aux|pdflatex -synctex=1 -interaction=nonstopmode %.tex|pdflatex -synctex=1 -interaction=nonstopmode %.tex

5. Then click *OK*

When editing the slideshow with [Texmaker](https://en.wikipedia.org/wiki/Texmaker):

1. Open `main.tex`
2. Go to the menu *Options*
3. Select *Define Current Document as "Master Document"*
4. Open any other file than `main.tex` for edition
5. Click on *Quick Build* to compile

This will produce `main.pdf` with all the included sections, parts and appendices, just like if the focus was on `main.tex`.

## :bar_chart: Making your slideshow

This template is based on LaTeX Beamer. For standard documentation about environments and commands, please refer to [its documentation](https://tug.ctan.org/macros/latex/contrib/beamer/doc/beameruserguide.pdf).



### Adapting the heading slide

You should start this by setting the base information in `main.tex`. This includes the PDF, title, subtitle, author, institute and date information.

You can then start making the slideshow.

### Tuning parts

This template includes predefined part files of the slideshow that should be filled in progressively as you produce content.

Parts that you should adapt:

- `parts/appendices.tex`: here you can define custom appendix slides with the `appframe` block, setting a title and identifier for cross-reference in slides.
- `parts/bibliography.bib`: bibliography entries in BibTeX format.
- `parts/hyperlinks.tex`: here you can define hyperlinks to be used in slides with command `\newhyperlink{ID}{mouseover-title}{URL}`.
- `parts/references.tex`: here you can add reference slides with command `\refframe{title}{keyword-used-in-bib}` where _keyword-used-in-bib_ corresponds to a keyword set in the `keywords` attribute of BibTeX references from `bibliography.bib`.

### Adding sections

This template uses sections with the usual `\section{MyTitle}` command that yields an outline slide. However, this can be customized adding an image and/or an italic text on the right part.

This can be defined as follows:

- Outline image: put the image in the `figures` folder with a filename starting with `outline-` and the name of the section (for the current example, then `figures/outline-MyTitle.png`).
- Outline text: put the text file in the `figures` folder with a filename starting with `outline-` and the name of the section (for the current example, then `figures/outline-MyTitle.txt`).

### Adding slides

Slides are split into 2 main parts:

- Body: this contains normal slides, composing the body of the slideshow, with a first progress bar.
- Appendices: this contains reference and appendix slides allowing to include alternative content in support of the body, with a second progress bar.

The custom frame style defines 4 types:

1. `myframe`: stands for a content slide (sorted in the main body of the slideshow) with a title and subtitle that is defined as an environment (using `\begin` and `\end`). It also includes in an upper banner the sections and subsections, including links to the related slides, for easy navigation.
2. `questionframe`: this can be invoked to add a question slide where required, typically in the `sections/conclusion.tex`.
3. `appframe`: stands for an appendix slide (sorted in additional slides after references) with a title and subtitle that is defined as an environment (using `\begin` and `\end`), automatically assigning appendix uppercase letters. This type of slide does not contain the upper banner with the section and subsection links for sparing space while providing alternative content.
4. `refframe`: stands for a references slide (sorted in additional slides after the conclusion, restarting the slide counter and progress bar) with a title that is defined as a command (using `\refframe` directly and NOT block begin-end) and that sorts cited references from `parts/bibliography.bib` based on the `keywords` attribute from BibTeX entries.

The template (defining frames in `styles/customframe.sty`) also provides a few useful additional commands:

- `appref`: this allows to display a help icon in the upper right corner under the subtitle of a slide that provides a link to the referenced appendix.
- `appret`: this allows to display a backward icon on an appendix slide to go back to a referenced slide (as of the identifier defined in the `myframe` block).
- `framelogo`: this sets a comma-separated list of logos to be displayed in the upper right corner in the title banner according to the following format: `{URL}/image-filename-in-logos-folder`.
- `timeline`: this is set by defining a start year (by default, 2000) and then providing years that are to be highlighed, one per slide.

### Custom objects

A few custom blocks are defined for convenience and may regularly be used:

- `myblock`: this defines a grey frame with rounded corners, a shadow and a label above.
- `myblock2`: this defines a text area (a block with no style).
- `twocolumnsblock`: this defines two blocks aside, without an area to separate them.
- `twocolumnsblocksep`: this defines two blocks aside, with an area (with width 15% of `\linewidth`) to separate them.


## :star: Related Projects

You may also like these:

- [TeX Book Template](https://github.com/academic-templates/tex-book-template): A template for writing a nice book with LaTeX.
- [TeX Cheat Sheet Template](https://github.com/academic-templates/tex-cheat-sheet-template): A template for creating a nice cheat sheet with LaTeX.
- [TeX Course Index Template](https://github.com/academic-templates/tex-course-index-template): A template for writing a condensed course index leveraging LaTeX indexing.
- [TeX Master Thesis Template](https://github.com/academic-templates/tex-master-thesis-template): A template for writing a nice master thesis dissertation with LaTeX.
- [TeX Poster Template](https://github.com/academic-templates/tex-poster-template): A template for creating a nice scientific poster with LaTeX.


## :clap: Supporters

[![Stargazers repo roster for @dhondta/tex-slideshow-template](https://reporoster.com/stars/dark/dhondta/tex-slideshow-template)](https://github.com/dhondta/tex-slideshow-template/stargazers)

[![Forkers repo roster for @dhondta/tex-slideshow-template](https://reporoster.com/forks/dark/dhondta/tex-slideshow-template)](https://github.com/dhondta/tex-slideshow-template/network/members)

<p align="center"><a href="#"><img src="https://img.shields.io/badge/Back%20to%20top--lightgrey?style=social" alt="Back to top" height="20"/></a></p>

