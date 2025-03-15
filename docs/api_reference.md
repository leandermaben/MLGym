# MLGym API Reference

This document provides a comprehensive reference for the MLGym API, including classes, methods, and functions.

## Core Modules

### mlgym.environment

#### Environment

The main environment class that manages the interaction between agents and tasks.

```python
class Environment:
    def __init__(self, config_path=None, config=None):
        """
        Initialize the environment.
        
        Args:
            config_path (str, optional): Path to the environment configuration file.
            config (dict, optional): Environment configuration dictionary.
        """
        
    def reset(self, task_id=None):
        """
        Reset the environment with a specific task.
        
        Args:
            task_id (str, optional): ID of the task to load. If None, a random task is selected.
            
        Returns:
            observation: Initial observation from the environment.
        """
        
    def step(self, action):
        """
        Take a step in the environment based on the agent's action.
        
        Args:
            action: Agent's action.
            
        Returns:
            observation: Next observation from the environment.
            reward: Reward for the action.
            done: Whether the episode is complete.
            info: Additional information.
        """
        
    def render(self, mode='human'):
        """
        Render the environment.
        
        Args:
            mode (str): Rendering mode ('human', 'rgb_array', etc.).
            
        Returns:
            Rendering of the environment based on the specified mode.
        """
```

#### Task

Base class for all tasks in MLGym.

```python
class Task:
    def __init__(self, config):
        """
        Initialize a task.
        
        Args:
            config (dict): Task configuration.
        """
        
    def reset(self):
        """
        Reset the task.
        
        Returns:
            observation: Initial observation for the task.
        """
        
    def step(self, action):
        """
        Process an action and return the next observation.
        
        Args:
            action: Agent's action.
            
        Returns:
            observation: Next observation.
            reward: Reward for the action.
            done: Whether the task is complete.
            info: Additional information.
        """
        
    def evaluate(self, trajectory):
        """
        Evaluate the agent's performance on the task.
        
        Args:
            trajectory: Sequence of observations and actions.
            
        Returns:
            metrics: Dictionary of evaluation metrics.
        """
```

### mlgym.agent

#### Agent

Base class for all agents in MLGym.

```python
class Agent:
    def __init__(self, config):
        """
        Initialize an agent.
        
        Args:
            config (dict): Agent configuration.
        """
        
    def reset(self):
        """
        Reset the agent's state.
        """
        
    def act(self, observation):
        """
        Generate an action based on the observation.
        
        Args:
            observation: Observation from the environment.
            
        Returns:
            action: Agent's action.
        """
        
    def update(self, observation, reward, done, info):
        """
        Update the agent's state based on environment feedback.
        
        Args:
            observation: New observation.
            reward: Reward received.
            done: Whether the episode is complete.
            info: Additional information.
        """
```

### mlgym.tools

#### Tool

Base class for all tools in MLGym.

```python
class Tool:
    def __init__(self, config=None):
        """
        Initialize a tool.
        
        Args:
            config (dict, optional): Tool configuration.
        """
        
    def __call__(self, *args, **kwargs):
        """
        Execute the tool with the provided arguments.
        
        Returns:
            result: Result of the tool execution.
        """
```

### mlgym.evaluation

#### Evaluator

Class for evaluating agent performance.

```python
class Evaluator:
    def __init__(self, config=None):
        """
        Initialize an evaluator.
        
        Args:
            config (dict, optional): Evaluator configuration.
        """
        
    def evaluate(self, agent, task, num_episodes=1):
        """
        Evaluate an agent on a task.
        
        Args:
            agent: Agent to evaluate.
            task: Task to evaluate on.
            num_episodes (int): Number of episodes to run.
            
        Returns:
            metrics: Dictionary of evaluation metrics.
        """
        
    def generate_report(self, metrics, output_path=None):
        """
        Generate an evaluation report.
        
        Args:
            metrics: Evaluation metrics.
            output_path (str, optional): Path to save the report.
            
        Returns:
            report: Evaluation report.
        """
```

## Utility Functions

### mlgym.utils

```python
def load_config(config_path):
    """
    Load a configuration file.
    
    Args:
        config_path (str): Path to the configuration file.
        
    Returns:
        config (dict): Loaded configuration.
    """
    
def register_task(task_id, task_class):
    """
    Register a task with MLGym.
    
    Args:
        task_id (str): ID for the task.
        task_class: Task class to register.
    """
    
def register_agent(agent_id, agent_class):
    """
    Register an agent with MLGym.
    
    Args:
        agent_id (str): ID for the agent.
        agent_class: Agent class to register.
    """
    
def register_tool(tool_id, tool_class):
    """
    Register a tool with MLGym.
    
    Args:
        tool_id (str): ID for the tool.
        tool_class: Tool class to register.
    """
```

## Configuration Reference

### Environment Configuration

```yaml
environment:
  # General environment settings
  max_steps: 100
  timeout: 3600
  
  # Observation space configuration
  observation_space:
    type: "dict"
    components:
      task_description: "text"
      context: "text"
      feedback: "text"
      
  # Action space configuration
  action_space:
    type: "dict"
    components:
      tool_name: "categorical"
      tool_args: "dict"
```

### Task Configuration

```yaml
task:
  id: "classification_task"
  description: "Train a classifier on the provided dataset."
  
  # Task-specific parameters
  dataset: "iris"
  metrics: ["accuracy", "f1_score"]
  
  # Evaluation parameters
  evaluation:
    test_split: 0.2
    cv_folds: 5
```

### Agent Configuration

```yaml
agent:
  id: "llm_agent"
  model: "gpt-4"
  
  # Agent-specific parameters
  temperature: 0.7
  max_tokens: 1000
  
  # Available tools
  tools: ["execute_python", "execute_bash", "str_replace_editor"]
```

## Next Steps

- Learn about [available tasks](./tasks.md)
- Understand [agent implementation](./agents.md)
- Explore the [environment details](./environment.md)