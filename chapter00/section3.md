# Prior Information and Bayesian Inverse Problems

How do we supply prior information about a solution to an inverse problem,
in order to make it well defined and stable with respect to data errors?
The key idea is that we must identify important properties of the
desired solution, and then impose these properties when solving the problem.

- We may know that the size of the solution elements, or the size of
a derivative of the solution, cannot be large.
A small size of the solution's derivative implies that the solution is smooth.
- We may know that the solution vector should be sparse, i.e., it should have
many zero elements.
An astronomer may want to impose sparsity on the pixels of a deblurred image of
the night sky in order to improve the sharpness of the image.
- We may know that the solution must have certain features that we can
conveniently express using a carefully selected basis.
If the solution is known to be periodic then we should use a
trigonometric basis.

One way to impose such prior information is to use a method called
regularization [H10, N98], where we minimize a linear combination of
a data-fitting term and a regularization term that
penalizes solutions that do not adhere to the prior information.
As an example we mention Tikhonov regularization, which some readers may
already be familiar with, and which takes the form
$$
    \min_x \| A\, x - b \|_2^2 + \lambda^2 \, \| x \|_2^2 \ .
$$
Here, $\lambda$ is a parameter that balances the weight given to
the two objectives of fitting the data and penalizing a large norm.
Assuming again iid Gaussian noise in the data vector $b$, the
regularized solution follows a Gaussian distribution with covariance matrix
$\Sigma = \sigma^2 \bigl( A^TA + \lambda^2 I\bigr)^{-1}$.
The flexibility of regularization methods lies in the fact that
we can often find regularization terms (such as $\| x \|_2^2$)
that correspond to our prior information.

A different approach to solving inverse problem - which is the one that underlies uncertainty quantification and CUQIpy - is to formulate the inverse problem in a statistical framework in the form of a **Bayesian inverse problem**. Here, both the data $b$ and the solution $x$ are considered to be a random variables. Unlike traditional regularization methods that seek a single solution, the Bayesian approach treats the inverse problem as a statistical question, producing a full probability distribution for the solution~$x$. This is called the posterior distribution and it accounts for observational noise, uses prior information about the solution, and provides a complete quantification of uncertainty in the solution. See, e.g., [CS] for details.

To understand Bayesian inverse problems and the way they are formulated and used in CUQIpy, we need to introduce four important statistical tools such that they are readily available in the rest of the book. See, e.g., [CS, Chapter1] for more details. For simplicity we consider the linear forward model $b = A\, x$ where $A$ is a matrix, $b$ is the measured data, and $x$ is the solution.

**Data distribution** $\pi(b | x)$. This is a statistical distribution that specifies how likely it is to observe the data $b$ given the parameter or parameter-vector $x$. A key point is that we assume the noisy data can be explained by a forward model (here $b = A\, x$), and therefore the data distribution is conditioned in the variable~$x$. The second key point is that we assume a statistical description of the noise, and this assumption informs the specific expression for $\pi(b | x)$.

**Likelihood function** $L(x | b=b_{\mathrm{obs}})$. We obtain the likelihood function from the data distribution
by fixing the variable $b$ to be the observed data $b_{\mathrm{obs}}$. Hence, the likelihood function quantifies the probability of observing the noisy data $b_\text{obs}$ for each possible value of $x$, according to the predictions made by the forward model. As an example, for our linear forward model and with iid Gaussian noise we have
$$
    L(x | b=b_{\mathrm{obs}}) \propto
    \exp\biggl( - \frac{\|A\, x-b_{\mathrm{obs}}\|_2^2}{2\,\sigma^2} \biggr)\ .
$$

**Prior $\pi(x).$** This is a distribution function that expresses our knowledge, or belief, about the solution $x$ to the inverse problem. In Bayesian inverse problems it is used to enforce that we prefer solutions that adhere to our prior knowledge, and it plays the same role as the regularization term in classical regularization methods. The prior may be determined from past information or previous experiments, or it can express a subjective assessment of a domain expert [Rob, Chapter 3].

**Posterior $\pi(x | b_{\mathrm{obs}}).$** This  function expresses the probability of $x$ according to the measured data as well as our prior information. Hence, it is conditioned on $b_{\mathrm{obs}}$ and it expresses what is known about the solution after the data has been collected and the prior is imposed. The aim of a Bayesian inverse problem is to characterize and compute this probability function.

We note that some presentations of Bayesian inverse problems skip the introduction of the data distribution $\pi(b | x)$.
We include it in CUQIpy and in this book, because we believe this makes it easier and more intuitive to formulate and understand how the forward model and the noise model enter the likelihood function.

Given these important tools, **Bayes' theorem** from statistics (see, e.g., [CS, \S 1.2.2]) gives the following expression for the posterior:
$$
    \pi(x|b_{\mathrm{obs}}) = \frac{L(x | b=b_{\mathrm{obs}}) \, \pi(x)}{\pi(b)} \ .
$$
Here, the denominator (called the marginal probability or marginal distribution) is a constant with respect to $x$; it can always be determined such that the fraction integrates to~1. Throughout, we will therefore write
$$
    \pi(x|b_{\mathrm{obs}}) \propto L(x | b=b_{\mathrm{obs}}) \, \pi(x) \ .
$$
The important lesson here is that in order to quantify the uncertainties in $x$ in a Bayesian inverse problem, we need to specify the data distribution (i.e., the forward model and the distribution of the noise) as well as
the prior for the solution. A key point here is that the prior, when properly chosen, helps take care of the violation
of the Hadamard conditions in an ill-posed problem. In the following chapters we have much more to say about all this.

In Bayesian inverse problems and uncertainty quantification the goal is thus to determined the posterior distribution for $x$. We need to know its "shape" and characteristics because it tells us everything we want to know about the random variable $x$. For example, we can produce point estimates of $x$, and we can compute variances, covariances, and higher-order moments.