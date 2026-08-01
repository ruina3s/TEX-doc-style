# 项目介绍

本项目是一个关于LaTeX的**自定义笔记格式**项目，自定义了`R3S-tex-doc`的样式。作用于`ctexbook`与`ctexart`两种文档类。

---

## 1. 项目结构

```
TEX-doc-style
├── demo/                   ← 演示目录
├── img/                    ← 图片目录
├── old/                    ← 开发目录
├── demo.pdf                ← 结果演示
├── demo.tex                ← 演示模板
├── R3S-tex-doc.sty         ← 样式文件
├── template-article.tex    ← 文章、笔记模板目录
├── template-book.tex       ← 书籍模板目录
└── README.md               ← 项目介绍目录 ！（本文）
```

---

## 2. 快速开始

下载本项目或克隆本项目到本地本地。
直接使用两个template文件即可（内附简易说明）。

也可以直接在`.tex`文件中使用`\usepackage{R3S-tex-doc}`来调用样式。

>　也可以参考demo.pdf与对应的demo.tex文件进行使用。

## 3. 功能说明（语法）
1. 表格
```tex
    \begin{table}[htbp] % htbp用于定位
        \caption{表格演示}
        \centering %剧中
        \begin{tabular}{lccc}
            \toprule
            表头&列1&列2&列3 \\ % \\换行 &换列
            \midrule
            行1&text11&text12&text13 \\
            行2&text21&text22&text23 \\ 
            \bottomrule
        \end{tabular}        
    \end{table}
    
    \begin{center}
        \begin{tabular}{|c|c|c|}
            \hline
            1&2&3 \\ \hline
            4&5&6 \\ \hline
            7&8&9 \\ \hline
        \end{tabular}
    \end{center}
    
    \begin{center}
        \begin{tabular}{|c|c|c|}
            \hline
            1&2&3 \\ \hline
            \multicolumn{2}{|c|}{4} &5 \\ \hline
            6& \multicolumn{2}{|c|}{7} \\ \hline
            \multicolumn{3}{|c|}{8} \\ \hline
        \end{tabular}
    \end{center}

    \begin{tabular}{|l|c|c|c|}
        \toprule
        % 横向合并示例：表头跨3列
        \multicolumn{1}{c}{表头} & \multicolumn{3}{c}{合并的3列标题} \\
        \cmidrule(lr){2-4}  % 在第2-4列画横线
        表头 & 列1 & 列2 & 列3 \\
        \midrule
        
        % 纵向合并示例：行1-行2 的第一列合并
        \multirow{2}{*}{合并行} & text11 & text12 & text13 \\
                                & text21 & text22 & text23 \\
        
        \midrule
        
        % 横向+纵向同时合并的复杂示例
        \multirow{2}{*}{复杂合并} & \multicolumn{2}{c}{横向合并两列} & text13 \\
        \cmidrule(lr){2-3}
                                  & text21 & text22 & text23 \\
        
        \bottomrule
    \end{tabular}
```

2. 图片
```tex
    \begin{center}
        % 测试图片过大所以调整大小
        \includegraphics[scale=0.2]{img/测试用JPG.jpg}
        \includegraphics[scale=0.2]{img/测试用PNG.png}        
    \end{center}
``` 

3. 列表
```tex
    % 无序列表示例
    \begin{itemize}
        \item 战争
        \item 疾病
        \item 命运
        \item 死亡
    \end{itemize}

    % 列表嵌套示例
    \begin{itemize}
        \item test1
        \begin{itemize}
            \item 123
            \item 345
        \end{itemize}
        \item test2
    \end{itemize}
    
    % 有序列表示例
    \begin{enumerate}
        \item kaiser
        \item number
        \item lucy
    \end{enumerate}
```

4. 代码块
本样式引入了listings包，用于代码块的展示。旧版的太简陋了，没有语法高亮、没有行号、没有背景。
```tex
    \begin{lstlisting}[language=python]
        test = {"lily":18,"lucy":19,"luck":20}

        for key in test.keys():
            print(key)
            print(test[key])

        for value in test.values():
            print(value)

        for k,v in test.items():
            print(k,v)
    \end{lstlisting}
```

5. 自定义颜色框
```tex
    % 在环境内容开始前加一个字符就正常显示，不然会吞掉一个字符
    \begin{dy}{测试}
    :这是一个测试定义
    \end{dy}
    \begin{dl}{}
    :这是一个测试定理
    \end{dl}
    \begin{lz}{}
    :这是一个测试例子
    \end{lz}
    \begin{ts}{}
    :这是一个测试提示
    \end{ts}
    \begin{cw}{}
    :这是一个测试错误
    \end{cw}
    \begin{lx}{}
    :这是一个测试练习
    \end{lx}
```

6. 数学公式
这里就不演示了，使用tex就是为了数学公式！

7. 练习环境
定义了练习环境，用于展示数学练习。
同时定义了答案环境和解释环境（默认两者都显示）。可单独在`.tex`文件中通过`\showanswerfalse`隐藏答案。`\showexplanationsfalse`隐藏解释。
```tex
    \begin{exercise}
        求极限 $\displaystyle \lim_{x\to 0} \frac{\sin 3x}{x}$.
    \end{exercise}
    \begin{answer}
        3
    \end{answer}
    \begin{explanation}
        利用重要极限，$\displaystyle \lim_{x\to 0} \frac{\sin 3x}{x}=3\lim_{x\to 0}\frac{\sin 3x}{3x}=3\times 1=3$.
    \end{explanation}
```

8.分栏
分栏没有特别定义、只是在样式中引入了multicols包，用于分栏。
```tex
当第连的里大郭平屯杨略丑求清送事，句杀燕入本火土不陈云必大而不后司，亲召是疾反秦，
皇派真你斯无一不救杨侯反的同，土希把正尝不往而忧你作使马也的种，了长在但，光九非间洪松冒自君朗逃尘得谋头位，
入书尚办不的心回君到，于上葬极仅认不老苟作十下无说赏禀，不恨若韩。
\setlength{\columnseprule}{0.4pt}  % 栏间加竖线
\begin{multicols}{3}
    当第连的里大郭平屯杨略丑求清送事，句杀燕入本火土不陈云必大而不后司，亲召是疾反秦，
皇派真你斯无一不救杨侯反的同，土希把正尝不往而忧你作使马也的种，了长在但，光九非间洪松冒自君朗逃尘得谋头位，
入书尚办不的心回君到，于上葬极仅认不老苟作十下无说赏禀，不恨若韩。
\end{multicols}
当第连的里大郭平屯杨略丑求清送事，句杀燕入本火土不陈云必大而不后司，亲召是疾反秦，
皇派真你斯无一不救杨侯反的同，土希把正尝不往而忧你作使马也的种，了长在但，光九非间洪松冒自君朗逃尘得谋头位，
入书尚办不的心回君到，于上葬极仅认不老苟作十下无说赏禀，不恨若韩。
```