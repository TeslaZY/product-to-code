---
name: uv-skill
description: Python package and project manager, 10-100x faster than pip. Use when managing Python dependencies, creating virtual environments, installing Python versions, or working with Python projects. Covers project initialization, dependency management, virtual environments, Python version management, script execution, tools, and pip-compatible commands.
---

# UV

uv is an extremely fast Python package and project manager written in Rust. It replaces pip, pip-tools, pipx, pyenv, virtualenv, and more with a single tool.

## Quick Start

### Install dependencies in an existing project

```bash
uv sync
```

### Create a new project

```bash
uv init my-project
cd my-project
uv add requests
```

### Run a command with uv

```bash
uv run python script.py
```

## Core Capabilities

### 1. Project Management

uv manages projects with lockfiles and virtual environments.

**Initialize a new project:**
```bash
uv init [name]
```

**Add dependencies:**
```bash
uv add <package>              # Add to main dependencies
uv add --dev <package>         # Add to dev dependencies
uv add --script <script.py> <package>  # Add inline dependency
```

**Remove dependencies:**
```bash
uv remove <package>
```

**Update dependencies:**
```bash
uv lock                        # Update lockfile
uv sync                        # Sync environment with lockfile
```

### 2. Virtual Environments

**Create a virtual environment:**
```bash
uv venv                        # Create .venv
uv venv .env                   # Create custom named env
uv venv --python 3.12          # Use specific Python version
```

**Activate (manual):**
```bash
source .venv/bin/activate      # macOS/Linux
.venv\Scripts\activate         # Windows
```

**Run commands in the environment:**
```bash
uv run <command>               # Run in project env
uv run --with <package> <command>  # Add temporary dep
```

### 3. Python Version Management

**Install Python versions:**
```bash
uv python install 3.12         # Install latest 3.12.x
uv python install 3.11 3.12    # Install multiple
uv python install 3.12.0      # Install exact version
uv python install pypy3.10     # Install PyPy
```

**Set Python version for project:**
```bash
uv python pin 3.12             # Pin to 3.12.x
```

**List available Python versions:**
```bash
uv python list                 # List installed versions
uv python find 3.12            # Find available 3.12.x versions
```

### 4. Script and Tool Execution

**Run single-file scripts with dependencies:**
```bash
# Create script with inline metadata
uv run script.py

# Add dependency to a script
uv add --script script.py requests
```

**Run tools temporarily (uvx):**
```bash
uvx ruff check .               # Run ruff without installing
uvx pycowsay "hello"
```

**Install tools globally:**
```bash
uv tool install ruff           # Install and make available as command
uv tool list                   # List installed tools
uv tool uninstall ruff         # Uninstall
```

### 5. Pip-Compatible Interface

Use uv as a drop-in pip replacement for faster operations.

**Install packages:**
```bash
uv pip install <package>
uv pip install -r requirements.txt
```

**Create virtual environment:**
```bash
uv venv
source .venv/bin/activate
uv pip install <package>
```

**Compile requirements:**
```bash
uv pip compile requirements.in --output-file requirements.txt
```

## Project Structure

uv projects use these files:

- `pyproject.toml` - Project metadata and dependencies
- `uv.lock` - Lockfile (auto-generated)
- `.python-version` - Pinned Python version (optional)
- `README.md` - Project readme
- `src/` - Source code (if applicable)

## Common Patterns

### Adding development dependencies

```bash
uv add --dev pytest black ruff
```

### Running tests

```bash
uv run pytest
```

### Building and publishing

```bash
uv build
uv publish
```

### Using with Docker

```dockerfile
COPY uv.lock pyproject.toml ./
RUN uv sync --frozen
```

## Resources

See [REFERENCES.md](REFERENCES.md) for comprehensive command reference and advanced usage patterns.
