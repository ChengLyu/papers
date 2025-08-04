# Papers

## Reinforcement Learning

[*Swift-Sarsa: Fast and Robust Linear Control*](https://www.arxiv.org/abs/2507.19539)

Learn value function. Discrete action space. Linear control.
$$v_{t-1,t}[action] = \sum_{i\in\text{feature dimension}}w^{action}_{t-1}[i]\phi_t[i]$$
TD error for learning:
$$\delta'_t = r_t + \gamma v_{t-1,t}[action_t] - v_{t-2, t-1}[action_{t-1}]$$
Difference over SwiftTD: **eligibility vector** update rule. Policy: $\epsilon$-greedy or softmax. Experiment: $n$ dimension observation only has the first $m$ dimensions valid ($m << n$), with the remaining dimensions noisy. The controler can learn the valid signals.

**TODO**
- SwiftTD: Swifttd: A fast and robust algorithm for temporal difference learning.
- Sarsa: True online temporal-difference learning.
- TD learning.