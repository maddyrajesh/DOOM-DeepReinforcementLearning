# Deep Reinforcement learning Applied to DOOM.

## Getting Started

### Prerequisites

- Operating system enabling the installation of VizDoom (there are some building problems with Ubuntu 16.04 for example), we use Ubuntu 18.04.
- NVIDIA GPU + CUDA and CuDNN (for optimal performance for deep Q learning methods).
- Python 3.6 (in order to install tensorflow).

### Installation

- Install VizDoom package according to your operating system, see https://github.com/mwydmuch/ViZDoom/blob/master/doc/Building.md
- Install pytorch.
```
conda install pytorch torchvision -c pytorch
```
- Install tensorflow with GPU support, see https://www.tensorflow.org/install/pip
- Install tensorboard and tensorboardX.
```
pip install tensorboard
pip install tensorboardX
```
- Install moviepy.
```
pip install moviepy
```
- Clone this repo
```
git clone hhttps://github.com/maddyrajesh/DOOM-DeepReinforcementLearning
cd DOOM-DeepReinforcementLearning
```

## Deep Q Learning

```
cd "Deep Q Learning"
```

### Repositories

- scenarios : Configurations and .wad files of the following scenarios (basic, deadly corridor and defend the center).
- weights   : The weights of training each scenario will be saved here.

### Training

- You can view training rewards, game variables and loss plots by running ```tensorboard --logdir runs``` and clicking the URL http://localhost:6006
- Train a model with train.py , for example:

```
python train.py --scenario basic --window 1 --batch_size 32 --total_episodes 100 --lr 0.0001 --freq 20
```

### Testing

- The previous command saves training weights in weights/basic/ each 20 episodes. You can use the following command to view your agent playing:

```
python play.py --scenario basic --window 1 --weights weights/none_19.pth --total_episodes 20 --frame_skip 2
```

## A3C & Curiosity

```
cd "A3C_Curiosity"
```

### Repositories

- scenarios : Configurations and .wad files of the following scenarios (basic, deadly corridor, defend the center, defend the line and my way home).
- saves   : Models, tensorboad summaries and workers gifs during training will be saved here.

### Training

- You can view training rewards, game variables and loss plots by running ```python utils/launch_tensorboard.py```
- Train a model with main.py , for example:
    - Deadly corridor with default parameters : 
    ```
    python main.py --scenario deadly_corridor --actions all --num_workers 12 --max_episodes 1600
    ```
    - Basic with default parameters : 
    ```
    python main.py --scenario basic --actions single --num_workers 12 --max_episodes 1200
    ```
    - Deadly corridor with default parameters with PPO: 
    ```
    python main.py --use_ppo --scenario deadly_corridor --actions all --num_workers 12 --max_episodes 1600
    ```
    - Deadly corridor with default parameters with curiosity: 
    ```
    python main.py --use_curiosity --scenario deadly_corridor --actions all --num_workers 12 --max_episodes 1600
    ```

See utils/args.py for more parameters.

### Testing

- You can use the following command to view your agent playing using the last trained model:

```
python main.py --play --scenario deadly_corridor --actions all --play_episodes 10
```

