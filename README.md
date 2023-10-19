# OpenAI_Gym_RL_Algorithms_Database

> About

- A database of various RL algorithms implemented in PyTorch for the OpenAI Gym Environments with code and explanations.
- All the algorithm implementations are from [sweetice's Deep-reinforcement-learning-with-pytorch repo](https://github.com/sweetice/Deep-reinforcement-learning-with-pytorch/tree/master).
- Each algorithm code is accompanied by a detailed analysis created for my personal learning.
- Refer to `RLAlgorithmsBreakdown.ipynb` for quick reference to each algorithm's architecture, also included below.

> Model Architecture Overview

### DQN

```
Action Space: Discrete
```
```
Q Network: state + action -> expected reward
```
```
Model Dependency:
Target Q Network (discounted reward) -> Q Network; Q Network (update) -> Target Q Network
```
```
Note: apply Q network to each action to find the best action
```


### Policy Gradient

```
Action Space: Discrete
```
```
Actor: state -> probability for each action
```
```
Model Dependency:
- Use reward collected per game-play to calculate discounted reward per game-play step; multiply the discounted reward with negated log probability of action for each game-play step to get the Actor loss
```

### Actor-Critic

```
Action Space: Discrete
```
```
Actor: state -> probability for each action
Critic: state -> expected reward
```
```
Model Dependency:
- Use reward collected per game-play to calculate discounted reward per game-play step; multiply the discounted reward with negated log probability of action for each game-play step to get the Actor loss
- Use the L1 Loss Function for expected reward and actual reward for Critic loss
- Critic is used to calculate the advantage of Actor's action (actual reward - expected reward)
```

### A2C

```
Action Space: Discrete
```
```
Actor: state -> probability for each action
Critic: state -> expected reward
```
```
Model Dependency:
- Use reward collected per game-play to calculate discounted reward per game-play step; multiply the discounted reward with negated log probability of action for each game-play step to get the Actor loss
- Critic is used to calculate the advantage of Actor's action (actual reward - expected reward)
- Use the mean of advantage^2 to calculate the Critic loss
```
``` 
Note 1: Actor-Critic model applied to multiple environments in parallel, and the loss combined during backpropagation
```
```
Note 2: Entropy can be used to favor exploration of action space
```

### DDPG

```
Action Space: Continuous
```
```
Actor: state -> continuous action 
Q Network: state + action -> expected reward
```
```
Model Dependency:
Actor + Target Q Network (discounted reward) -> Q Network, Q Network -> Actor; Q Network (update) -> Target Q Network
```

### PPO

```
Action Space: Discrete
```
```
Actor: state -> probability for each action
Critic: state -> expected reward
```
```
Model Dependency:
- Use reward collected per game-play to calculate discounted reward per game-play step; multiply the discounted reward with negated log probability of action for each game-play step to get the Actor loss
- Use the MSE Loss Function for expected reward and actual reward for Critic loss
- Critic is used to calculate the advantage of Actor's action (actual reward - expected reward)
```
```
Note: Ratio of probability of selecting an action from updated network and original network is used to control the rate of network update
```

### SAC

```
Action Space: Continuous
```
```
Actor: state -> mean and std for action distribution 
Critic: state -> expected reward
Q Network (optionally dual): state + action -> expected reward
```
```
Model Dependency:
Target Critic (discounted reward) -> Q Network; Q Network -> Actor; Q Network + Actor -> Critic; Critic (update) -> Critic
```
```
Note: Additionally, entropy can be used to encourage exploration
```

### TD3

```
Action Space: Continuous
```
```
Actor: state -> action value
Dual Q Network: state + action -> expected reward
```
```
Model Dependency:
Actor + Target Q Networks (discounted reward) -> Q Networks; Q Network No.1 (delayed for stability) -> Actor; Q Networks (update) -> Target Q Networks
```
```
Note 1: Delayed Actor update is used to stablise training
```
```
Note 2: Noise filter is used in the implementation to stablise training
```
