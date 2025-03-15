# MLGym Agents

This document describes the agent architecture, configuration, and implementation details for MLGym.

## Agent Overview

In MLGym, an agent is an AI system that interacts with the environment to solve machine learning tasks. Agents receive task descriptions, analyze problems, develop solutions, and execute actions using available tools.

## Agent Architecture

The base agent implementation is defined in `mlgym/agent/base.py`. The key components include:

1. **Observation Processing**: Handling environment observations and converting them to a format suitable for the agent
2. **Action Generation**: Producing actions based on observations and history
3. **History Management**: Maintaining a record of past interactions
4. **Tool Usage**: Utilizing available tools to solve tasks

## Agent Types

MLGym supports different types of agents:

### LLM-based Agents

These agents use Large Language Models (LLMs) to generate actions:

- **OpenAI Models**: GPT-4, GPT-3.5, etc.
- **Anthropic Models**: Claude, Claude Instant, etc.
- **Open Source Models**: Llama, Mistral, etc.

### Custom Agents

You can implement custom agents by extending the base agent class and implementing the required methods.

## Agent Configuration

Agents are configured using YAML files in the `configs/agents/` directory. A typical agent configuration includes:

```yaml
# Example agent configuration
name: "default_agent"
model:
  provider: "openai"  # or "anthropic", "litellm", etc.
  name: "gpt-4"
  temperature: 0.7
  max_tokens: 4096
tools:
  - name: "python_executor"
    enabled: true
  - name: "file_manager"
    enabled: true
  - name: "data_analyzer"
    enabled: true
prompt:
  system: "You are an AI research assistant tasked with solving machine learning problems."
  format: "markdown"
history:
  max_turns: 20
  include_system_messages: true
```

### Configuration Parameters

- **name**: Unique identifier for the agent
- **model**: LLM configuration
  - **provider**: Model provider (OpenAI, Anthropic, etc.)
  - **name**: Model name
  - **temperature**: Sampling temperature (0.0-2.0)
  - **max_tokens**: Maximum tokens in the response
- **tools**: List of tools available to the agent
- **prompt**: Agent prompt configuration
- **history**: Conversation history settings

## Agent Implementation

### Base Agent Class

The `BaseAgent` class in `mlgym/agent/base.py` provides the foundation for all agents:

```python
class BaseAgent:
    def __init__(self, config):
        self.config = config
        self.history = []
        # Initialize other components

    def process_observation(self, observation):
        # Process the environment observation
        pass

    def generate_action(self, observation):
        # Generate an action based on the observation
        pass

    def update_history(self, observation, action):
        # Update the interaction history
        pass

    def reset(self):
        # Reset the agent state
        pass
```

### History Processing

The `mlgym/agent/history_processors.py` module contains utilities for managing and processing agent interaction history:

- Truncating history to fit token limits
- Formatting history for different model providers
- Extracting relevant information from past interactions

### Output Parsing

The `mlgym/agent/parsing.py` module handles parsing agent outputs:

- Extracting structured actions from text responses
- Handling tool calls and parameters
- Error recovery for malformed outputs

## Using Different Models

MLGym supports various LLM providers through configuration:

### OpenAI

```yaml
model:
  provider: "openai"
  name: "gpt-4"
  temperature: 0.7
```

### Anthropic

```yaml
model:
  provider: "anthropic"
  name: "claude-3-opus-20240229"
  temperature: 0.7
```

### LiteLLM (Multi-provider)

```yaml
model:
  provider: "litellm"
  name: "claude-3-5-sonnet-20240620"
  temperature: 0.7
```

## Creating Custom Agents

To create a custom agent:

1. Create a new Python class that extends `BaseAgent`
2. Implement the required methods (`process_observation`, `generate_action`, etc.)
3. Create a configuration file in `configs/agents/`
4. Register your agent in the agent registry if needed

Example custom agent:

```python
from mlgym.agent.base import BaseAgent

class MyCustomAgent(BaseAgent):
    def __init__(self, config):
        super().__init__(config)
        # Custom initialization

    def process_observation(self, observation):
        # Custom observation processing
        return processed_observation

    def generate_action(self, observation):
        # Custom action generation logic
        return action
```

## Best Practices

1. **Prompt Engineering**: Craft clear, specific prompts that guide the agent toward effective problem-solving
2. **Tool Selection**: Configure appropriate tools for each task
3. **Temperature Tuning**: Adjust temperature based on task requirements (lower for deterministic tasks, higher for creative tasks)
4. **History Management**: Configure history settings to provide sufficient context without exceeding token limits
5. **Error Handling**: Implement robust error handling for agent outputs

## Debugging Agents

To debug agent behavior:

1. Enable verbose logging in the agent configuration
2. Use the trajectory visualizer to inspect agent-environment interactions
3. Analyze agent outputs and tool usage patterns
4. Check for common issues like token limit exceeded, tool usage errors, or parsing failures

For more information on debugging, see the [FAQ](./faq.md) section.