# Report

### Learning Algorithm

dqn with experience replay

The input to the network has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around the agent's forward direction. This is followed by 2 hidden Linear Layers of size 64 activated by a RELU activation function. The output has a size of 4, the number of possible actions.


hyperparameters:

GAMMA = 0.99            # discount factor
TAU = 1e-3              # for soft update of target parameters
LR = 5e-4               # learning rate 
UPDATE_EVERY = 4        # how often to update the network

### Results

Training Graph

<img width="560" alt="Training Graph" src="https://github.com/vladfatu/project-navigation-udacity/assets/1000350/f870c385-c906-4fdb-b0bf-e085a23ef3b2">

### Future Improvements

- double DQN
- dueling DQN
- prioritized experience replay!
