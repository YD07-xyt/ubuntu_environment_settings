# ros2学习

# 参考:
https://fishros.com/




### 坐标变换 
https://fishros.com/d2lros2/#/humble/chapt6/get_started/1.%E7%A9%BA%E9%97%B4%E5%9D%90%E6%A0%87%E6%8F%8F%E8%BF%B0  
平移旋转复合变换
 $$\boldsymbol{_{C}^{A}P = {_{B}^{A}R} \cdot {_{C}^{B}P} + {_{B}^{A}P}}$$


### 绕某一轴旋转$\boldsymbol{\theta}$角的旋转矩阵
 
新的坐标系 绕原坐标系 某一坐标轴旋转任意角度时，对应旋转矩阵如下：
 
绕
$\boldsymbol{x}$
轴旋转
$\boldsymbol{\theta}$
后姿态矩阵
 
$$
R(x,\theta) = \begin{bmatrix} 
1 & 0 & 0 \\ 
0 & \cos\theta & -\sin\theta \\ 
0 & \sin\theta & \cos\theta 
\end{bmatrix}
$$
 
绕
$\boldsymbol{y}$
轴旋转
$\boldsymbol{\theta}$
后姿态矩阵
 
$$
R(y,\theta) = \begin{bmatrix} 
\cos\theta & 0 & \sin\theta \\ 
0 & 1 & 0 \\ 
-\sin\theta & 0 & \cos\theta 
\end{bmatrix}
$$
 
绕
$\boldsymbol{z}$
轴旋转
$\boldsymbol{\theta}$
后姿态矩阵
 
$$
R(z,\theta) = \begin{bmatrix} 
\cos\theta & -\sin\theta & 0 \\ 
\sin\theta & \cos\theta & 0 \\ 
0 & 0 & 1 
\end{bmatrix}
$$
 
（可用于坐标系旋转、位姿变换等场景，代入
$\theta$
值即可计算具体旋转矩阵 ）


### 四元数

https://krasjet.github.io/quaternion/

https://github.com/CatOnly/CrashNote/tree/master/LinearAlgebra


https://qiita.com/HMMNRST/items/0a4ab86ed053c770ff6a


如果我们想让 2D 空间中任意一个向量 v 旋转 θ 度，那么我们就可以使用
这个矩阵对 v 进行变换：

**Theorem 1: 2D 旋转公式（矩阵型）**:  
$$R(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$$  
$$v' = R(\theta)v$$  

**Theorem 2: 2D 旋转公式（复数积型）**
 $$ v' = zv   
    = (\cos(\theta) + i\sin(\theta))v $$ 

**Theorem 3: 2D 旋转公式（指数型）**

如果我们定义  $ r = \|z\| $，我们就得到了复数的极坐标形式  
$ z = re^{i\theta}$ 。
 
 $$ v' = re^{i\theta}v. $$ 


如果仅需要旋转  $\theta$ 度的话，可以令缩放因子  $r = 1$，那么变换后的结果就是：
 $$ v' = e^{i\theta}v $$ 

***这三种 2D 旋转公式其实都是等价的，根据不同的需求我们可以使用旋转的不同形态。在我们之后讨论四元数的时候，我们也会看到非常类似的公式。***


如果我们有两个代表 2D 旋转的单位复数  $ z_1 = \cos(\theta) + i\sin(\theta) $， $ z_2 = \cos(\phi) + i\sin(\phi) $ 以及一个向量  $ v = x + yi $。

所以，当我们对两个 2D 旋转进行复合时，而且与施加的次序无关，这个等效变换是：


 $$ z_{\text{net}} = (\cos(\theta) + i\sin(\theta))(\cos(\phi) + i\sin(\phi)) $$ 

 $$ = \cos(\theta + \phi) + i\sin(\theta + \phi). $$ 

***复合时，所得到的变换  $ z_{\text{net}} $ 仍是一个旋转，旋转的旋转角是  $ z_1 $ 与  $ z_2 $ 旋转角之和。***


### 齐次矩阵
有没有一种方法，可以让旋转矩阵和平移向量合并到同一个矩阵里呢？

答案是有的，我们可以将  
$3 \times 3$
 的旋转矩阵和  $3 \times 1$ 的平移矩阵进行组合，并添加一行  $(0, 0, 0, 1)$ 使其变成一个  $4 \times 4$ 的方阵，其组合方式如下：

**旋转矩阵**  


$$R = \begin{bmatrix} r_{11} & r_{12} & r_{13} \\ r_{21} & r_{22} & r_{23} \\ r_{31} & r_{32} & r_{33} \end{bmatrix}$$  
（旋转矩阵）

**平移矩阵**  
$$P = \begin{bmatrix} x \\ y \\ z \end{bmatrix}$$  
 （平移矩阵）

**合并成齐次变换矩阵** 
 
 $$T = \begin{bmatrix} r_{11} & r_{12} & r_{13} & x \\ r_{21} & r_{22} & r_{23} & y \\ r_{31} & r_{32} & r_{33} & z \\ 0 & 0 & 0 & 1 \end{bmatrix}$$   
（齐次矩阵）

矩阵是支持分块运算的，我们可以将上面的矩阵进行分块
$$
T = \begin{bmatrix} R & P \\ 0 & 1 \end{bmatrix} $$    
（齐次矩阵）
