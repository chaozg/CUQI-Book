# 5. Implicit priors

(implicit-paper-summary)=

Throughout the previous chapters and sections, many different priors have been constructed using CUQIpy distributions. These distributions implement the prior density $p(\mathbf{x})$, or equivalently the prior log density $\log(p(\mathbf{x}))$. These densities are used by general purpose samplers, such as those based on Metropolis-Hastings acceptance. However, not all samplers make use of the densities, some make use other quantities derived from the prior density, for example, the log density gradient $\nabla \log(p(\mathbf{x}))$. 

It is easy to compute $p(\mathbf{x})$ from $\log(p(\mathbf{x}))$ and vice versa, but computing the prior density from $\nabla \log(p(\mathbf{x}))$ can be very expensive as it requires solving a high-dimensional partial differential equation. For this reason want to classifiy priors differently based on the easy accesability of the prior density. The former we call **explicit priors** with all others being **implicit priors**.

In the paper {cite}`everink2025computational`, we identified some implicit priors that we made available in CUQIpy:

#### Parameterized implicit priors
Instead of directly assigning a prior density to the unknown parameter $\mathbf{x}$, it is common to parameterize this unknown using some generative model $G$ such that $\mathbf{x} = G(\mathbf{z})$. The new auxiliary unknown $\mathbf{z}$ fully determines $\mathbf{x}$, so an auxiliary prior density $p($\mathbf{z}$)$ fully determines the prior distribution of $\mathbf{x}$. However, for many generative models $G$, the prior density $p(\mathbf{x})$ is expensive to compute or does not even exist. Then it is more efficient to sample from the posterior by sampling from the auxiliary posterior $p(\mathbf{z}\mid \mathbf{y})$ and transform these samples back using the generative model.

This approach can be very useful for efficienty enforcing constraints, an example of solving a PDE-based inverse problem using this can be found at `PDE-based-heat-problem`.

#### Regularized linear randomize-then-optimize
Randomize-then-optimize is a framework for using optimization algorithms to sample from posteriors, allowing almost any efficient optimization algorithm to be used as an efficient sampler. Especially in the case where the likelihood corresponds to a linear inverse problem with additive Gaussian noise and the prior is Gaussian, sampling can be done very efficiently by solving randomized linear least squares problems. This naturally leads to applying regularization to this randomized linear least squares problem to incorporate additional prior information.

An example of the use of both linear randomize-then-optimize and its regularized variant can be found at {ref}`regularized-linear-rto`.

#### Langevin-based implicit priors
The unadjusted Langevin algorithm (ULA) is an example of a powerful sampling algorithm that uses the gradient of the log likelihood and the gradient of the prior log density $\nabla \log(p(\mathbf{x}))$. Further variants of Langevin-based algorithms have been developed that make use of other prior information, for example, Moreau-Yoshida ULA (MYULA) and Plug-and-Play ULA (PNP-ULA) both make use of denoisers instead of prior densities.

An example of the use of MYULA in CUQIpy can be found in {ref}`MYULA`.

More information on implicit priors can be found in the dedicated chapter {ref}`implicit-prior-chapter` and the summary of the paper {cite}`everink2025computational` in {ref}`implicit-paper-summary`.