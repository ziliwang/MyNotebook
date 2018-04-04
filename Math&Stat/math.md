#### Covariance
$$Cov(X, Y) = E[(X-E(X))(Y-E[Y])] = E[XY]-E[X]E[Y]$$
#### Covariance Matrix
$X\in \Bbb R^{n*m}$, where $n$ samples and $m$ variables. if $\Bbb E[x]=0$, we called centered matrix. if not, then do: $$x_{ij}=x_{ij} - \Bbb E[x_{* :j}]$$
then covariance matrix $Var[x]$:
$$Var[x] = \frac{1}{n-1}X^TX$$
$Var[x]_ {ij}=Cov(x_i, x_j)$
#### Entropy
Shannon defined the entropy $H$ (Greek capital letter eta) of a discrete random variable $X$ with possible values ${x_1, ..., x_n}$ and probability mass function P(X) as:
$$H(x)=\sum_{i=1}^{n}{P(x_i)I(x_i)}=-\sum_{i=1}^{n}{P(x_i)\log_bP(x_i)}$$
#### Cross Entropy
The cross entropy for the distributions $P$ and $Q$ over a given set is defined as follows:
$$H(P,Q)=E_P[- \log Q]=-\sum_i{P(i) \log Q(i)}=H(P) + D_{KL}(P||Q)$$
#### Kullback–Leibler divergence (also called relative entropy)
For discrete probability distributions $P$ and $Q$, the Kullback–Leibler divergence from $Q$ to $P$ is defined to be:
$$D_{KL}(P||Q)=-\sum_i{P(i)\log\frac{Q(i)}{P(i)}}$$
$$=-\sum_i{P(i) \log Q(i)} + \sum_i{P(i) \log P(i)}=H(P,Q)-H(P)$$
ps.:
  - KL散度表示P，Q两概率分布的差异。最小化KL散度，也就是最小化相对熵。
  - The cross entropy $H(p,q)$ can be interpreted as the number of bits per message needed (on average) to encode events drawn from true distribution $p$, if using an optimal code for distribution $q$.
  - $D_{KL}(p||q)$ can be interpreted as the expected number of **extra** bits per message needed to encode events drawn from true distribution $p$, if using an optimal code for distribution $q$ rather than $p$.
  - KL散度是两分布的差异，而交叉熵是q分布来表示p分布所需的信息量。
