# A Neural Stochastic Volatility Model  
* [原文](https://arxiv.org/abs/1712.00504)

#### abstract  
* The authors propose a recurrent neural network approach for constructing a
stochastic volatility model for financial time series. They introduce an
inference network based on a recurrent neural network that computes the
approximation to the posterior distribution for the latent variables given the
past data. This variational approximation is used to maximize the marginal
likelihood in order to learn the parameters of the model. The proposed method
is validated in experiments with synthetic and real-world time series, showing
to outperform parametric GARCH models and a Gaussian process volatility model.

#### review of this paper
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
5. ...

#### Introduction
* The volatility of the price movements reflects the **ubiquitous
uncertainty** within financial markets
* volatility is important for **investment, risk management, security valuation
and monetary policy making**
* Volatility is measured typically by employing the **standard
deviation** of price change in a fixed time interval, such as
a day, a month or a year.
* One of the primary challenges
in designing volatility models is to identify **the existence
of latent stochastic processes** and to characterise the underlying
dependences or interactions between variables within
a certain time span
* 過去的方法: ARCH model (Engle 1982) and the extension, generalised ARCH (GARCH) (Bollerslev
1986). As an alternative to the GARCH model family, the class
of stochastic volatility (SV) models specify the variance
to follow some latent stochastic process (Hull and White
1987).
* 此篇的方法: In this paper, we take a fully **data driven** approach and determine
the configurations with as few exogenous input as
possible, or even purely from the historical data
* We propose
a neural network re-formulation of stochastic volatility
by leveraging stochastic models and recurrent neural networks
(RNNs)
* the proposed model is rooted in **variational inference** and
equipped with the latest advances of stochastic neural networks.
The model inherits the fundamentals of **SV model**
and provides a general framework for volatility modelling;
it extends previous sequential frameworks with autoregressive
and bidirectional architecture and provide with a more
systematic and volatility-specific formulation on stochastic
volatility modelling for financial time series. We presume
that the **latent variables** follow a Gaussian autoregressive
process, which is then utilised to model the variance process.
two major classes of volatility models in financial study as the special
cases with specific weights and activations on neurons.
#### Related Work
* 略
#### Preliminaries: Volatility Models
* we presume the conditional variance
to have dependency – either **deterministic** or **stochastic** – on
history, which results in two categories of volatility models.
* **Deterministic Volatility Models: the GARCH
Model Family**  
  * 略
* **Stochastic Volatility Models**  
  * 略
* **Volatility Models in a General Form**  
  * 略
#### Neural Stochastic Volatility Models
* In this section, we establish the neural stochastic volatility
model (NSVM) for volatility estimation and prediction.

