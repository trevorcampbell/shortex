# ShorTeX.sty
## LaTeX style file for more efficient, more readable mathematical documents

Standard LaTeX syntax can be quite painful to read and type, especially when it comes to typesetting math:
```latex
See Equation \ref{eq:foo}.
\begin{align}
X_n &\in \mathcal{X} \notag\\
X_n &\overset{\text{p}}{\to} X \label{eq:foo}\\
\mathbb{E}\left[X\right] &= \int_0^1 6\frac{\mathrm{d} 4y^2}{\mathrm{d} y}\mathrm{d}y \notag\\
\mathbb{P}\left(X_n \in \mathcal{A}\right) &= \hat{\mathbb{C}} \notag\\
X_n &\sim \mathcal{N}(\hat{\mu}, \hat{\sigma}). \notag
\end{align}
```

The `shortex.sty` style file includes a number of packages and macros to help make typesetting
mathematical documents in LaTeX less painful and LaTeX code easier to read. 
For example, here is the same expression as above in `shortex.sty` syntax:
```latex
See \cref{eq:foo}.
\[
X_n &\in \mcX\\
X_n &\convp X \label{eq:foo}\\
\EE\left[X\right] &= \int_0^1 6\der{4y^2}{y}\dee y\\
\Pr\left(X_n \in \mcA\right) &= \bhC\\
X_n &\dist \distNorm(\hmu, \hSigma)
\]
```

## Suggested usage

The best way to use ShorTeX is to download a copy of `shortex.sty` and put it
in your document's root folder. Then in your document's preamble, type:
```latex
\usepackage[autonum]{shortex}
```
**Note: ShorTeX requires you to compile your document 4 times.**

Do not install ShorTeX system-wide (yet). This repository has not reached
a stable v1.0, and we updating things regularly without any guarantee of 
backwards compatibility. So to avoid accidentally breaking old documents, just
include a self-contained copy of `shortex.sty` with each document.

## Features

### Automatic reference typing

Typically to use a reference in LaTeX you have to write the name of the type of reference
yourself. For example, if you want to reference a figure, you would use something like
```latex
In Figure \ref{fig:the_figure}, you can see...
```
or for multiple figures, you might use
```latex
Figures \ref{fig:the_figure}, \ref{fig:the_other_figure}, and \ref{fig:the_third_one} show that...
```

The `cleveref` package simplifies this process significantly. Use the `\cref` command to automatically
typeset the names of the objects you're referencing (including properly handling multiple references). The 
above two examples become

```latex
In \cref{fig:the_figure}, you can see...
```
and
```latex
\cref{fig:the_figure,fig:the_other_figure,fig:the_third_one} show that...
```
This works for many different reference types (Figure, Algorithm, Equation, Table, etc),
and can be extended if needed. See [the cleveref package](https://ctan.org/pkg/cleveref?lang=en) for more.

### Simplified equations and automatic equation numbering
Typically when you typeset equations, you have to choose between `$...$`, `$$...$$`, 
`\begin{align}...\end{align}`, `\begin{aligned}...\end{aligned}`, `\begin{equation}...\end{equation}`, 
not to mention starred versions of those environments and `\nonumber`/`\notag` commands, depending 
on whether/where you want equation numbers,
display or in-text math, etc. This leads to verbose, inconsistent code.

The `shortex` package provides two major improvements. First, we replace 
the `align` environment with a much less verbose `\[ ... \]` syntax,
```latex
\[
   A &= B + C\\
   D &\leq E
\]
```
And second, there are *only two commands* you need to use:
single dollar signs for in-text math,
```latex
This is some in-text math $a+b=c$
```
and square brackets for display math mode,
```latex
\[
   a+b = c \label{eq:the_equation}
\]
```
The `autonum` package automatically decides which equations to provide numbers based 
on *which equations you reference*. For example, in the above display math, I used
the label `eq:the_equation`. If I use the command `\cref{eq:the_equation}` somewhere
in the document, that equation will *automatically* be assigned a number. If not, it
won't get a number. See [the autonum package](https://ctan.org/pkg/autonum?lang=en) for more.

**Note: You must compile your document 4 times for this to work properly.** 

### Convenient math commands
The `shortex.sty` file has a huge list of shortened commands for mathematical symbols.
I'll list a few of the most common ones I use here, but please go through the style file
to see the full list.

You can see the difference in clarity below. Here is some basic LaTeX math syntax:
```latex
\begin{align}
X_n &\in \mathcal{X}\\
X_n &\overset{\text{p}}{\to} X\\
\mathbb{E}\left[X\right] &= \int_0^1 6\frac{\mathrm{d} 4y^2}{\mathrm{d} y}\mathrm{d}y\\
\mathbb{P}\left(X_n \in \mathcal{A}\right) \leq 
X_n \sim \mathcal{N}(\hat{\mu}, \hat{\sigma}).
\end{align}
```

And here is the exact same expression using `shortex.sty` syntax:
```latex
\[
X_n &\in \mcX\\
X_n &\convp X\\
\EE\left[X\right] &= \int_0^1 6\der{4y^2}{y}\dee y\\
X_n \dist \distNorm(\hmu, \hSigma)
\]
```



#### Sets
```latex
\reals      % real numbers
\rats       % rational numbers
\nats       % natural numbers
\comps      % complex numbers
```

#### General Purpose
```latex
\defined    % := for "defined as"
\defines    % =: for "defines"
\argmax     % argmax
\argmin     % argmin
\st         % s.t., such that 
```


#### Theorem Environments
```latex
\bthm ... \ethm  % unnumbered theorem
\blem ... \elem  % unnumbered lemma
\bprop ... \eprop  % unnumbered proposition
\bcor ... \ecor  % unnumbered corollary
```
and to get the numbered version of these, just insert an `n` :
```latex
\bnthm ... \enthm  % unnumbered theorem
\bnlem ... \enlem  % unnumbered lemma
\bnprop ... \enprop  % unnumbered proposition
\bncor ... \encor  % unnumbered corollary
```

You can create a proof block below a result statement using
the `\bprf ... \eprf` block:
```latex
\bthm
here is the theorem statement.
\ethm
\bprf
here is the proof
\eprf
```

You can also put a proof later on in the document (e.g. in the 
appendix) by using the `\bprfof{...} ... \eprfof` block and referencing
a labelled and numbered theorem
```latex
\bnthm \label{thm:the_theorem}
here is the theorem statement.
\enthm

% (more of your document here)

\bprfof{\cref{thm:the_theorem}}
here is the proof
\eprf
```

#### Probability / Stats

Text-mode shortcuts:
```latex
\iid        % i.i.d.
\as         % a.s.
\aev        % a.e.v.
```

Math-mode shortcuts:
```latex
\convas     % converges almost surely to
\convp      % converges in probability to
\convd      % converges in distribution to
\eqd        % equal in distribution to
\eqas       % equal almost surely to

\dist       % distributed as
\distind    % distributed independently as
\distiid    % distributed iid as

\Pr         % the probability of
\EE         % expectation
\var        % variance
\cov        % covariance
```

Distributions (there are quite a few more in `shortex.sty`, and you can define new ones using the `\distNamed` command)
```latex
\distBern
\distNorm
\distUnif
\distGam
\distPoiss
\distBeta
\distExp
\distMulti
```

#### Calculus

```latex
\dee              % a math roman numeral "d", useful for integrals, e.g. "dt"
\der{...}{...}    % derivatives, e.g. \der{F}{t} will show dF/dt
\dder{...}{...}   % second derivatives
\D{...}{...}      % partial derivatives
\DD{...}{...}     % partial second derivatives
```

#### Accented symbols
To insert a bar over most characters, just put a `\b` in front of it. For example,
```latex
\ba       % overbar a
\bG       % overbar G
\balpha   % overbar alpha
```

This exact same pattern applies to many different style changes. Here is a list of useful ones:
```latex
\h...     % hat
\t...     % tilde
\mc...    % mathcal
\bh...    % bold hatted
\wh...    % wide hatted
\bt...    % bold tilde
\bi...    % bold italic
\mf...    % mathfrak
```
Each of these accents does not work for *all* characters, but it works for a lot of them (even greek letters).


### Lists

To typeset an unnumbered list, use `\bitems...\eitems`:
```latex
\bitems
\item Here is an item
\item Here is another
\eitems
```

To typeset a numbered list, use `\benum...\eenum`:
```latex
\benum
\item Here is an item
\item Here is another
\eenum
```

