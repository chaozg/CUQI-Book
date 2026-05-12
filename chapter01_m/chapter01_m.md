# Chapter 11: BIPs with implicit prior

(implicit-prior-chapter)=

> ⚠️ **Contents to be added:** Add intro to the chapter. 

> ⚠️ **This is just a chapter concept.. not finalized yet** 

Recall from {ref}`implicit-prior-section`

- short recap of what are implicit priors, and thier categoraization, refer to previous section on implicit priors.

- What we present in this chapter:
  - A relatively simple BIP examples that use the second and third type of implicit priors (an examples of the first type can be found in {ref}`PDE-based-heat-problem`)
  - In both examples, we infer a square signal, shown below, which represents different quantities depending on the example. The signal is chosen for simplicity, but also because it illustrates the ability of implicit priors to capture features in the inferred signal, such as sharp edges and positivity.

```{figure} figures/square_signal.jpg
:label: FigureSquare
:alt: Figure Square Signal
:width: 400px
:align: center
The square signal, which is used as the true signal in the examples in this chapter. The signal represents different quantities depending on the example, e.g., a conductivity field or an image.
```
- can talk a bit about implict prior limitations

Refer to {cite}`everink2025computational` for additional theoretical background, details about the implicit prior framework in CUQIpy and additional examples, including combining implicit priors with hyperparameters, which we do not discuss in this chapter for brevity. 


