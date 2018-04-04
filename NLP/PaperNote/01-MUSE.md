# paper title
WORD TRANSLATION WITHOUT PARALLEL DATA
ICLR 2018
# What To Solve
bilingual vector space.
# How
## part 1: adversarial approach(GAN network)
include:
  - discriminator: $P_{\theta_D}$
    $$\mathcal L (\theta_D|W) = -\frac{1}{n}\sum_{i=1}^{n}{logP_{\theta_D}(source=1|W_{x_i})}-\frac{1}{m}\sum_{j=1}^{m}logP_{\theta_D}(source=0|y_j)$$
  - mapping: $W$
  $$\mathcal L (W|\theta_D) = -\frac{1}{n}\sum_{i=1}^{n}{logP_{\theta_D}(source=0|W_{x_i})}-\frac{1}{m}\sum_{j=1}^{m}logP_{\theta_D}(source=1|y_j)$$

$$x=\{x_1, ..., x_n\}$$
$$y=\{y_1,...,y_m\}$$
$$Wx=\{Wx_1,...,Wx_n\}$$
### train parameters and tricks
 - discriminator($P_{\theta_D}$): MP( 2 hidden layer with size 2048)
 - dropout rate: 0.1
 - include a smoothing coefficient s = 0.2 in the discriminator predictions(???)
 - activation func: Leaky-ReLU
 - batch size: 32
 - lr: 0.1
 - lr decay: 0.95 both for the $P_{\theta_D}$ and $W$($\alpha = \frac{1}{1+decay_rate*epoch_num}\alpha$)
 - learn rate dive 2 every time our unsupervised validation criterion decreases.
 - orthogonal constraint: $$W \leftarrow (1+\beta)W - \beta(WW^T)W$$
 $$W \leftarrow W + (1 - WW^T)\beta W$$
   - monolingual quality of the embeddings
   - training procedure more stable in our experiments
### validation
use CSLS translate 10k most frequent sourcewords, and use then compute the average cosine similarity between these deemed translations, and use this average as a validation metric.
$$\sum{cosine(Wx_{top10k}, CSLS(Wx_{top10k},y))}$$
## part 2: refinement
as the results are still not on par with the supervised approach. beacause:
 - adversarial approach tries to align all words irrespective of their frequencies. However, rare words have embeddings that are less updated and are more likely to appear in different contexts in each corpus, which makes them harder to align.
 - Under the assumption that the mapping is linear, it is then better to infer the global mapping using only the most frequent words as anchors.
### Base: Procrustes algorithm
$$W^* = \arg \min_{W \in O_d(\Bbb{R})}||WX-Y||_\mathbf{F}=UV^T, with \  U\Sigma V^T = \mathbf{SVD}(YX^T)$$

**the key of this step is to build high accuary synthetic parallel vocabulary**

### Method on synthetic parallel vocabulary
#### rules:
  - most frequent words
  - mutual nearest neighbors
#### methdo 1: NN(nearest neighbor)
#### methdo 2: ISF(inverted soft-max)
#### methdo 3: CSLS(CROSS-DOMAIN SIMILARITY LOCAL SCALING)
  - $\mathcal N_T(Wx_s)$: K target language words which is nearest neighbors of mapped source language word
  - $\mathcal N_S(y_t)$: K source language words which is nearest neighbors of mapped target language word
  - mean similarity: $$r_T(Wx_s)=\frac{1}{K}\sum_{y_t\in\mathcal{N}_T(Wx_s)}{cos(Wx_s, y_t)}$$
  - same as $r_S(y_t)$
  - $$CSLS(Wx_s, y_t) = 2 cos(Wx_s, y_t) - r_T(Wx_s) - r_S(y_t) $$
