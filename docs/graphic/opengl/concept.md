# OpenGL基本概念

## 点，线，面

你可能对**点、线、面**这些术语在**数学**中的含义已经有了一个很好的理解。在OpenGL中也有这些基本概念，他们所对应的含义和在数学中**类似，但又不完全相同。**
一种差异来自于**计算机存储和计算能力的局限性**。对计算机而言，浮点计算的精度都是有限的，并且具有**取舍误差**。因此，在OpenGL中描述点，线和面的坐标时也会遭受这样的问题。
另一个更重要的区别来自于光栅图形显示的局限性。在显示器上，最小的可显示单位是**像素**，尽管像素的宽度可能小于 $\frac{1}{100}$ 英寸，但它们仍远大于数学中**无穷小**（对于点）和**无穷细**（对于线）的概念。

### 点

在OpenGL中，点也被称为 **“顶点（Vertex）”** 。一个顶点由一组**四维**浮点型坐标 $(x,y,z,w)$ 表示。**在一般情况下，$w$ 会被自动设为 $1$，用户只需要操作其中的前三个数值**，当 $w$ 不为 $1$ 时，这个点代表一个**欧几里得空间**中对应坐标为 $(\frac{x}{w},\frac{y}{w},\frac{z}{w},w)$ 的三维点。这么做的原因将很快在下文中得到解释。

### 线

在OpenGL中，“线”是指**线段**，而不是数学上能够无限延伸的“直线”或者“射线”。在OpenGL中，一根线是由其在两端的顶点所指定的。

### 多边形

在OpenGL中，多边形是由**一组线段闭合包围成环所组成的**，其中线段由其端点处的顶点指定。
在数学中，多边形可能会十分复杂，因此OpenGL对多边形进行了一些严格的限制。

1. OpenGL多边形的**边缘不能相交**（数学家将满足此条件的多边形称为**简单多边形**）。
2. OpenGL多边形必须是**凸多边形**，即**如果给定多边形内部的任何两个点，连接它们的线段也应当位于该多边形的内部**。
3. OpenGL多边形所围成的区域必须是**单连通区域**，即多边形内部不能有“洞”。

## 齐次坐标

用户通常处理的都是二维和三维的顶点，但实际上，它们在OpenGL内部都被视为**包含四个坐标的三维齐次顶点**。如果一个四维向量 $(x,y,z,w)$ 中的**至少一个元素非零**，则这个向量表示一个**齐次顶点**。**$w$ 可以理解为一个比例系数，用于对三维坐标进行缩放**。若**实数 $a$ 不为零**，则 $(x,y,z,w)$ 和 $(ax,ay,az,aw)$ 表示一个相同的齐次顶点 **（因为 $\frac{x}{w}=\frac{ax}{aw},\frac{y}{w}=\frac{ay}{aw},\frac{z}{w}=\frac{az}{aw}$）** 。一个**三维欧几里德空间**中的点 $(x,y,z)$ 对应一个 $(x,y,z,1.0)$ 的齐次顶点，而一个**二维欧几里得空间**中的点 $(x,y)$ 对应一个 $(x,y,0.0,1.0)$ 的齐次顶点。

当 $w = 0.0$ 时，齐次坐标不对应于任何一个欧氏空间中的点，而是对应于一个理想化的 **“无穷大点”** 。要想理解这一概念的意义并不困难，例如若要考虑点 $(1,2,0,0)$ 的意义，只需要注意到当 ** $w$ 逐渐趋向于0时** （例如当 $w=1,0.01,0.001$ 时分别对应欧氏空间中的$(1,2),(100,200),(10000,20000)$），这一点沿直线 $y=2x$ 逐渐**趋向于无穷大**，因此可将 $(1,2,0,0)$ 视为直线 $y=2x$ 方向上的**无穷远点**。

**PS：OpenGL可能无法正确处理 $w<0$ 的齐次坐标。为确保你的代码可在OpenGL上正确运行，请仅使用非负 $w$ 值。**

## 坐标变换

### 顶点变换

如果要对一个顶点进行某些**线性变换操作**（如旋转，平移，缩放，投影等），可以通过引入一个**同阶数的方阵**（对于一个齐次坐标则需要引入一个4*4的方阵）并通过**矩阵乘法**来完成。即如果 $v$ 代表一个齐次坐标顶点，$M$ 为一个特定的4阶变换方阵，则 $Mv$ 的结果就代表顶点  $v$ 在变换 $M$ 下的象。

**PS：变换矩阵 $M$ 通常要求为非奇异矩阵，即M可逆。尽管这不是硬性规定，但如果 $M$ 为奇异矩阵，其变换结果可能会出现问题。**

### 法线变换（平面变换）

由**解析几何**知识可知，一条**法线**对应**唯一一个垂直于该法线的平面**。在OpenGL中，法线的变换方式与顶点的变换方式略有不同。

设**齐次坐标下**平面方程为 $ax+by+cz+dw=0$，则行向量 $(a,b,c,d)$ 可以**唯一表示一张齐次平面**，其中 $a,b,c,d$ 中的至少一个非零。如果 $q$ 为非零实数，则 $(a,b,c,d)$ 和 $(qa,qb,qc,qd)$ 表示同一平面。若 $ax_0+by_0+cz_0+dw_0=0$，则点 $(x_0,y_0,z_0,w_0)^T$ 在平面 $(a,b,c,d)$ 上。

若 $p$ 为一齐次平面，$v$ 为一齐次顶点，则 **$v$ 位于平面 $p$ 上** 可表示为 $pv=0$。如果 $M$ 是一个**非奇异变换矩阵**，则 $pv=0$ 等效于 $pM^{-1}Mv=0$，即 $Mv$ 在平面 $pM^{-1}$ 上。因此，$pM^{-1}$ 是平面 $p$ 在变换 $M$ 下的象。

## 变换矩阵

下面列出了一些OpenGL中常用的变换操作及其对应的变换矩阵：

### 平移变换

对于一个平移指令 **（例如`glTranslate(x,y,z)`）** ，OpenGL会生成一个对应的平移矩阵T：

$T=\begin{bmatrix}
1 & 0 & 0 &x \\ 
0 & 1 & 0 &y \\ 
0 & 0 & 1 &z \\ 
0 & 0 & 0 &1 
\end{bmatrix}$

在一个齐次坐标系中，若记一点的原坐标为 $A=(x_0,y_0,z_0,w)^T$，则其经平移变换 $T$ 后的坐标则为 $A'=TA=(x_0+x,y_0+y,z_0+z,w)^T$

### 缩放变换

对于一个缩放指令 **（例如`glScale(x,y,z)`）** ，OpenGL会生成一个对应的缩放矩阵S：

$S=\begin{bmatrix}
x & 0 & 0 &0 \\ 
0 & y & 0 &0 \\ 
0 & 0 & z &0 \\ 
0 & 0 & 0 &1 
\end{bmatrix}$

在一个齐次坐标系中，若记一点的原坐标为 $A=(x_0,y_0,z_0,w)^T$，则其经缩放变换 $S$ 后的坐标则为 $A'=SA=(x \cdot x_0,y \cdot y_0,z \cdot z_0,w)^T$

### 旋转变换

对于一个旋转指令 **（例如`glRotate(a,x,y,z)`，参数中a为旋转角度，(x,y,z)为旋转轴向量（右手原则））** ，OpenGL会按如下步骤生成一个对应的旋转矩阵R：

1. 取 $v=(x,y,z)^T$ 并求出其单位向量 $u=\frac{v}{||v||}=(x',y',z')^T$ **（||v||为v的模）**
2. 令$S=\begin{bmatrix}
 0 & -z' & y' \\ 
z' & 0 & -x' \\ 
-y' & x' & 0 
\end{bmatrix}$，$M=uu^T+(cosa)(I-uu^T)+(sina)S$
3. 易见 $M$ 为一个3*3矩阵，设 $M=\{m_{ij}\}$，则$R=\begin{bmatrix}
 m_{11} &m_{12} & m_{13} & 0 \\ 
m_{21} & m_{22} & m_{23} &0 \\ m_{31} & m_{32} & m_{33} &0 \\ 0 & 0 & 0 &1 
\end{bmatrix}$

### 透视投影

对于一个透视投影指令 **（例如`glFrustum(l,r,b,t,n,f)`）** ，OpenGL会生成一个对应的变换矩阵P：

$P=\begin{bmatrix}
\frac{2n}{r-l} & 0 & \frac{r+l}{r-l} &0 \\ 
0 & \frac{2n}{t-b} & \frac{t+b}{t-b} &0 \\ 
0 & 0 & \frac{-(f+n)}{f-n} &\frac{-2fn}{f-n} \\ 
0 & 0 & -1 &0 
\end{bmatrix}$

### 正投影

对于一个正投影指令 **（例如`glOrtho(l,r,b,t,n,f)`）** ，OpenGL会生成一个对应的变换矩阵P：

$P=\begin{bmatrix}
\frac{2}{r-l} & 0 & 0 &\frac{r+l}{r-l} \\ 
0 & \frac{2}{t-b} & 0 &\frac{t+b}{t-b} \\ 
0 & 0 & \frac{-2}{f-n} &\frac{f+n}{f-n} \\ 
0 & 0 & 0 &1 
\end{bmatrix}$