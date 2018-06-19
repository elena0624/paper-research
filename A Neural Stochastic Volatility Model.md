## [A Neural Stochastic Volatility Model](https://arxiv.org/abs/1712.00504)
### abstract  
* The authors propose a recurrent neural network approach for constructing a
stochastic volatility model for financial time series. They introduce an
inference network based on a recurrent neural network that computes the
approximation to the posterior distribution for the latent variables given the
past data. This variational approximation is used to maximize the marginal
likelihood in order to learn the parameters of the model. The proposed method
is validated in experiments with synthetic and real-world time series, showing
to outperform parametric GARCH models and a Gaussian process volatility model.

### review of this paper
(https://openreview.net/forum?id=B1IzH7cxl)
1. This paper=> one-timestep-ahead forcast. Can do longer-horizon forecasts
2. Better to look into R packages such as `stochvol’ and ‘fGarch’ to get implementations of a variety of models that can serve as useful baselines.
3. The method proposed seems technically correct, with the exception that in
equation (19) the inference model is doing filtering and not smoothing, in the
sense that the posterior for z_t' only depends on those other z_t and x_t
values with t<t', but in the true posterior p(Z|X) each z_t depends on all the
X.
4. 前篇有類似概念 Sequential Neural Models with Stochastic Layers Fraccaro, Marco and S\o nderby,
S\o ren Kaae and Paquet, Ulrich and Winther, Ole In NIPS 2016.
5. 
