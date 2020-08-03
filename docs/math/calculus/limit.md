# 一元函数及数列极限

## 数列极限

### 定义

> **设 $\{a_n\}$ 为一数列，$a \in \mathbb{R}$，若 $\forall \varepsilon>0, \exists N>0$，使得当 $n>N$ 时，有 $|a_n-a|<\varepsilon$，则称 $\{a_n\}$ 收敛于 $a$，记为 $\lim\limits_{n \to \infty}a_n=a$**

### 基本性质

#### 唯一性

> **若 $\lim\limits_{n \to \infty}a_n=a$ 存在，则 $a$ 唯一**


#### 有界性

> **若 $\lim\limits_{n \to \infty}a_n=a$ 存在，则 $\{a_n\}$ 有界**


#### 保号性

> **若 $\lim\limits_{n \to \infty}a_n=a>0$，则 $\forall 0<b<a, \exists N>0$，使得当 $n>N$ 时，$a_n>b$**


#### 保不等式性

> **若 $\lim\limits_{n \to \infty}a_n=a,\lim\limits_{n \to \infty}b_n=b$， $\exists N>0$，使得当 $n>N$ 时，$a_n \geq b_n$，则 $a \geq b$**


#### 迫敛性（夹逼准则）

> **设 $\{a_n\}\{b_n\}\{c_n\}$ 三个数列，$\lim\limits_{n \to \infty} a_n=\lim\limits_{n \to \infty}b_n=a$，若 $\exists N>0$，使得当 $n>N$ 时，$a_n \leq c_n \leq b_n$，则 $\lim\limits_{n \to \infty}c_n=a$**




## 函数极限

### 定义

> **设 $f(x)$ 在 $x_0$ 的某个去心邻域内有定义，$A \in \mathbb{R}$，若 $\forall \varepsilon>0,\exists \delta>0$，使得当 $0<|x-x_0|<\delta$ 时，有 $|f(x)-A|<\varepsilon$，则称 $f(x)$ 当 $x$ 趋于 $x_0$ 时的极限为 $A$，记为 $\lim\limits_{x \to x_0}f(x)=A$**