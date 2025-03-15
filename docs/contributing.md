# Contributing to MLGym

Thank you for your interest in contributing to MLGym! This document provides guidelines and instructions for contributing to the project.

## Code of Conduct

Please read and follow our [Code of Conduct](../CODE_OF_CONDUCT.md) to ensure a positive and inclusive environment for everyone.

## Getting Started

### Setting Up Your Development Environment

1. **Fork the Repository**
   
   Start by forking the MLGym repository on GitHub.

2. **Clone Your Fork**
   
   ```bash
   git clone https://github.com/YOUR_USERNAME/MLGym.git
   cd MLGym
   ```

3. **Set Up the Development Environment**
   
   ```bash
   # Create a virtual environment
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   
   # Install dependencies
   pip install -e ".[dev]"
   ```

4. **Set Up Pre-commit Hooks**
   
   ```bash
   pre-commit install
   ```

### Development Workflow

1. **Create a Branch**
   
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Your Changes**
   
   Implement your feature or fix the bug.

3. **Run Tests**
   
   ```bash
   pytest
   ```

4. **Submit a Pull Request**
   
   Push your changes to your fork and submit a pull request to the main repository.

## Contribution Guidelines

### Code Style

MLGym follows the [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guide for Python code. We use [Black](https://black.readthedocs.io/en/stable/) for code formatting and [isort](https://pycqa.github.io/isort/) for import sorting.

```bash
# Format your code
black .
isort .
```

### Documentation

- All public functions, classes, and methods should have docstrings following the [Google style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings).
- Update or add documentation for any changes you make.
- Include examples where appropriate.

### Testing

- Write tests for new features and bug fixes.
- Ensure all tests pass before submitting a pull request.
- Aim for high test coverage.

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification for commit messages:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

Types include:
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

### Pull Requests

- Keep pull requests focused on a single change.
- Update the documentation if necessary.
- Add tests for new features or bug fixes.
- Ensure all tests pass.
- Reference any related issues.

## Adding New Components

### Adding a New Task

1. Create a new task class in `mlgym/environment/tasks/`.
2. Implement the required methods: `__init__`, `reset`, `step`, and `evaluate`.
3. Register the task in `mlgym/environment/tasks/__init__.py`.
4. Add task configuration in `configs/tasks/`.
5. Add tests for the new task.
6. Update documentation.

### Adding a New Agent

1. Create a new agent class in `mlgym/agent/agents/`.
2. Implement the required methods: `__init__`, `reset`, `act`, and `update`.
3. Register the agent in `mlgym/agent/agents/__init__.py`.
4. Add agent configuration in `configs/agents/`.
5. Add tests for the new agent.
6. Update documentation.

### Adding a New Tool

1. Create a new tool class in `mlgym/tools/`.
2. Implement the required methods: `__init__` and `__call__`.
3. Register the tool in `mlgym/tools/__init__.py`.
4. Add tool configuration in `configs/tools/`.
5. Add tests for the new tool.
6. Update documentation.

## Release Process

1. Update the version number in `pyproject.toml`.
2. Update the changelog.
3. Create a new release on GitHub.
4. Publish the package to PyPI.

## Getting Help

If you have questions or need help, you can:
- Open an issue on GitHub
- Join our [Discord community](https://discord.gg/Zep3cyHhjJ)
- Contact the maintainers directly

## Thank You

Your contributions are greatly appreciated! By contributing to MLGym, you're helping to advance research in AI and machine learning.