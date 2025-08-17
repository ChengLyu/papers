# Papers

## Reinforcement Learning

[*Swift-Sarsa: Fast and Robust Linear Control*](https://www.arxiv.org/abs/2507.19539)

Learn value function. Discrete action space. Linear control.
$$v_{t-1,t}[action] = \sum_{i\in\text{feature dimension}}w^{action}_{t-1}[i]\phi_t[i]$$
TD error for learning:
$$\delta'_t = r_t + \gamma v_{t-1,t}[action_t] - v_{t-2, t-1}[action_{t-1}]$$
Difference over SwiftTD: **eligibility vector** update rule. Policy: $\epsilon$-greedy or softmax. Experiment: $n$ dimension observation only has the first $m$ dimensions valid ($m << n$), with the remaining dimensions noisy. The controler can learn the valid signals.

[*SwiftTD:A Fast and Robust Algorithm for Temporal Difference Learning*](https://rlj.cs.umass.edu/2024/papers/Paper111.html)

"Predicting the future is also a way to encode knowledge about the world."

What does "Temporal Difference" mean more specifically?
- Ref: **Sutton, R. S. (1988). Learning to predict by the methods of temporal differences. Machine Learning.**

$\lambda$-Return:
$$G^{\lambda}_t := (1-\lambda)\sum_{n=1}^{\infty}\lambda^{n-1}G_{t:t+n}$$
where
$$G_{t:t+n} := r_{t+1} + \gamma r_{t+2} + \ldots + \gamma^{n-1}r_{t+n} + \gamma^n v_{t+n}$$
Here $v_{t+n}$ is the agent's estimate of the sum of fututure discounted rewards at time $t+n$.

**Intuition: Average over time spanned discounted rewards with agent's estimation.**

It's the proxy loss for the performance/inference evaluation error
$$\text{Lifetime error}(T)=\frac{1}{T}\sum_{t=1}^T(v_t - \sum_{j=t+1}^{T}\gamma^{j-t-1}r_j)^2$$

Learning parameters: Weights of an agent.

Learning objective: $(v_t - G^\lambda_t)^2$ (online moving objective) -- **Is this what the name "difference" indicates**?

Control: Linear. $v_t = \sum_{i=1}^nw_{t-1}[i]\phi_t[i]$.

Step-size hyperparameter:
- TD($\lambda$): $\delta_t := r_t + \gamma v_{t-1, t} - v_{t-1, t-1}$.
- True Online TD($\lambda$): $\delta'_t := r_t + \gamma v_{t-1, t} - v_{t-2, t-1}$.
- TD($\lambda$) allows to "look ahead": $v_{t-1, t-1}$, while True Online TD($\lambda$) does not.

### Key idea in the paper
Learn the non-homogeneous per weight/feature update step-size.

It borrows idea of "Incremental Delta-bar Delta (IDBD)". IDBD does step-size optimization, while RMSProp/Adam does step-size normalization.
