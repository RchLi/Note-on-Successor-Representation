# Note on Successor Representation
Succesor representation provides a simple way to decompose value function into reward dynamic and state transition dynamic. Below is the mathematical derivation.

$$
\begin{align*}
    V(s) &= \sum_{k=0}^\infty \gamma^k E[R_{t+k+1} | S_t = s] \\
    &= \sum_{k=0}^\infty \gamma^k E[E[R_{t+k+1}|S_{t+k}, S_t=s]] &\text{; } E[A] = E[E[A|B]]\\
    &= \sum_{k=0}^\infty \gamma^k\sum_{s^\prime}E[R_{t+k+1}|S_{t+k}=s^\prime, S_t = s]P(S_{t+k}=s^\prime|S_t=s) \\
    &= \sum_{k=0}^\infty \gamma^k\sum_{s^\prime}E[R_{t+k+1}|S_{t+k}=s^\prime]P(S_{t+k}=s^\prime|S_t=s) &\text{; }E[R_{t+k+1}|S_{t+k}, S_t]=E[R_{t+k+1}|S_{t+k}]=E[R_{t+1}|S_{t}]\\
    &= \sum_{s^\prime} \sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s)E[R_{t+1}|S_{t}=s^\prime]\\
    &= \sum_{s^\prime} E[R_{t+1}|S_{t}=s^\prime]\sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s)
\end{align*}
$$
Now let reward dynamic be captured by $r(s) = E[R_{t+1}|S_t=s]$ and state transition dynmic captured by **successor representation**   $M(s, s^\prime) =\sum_{k=0}^\infty\gamma^kP(S_{t+k}=s^\prime|S_t=s)$, we get
$$
V(s) = \sum_{s^\prime} r(s^\prime)M(s, s^\prime)
$$