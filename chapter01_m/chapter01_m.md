# Chapter 11: BIPs with implicit prior

(implicit-prior-chapter)=

In this chapter, we discuss how to solve Bayesian inverse problems using implicit priors in CUQIpy. Recall from {ref}`implicit-paper-summary` that we call priors implicit if the prior probability density $p(\mathbf{x})$ is either intractable or nonexistent.

We have already seen the example of constraints through generative models in `PDE-based-heat-problem`. In this chapter, we focus on two other implicit priors. First, in `regularized-linear-rto`, we show how to construct implicit priors that combine variational regularization with Gaussian priors. Second, in {ref}`MYULA`, we show how to define priors using denoising algorithms.

In both example, we consider the relatively simple inverse problems of inferring a square signal, shown below, from measuring the convolution of the signal. This signal is chosen for simplicity, but also because it illustrates the ability of implicit priors to capture features in the inferred signal, such as sharp edges and positivity.

```{figure} figures/square_signal.jpg
:label: FigureSquare
:alt: Figure Square Signal
:width: 400px
:align: center
The square signal, which is used as the true signal in the examples in this chapter. The signal represents different quantities depending on the example, e.g., a conductivity field or an image.
```

Additional information about implicit priors and their implementation in CUQIpy can be found in {cite}`everink2025computational`, including theory and practical considerations like hyperparameter tuning, which we do not discuss in this chapter for brevity. 
