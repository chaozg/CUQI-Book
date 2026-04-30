# Errors and Uncertainties and Why They Matter

Measured data inevitably contain errors, and we must understand how such errors influence the results that we compute. In other words, we want to understand the uncertainties in our results caused by
the errors in the data. The CUQIpy package provides computational methods that allow us to do that, and this chapters provides the conceptual background for formulating and performing this uncertainty quantification.

__Errors__ in measured data are unavoidable.
They have many causes, such as imperfections in the measurement device
and spurious signals that we cannot avoid recording.
In this work we consider the errors to be random (as opposed to
deterministic or systematic errors), and we often know -- or can estimate -- their size
and their statistical distribution.

__Uncertainty__ is, by definition, ``a lack of sureness about something.''
In our context it refers to the fact that random data errors inevitably lead to
an error in the computed solution, and hence this solution has some degree
of uncertainty. It is desirable to characterize this uncertainty; for example, we want
to know the size and properties of the uncertainty.

__Quantification__ refers, in this respect, to the act of
rigorously determining the amount and type of uncertainty in the solution,
given statistical information about the data errors.
This is done using well-defined mathematical/statistical methods and tools.
Uncertainty quantification implies that we want more details than just, e.g.,
a bound for the error in the solution.

There are potentially other types of errors than those coming from the
measured data.
We use a mathematical model
to describe the data, and this model may also be influenced by errors
e.g., when we neglect second-order terms in complex models or when
some model parameters are slightly incorrect.
Moreover, our computations are always influenced, to some degree,
by floating-point errors on the computer [B, \S 1.4].
Neither type of errors can be handled by the CUQIpy software, and we
will therefore not discuss them here.

It is instructive to illustrate the uncertainty due to data errors
with two simple examples of parameter estimation.
The first problem in linear, and we have an explicit formula for the
solution's covariance matrix which helps illustrate basic aspects of
uncertainty quantification.
The second problem is nonlinear and thus well suited for illustrating
how computational uncertainty quantification can be performed in practise
when no analytical expressions are available.

## Example 1: Linear regression.

We are given a linear function
$$f(t) = \alpha\, t + \beta \ ,$$
where the two parameters $\alpha$ and $\beta$ are unknown.
We assume that the noisy data $(t_i,y_i)$, $i=1,2,\ldots,m$ are given by
