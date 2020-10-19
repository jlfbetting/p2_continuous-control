# Report

### Learning algorithm.

The algorithm uses a Deep Deterministic Policy Gradient (DDPG) Agent. The code is based on the one given in lesson 5 of the Policy-Based Methods chapter of the nanodegree.
Four neural networks are used: critic_local, critic_target, actor_local and actor_target.

The architecture of the actor networks is as follows:
* input layer size = 33 (state space).
* 2 hidden layers of each 200 hidden units, with `ReLU` activation layers, and a batch normalization layer after the first hidden layer.
* output layer size = 4 (the action space), with a tanh activation layer.

The architecture of the critic networks is as follows:
* input layer size = 4 (action space).
* 2 hidden layers of each 200 hidden units, with `ReLU` activation layers, and a batch normalization layer after the first hidden layer.
* output layer size = 1 (no activation layer).

The use of batch normalization layers was also described in the paper by Lillicrap et al. (2016, section 3). Gradient clipping was added (as given as a hint on the Udacity benchmark description page). I also made sure that the local networks get the same weights as the corresponding target networks at initialization. Two hyperparameters, `LEARN_EVERY` and `LEARN_TIMES`, were added to the original code. After every `LEARN_EVERY` steps, both networks are trained `LEARN_TIMES` times, each time with a different memory sample. The hyperparameter values were determined experimentally, I obtained the following values:

* `BUFFER_SIZE` = 1e5       (replay buffer size)
* `BATCH_SIZE` = 256        (minibatch size)
* `GAMMA` = 0.95            (discount factor)
* `TAU` = 5e-2              (for soft update of target parameters)
* `LR_ACTOR` = 1e-4         (learning rate of the actor)
* `LR_CRITIC` = 1e-4        (learning rate of the critic)
* `WEIGHT_DECAY` = 0        (L2 weight decay)
* `LEARN_EVERY` = 100       (learn after this number of steps)
* `LEARN_TIMES` = 40        (number of sampling and training per cycle)

I also used a `random_seed` value of 10 in the notebook, which turned out to work well.

### Plot of rewards
 The plot below shows how the score changes as more episodes are simulated. On average, the score goes up. The environment was solved in 354 episodes, as can be seen in the notebook. The actor_local network gave an average score over 100 episodes of 30.04.
 ![Episode-score plot](https://github.com/jlfbetting/p2_continuous-control/blob/main/plot_solved.png)
 
 ### Ideas for future work
* We could experiment with adding more elements to the neural networks, such as dropout layers.
* We could use Prioritized Experience Replay (as introduced in the lesson on Deep Q-Networks, and in [this paper](https://arxiv.org/abs/1511.05952)). Instead of sampling the experiences linearly, we could prioritize the more important experiences (i.e. those experiences from which the network can learn the most) so that training goes more efficiently.


