# 🚀 LunarLander-v3 — Deep Q-Network (DQN)

A Deep Reinforcement Learning project that trains an autonomous agent to successfully land a lunar module in the **LunarLander-v3** environment using a **Deep Q-Network (DQN)** implemented with PyTorch.

The agent learns completely through interaction with the environment using **experience replay, a target network, epsilon-greedy exploration, and soft target updates**.

---

## 🎯 Project Objective

Train an AI agent to learn how to control a lunar lander and achieve a stable landing without manually controlling it.

The agent learns which action to take based on the current state of the lander.

```text
LunarLander Environment
          ↓
       State
          ↓
     Neural Network
          ↓
      Q-Values
          ↓
    Select Action
          ↓
     Environment
          ↓
       Reward
          ↓
    Experience Replay
          ↓
       Training
```

---

## 🧠 Algorithm

This project uses a **Deep Q-Network (DQN)**.

Instead of maintaining a traditional Q-table, a neural network approximates the Q-value function:

```text
Q(state, action)
```

The action with the highest predicted Q-value is selected during exploitation.

### DQN Architecture

```text
Input: 8-dimensional state
          ↓
     Fully Connected
        64 neurons
          ↓
        ReLU
          ↓
     Fully Connected
        64 neurons
          ↓
        ReLU
          ↓
     Fully Connected
     4 action values
```

---

## 🎮 Environment

Environment:

**LunarLander-v3**

The environment provides an **8-dimensional state** describing the lander's position, velocity, angle, angular velocity, and leg-contact information.

The agent has **4 possible actions**:

| Action | Description       |
| -----: | ----------------- |
|    `0` | Do nothing        |
|    `1` | Fire left engine  |
|    `2` | Fire main engine  |
|    `3` | Fire right engine |

---

## 🔄 Reinforcement Learning

The agent follows the standard reinforcement-learning loop:

```text
State
  ↓
Choose Action
  ↓
Receive Reward
  ↓
Observe Next State
  ↓
Store Experience
  ↓
Sample Mini-Batch
  ↓
Update Neural Network
```

Each experience contains:

```text
(state, action, reward, next_state, done)
```

---

## 🗃️ Experience Replay

A replay buffer stores previously observed experiences.

The agent randomly samples a mini-batch of experiences during training.

This helps reduce correlations between consecutive experiences and improves training stability.

```python
replay_buffer_size = 100000
minibatch = 150
```

---

## 🎯 Target Network

The implementation uses two neural networks:

```text
Local Network
     ↓
Learns Q-values

Target Network
     ↓
Provides stable Q-targets
```

The target network is updated using a soft update:

```text
θ_target ← τ θ_local + (1 - τ) θ_target
```

where:

```text
τ = 0.001
```

---

## 🎲 Epsilon-Greedy Exploration

During training, the agent balances exploration and exploitation.

```text
ε = 1.0  → mostly random actions
     ↓
ε decreases
     ↓
ε = 0.01 → mostly learned actions
```

Parameters:

```python
epsilon_starting_value = 1.0
epsilon_ending_value = 0.01
epsilon_decay_value = 0.995
```

During testing, epsilon is set to `0`, so the trained agent selects the learned action without random exploration.

---

## ⚙️ Training Configuration

```text
Learning Rate       : 5e-4
Discount Factor     : 0.99
Replay Buffer       : 100,000
Mini-batch Size     : 150
Target Update τ     : 0.001
Maximum Episodes    : 5,000
Maximum Steps       : 1,000
```

Training automatically stops when the average score over the latest 100 episodes reaches:

```text
200
```

---

## 🎥 Successful Landing Detection

After training, the agent is evaluated without exploration.

The program tests the trained model and searches for a successful landing.

Only when:

```text
Score >= 200
```

the episode is saved as:

```text
successful_landing.mp4
```

This keeps the final output focused on a successful demonstration rather than saving every test episode.

---

## 📁 Project Structure

```text
LunarLander-DQN/
│
├── lunar_landing_deep_q.ipynb
├── successful_landing.mp4
└── README.md
```

---

## 🛠️ Technologies Used

* Python
* PyTorch
* Gymnasium
* NumPy
* Pygame
* ImageIO
* Matplotlib / Jupyter display utilities

---

## ▶️ Installation

Clone the repository:

```bash
git clone https://github.com/utkarshsingh171/lunar_landing_reinforcement.git
```

Install dependencies:

```bash
pip install gymnasium
pip install "gymnasium[box2d]"
pip install torch
pip install numpy
pip install imageio
```

For MP4 video support, you may also need:

```bash
pip install imageio-ffmpeg
```

---

The agent will:

1. Create the LunarLander environment.
2. Initialize the DQN agent.
3. Train using reinforcement learning.
4. Track the average score.
5. Stop when the environment is considered solved.
6. Test the trained model.
7. Search for a successful landing.
8. Save the successful episode as `successful_landing.mp4`.

---

## 📊 Training Output

Example:

```text
Episode 0 avg score: -XXX.XX
Episode 10 avg score: -XXX.XX
Episode 20 avg score: -XXX.XX
...
Episode XXX avg score: 2XX.XX

Congratulations, solved in XXX episodes
```
---

## 🎥 Demo

The repository includes a successful landing demonstration:

**`successful_landing.mp4`**

https://github.com/user-attachments/assets/535a13fa-c79d-44d7-9729-a188cb7f4377



The video is generated automatically after the trained DQN agent achieves a successful landing during evaluation.

---

## 🔬 Future Improvements

Possible extensions include:

* Double DQN
* Dueling DQN
* Prioritized Experience Replay
* Reward analysis
* Training-performance graphs
* Model checkpointing
* Multiple evaluation episodes
* Hyperparameter optimization
* Comparison with PPO
* Conversion to a Spiking Neural Network (SNN)
* Comparison between ANN-based and biologically inspired agents

---

## 📌 Key Learning

This project demonstrates how an agent can learn control behavior **without being explicitly programmed with the rules for landing**.

The neural network learns an approximation of:

```text
State → Q-values → Action
```

through repeated interaction with the environment and feedback from rewards.

---

## 👨‍💻 Author

**Utkarsh Singh**

Computer Science Engineering Student
Interested in Artificial Intelligence, Machine Learning, Reinforcement Learning, and Biologically Inspired AI.
