# Python
## Pytorch
### OpenAI gym
```python
import gym
env = gym.make('CartPle-v0')

for i in range(10):
  env.reset()
  for t in range(100):
    env.render()
    action = env.action_space.sample()
    observation, reward, done, info = env.step(action)
    print(observation)

env.close()
```
- env.reset() : 새로운 에피소드(initial env)를 불러옴(reset)
- env.render() : 행동(action) 을 취하기 이전에 환경에 대한 얻은 관찰값(observation)적용하여 그림
- env.step() : 행동(action)을 취한 이후에 환경에 대한 얻은 관찰값(observation)적용하여 제어
- 
