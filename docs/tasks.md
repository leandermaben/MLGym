# MLGym Tasks

MLGym-Bench consists of 13 diverse and open-ended AI research tasks from various domains. This document provides details about each task, its objectives, and configuration.

## Task Overview

MLGym tasks span multiple domains of machine learning research:

1. **Computer Vision**
   - Image Classification (CIFAR-10, Fashion MNIST)
   - Image Captioning (COCO)

2. **Natural Language Processing**
   - Language Modeling (FineWeb)
   - Natural Language Inference (MNLI)

3. **Reinforcement Learning**
   - Breakout (MinAtar)
   - Mountain Car Continuous
   - Meta Maze

4. **Game Theory**
   - Prisoner's Dilemma
   - Battle of Sexes
   - Blotto

5. **Regression**
   - House Price Prediction

6. **Algorithmic**
   - 3SAT Time

## Task Configuration

Tasks are configured using YAML files located in the `configs/tasks/` directory. Each task configuration includes:

- Task description and objectives
- Environment parameters
- Evaluation metrics
- Available tools and resources
- Time and resource constraints

## Available Tasks

### Computer Vision Tasks

#### Image Classification (CIFAR-10)

```yaml
# configs/tasks/imageClassificationCifar10.yaml
```

Objective: Develop a model to classify images into 10 categories.

Features:
- 60,000 32x32 color images
- 10 classes (airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck)
- Training set: 50,000 images
- Test set: 10,000 images

#### Image Classification (Fashion MNIST)

```yaml
# configs/tasks/imageClassificationFMnist.yaml
```

Objective: Develop a model to classify fashion items.

Features:
- 70,000 28x28 grayscale images
- 10 classes of clothing items
- Training set: 60,000 images
- Test set: 10,000 images

#### Image Captioning (COCO)

```yaml
# configs/tasks/imageCaptioningCOCO.yaml
```

Objective: Generate descriptive captions for images.

Features:
- MS COCO dataset
- Evaluation using BLEU, METEOR, CIDEr metrics
- Requires both vision and language understanding

### Natural Language Processing Tasks

#### Language Modeling (FineWeb)

```yaml
# configs/tasks/languageModelingFineWeb.yaml
```

Objective: Train a language model to predict the next token in a sequence.

Features:
- FineWeb dataset
- Evaluation using perplexity
- Requires understanding of language patterns and context

#### Natural Language Inference (MNLI)

```yaml
# configs/tasks/naturalLanguageInferenceMNLI.yaml
```

Objective: Determine if a hypothesis entails, contradicts, or is neutral to a premise.

Features:
- MultiNLI dataset
- 433k sentence pairs
- Genre diversity (fiction, government, telephone, travel, etc.)

### Reinforcement Learning Tasks

#### Breakout (MinAtar)

```yaml
# configs/tasks/rlBreakoutMinAtar.yaml
```

Objective: Develop an RL agent to play Breakout.

Features:
- Simplified Atari environment
- Visual input
- Discrete action space

#### Mountain Car Continuous

```yaml
# configs/tasks/rlMountainCarContinuous.yaml
```

Objective: Control a car to reach the top of a hill.

Features:
- Continuous action space
- Sparse reward
- Requires exploration and momentum management

#### Meta Maze

```yaml
# configs/tasks/rlMetaMaze.yaml
```

Objective: Navigate through procedurally generated mazes.

Features:
- Procedurally generated environments
- Tests generalization capabilities
- Requires efficient exploration strategies

### Game Theory Tasks

#### Prisoner's Dilemma

```yaml
# configs/tasks/prisonersDilemma.yaml
```

Objective: Develop a strategy for the iterated prisoner's dilemma.

Features:
- Classic game theory problem
- Tests cooperation vs. competition strategies
- Requires understanding of opponent modeling

#### Battle of Sexes

```yaml
# configs/tasks/battleOfSexes.yaml
```

Objective: Develop a strategy for the battle of sexes game.

Features:
- Coordination game with conflicting preferences
- Tests coordination and negotiation strategies
- Requires understanding of mixed strategies

#### Blotto

```yaml
# configs/tasks/blotto.yaml
```

Objective: Develop a strategy for the Colonel Blotto game.

Features:
- Resource allocation game
- Tests strategic thinking and resource management
- Requires understanding of opponent prediction

### Regression Tasks

#### House Price Prediction

```yaml
# configs/tasks/regressionHousePrice.yaml
```

Objective: Predict house prices based on features.

Features:
- Real estate dataset
- Multiple features (size, location, amenities, etc.)
- Evaluation using RMSE and MAE

### Algorithmic Tasks

#### 3SAT Time

```yaml
# configs/tasks/3SATTime.yaml
```

Objective: Develop an efficient algorithm for the 3SAT problem.

Features:
- Boolean satisfiability problem
- NP-complete
- Tests algorithm design and optimization skills

## Adding New Tasks

To add a new task to MLGym:

1. Create a new task configuration file in `configs/tasks/`
2. Implement the task logic in `mlgym/environment/tasks.py`
3. Register the task in `mlgym/environment/registration.py`
4. Add any necessary datasets or resources

For detailed instructions on creating custom tasks, see the [Contributing Guide](./contributing.md).

## Task Evaluation

Each task has specific evaluation metrics defined in its configuration. Common evaluation approaches include:

- **Supervised Learning**: Accuracy, F1-score, RMSE, etc.
- **Reinforcement Learning**: Cumulative reward, success rate
- **Game Theory**: Win rate, payoff
- **NLP/Vision**: Task-specific metrics (BLEU, perplexity, etc.)

For more details on evaluation, see the [Evaluation Guide](./evaluation.md).