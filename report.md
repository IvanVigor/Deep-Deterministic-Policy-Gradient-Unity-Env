# Project Report

This is a small reporta associate to the Deep Determinist Policy Gradient (DDPG) network developed for the Udacity virtual environment.

![Alt Text](https://gitee.com/mirrors/Unity-ML-Agents/raw/master/docs/images/reacher.png)

## Environment Introduction

In this environment, a double-jointed arm can move to target locations. The double-jointed arm will receive a reward  a reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

For this environment we used only single double-jointed arm. It has been studied that using multiple arms may reduce the training effort thanks to the [sharing of experience](https://ai.googleblog.com/2016/10/how-robots-can-acquire-new-skills-from.html).

## Deep Determinist Policy Gradient (DDPG)

The environment in which this model has been trained is based on one single double-joined arm. THe code can be adapted easily to 20 jointed-arms architecture. The DDPG is a model which iterativelly learns an optimal policy using the Q-Learning algorithm. Q-Learning is reached thanks to the usage of Bellman equation:

![Alt Text](https://spinningup.openai.com/en/latest/_images/math/339d9f6adec072789c579d36f9d1791e6246b075.svg)

## PyTorch Network



## HyperParameters

This is the list of hyperparameters that has been used for the model training procedure. These values are also the inside the ddpg_agent.py file code global variables. 

*  ```BUFFER_SIZE = int(1e5)  # replay buffer size```
* ```BATCH_SIZE = 1000       # minibatch size```
* ```GAMMA = 0.99            # discount factor```
* ```TAU = 1e-3              # for soft update of target parameters```
* ```LR_ACTOR = 1e-3         # learning rate of the actor ```
* ```LR_CRITIC = 1e-3        # learning rate of the critic```
* ```WEIGHT_DECAY = 0        # L2 weight decay```
* ```ITERATION_LEARNING = 2  # number of times to iterate the training process```
* ```FREQUENCY_LEARNING = 15 # after how many steps it is required a training process```
* ```NOISE_OU = 0.25         # noise mean ```


## Results

![Results](https://raw.githubusercontent.com/IvanVigor/Deep-Deterministic-Policy-Gradient-Unity-Env/master/pictures/index.png)

## Future Work

I think that there are several rooms of improvement, by working on multiple aspects.


