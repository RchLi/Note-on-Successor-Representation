# Note on Successor Representation

## From value function To SR
Succesor representation provides a simple way to decompose value function into reward dynamic and state transition dynamic. Below is the mathematical derivation.

$$
\begin{align*}
    V(s) &= \sum_{k=0}^\infty \gamma^k E[R_{t+k+1} | S_t = s] \\
    &= \sum_{k=0}^\infty \gamma^k E[E[R_{t+k+1}|S_{t+k}, S_t=s]] &\text{; } E[A] = E[E[A|B]]\\
    &= \sum_{k=0}^\infty \gamma^k\sum_{s^\prime}E[R_{t+k+1}|S_{t+k}=s^\prime, S_t = s]P(S_{t+k}=s^\prime|S_t=s) \\
    &= \sum_{k=0}^\infty \gamma^k\sum_{s^\prime}E[R_{t+1}|S_{t}=s^\prime]P(S_{t+k}=s^\prime|S_t=s) &\text{; Markov property}\\
    &= \sum_{s^\prime} \sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s)E[R_{t+1}|S_{t}=s^\prime]\\
    &= \sum_{s^\prime} E[R_{t+1}|S_{t}=s^\prime]\sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s)
\end{align*}
$$
Now let reward dynamic be captured by $r(s) = E[R_{t+1}|S_t=s]$ and state transition dynamic captured by **successor representation**   $M(s, s^\prime) =\sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s)$, we get
$$
V(s) = \sum_{s^\prime} r(s^\prime)M(s, s^\prime)
$$

For simplicity, notation for policy $\pi$ is ommited in the derivation. Note that both $r(s)$ and $M(s,s^\prime)$ is affected by $\pi$.

## Learning SR
Notice that 

$$
\begin{align*}
  M(s, s^\prime) &=\sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s) \\
&= E[\sum_{k=0}^\infty\gamma^k \mathbb{I}(S_{t+k}=s^\prime)|S_t=s]
\end{align*}
$$

Thus SR can be learned with traditional MC method or TD learning.
