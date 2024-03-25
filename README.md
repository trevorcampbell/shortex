# ShorTeX.sty
## LaTeX style file for more efficient, more readable math

Standard LaTeX syntax can be quite painful to read and type, especially when it comes to typesetting math:
```latex
See Equation \ref{eq:foo}.
\begin{align}
X_n &\in \mathcal{X} \notag\\
X_n &\overset{\text{p}}{\to} X \label{eq:foo}\\
\mathbb{E}\left[X\right] &= \int_0^1 6\frac{\mathrm{d} 4y^2}{\mathrm{d} y}\mathrm{d}y \notag\\
\mathbb{P}\left(X_n \in \mathcal{A}\right) &= \hat{\mathbb{C}} \notag\\
X_n &\sim \mathcal{N}(\hat{\mu}, \hat{\Sigma}). \notag
\end{align}
```

The `shortex.sty` style file includes a number of packages and macros to help make typesetting
mathematical documents in LaTeX less painful and LaTeX code easier to read. 
For example, here is the same expression as above in `shortex.sty` syntax:
```latex
See \cref{eq:foo}.
\[
X_n &\in \fcX\\
X_n &\convp X \label{eq:foo}\\
\ex\lt[X\rt] &= \int_0^1 6\der{4y^2}{y}\dee y\\
\pr\lt(X_n \in \fcA\rt) &= \fbhC\\
X_n &\dist \distNorm(\fhmu, \fhSigma)
\]
```

## Suggested usage

The best way to use ShorTeX is to download a copy of `shortex.sty` and put it
in your document's root folder. Then in your document's preamble, type:
```latex
\usepackage{shortex}
```
**Note: ShorTeX requires you to compile your document 4 times.**

Do not install ShorTeX system-wide. This repository has not reached
a stable v1.0, and we are updating things regularly without any guarantee of 
backwards compatibility. So to avoid accidentally breaking old documents, just
include a self-contained copy of `shortex.sty` with each document.

## Documentation

Package features are detailed in `shortex.pdf` in this repository. 

## Contributing Guide

ShorTeX follows a few rules for including shortcuts and packages.

### Packages

A package should be included in ShorTeX if it satisfies one of a few criteria:
- It makes basic LaTeX functionality significantly easier to use (`autonum`, `cleveref`)
- It is commonly included in mathematical/computational documents anyway, but may be annoying to configure each time (`hyperref`, `graphicx`, `algorithm`, `algpseudocode`, `amsmath`, `amsthm`, `mathtools`, etc)
- It makes improvements to LaTeX typesetting or internal functionality without code changes (`booktabs`, `microtype`, `marginnote`)
- It is necessary for other functionality in ShorTeX (e.g. `xifthen`, `xstring`, `xcolor`)

### Macros

Todo

