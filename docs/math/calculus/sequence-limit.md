# 数列极限

## 数列

**数列**是指**将一串数按照一定的顺序依次列出来形成的一个序列**。例如将自然数依次列举出来写成 $1,2,3,...,n$，便形成了一个数列。对于一般的数列，我们通常使用**变量+下标**的方法来表示其中的每一项，下标从 $1$ 开始按照自然数顺序依次递增，下标越大，代表的项在序列中就越靠后，例如 $x_1,x_2,x_3,...,x_n,x_{n+1},...$。数列可以通过依次列举其中的项来表示，也可以通过指定特定的规律来生成一个序列。例如指定首项和公差，便可以得到一个**等差数列**；指定首项和公比，便可以得到一个**等比数列**。

## 数列极限的概念

数列的极限就是考察数列在无穷多项以后的变化趋势，如果一个数列在无穷多项后变化趋于稳定，我们便称一个数列存在极限。例如定义 $a_n=\frac{1}{n}$，则可以发现随着n的增大，$a_n$ 的值会越来越靠近0，因此我们便可以认为**“ $a_n$ 趋向于0”**。

### 定义

一个数列趋向于 $A$ 可通俗的理解为**“无限地靠近A”**，但这种叙述方式无法给出一个精确且定量的概念，因此我们需要一个严格的分析定义来消除这种不确定性。这个定义是由**柯西**最先提出，并由**魏尔斯特拉斯**完善而成的：

> $Definition$：**设 $\{a_n\}$ 为一数列，$a \in \mathbb{R}$，若 $\forall \varepsilon>0, \exists N>0$，使得当 $n>N$ 时，有 $|a_n-a|<\varepsilon$，则称 $\{a_n\}$ 收敛于 $a$，记为 $\lim\limits_{n \to \infty}a_n=a$**

按照该定义，我们便可以严格的证明一个数列的极限是否为一个确切值。

> $Example$：求证 $\lim\limits_{n \to \infty} \frac{1}{n}=0$
>
> **证明：** $\forall \varepsilon >0$，取 $N=\frac{1}{\varepsilon}$，则当 $n>N$ 时
>
> $\left| \frac{1}{n} - 0\right|<\varepsilon$
>
> $\therefore \lim\limits_{n \to \infty} \frac{1}{n}=0$

## 数列极限性质

数列的极限有以下一些基本性质。

### 唯一性

> **若 $\lim\limits_{n \to \infty}a_n=a$ 存在，则 $a$ 唯一**


### 有界性

> **若 $\lim\limits_{n \to \infty}a_n=a$ 存在，则 $\{a_n\}$ 有界**


### 保号性

> **若 $\lim\limits_{n \to \infty}a_n=a>0$，则 $\forall 0<b<a, \exists N>0$，使得当 $n>N$ 时，$a_n>b$**


### 保不等式性

> **若 $\lim\limits_{n \to \infty}a_n=a,\lim\limits_{n \to \infty}b_n=b$， $\exists N>0$，使得当 $n>N$ 时，$a_n \geq b_n$，则 $a \geq b$**

## 数列极限的求法

对于一般的数列，我们可以通过初等变形以及一些基本的极限结论得到其极限值。

> $Example$：求 $\lim\limits_{n \to \infty} \sqrt{n+1} - \sqrt{n}$
>
> **解：**$\sqrt{n+1} - \sqrt{n} = \frac{1}{\sqrt{n+1}+\sqrt{n}}$
>
> $\because \lim\limits_{n \to \infty} \frac{1}{\sqrt{n+1}+\sqrt{n}} = 0$
>
> $\therefore \lim\limits_{n \to \infty} \sqrt{n+1} - \sqrt{n}=0$

### 迫敛性（夹逼准则）

对于一些较为复杂的极限，我们往往无法直接求出其极限值。但有时如果我们能对数列进行适当的放缩，并能求出放缩后数列的极限值，也能得到该数列的极限值。这建立在如下定理的基础之上：

> $Theorem$：**设 $\{a_n\}\{b_n\}\{c_n\}$ 三个数列，$\lim\limits_{n \to \infty} a_n=\lim\limits_{n \to \infty}b_n=a$，若 $\exists N>0$，使得当 $n>N$ 时，$a_n \leq c_n \leq b_n$，则 $\lim\limits_{n \to \infty}c_n=a$**
>
> **证明：**$\because \lim\limits_{n \to \infty} a_n=\lim\limits_{n \to \infty}b_n=a$
>
> $\therefore \forall \varepsilon > 0$
>
> $\exists N_1>0$，使得当 $n > N_1$ 时，$a_n>a-\varepsilon$
>
> $\exists N_2>0$，使得当 $n > N_2$ 时，$a_n>a-\varepsilon$ 
>
> 取 $N_0=\max \{N_1,N_2\}$，则当 $n>N_0时$
>
> $a-\varepsilon < a_n \leq c_n \leq b_n < a+\varepsilon$
>
> 即 $|c_n-a|<\varepsilon$
>
> $\therefore \lim\limits_{n \to \infty}c_n=a$

运用该定理，我们可以求解一些较为复杂的极限。

> $Example$：求 $\lim\limits_{n \to \infty}\sqrt[n]{2^n+3^n+4^n+5^n}$
>
> 解：$5 \leq \sqrt[n]{2^n+3^n+4^n+5^n} \leq \sqrt[n]{4} \cdot 5$
>
> $\because \lim\limits_{n \to \infty}\sqrt[n]{4} \cdot 5 = 5$
>
> $\therefore \lim\limits_{n \to \infty}\sqrt[n]{2^n+3^n+4^n+5^n}=5$