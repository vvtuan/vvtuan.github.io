---
layout: post
title: "Beamer in LaTeX"
subtitle: "Beamer"
date:  2021-04-22
categories: [Beamer]
tags: [Beamer, LaTeX]
---

[TOC]

## Learn

https://en.wikibooks.org/wiki/LaTeX/Presentations

## Theme

```latex
\usetheme{default}
%\usetheme{Warsaw}
```

## Bookmark Vietnamese

```latex
\documentclass[hyperref={unicode}]{beamer}
```

## Not show header, footer

```latex
%\usepackage{beamerthemesplit}
```

## Numbering sections and subsections

https://tex.stackexchange.com/questions/400932/beamer-automating-numbering-sections-and-subsections

## Divide long presentation into multiple pdfs

Using the `\lecture{<name>}{<label>}` command of beamer makes it easy to create a pdf with just a specific part of the slides.

```latex
\documentclass{beamer}

\includeonlylecture{lec2}

\begin{document}

\lecture{lecture 1}{lec1}
\begin{frame}
  content 1
\end{frame}

\lecture{lecture 2}{lec2}
\begin{frame}
  content 2
\end{frame}

\end{document}
```

## Short and long presentations

https://tex.stackexchange.com/a/276129

You can label each frame `\begin{frame}[label=both]` and then use

```tex
\includeonlyframes{<frame label list>}
```

A sample:

```latex
\documentclass{beamer}
%\includeonlyframes{title,both,short1,both1}      %% for short
\includeonlyframes{title,both,long1,long2,both1}  %% for long
\begin{document}

\title{Presentation}
\begin{frame}[label=title]
\titlepage
\end{frame}

\begin{frame}[label=both]{Issue 1} % both
both
\end{frame}

\begin{frame}[label=short1]{Issue 2 - the gist of it} % only short
short 1
\end{frame}

\begin{frame}[label=long1]{Issue 2 - the detailed version } % only long
long 1
\end{frame}

\begin{frame}[label=long2]{Issue 2 - the detailed version, contd.} % only long
long 2
\end{frame}

\begin{frame}[label=both1]{Issue 3} % both
both 1
\end{frame}

% etc.

\end{document}
```

