# Project Report

This is a small reporta associate to the Deep Determinist Policy Gradient (DDPG) network developed for the Udacity virtual environment.

![Alt Text](https://gitee.com/mirrors/Unity-ML-Agents/raw/master/docs/images/reacher.png)

## Environment Introduction

In this environment, a double-jointed arm can move to target locations. The double-jointed arm receive a reward of +0.1 for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

For this environment we used only single double-jointed arm. It has been studied that using multiple arms may reduce the training effort thanks to the [sharing of experience](https://ai.googleblog.com/2016/10/how-robots-can-acquire-new-skills-from.html).

## Deep Determinist Policy Gradient (DDPG)

The environment in which this model has been trained is based on one single double-joined arm. The code can be adapted easily to 20 jointed-arms architecture. The DDPG is a model which iterativelly learns an optimal policy using the Q-Learning algorithm. Q-Learning is reached thanks to the usage of Bellman equation:

![Bellman](https://spinningup.openai.com/en/latest/_images/math/339d9f6adec072789c579d36f9d1791e6246b075.svg)

DDPG learns the optimal action-value function and then define the best action to perform. When you have an optimal action-value in a discrete space is particular easy to identify the best action. In a continous space the things change a little bit. In this latter, you may need a differentiable action-space function in any point in order to adopt a gradient approach for the identification of the right action. 

The main goal of DDPG based on a neural network is the minimization of the mean-squared Bellman error (MSBE). This function describe how closely the action-value function is going to satisfy the BellMan Equation

![Error](https://spinningup.openai.com/en/latest/_images/math/d193a1fae2f39357adc458987f0301518f3cd669.svg)

The DDPG classical implementation uses several methodologies / tricks for improving their performances:

* **Replay Buffer:** The models exploit a buffer of previous experiences in order to learn from uncorrelated events.

* **Two Target Agent:** Due to the influenced weight updates a common approach is to fix them in another network in order to maintain a fixed target. The main reason is associate to the fact that we are training over the same parameters which are used for MSBE minimization.

* **Ornstein–Uhlenbeck Noise:** This is an approach used for defining the exploration and exploitation trade-off. 

The good performances of this project are achieved with a fine tuning over these three properties above. For this project I have also added a clipping method for the gradient in order to avoid excessive weights update. 

```torch.nn.utils.clip_grad_norm(self.critic_local.parameters(), 1)```


## PyTorch Network

The PyTorch architecture is based on a Feed-Forward Neural Network with two hidden layer for both actor and critic. The first hidden layer is 256 and the second is 128 hidden units. 

The Actor Model:
* ```Hidden: (input, 256) - ReLU```
* ```Hidden: (256, 128) - ReLU```
* ```Output: (128, 4) - TanH```

The Critic Model:
* ```Hidden: (input, 256) - ReLU```
* ```Hidden: (256 + action_size, 128) - ReLU```
* ```Output: (128, 1) - Linear```

![FFNN](http://neuralnetworksanddeeplearning.com/images/tikz11.png)

## HyperParameters

This is the list of hyperparameters that has been used for the model training procedure. These values are also the inside the ddpg_agent.py file code global variables. 

*  ```BUFFER_SIZE = int(1e5)  # replay buffer size```
* ```BATCH_SIZE = 1000       # minibatch size```
* ```GAMMA = 0.99            # discount factor```
* ```TAU = 1e-3              # for soft update of target parameters```
* ```LR_ACTOR = 1e-3         # learning rate of the actor ```
* ```LR_CRITIC = 1e-3        # learning rate of the critic```
* ```WEIGHT_DECAY = 0        # L2 weight decay```
* ```ITERATION_LEARNING = 6  # number of times to iterate the training process```
* ```FREQUENCY_LEARNING = 20 # after how many steps it is required a training process```
* ```NOISE_OU = 0.25         # noise mean ```

## Results

The model reaches a score of 30.0 points on average for a sliding window of 100 Episodes. Once the goal had been reached, the weights were saved for further improvements or evaluation. 

![Results](https://raw.githubusercontent.com/IvanVigor/Deep-Deterministic-Policy-Gradient-Unity-Env/master/pictures/index.png)

## Future Work

I think that there are several rooms of improvement, by working on multiple aspects.

- The adoption of CNN architecture for converting the states into an image should be an interesting improvement to the model
- Adopt the same solution for the 20 Agents scenario. Then it is interesting to evaluate the temporal difference between single agent and multiple. There is an interesting article related to the sharing experience of robots.
- Improve the hyperparamers selection with a Grid-Search
- Insert a Noise decay term, for exploring new solutions and then reduce the e-greedy policy. 

