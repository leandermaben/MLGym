# Frequently Asked Questions (FAQ)

This document addresses common questions about MLGym, its usage, and troubleshooting.

## General Questions

### What is MLGym?

MLGym is a framework for benchmarking AI research agents on machine learning tasks. It provides a standardized environment for evaluating how well AI agents can perform various machine learning tasks, from data preprocessing to model training and evaluation.

### How is MLGym different from OpenAI Gym?

While both frameworks use the Gym interface, MLGym is specifically designed for machine learning tasks rather than reinforcement learning environments. MLGym focuses on evaluating AI research agents' ability to solve ML problems, while OpenAI Gym provides environments for training reinforcement learning agents.

### What types of tasks does MLGym support?

MLGym supports a wide range of machine learning tasks, including:
- Classification
- Regression
- Clustering
- Feature engineering
- Model selection
- Hyperparameter tuning
- Data cleaning and preprocessing
- Exploratory data analysis
- Neural network architecture design
- And more

### Who should use MLGym?

MLGym is designed for:
- AI researchers studying agent capabilities for ML tasks
- ML practitioners evaluating automated ML solutions
- Developers building AI assistants for data science
- Educators teaching ML concepts through interactive environments

## Installation and Setup

### How do I install MLGym?

```bash
pip install mlgym
```

For development installation:

```bash
git clone https://github.com/leandermaben/MLGym.git
cd MLGym
pip install -e ".[dev]"
```

### What are the system requirements?

- Python 3.8 or higher
- Docker/Podman (for containerized execution)
- 8GB+ RAM recommended
- GPU recommended for some tasks but not required

### How do I set up MLGym with GPU support?

Ensure you have CUDA installed, then install MLGym with GPU dependencies:

```bash
pip install "mlgym[gpu]"
```

Configure GPU usage in your environment configuration:

```yaml
environment:
  use_gpu: true
  gpu_memory_limit: 4096  # MB
```

## Usage

### How do I run a simple experiment?

```python
from mlgym import Environment
from mlgym.agent import LLMAgent

# Initialize environment and agent
env = Environment(config_path="configs/environment/default.yaml")
agent = LLMAgent(config_path="configs/agent/llm_agent.yaml")

# Run an episode
observation = env.reset(task_id="classification_task")
done = False
while not done:
    action = agent.act(observation)
    observation, reward, done, info = env.step(action)

# Get evaluation results
results = env.get_results()
print(results)
```

### How do I create a custom task?

1. Create a new task class that inherits from `mlgym.environment.Task`:

```python
from mlgym.environment import Task

class MyCustomTask(Task):
    def __init__(self, config):
        super().__init__(config)
        # Initialize task-specific attributes
        
    def reset(self):
        # Reset the task state
        return initial_observation
        
    def step(self, action):
        # Process the action and update task state
        return observation, reward, done, info
        
    def evaluate(self, trajectory):
        # Evaluate the agent's performance
        return metrics
```

2. Register your task:

```python
from mlgym.environment import register_task

register_task("my_custom_task", MyCustomTask)
```

### How do I use my own agent with MLGym?

Create a custom agent class that inherits from `mlgym.agent.Agent`:

```python
from mlgym.agent import Agent

class MyCustomAgent(Agent):
    def __init__(self, config):
        super().__init__(config)
        # Initialize agent-specific attributes
        
    def reset(self):
        # Reset the agent state
        
    def act(self, observation):
        # Generate an action based on the observation
        return action
        
    def update(self, observation, reward, done, info):
        # Update the agent's state based on feedback
```

## Troubleshooting

### Common Errors

#### ImportError: No module named 'mlgym'

Make sure you have installed MLGym correctly:

```bash
pip install mlgym
```

#### RuntimeError: Docker not found

MLGym requires Docker or Podman for containerized execution. Install Docker and ensure it's running:

```bash
# Check Docker status
docker --version
systemctl status docker  # Linux
```

#### MemoryError during task execution

Some tasks require significant memory. Try:
1. Increasing available memory
2. Reducing batch sizes in task configuration
3. Using the `low_memory` option in environment configuration

#### GPU-related errors

If you encounter GPU errors:
1. Check CUDA installation: `nvidia-smi`
2. Ensure compatible versions of CUDA and PyTorch
3. Try running with CPU only by setting `use_gpu: false` in configuration

### How do I debug an agent's behavior?

1. Enable verbose logging:

```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

2. Use the trajectory visualizer:

```python
from mlgym.utils.visualization import visualize_trajectory

visualize_trajectory(trajectory, output_path="trajectory.html")
```

3. Inspect intermediate outputs:

```python
env = Environment(config_path="configs/environment/default.yaml", debug=True)
```

## Performance Optimization

### How can I make MLGym run faster?

1. Use GPU acceleration when available
2. Reduce the complexity of tasks
3. Use efficient agent implementations
4. Optimize tool implementations
5. Use containerized execution with resource limits

### How can I reduce memory usage?

1. Process data in smaller batches
2. Use memory-efficient data structures
3. Clean up unused objects
4. Set memory limits in configuration
5. Use the `low_memory` option

## Community and Support

### How do I report a bug?

Please report bugs on our [GitHub Issues page](https://github.com/leandermaben/MLGym/issues) with:
1. A clear description of the bug
2. Steps to reproduce
3. Expected vs. actual behavior
4. System information

### How do I request a feature?

Feature requests can be submitted on our [GitHub Issues page](https://github.com/leandermaben/MLGym/issues) with the "feature request" label.

### How do I contribute to MLGym?

See our [Contributing Guide](./contributing.md) for detailed instructions.

### Where can I get help?

- [GitHub Issues](https://github.com/leandermaben/MLGym/issues)
- [Discord Community](https://discord.gg/Zep3cyHhjJ)
- [Documentation](https://github.com/leandermaben/MLGym/docs)