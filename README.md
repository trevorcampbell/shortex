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
X_n &\in \scX\\
X_n &\convp X \label{eq:foo}\\
\E\lt[X\rt] &= \int_0^1 6\der{4y^2}{y}\d y\\
\P\lt(X_n \in \scA\rt) &= \shkC\\
X_n &\dist \Norm(\shmu, \shSigma)
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

The high-level goal of ShorTeX is to make LaTeX...
- **readable:** make LaTeX math code shorter and more readable.
- **brief & easy to type:** avoid the verbose commands and boilerplate common in LaTeX,
  and avoid multi-key presses (curly braces, capital letters, etc) where reasonable.
- **consistent & memorable:** make commands easy to remember and follow
  consistent patterns.
- **clear & opinionated:** there should be one ShorTex way of doing things.
- **robust:** make editing LaTeX documents without accidentally breaking things
  (e.g. references, equation numbers, etc) easier.

...without breaking original LaTeX commands so that users can employ as much or as little ShorTeX as they want.
ShorTeX includes a few different categories of functionality towards this goal.
Contributors to this package should try to justify proposed inclusions
based on the below guidelines (or propose different guidelines, of course!).

### Packages

A package may be included in ShorTeX if it satisfies one of a few criteria:
- It makes basic LaTeX functionality significantly easier to use (e.g.,
  `autonum`, `cleveref`).
- It is commonly included in mathematical/computational documents anyway, but
  results in a lot of boilerplate each time (e.g., `hyperref`, `graphicx`,
  `algorithm`, `algpseudocode`, `amsmath`, `amsthm`, `mathtools`, etc).
- It makes improvements to LaTeX typesetting or internal functionality without
  code changes (e.g., `booktabs`, `microtype`, `marginnote`).
- It is necessary for other functionality in ShorTeX (e.g., `xifthen`,
  `xstring`, `xcolor`).

Opinionated default arguments for packages included in ShorTeX are preferred.
If a package usually needs to be configured carefully on a case-by-case basis,
that's a signal that it may not be a good idea to include in ShorTeX. But if
there are a small number of common configurations, ShorTeX should expose those
in a compact way.

### Shorthands for environments, other non-printing macros

Non-printing macros are those that do not directly appear in the typeset document,
such as environments, commands that change alignment and spacing, etc.
Commonly used, bulky non-printing macros should be replaced in ShorTeX
with lowercase, short, and memorable macros without curly braces.
Occasionally curly braces are necessary for arguments, but
arguments in curly braces can often be simplified by specifying common argument values.

Environments in particular should be specified with a pair of macros `\b...` and `\e...`
where `...` is a readable/memorable lowercase shorthand. For example,
`\begin{theorem}...\end{theorem}` becomes `\bthm...\ethm`, and
`\begin{figure}...\end{figure}` becomes `\bfig...\efig`.
- Unnumbered theorem-like environments append a `u`; so `\bthm...\ethm` becomes
  `\bthmu...\ethmu`.
- Starred versions of other environments append an `s` (because there is no
  consistent behaviour of a star outside of theorem-like environments); so
  `\bfig...\efig` becomes `\bfigs...\efigs`.

### Shorthands for common editing tasks

There are certain tasks that are commonly performed across a wide range of
documents for which users tend to define their own special one-off commands.
Examples of this are a command to shrink whitespace in math mode, 
as well as a set of commands to add comments/highlights/margin
notes to documents. ShorTeX should include shorthand macros to automate these
common tasks with a simple syntax.

### Math macros that "fill in the gaps"

ShorTeX should include macros to implement commonly used math
symbols/operations that are clearly missing from LaTeX with usual math packages. The
syntax should be as unsurprising as possible and follow the patterns existing
in LaTeX with usual math packages. For example, there are `\max` and `\min`
macros in LaTeX for maximization and minimization, but no macros for argmax,
argmin, essential supremum, etc. As another example, there is `\sum` and
`\prod` command for sums and products, but no macros for other common operations "over a range of
items" like unions, intersections, etc. There are `\widehat` and
`\widetilde` macros, but no `\widebar`. 

### Math macros for common functions and operations

For functions and operators (e.g., trace, rank, variance, support, probability), ShorTeX should
generally include lowercase macros that mimic the typeset appearance of the function/operator name.

### Math macros for unwieldy/unreadable expressions

ShorTeX should include macros to make very common, but otherwise bulky/difficult-to-read 
mathematical syntax clearer. Common examples of this are long style/accent combinations, like 
`\bar{\mathbb{A}}`, over/underset expressions like `\overset{\text{p}}{\to}`, 
delimiters like `\left\{ ... \right\}`, and accented names and words like ``c\`{a}dl\`{a}g``.
The macro names should be short, memorable, and avoid curly braces and multikey presses.

