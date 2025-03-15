# MLGym Architecture Overview

MLGym is designed as a framework for benchmarking AI research agents on machine learning tasks. This document provides a high-level overview of the MLGym architecture.

## System Architecture

![MLGym Architecture](../assets/figs/mlgym.png)

MLGym follows a modular architecture with the following key components:

1. **Environment**: The core environment that presents tasks to agents and processes their actions
2. **Agent**: The AI research agent that interacts with the environment to solve ML tasks
3. **Tasks**: A collection of ML research tasks from various domains
4. **Tools**: Utilities available to agents for solving tasks
5. **Evaluation**: Metrics and methods for evaluating agent performance

## Component Interactions

The MLGym framework operates on the following workflow:

1. The environment loads a task configuration and initializes the task
2. The agent receives the task description and context
3. The agent interacts with the environment by:
   - Analyzing the task
   - Planning a solution approach
   - Executing actions using available tools
   - Observing results and adapting its approach
4. The environment evaluates the agent's performance based on task-specific metrics
5. Results are recorded for analysis

## Containerized Execution

MLGym uses containerization (Docker/Podman) to provide:

- Isolated execution environments for each task
- Consistent dependencies across different systems
- Resource management and monitoring
- Security boundaries

The container includes all necessary dependencies for ML tasks, including:
- Python libraries for data science and ML
- Development tools
- GPU support for accelerated computation

## Key Modules

### mlgym.environment

The environment module defines the core environment class and task interfaces. It handles:
- Task registration and loading
- Observation and action space definitions
- Agent-environment interaction loop
- Reward calculation and evaluation

### mlgym.agent

The agent module provides the base agent implementation and utilities for:
- Processing environment observations
- Generating actions
- Maintaining interaction history
- Parsing agent outputs

### mlgym.tools

The tools module contains utilities that agents can use to solve tasks, such as:
- Code execution tools
- Data manipulation utilities
- Visualization helpers
- File system operations

### mlgym.evaluation

The evaluation module provides metrics and methods for assessing agent performance:
- Task-specific evaluation metrics
- Performance tracking
- Result aggregation and analysis

## Configuration System

MLGym uses a YAML-based configuration system for:

1. **Task Configuration**: Defines task parameters, evaluation metrics, and environment settings
2. **Agent Configuration**: Specifies agent model, parameters, and available tools
3. **Runtime Configuration**: Controls execution parameters like timeouts and resource limits

## Trajectory Recording

MLGym records agent trajectories (sequences of observations, actions, and rewards) for:
- Debugging and analysis
- Visualization through the trajectory visualizer
- Comparison of different agents or approaches
- Training data for future agent improvements

## Next Steps

- Learn about [available tasks](./tasks.md)
- Understand [agent implementation](./agents.md)
- Explore the [environment details](./environment.md)