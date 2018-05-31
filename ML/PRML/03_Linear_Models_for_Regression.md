## 3.1 线性基函数模型
#### 线性回归公式
$$y(\mathbf x, \mathbf w)=\mathbf w^T \phi(\mathbf x)$$
$\phi(\mathbf x)$表示基函数
#### 常见的基函数
##### 高斯基函数（gaussian basis function）
$$\phi_j(x) = \exp{-\frac{(x-u_j)^2}{2s^2}}$$
$u_j$控制基函数的位置，$s$控制基函数空间大小。
##### sigmoid基函数
$$\phi_j(x)=\sigma(\frac{x-u_j}{s})$$
$$\sigma(a) = \frac{1}{1+\exp(-a)}$$
##### tanh基函数
$$\tanh(a)=2\sigma(a)-1$$
### 3.1.1 最大似然和最小均方
#### 最大似然
线性回归的损失函数可被视作gaussian noise model下的最大似然 。
线性回归公式
$$t = y(\mathbf x, \mathbf w) + \epsilon$$
其中$\epsilon$是均值为0，precision（方差倒数）为$\beta$的正态分布。所以：
$$p(t|\mathbf x, \mathbf w, \beta) = \mathcal N(y(\mathbf x, \mathbf w), \beta^{-1})$$
考虑到$\mathbf x$会一直出现在条件中，所以后面的公式就给省略掉了。
$$\ln p(\mathbf | \mathbf w, \beta)=\sum_{n=1}^N{\ln \mathcal N(t_n|\mathbf w^T \phi(\mathbf x_n), \beta^{-1})}=\frac{N}{2} \ln \beta-\frac{N}{2} \ln (2\pi)-\beta E_D(\mathbf w)$$
$$E_D(w)=\frac{1}{2}\sum_{n=1}^{N}{\{t_n- \mathbf w^T\phi(\mathbf x_{n})\}}^2$$
根据最大似然，最大化$\ln p$就等同于最小化$E_D$,log似然的梯度：
$$\nabla \ln p(\mathbf | \mathbf w, \beta)=\sum_{n=1}^{N}{\{t_n-\mathbf w ^ T \phi(\mathbf x_n)\}}\phi(\mathbf x_n)^T$$
令$\nabla = 0$:
$$\mathbf w_{ML} = (\Phi ^T \Phi )^{-1} \Phi ^ T$$
其中：
$$\Phi = \ [ \left(\begin{array}{ccc}
\phi_0(\mathbf x_1) & \phi_1(\mathbf x_1) & \cdots & \phi_{M-1}{\mathbf x_1}  \\
\phi_0(\mathbf x_2) & \phi_1(\mathbf x_2) & \cdots & \phi_{M-1}{\mathbf x_2} \\
\vdots & \vdots & \ddots & \vdots \\
\phi_0(\mathbf x_N) & \phi_1(\mathbf x_N) & \cdots & \phi_{M-1}{\mathbf x_N}
\end{array}
\right) \ ] $$
### 3.1.2 最小均方的几何意义
简单来讲，基函数构成向量空间$S$，$\mathbf y$是由基函数向量的线性组合构成的，所以$\mathbf y$也在$S$里，对于向量$\mathbf t$，最小均方的几何意义在于最小化$\mathbf t$和$\mathbf y$的几何距离的平方。
### 3.1.3 连续学习（Sequential learning）
sequential algorithm，也被称为on-line algorithm，其定义为：每次输入数据点，更新模型参数。
#### 随机梯度下降（stochastic gradient descent， SGD）
$$\mathbf w^{(n+1)} = \mathbf w^{(n)} - \eta \nabla E_n$$
#### 最小均方算法（least-mean-squares，LMS）
$$\mathbf w = \mathbf w + \eta(t_n- \mathbf w \phi_n)\phi_n$$
### 3.1.4 正则化最小均方
##### 权值衰减（weight decay）
使用正则子在学术上称作权值衰减，其鼓励不被支持的数据权值减为0。
##### 参数缩放（parameter shrinkage）
权值衰减是参数缩放的实例。参数缩放是统计学概念。
##### 岭回归
又称作二范式，$\sum_{j=1}^{M}|w_j|^q$,q=2。常用
##### 拉索（lasso）回归
又称作一范式，$\sum_{j=1}^{M}|w_j|^q$,q=1.
### 3.1.5 多维输出
#### 最大似然
$$y(\mathbf x, \mathbf W)=\mathbf W^T\phi(\mathbf x)$$
$$W_{ML}=(\Phi^T\Phi)^{-1}\Phi^T\mathbf T$$
