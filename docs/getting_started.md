# Getting Started with MLGym

This guide will help you set up MLGym and run your first experiment.

## Installation

### Prerequisites

- Python 3.11 or higher
- Docker or Podman (for containerized execution)
- NVIDIA GPU with CUDA support (recommended for some tasks)

### Step 1: Clone the Repository

```bash
git clone git@github.com:facebookresearch/MLGym.git
cd MLGym
```

### Step 2: Set Up Python Environment

```bash
conda create -y -n mlgym python=3.11
conda activate mlgym
pip install -e .
```

### Step 3: Configure Environment Variables

Create a `.env` file in the MLGym directory with the following content:

```bash
# Env variables
MLGYM_CONFIG_ROOT="<path_to_MLGYM_root>/configs"
MLGYM_TASK_CONFIG_DIR="<path_to_MLGYM_root>/configs/tasks"
MLGYM_WORKSPACE_PATH="<path_to_MLGYM_root>/workspace"
MLGYM_ENV_TIMEOUT=10000
MLGYM_ACTION_SHORT_TIMEOUT=60
MLGYM_ACTION_LONG_TIMEOUT=10000
MLGYM_MODEL_MAX_RETRIES=3

# API keys
OPENAI_API_KEY=""
ANTHROPIC_API_KEY=""
```

Replace `<path_to_MLGYM_root>` with the absolute path to your MLGym installation.

### Step 4: Set Up Container Runtime

#### Option A: Docker (Recommended for most users)

1. Install Docker following the [official instructions](https://docs.docker.com/desktop/).
2. For Linux users with NVIDIA GPUs, install the NVIDIA Container Toolkit:
   ```bash
   sudo dnf install -y nvidia-container-toolkit
   ```
3. Pull the MLGym container image:
   ```bash
   docker pull aigym/mlgym-agent:latest
   ```
4. Test the container:
   ```bash
   docker run -it --gpus all --name test aigym/mlgym-agent /bin/bash
   ls -la
   exit
   ```

#### Option B: Podman (Recommended for macOS)

1. Install Podman:
   - For Linux:
     ```bash
     # Follow instructions at https://podman.io/get-started
     systemctl --user enable podman.socket
     systemctl --user start podman.socket
     systemctl --user status podman.socket
     export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock
     ```
   - For macOS:
     ```bash
     brew install podman
     podman machine init
     podman machine start
     export DOCKER_HOST=unix://$(podman machine inspect --format '{{.ConnectionInfo.PodmanSocket.Path}}')
     ```
2. Pull the MLGym container image:
   ```bash
   podman pull aigym/mlgym-agent:latest
   ```

### Troubleshooting Container Setup

If you encounter Nvidia CDI spec errors on Linux (e.g., `Error: setting up CDI devices: unresolvable CDI devices nvidia.com/gpu=all`), run these commands:

```bash
sudo mkdir /etc/cdi
sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
sudo touch /etc/containers/nodocker
```

## Running Your First Experiment

### Using Docker

```bash
python run.py \
  --container_type docker \
  --task_config_path tasks/battleOfSexes.yaml \
  --model litellm:claude-3-5-sonnet-20240620 \
  --per_instance_cost_limit 4.00 \
  --agent_config_path configs/agents/default.yaml \
  --temp 1 \
  --gpus 0 \
  --max_steps 50 \
  --aliases_file ./docker/aliases.sh
```

### Using Podman

```bash
python run.py \
  --container_type podman \
  --task_config_path tasks/battleOfSexes.yaml \
  --model litellm:claude-3-5-sonnet-20240620 \
  --per_instance_cost_limit 4.00 \
  --agent_config_path configs/agents/default.yaml \
  --temp 1 \
  --gpus 0 \
  --max_steps 50 \
  --aliases_file ./docker/aliases.sh
```

### Command-Line Arguments

To see all available command-line arguments:

```bash
python run.py --help
```

## Visualizing Results

MLGym provides a web UI to inspect agent trajectories:

```bash
streamlit run demo/trajectory_visualizer.py -- --trajectory_dir <absolute_path_to_trajectories>

# Example
streamlit run demo/trajectory_visualizer.py -- --trajectory_dir $HOME/Projects/MLGym/trajectories/mlgym_bench_v0
```

To run the MLGym demo:

```bash
streamlit run demo/demo.py
```

## Next Steps

- Explore the [available tasks](./tasks.md)
- Learn about [agent configuration](./agents.md)
- Understand the [MLGym architecture](./architecture.md)