# MLGym Tools

MLGym provides a set of tools that agents can use to interact with the environment and solve machine learning tasks. This document describes the available tools, their functionality, and how to use them.

## Overview

Tools in MLGym are utilities that agents can invoke to perform specific actions, such as executing code, manipulating data, or interacting with the file system. These tools are designed to provide agents with the capabilities needed to solve complex ML tasks.

## Available Tools

### Code Execution Tools

These tools allow agents to execute code in various environments:

- **execute_python**: Executes Python code and returns the output
  - Parameters: `code` (string) - The Python code to execute
  - Returns: Output of the executed code and any errors

- **execute_bash**: Executes bash commands in the terminal
  - Parameters: `command` (string) - The bash command to execute
  - Returns: Command output and exit code

- **execute_ipython_cell**: Runs a cell of Python code in an IPython environment
  - Parameters: `code` (string) - The Python code to execute
  - Returns: Cell output, including rich display objects

### File System Tools

Tools for interacting with the file system:

- **str_replace_editor**: Edit files with string replacement operations
  - Commands: `view`, `create`, `str_replace`, `insert`, `undo_edit`
  - Supports viewing, creating, and modifying files

- **file_search**: Search for files matching specific patterns
  - Parameters: `pattern` (string) - The search pattern
  - Returns: List of matching files

### Data Manipulation Tools

Tools for working with data:

- **data_loader**: Load data from various formats (CSV, JSON, etc.)
  - Parameters: `path` (string), `format` (string)
  - Returns: Loaded data structure

- **data_visualizer**: Generate visualizations of data
  - Parameters: `data` (object), `visualization_type` (string)
  - Returns: Visualization output or path to saved visualization

### Web Tools

Tools for interacting with web resources:

- **web_read**: Read content from a webpage
  - Parameters: `url` (string) - The URL to read
  - Returns: Webpage content in markdown format

- **browser**: Interact with a browser using Python code
  - Parameters: `code` (string) - Python code for browser interaction
  - Supports navigation, form filling, clicking, etc.

## Tool Usage

Agents can invoke tools using a specific format in their responses. For example:

```
<function_calls>
<invoke name="execute_python">
<parameter name="code">
import numpy as np
print(np.random.rand(5))