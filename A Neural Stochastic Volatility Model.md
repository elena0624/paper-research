# A Neural Stochastic Volatility Model  
* [原文](https://arxiv.org/abs/1712.00504)

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
5. ...

### Introduction
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
### Related Work
* 略
### Preliminaries: Volatility Models
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
### Neural Stochastic Volatility Models
* In this section, we establish the neural stochastic volatility
model (NSVM) for volatility estimation and prediction.
#### Generating Observable Sequence
* hxt hzt denote the hidden states of the corresponding
RNNs. The MLPs map the hidden states of RNNs into
the means and deviations of variables of interest. The collection
of parameters Φ is comprised of the weights of RNNs
and MLPs. NSVM relaxes the conventional constraint that
the latent variable **zt is N (0, 1)** in a way that zt is no longer
i.i.d noise but **a time-varying signal from external process
with self-evolving nature**. As discussed above, this relaxation
will benefit the effectiveness in real scenarios
* One should notice that when the latent variable zt is obtained,
e.g. by inference (see details in the next subsection),
**the conditional distribution pΦ(X|Z)** (Eq. (14)) will be involved
in generating the observable xt instead of the joint
distribution **pΦ(X, Z)** (Eq. (15)). This is essentially the scenario
of predicting future values of the observable variable
given its history. We will use the term “generative model”
and will not discriminate the unconditional generative model
or the conditional one as it can be inferred in context.
這段是什麼意思?????
#### Inferencing the Latent Process
* The neural network implementation of the model, referred
to as the inference network, is designed to equip a cascaded
architecture with an autoregressive RNN and a bidirectional
RNN, where the bidirectional RNN incorporates both the
forward and backward dependencies on the entire observations
whereas the autoregressive RNN models the temporal
dependencies on the latent variables
#### Forecasting Observations in Future
* 略
### Experiment
#### Dataset and Pre-processing
* **Data**
  * The raw dataset comprises **162 univariate time series** of the
daily closing stock price, chosen from China’s A-shares and
collected from 3 institutions. 選擇標準: 存續期間長、缺值少
* **Pre-processing**
  * 移除abnormalities, 並內插補齊(by 20天的stochastic regression imputation並用gaussian distribution依據回歸的mean跟variance取)
  * The series is then transformed from actual prices st
into log-returns xt = log(st/st−1) and normalised
  * Moreover,
we combinatorically choose a predefined number **d** out
of 162 univariate log-return series and **aggregate** the selected
series **at each time step** to form a **d-dimensional multivariate
time series**, the choice of d is in accordance(按照) with the rank of
correlation，得出比原本大很多的dataset(c162取d)
#### Baseline
* We select several **deterministic volatility models** from the
GARCH family as baselines:
  1. Quadratic models: ARCH(1); GARCH(1,1); GJR-GARCH(1,1,1);
  2. Absolute value models: AVARCH(1); AVGARCH(1,1); TARCH(1,1,1);
  3. Exponential models: EARCH(1); EGARCH(1,1);
* Moreover, two **stochastic volatility models** are compared:
  1. MCMC volatility model: stochvol;
  2. Gaussian process volatility model GP-Vol 
* And more...
#### Model Implementation
