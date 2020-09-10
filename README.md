# gym_wrapper_dm_soccer
The OpenAI style Gym environment wrapper for DeepMind Soccer game https://github.com/deepmind/dm_control/tree/master/dm_control/locomotion/soccer

The environment is a multi-agent environment, so we created the wrapper based on the multi-agent Mujoco gym environment https://github.com/schroederdewitt/multiagent_mujoco/blob/master/src/multiagent_mujoco/mujoco_multi.py

#### Obesrvations 
The original observation is a dictionary, in our environment, for the ease of use, we concatenate all the values in the dictionary into a list of size (154,). 


#### Reward Shaping 

The oginal rewards are sparse, the agents will get 1.0 for goaling and -1.0 for losing as a team. The sparse reward makes learning extremely hard, so we added a reward shaping function, which is from the paper paper Arena: a toolkit for Multi-Agent Reinforcement
Learning https://arxiv.org/pdf/1907.09467.pdf

* we are planning to add more options for reward shaping


## How to use: 

1. Install gym : `pip install gym`
2. Install multiagent_mujoco following the instruction in https://github.com/schroederdewitt/multiagent_mujoco
3. Install Mujoco following the instruction https://github.com/openai/mujoco-py
4. Install dm_control following the instruction https://github.com/deepmind/dm_control/blob/master/README.md#installation-and-requirements
5. copy the soccer_wrapper.py into your code base, then 

```
import gym
import ma_gym
from src.multiagent_mujoco.mujoco_multi import MujocoMulti
from soccer_wrapper import DMSoccer


env = DMSoccer(team_size=1, time_limit=5)

obs = env.reset() 


done = False
while not done:
  actions = [] 
  for action_spec in range(len(obs)):
    action = np.random.uniform(
        -1, 1, size=(3,))
    actions.append(action)

  obs, reward, done, _ = env.step(actions)
```
