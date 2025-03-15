# MLGym Evaluation

This document describes the evaluation framework used in MLGym to assess agent performance on machine learning tasks.

## Evaluation Framework

MLGym provides a comprehensive evaluation framework that measures agent performance across various dimensions, including:

1. **Task Completion**: Whether the agent successfully completed the task
2. **Solution Quality**: The quality of the solution provided by the agent
3. **Efficiency**: Time and computational resources used by the agent
4. **Generalization**: Agent's ability to handle variations of the task

## Evaluation Metrics

### Task-Specific Metrics

Each task in MLGym has specific evaluation metrics tailored to its domain:

- **Classification Tasks**: Accuracy, precision, recall, F1 score
- **Regression Tasks**: Mean squared error, R-squared, mean absolute error
- **Reinforcement Learning Tasks**: Cumulative reward, episode length
- **Code Generation Tasks**: Correctness, efficiency, readability
- **Data Analysis Tasks**: Insight quality, visualization effectiveness

### General Metrics

In addition to task-specific metrics, MLGym tracks general performance metrics:

- **Time to Solution**: Time taken by the agent to complete the task
- **Action Efficiency**: Number of actions taken to complete the task
- **Tool Usage**: Distribution and effectiveness of tool usage
- **Error Rate**: Frequency and severity of errors made by the agent

## Evaluation Process

The evaluation process in MLGym follows these steps:

1. **Task Initialization**: The environment loads the task with specific evaluation parameters
2. **Agent Interaction**: The agent interacts with the environment to solve the task
3. **Metric Calculation**: The environment calculates performance metrics based on the agent's actions and outputs
4. **Result Recording**: Results are recorded for analysis and comparison
5. **Aggregation**: Results across multiple tasks are aggregated to assess overall agent capabilities

## Benchmark Suites

MLGym provides several benchmark suites for comprehensive agent evaluation:

- **Core ML Suite**: Basic machine learning tasks (classification, regression, clustering)
- **Advanced ML Suite**: Complex ML tasks (feature engineering, model selection, hyperparameter tuning)
- **Research Suite**: Cutting-edge ML research tasks
- **Applied ML Suite**: Real-world ML application tasks

## Leaderboards

MLGym maintains leaderboards that rank agent performance across different tasks and benchmark suites. Leaderboards provide:

- Overall rankings based on aggregate performance
- Task-specific rankings
- Detailed performance breakdowns
- Historical performance tracking

## Visualization and Analysis

MLGym provides tools for visualizing and analyzing evaluation results:

- **Performance Dashboards**: Interactive dashboards for exploring agent performance
- **Comparison Tools**: Tools for comparing multiple agents or agent versions
- **Trajectory Visualization**: Visualization of agent trajectories (sequences of observations and actions)
- **Error Analysis**: Tools for identifying and analyzing agent errors

## Running Evaluations

To run evaluations in MLGym:

```python
from mlgym.evaluation import evaluate_agent

# Evaluate an agent on a specific task
results = evaluate_agent(agent, task_id, num_episodes=10)

# Evaluate an agent on a benchmark suite
suite_results = evaluate_agent(agent, suite_id)

# Generate evaluation report
generate_report(results, output_path="evaluation_report.html")
```

## Custom Evaluation

MLGym supports custom evaluation metrics and procedures:

```python
from mlgym.evaluation import register_metric

# Define a custom metric
def my_custom_metric(agent_output, ground_truth):
    # Metric calculation logic
    return score

# Register the custom metric
register_metric("my_metric", my_custom_metric)
```

## Next Steps

- Learn about [available tasks](./tasks.md)
- Understand [agent implementation](./agents.md)
- Explore the [environment details](./environment.md)