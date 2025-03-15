# MLGym Environment

This document describes the MLGym environment architecture, components, and implementation details.

## Environment Overview

The MLGym environment is the core component that:
- Presents tasks to agents
- Processes agent actions
- Provides observations and feedback
- Evaluates agent performance
- Manages the interaction loop

## Environment Architecture

The environment implementation is primarily defined in `mlgym/environment/env.py`. The key components include:

1. **Task Management**: Loading and initializing tasks
2. **Observation Space**: Defining the structure of observations
3. **Action Space**: Defining the structure of actions
4. **Step Function**: Processing agent actions and returning new observations
5. **Reset Function**: Initializing or resetting the environment
6. **Evaluation**: Assessing agent performance

## Environment Components

### MLGymEnv Class

The `MLGymEnv` class is the main environment class that implements the core functionality:

```python
class MLGymEnv:
    def __init__(self, task_config, ...):
        # Initialize environment with task configuration
        pass

    def reset(self):
        # Reset the environment and return initial observation
        pass

    def step(self, action):
        # Process action and return (observation, reward, done, info)
        pass

    def render(self):
        # Render the current state (if applicable)
        pass

    def close(self):
        # Clean up resources
        pass
```

### Observation and Action Spaces

The environment defines observation and action spaces in `mlgym/environment/spaces.py`:

- **Observation Space**: Typically includes task description, context, feedback, and state information
- **Action Space**: Defines the structure of valid actions, including tool calls and parameters

### Task Implementation

Tasks are implemented in `mlgym/environment/tasks.py` and follow a common interface:

```python
class BaseTask:
    def __init__(self, config):
        # Initialize task with configuration
        pass

    def reset(self):
        # Reset task state and return initial observation
        pass

    def step(self, action):
        # Process action and return (observation, reward, done, info)
        pass

    def get_reward(self, action, result):
        # Calculate reward based on action and result
        pass

    def is_done(self):
        # Check if task is complete
        pass
```

### Task Registration

Tasks are registered in `mlgym/environment/registration.py` to make them available to the environment:

```python
register_task(
    id="image_classification_cifar10",
    entry_point="mlgym.environment.tasks:ImageClassificationCIFAR10Task",
    max_steps=50,
    description="Image classification task using CIFAR-10 dataset",
)
```

## Environment Utilities

The `mlgym/environment/utils.py` module provides utilities for:

- Loading and parsing task configurations
- Managing environment state
- Handling timeouts and resource limits
- Processing observations and actions

## Containerized Execution

MLGym uses containerization (Docker/Podman) to provide isolated execution environments:

1. The environment creates a container for each task
2. The task is executed within the container
3. The environment communicates with the container through a defined interface
4. Resources are monitored and limited according to configuration

## Environment Configuration

Environment behavior is configured through task configuration files in `configs/tasks/`:

```yaml
# Example task configuration
id: "image_classification_cifar10"
name: "Image Classification (CIFAR-10)"
description: "Develop a model to classify images into 10 categories."
max_steps: 50
timeout: 3600  # seconds
evaluation:
  metric: "accuracy"
  threshold: 0.7
resources:
  memory: "8G"
  cpu: 2
  gpu: 1
```

## Environment Variables

MLGym uses environment variables for configuration:

- `MLGYM_CONFIG_ROOT`: Path to configuration directory
- `MLGYM_TASK_CONFIG_DIR`: Path to task configuration directory
- `MLGYM_WORKSPACE_PATH`: Path to workspace directory
- `MLGYM_ENV_TIMEOUT`: Environment timeout in seconds
- `MLGYM_ACTION_SHORT_TIMEOUT`: Short action timeout in seconds
- `MLGYM_ACTION_LONG_TIMEOUT`: Long action timeout in seconds
- `MLGYM_MODEL_MAX_RETRIES`: Maximum retries for model calls

## Creating Custom Environments

To create a custom environment:

1. Extend the `MLGymEnv` class or implement a compatible interface
2. Define observation and action spaces
3. Implement the core methods (`reset`, `step`, etc.)
4. Configure the environment through YAML files

## Environment Lifecycle

1. **Initialization**: The environment is created with a task configuration
2. **Reset**: The environment is reset to its initial state
3. **Step Loop**: The agent interacts with the environment through the step function
4. **Evaluation**: The agent's performance is evaluated based on task-specific metrics
5. **Termination**: The environment is closed and resources are released

## Best Practices

1. **Resource Management**: Configure appropriate resource limits for tasks
2. **Timeout Handling**: Set reasonable timeouts for actions and environment steps
3. **Error Handling**: Implement robust error handling for agent actions
4. **Observation Design**: Provide clear, informative observations to guide the agent
5. **Reward Design**: Design rewards that effectively guide the agent toward task completion

## Debugging Environments

To debug environment behavior:

1. Enable verbose logging in the environment configuration
2. Use the trajectory visualizer to inspect environment-agent interactions
3. Check for common issues like resource limits, timeouts, or action processing errors

For more information on debugging, see the [FAQ](./faq.md) section.