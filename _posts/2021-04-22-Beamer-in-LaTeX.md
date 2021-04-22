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

