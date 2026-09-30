---
title: TeX 子文件精简总结
date: 2026-9-30
author: RUINA3S
tags: [tex, 子文件]
categories: [技术, tex, note]
description: “当需要编写大文件tex时或需要复用内容时的tex处理方式”
draft: false
---

# TeX 子文件精简总结

`article` 也可用，不是只有 `book`。`article` 子文件用 `\section`，不用 `\chapter`。

## 1. 子文件不单独编译：`\input` / `\include`

目录：

```text
main.tex
mystyle.sty
sec1.tex
```

`main.tex`：

```latex
\documentclass{article}
\usepackage{ctex}
\usepackage{mystyle}
\begin{document}

\input{sec1}

% 或：
% \include{sec1}

\end{document}
```

`sec1.tex`：

```latex
\section{第一节}

正文。
```

规则：

- 子文件不写 `\documentclass`、`\begin{document}`、`\end{document}`。
- 子文件不写 `\usepackage{mystyle}`。
- 子目录写 `\input{chapters/sec1}` 或 `\include{chapters/sec1}`。
- `\include` 在 `article` 中可用，但会另起一页；不想分页用 `\input`。

## 2. 子文件要单独编译：`subfiles`

同目录 `main.tex`：

```latex
\documentclass{article}
\usepackage{subfiles}
\usepackage{ctex}
\usepackage{mystyle}
\begin{document}

\subfile{sec1}

\end{document}
```

同目录 `sec1.tex`：

```latex
\documentclass[main.tex]{subfiles}
\begin{document}

\section{第一节}

正文。

\end{document}
```

子目录 `main.tex`：

```latex
\documentclass{article}
\usepackage{subfiles}
\usepackage{ctex}
\usepackage{mystyle}
\begin{document}

\subfile{chapters/sec1}

\end{document}
```

子目录 `chapters/sec1.tex`：

```latex
\documentclass[../main.tex]{subfiles}
\begin{document}

\section{第一节}

正文。

\end{document}
```

单独编译：

```bash
xelatex sec1.tex
```

或：

```bash
pdflatex sec1.tex
```

自己的 `mystyle.sty`：

- 主文件写 `\usepackage{mystyle}`。
- 子文件不重复写 `\usepackage{mystyle}`。
- 单独编译子文件时，`mystyle.sty` 必须能被 TeX 找到。
- 最简：`main.tex`、`sec1.tex`、`mystyle.sty` 同目录。
- 子目录编译：Linux/macOS 用 `TEXINPUTS=..: xelatex sec1.tex`；Windows cmd 先 `set TEXINPUTS=..;`，再 `xelatex sec1.tex`。

## 速查

| 需求 | 主文件 | 子文件 |
|---|---|---|
| 不单独编译 | `\input{sec1}` 或 `\include{sec1}` | 只写正文，如 `\section{...}` |
| 单独编译 | `\usepackage{subfiles}` + `\subfile{sec1}` | `\documentclass[main.tex]{subfiles}` + `\begin{document}` + 正文 + `\end{document}` |
| 自己的包 | `\usepackage{mystyle}` | 不重复加载 |
