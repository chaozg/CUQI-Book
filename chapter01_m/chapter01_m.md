---
authors:
  - name: Jasper Everink
---

(implicit-prior-chapter)=
# Chapter 11: BIPs with implicit prior

In this chapter, we discuss how to solve Bayesian inverse problems using implicit priors in CUQIpy. Recall from {ref}`implicit-priors` that we call priors implicit if the prior probability density $p(\mathbf{x})$ is either intractable or nonexistent.

Here, we focus on two implicit priors. First, we show how to construct implicit priors that combine variational regularization with Gaussian priors. Second, we show how to define priors using denoising algorithms. Enforcing prior information through generative models is not discussed in this chapter, and examples of such priors can be found in {ref}`PDE-based-heat-problem`. 

In both examples, we consider the relatively simple inverse problems of inferring a square signal, shown below, from observations of the signal through a forward model. This signal is chosen for simplicity, but also because it illustrates the ability of implicit priors to capture features in the inferred signal, such as sharp edges and positivity.

```{figure} figures/square_signal.jpg
:label: FigureSquare
:alt: Figure Square Signal
:width: 400px
:align: center
The square signal, which is used as the true signal in the examples in this chapter. The signal represents different quantities depending on the example, e.g., a conductivity field or an image.
```

Additional information about implicit priors and their implementation in CUQIpy can be found in {cite}`everink2025computational`, including theory and practical considerations like hyperparameter tuning, which we do not discuss in this chapter for brevity. 


