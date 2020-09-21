# templates-for-students

This directory contains some templates for the use of my students.

* The use of these templates is not mandatory.
* Probably you can find better ways to do things. The templates just reflect the way I would do things.
* I will update them from time to time.

## is-alpha-clemens.bst

This is a hacked version of a BibTeX bibliographic style, which also typesets the BibTeX fields URL, DoI and arXiv.
The contents of these fields is piped into TeX macros \bibformatURL, \bibformatDoI and \bibformatArXiv, which further format the entries.

My way of defining these macros is reflected in the following code snippet which I use in most of my recent TeX files. It is assumed
that the hyperref package is loaded.

```
  %%  Define a macro \murls for multiple urls which can format multiple urls when seperated by blanks 
  %   We use this in the bibliography
  %   See https://tex.stackexchange.com/questions/57865/how-to-use-multiple-urls-for-one-bibtex-reference
  \makeatletter
  \def\murls{\begingroup \catcode`\%=12\catcode`\#=12\relax\printurl}
  \def\printurl#1{\@URL#1 \@nil\endgroup}
  \def\@URL#1 #2\@nil{\url{#1}\ifx\relax#2\relax \else; \murls{#2\relax}\fi}
  \makeatother
  % We want to have clickable URLs but the bib style ist-alpha-clemens which we use does not support that.
  % We hacked the bib style to also format entries   DoI  URL  and  arXiv
  % Below we define, how this should be displayed in LaTeX
  \def\bibformatDoI#1{DoI: \url{https://doi.org/ #1}}
  \def\bibformatURL#1{URL: \murls{#1}}
  \def\bibformatArXiv#1{arXiv: #1 \href{https://arxiv.org/pdf/#1.pdf}{PDF} \href{https://arxiv.org/abs/#1}{Abstract}}
  %
  % That is the bibliography style we need for deadling with this.
  \bibliographystyle{/Users/cap/TEX/is-alpha-clemens}
```

