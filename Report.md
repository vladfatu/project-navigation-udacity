# Report

### Learning Algorithm

To solve this environment, I used a DQN with experience replay and fixed Q targets.

- #### Network architecture
The input to the network has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around the agent's forward direction. This is followed by 2 hidden Linear Layers of size 64 activated by a RELU activation function. The output has a size of 4, the number of possible actions.


- #### Hyperparameters

<strong>LR = 5e-4</strong> (learning rate)\
<strong>GAMMA = 0.99</strong> (discount factor)\
\
<strong>BUFFER_SIZE = 1e5</strong> (this is size of the replay buffer used to store experiences)\
<strong>BATCH_SIZE = 64</strong> (this is the number of random samples chosen from the replay buffer when training)\
\
<strong>UPDATE_EVERY = 4</strong> (how often to update the target network from the local one)\
<strong>TAU = 1e-3</strong> (factor used when updating the target network)


### Results

I was able to solve the environment in 378 episodes.

<img width="560" alt="Training Graph" src="https://github.com/vladfatu/project-navigation-udacity/assets/1000350/f870c385-c906-4fdb-b0bf-e085a23ef3b2">

### Future Improvements

- #### Double DQN
  The first improvement would be to implement a Double DQN. A problem DQNs have is that they tend to overestimate the Q values, especially in the first iterations when not enough states have been explored. With a Double DQN we try to solve this problem by changing the learning step to select the next best action from one network, but chosing the value of that action from another network. In our case we can use the target network to select the action and the local network to get the value of that action. The full description of this improvement can be found in [this research paper](https://arxiv.org/abs/1509.06461).

- #### Prioritized experience replay!
  Another improvement would be to choose better experiences from the replay buffer. In this case "better" means a greater TD error(a bigger difference between our prediction and the result). In practice, we would give each experience sample a probability to be chosen depending on the TD error. We need to make sure the probability is not 0 for any sample and there is still an element of randomness to it to prevent the algorithm from always choosing the same samples. We also need to change the update rule to take this probability into consideration. The full description for this method can be found in [this research paper](https://arxiv.org/abs/1511.05952).
  
- #### Dueling DQN
  Another improvement would be to change the architecture of the network to match a Dueling DQN. In a Dueling DQN, instead of having a single stream of Linear Layers that output Q-values for each action, we use 2 streams, one to estimate the state value and the other to estimate the advantages for each action. By "advantage" we mean the added benefit of taking a specific action(Q(s, a) - V(s)). These 2 streams converge to output the Q-values for each action. Although Dueling DQNs excel when the action space is big, which is not the case for this environment(4), it should still help train the agent faster. The full description for this improvement can be found in [this research paper](https://arxiv.org/abs/1511.06581).

