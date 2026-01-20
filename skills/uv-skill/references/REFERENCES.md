# UV Command Reference

Comprehensive reference for uv commands and options.

## Commands Index

### Project Commands

- `uv init [name]` - Create a new project
- `uv add <package>` - Add dependency to project
- `uv remove <package>` - Remove dependency from project
- `uv lock` - Update lockfile
- `uv sync` - Sync environment with lockfile

### Virtual Environment Commands

- `uv venv [path]` - Create virtual environment
- `uv run <command>` - Run command in project environment

### Python Commands

- `uv python install <version>` - Install Python version
- `uv python list` - List installed Python versions
- `uv python find <version>` - Find available Python versions
- `uv python pin <version>` - Pin Python version for project

### Tool Commands

- `uv tool install <package>` - Install tool globally
- `uv tool list` - List installed tools
- `uv tool uninstall <package>` - Uninstall tool
- `uv tool run <package>` - Run tool (same as uvx)
- `uvx <package>` - Run tool in ephemeral environment

### Pip Commands

- `uv pip install <package>` - Install package
- `uv pip uninstall <package>` - Uninstall package
- `uv pip list` - List installed packages
- `uv pip show <package>` - Show package info
- `uv pip freeze` - Output installed packages
- `uv pip compile` - Compile requirements

### Build/Publish Commands

- `uv build` - Build project distributions
- `uv publish` - Publish package to PyPI

## Key Options

### Common Options (applies to most commands)

- `--python <version>` - Specify Python version
- `--dev` - Operate on dev dependencies
- `--script <path>` - Operate on a script
- `--frozen` - Don't update lockfile
- `-q, --quiet` - Reduce output verbosity
- `-v, --verbose` - Increase output verbosity

### uv add options

- `--editable` - Install in editable mode
- `--extra <name>` - Add to optional dependency group
- `--index-url <url>` - Use custom index
- `--no-default-groups` - Skip default dev groups

### uv venv options

- `--python <version>` - Use specific Python version
- `--seed` - Include pip in environment
- `--prompt <name>` - Custom prompt

### uv pip compile options

- `--universal` - Platform-independent requirements
- `--output-file <path>` - Output file path
- `--upgrade` - Upgrade packages
- `--extra <name>` - Include extra

## Environment Variables

- `UV_PYTHON` - Path to Python interpreter
- `UV_PYTHON_VERSION` - Python version preference
- `UV_INDEX_URL` - Default package index URL
- `UV_NO_CACHE` - Disable caching
- `UV_PIP_BINARY` - Path to pip binary (for pip interface)

## Configuration Files

uv looks for configuration in:

1. `pyproject.toml` (project-level, in `[tool.uv]` section)
2. `uv.toml` (project-level)
3. `~/.config/uv/uv.toml` (user-level)

Example `pyproject.toml` configuration:

```toml
[project]
name = "my-project"
version = "0.1.0"
dependencies = [
    "requests>=2.31.0",
]

[project.optional-dependencies]
dev = ["pytest>=8.0.0", "ruff>=0.5.0"]

[tool.uv]
dev-dependencies = [
    "pytest>=8.0.0",
    "ruff>=0.5.0",
]
```

## Advanced Patterns

### Multiple dependency groups

```bash
uv add --extra docs sphinx
uv add --extra test pytest
uv sync --extra docs
```

### Overrides for dependencies

```bash
uv add --override package==1.0.0
```

### Using alternative package indexes

```bash
uv add --index-url https://pypi.org/simple package
uv add --extra-index-url https://my-private-index.com/simple private-package
```

### Workspace support

```bash
# Initialize workspace
uv init --workspace

# Add workspace member
uv init --member packages/package-name

# Add dependency from workspace member
uv add my-package --workspace
```

### Script with inline dependencies

```python
# /// script
# requires-python = ">=3.11"
# dependencies = [
#     "requests>=2.31.0",
# ]
# ///

import requests

response = requests.get("https://astral.sh")
print(response.status_code)
```

### Requirements file patterns

**requirements.in** (for compilation):
```
requests>=2.31.0
pytest>=8.0.0
```

**Compile to requirements.txt:**
```bash
uv pip compile requirements.in --output-file requirements.txt
```

### Using in CI/CD

**GitHub Actions:**
```yaml
- name: Set up uv
  run: curl -LsSf https://astral.sh/uv/install.sh | sh

- name: Install dependencies
  run: uv sync --frozen

- name: Run tests
  run: uv run pytest
```

**GitLab CI:**
```yaml
setup:
  script:
    - curl -LsSf https://astral.sh/uv/install.sh | sh
    - uv sync --frozen

test:
  script:
    - uv run pytest
```

### Docker multi-stage

```dockerfile
FROM python:3.12-slim as builder

RUN pip install uv
COPY . .

RUN uv venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN uv pip install --system -r requirements.txt

FROM python:3.12-slim
COPY --from=builder /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

CMD ["python", "main.py"]
```

## Troubleshooting

### Slow resolution

```bash
uv add --upgrade-package package-name
```

### Cache issues

```bash
rm -rf ~/.cache/uv
```

### Python version not found

```bash
uv python install 3.12
uv venv --python 3.12
```

### Lockfile conflicts

```bash
uv lock --upgrade
```

### Verbose output for debugging

```bash
uv add package -vv
```
