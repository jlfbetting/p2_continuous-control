# Report

### Learning algorithm.

The algorithm uses a Deep Deterministic Policy Gradient (DDPG) Agent. The code is based on the code given in lesson 5 of the Policy-Based Methods chapter of the nanodegree.
Four neural networks are used: critic_local, critic_target, actor_local and actor_target. The critic networks contain of two fully connected layers of 200 neurons each, with ReLU activation functions.
Between the two layers, I put a batch normalization layer (as was described in the paper by Lillicrap et al. (2016, section 3).
The actor networks contain a third layer
I also added gradient clipping (as given as a hint on the Udacity benchmark description page). I added a line to make sure that the local networks get the same weights as the corresponding target networks at initialization.
I added two hyperparameters, `LEARN_EVERY` and `LEARN_TIMES`. After every `LEARN_EVERY` steps, both networks are trained `LEARN_TIMES` times, each time with a different memory sample.
The hyperparameter values were determined experimentally, with the following values:

* `BUFFER_SIZE` = 1e5       (replay buffer size)
* `BATCH_SIZE` = 256        (minibatch size)
* `GAMMA` = 0.95            (discount factor)
* `TAU` = 5e-2              (for soft update of target parameters)
* `LR_ACTOR` = 1e-4         (learning rate of the actor)
* `LR_CRITIC` = 1e-4        (learning rate of the critic)
* `WEIGHT_DECAY` = 0        (L2 weight decay)
* `LEARN_EVERY` = 100       (learn after this number of steps)
* `LEARN_TIMES` = 40        (number of sampling and training per cycle)

I also used a `random_seed` value of 10, which worked well.

### Plot of rewards
The environment was solved in 354 episodes, as can be seen in the notebook. The actor_local network gave an average score over 100 episodes of 30.04. The plot below shows the 
