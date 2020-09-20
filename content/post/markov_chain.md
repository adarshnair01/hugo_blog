+++
title = "Discrete Markov-chain in layman's terms: Part 1"
description = "Explaining Markov Chain in layman terms"
tags = [
    "data",
    "science",
    "markov",
    "chain",
    "machine learning",
    "ai",
    "ml",
]
date = "2020-09-19"
categories = [
    "data science",
    "markov chain",
]
menu = "main"

math= true
+++

Because of current technology advances, machine learning nowadays is able to make decision close to what human would make, on its own. It was birthed from pattern recognition and the belief that computers will teach without being programmed to accomplish particular tasks; researchers involved in artificial intelligence needed to think if computers would learn from data. This repetitive view of machine learning is crucial because as models are exposed to current information, they are able to independently change. They learn from past calculations to make honest, repeatable conclusions and outcomes. It’s the field that’s not original – but one that has gained fresh strength.

In the hands of metereologists, ecologists, computer scientists, business engineers and other people who want to understand large phenomena, Markov chains will prove to be rather huge and powerful. For instance, the Google uses Page Rank algorithm to define the order of search results, is one form of Markov chain. Markov chain is a stochastic activity, but it differs from the common stochastic operation in a way that the Markov chain must be memory-less. That is, (the amount of) next actions are not dependent upon the ways that led up to the immediate state. That is called the Markov property.

# Problem Statement
Consider a labor who, at any given time $ t $ , is either jobless (state 1) or employed (state 2).
In terms of a Markov model, we have two states
> $ S \in \\{ jobless, employed\\} $

Suppose that, over a one month period,
A jobless labor finds a job with probability $ \alpha \in (0, 1) $.
>$ \mathbb P(jobless, employed) = \alpha $

An employed labor loses her job and becomes jobless with probability $ \beta \in (0, 1) $.
>$ \mathbb P(employed, jobless) = \beta $  

We can state transition probabilities in the form of a matrix</p>
$$P
= \left(
\begin{array}{cc}
    1 - \alpha & \alpha \\\\
    \beta & 1 - \beta
\end{array}
  \right)$$

Once we have the values $ \alpha $ and $ \beta $, we can address a range of questions, such as
* What is the average duration of employment?
* Over the long-run, what fraction of time will a labor jobless?
* Conditional on employment, what is the probability of becoming jobless at least once over the next 12 months?

# Formulate Problem
![markov_example](https://lh3.googleusercontent.com/pw/ACtC-3cb_hJasJEgfJ_kiSWOcLI1eQRbCJ0kGh_ijrdm3SbIVr-r5gc8RHHTmWq2UDMKBG9rH872bowGO5CekTPCU9oKechNInGLdaoebLgQnZg8s9vSvcfnJGPTnpe43eXy5tYGc2bYbGCe03kpuYoQFt8_6g=w934-h589-no?authuser=0)

We can create a transition matrix for any problem. For example, The probabilities of job conditions (modeled as either jobless or employed), given the state on the preceding month, can be represented by a transition matrix:

$$P
= \left[
\begin{array}{cc}
    0.6 & 0.4 \\\\
    0.3 & 0.7
\end{array}
  \right]$$

The matrix P represents the labor job model in which a employed month is 60% likely to be followed by another employed month, and jobless month is 70% likely to be followed by another jobless month.The columns can be labeled "jobless" and "employed", and the rows can be labeled in the same order.

*Note: The rows of P sum to 1: this is because P is a stochastic matrix*.

## Solution

As of now the labor is jobless. This is represented by a vector in which the "jobless" entry is 100%, and the "employed" entry is 0%:

$$ x^{(0)} = \left[\begin{array}{cc}
    1 & 0
\end{array}
  \right]$$

Status of first month can be predicted by:
$$
x^{(1)} = x^{(0)} \cdot P =
\left[\begin{array}{cc}
    1 & 0
\end{array}
  \right]
\left[
  \begin{array}{cc}
      0.6 & 0.4 \\\\
      0.3 & 0.7
  \end{array}
    \right]
    =\left[\begin{array}{cc}
        0.6 & 0.4
    \end{array}\right]
$$
Thus, there is a 60% chance that for first month also he will be jobless.

Let us predict status for second month in the similar manner.
$$
x^{(2)} = x^{(1)} \cdot P = x^{(0)} \cdot P^{2} =
\left[\begin{array}{cc}
    1 & 0
\end{array}
  \right]
\left[
  \begin{array}{cc}
      0.6 & 0.4 \\\\
      0.3 & 0.7
  \end{array}
    \right]^{2}
    =\left[\begin{array}{cc}
        0.48 & 0.52
    \end{array}\right]
$$
$$
x^{(2)} = x^{(1)} \cdot P =
\left[\begin{array}{cc}
    0.6 & 0.4
\end{array}
  \right]
\left[
  \begin{array}{cc}
      0.6 & 0.4 \\\\
      0.3 & 0.7
  \end{array}
    \right]
    =\left[\begin{array}{cc}
        0.48 & 0.52
    \end{array}\right]
$$

By passing months probability of employment for that labor is getting better.

I ran a script on this probability matrix with initial state. Below table shows state probability after each iteration.

| Iteration   | Jobless     | Employed    |
| ----------- | ----------- | ----------- |
| 1           | 1.0         | 0.0         |
| 2           | 0.6         | 0.4         |
| 3           | 0.444       | 0.556       |
| 4           | 0.4332      | 0.5668      |
| 5           | 0.42996     | 0.57004     |
| 6           | 0.42898     | 0.57101     |
| 7           | 0.42869     | 0.57130     |
| 8           | 0.42860     | 0.57139     |
| 9           | 0.42858     | 0.57142     |
| 10          | 0.42858     | 0.57142     |

We obtain the same result! In other words, the state vector converged to a steady-state vector. In this case that steady-state vector is

$$ x^{(0)} = \left[\begin{array}{cc}
    0.42858 & 0.57142
\end{array}
  \right]$$

## Steady state
The steady-state vector($ s_{ss} $) of the transition matrix $ P $ is the unique probability vector that satisfies this equation:
$$ P \cdot x_{ss} = x_{ss}$$

![markov_steady_state](https://lh3.googleusercontent.com/pw/ACtC-3c2jf_SJgWYMfvtg7qmdat_HZxbXFhUCbY63Zxp3WZ3rHDJKbejdh6SOP9wphOc6jNEXHjMNv2fLE4ezSkpIV-eVD0AqcPzfcpeVyH5udBNjhhFq7YMEsDFOAVYy-cCjGEVabf-Qw0TMkqxRBnajFcziw=w640-h480-no?authuser=0)

Irrespective of the starting state, eventually equilibrium will be achieved.

I hope you enjoyed basic introduction on discrete Markov Chains. Will continue further on my next post.

Thanks for reading!
