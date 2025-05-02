### Dockerfile – Optimized and Secure Python App
```
# ============================
# 🌱 Stage 1: Builder Stage
# ============================
FROM python:3.11-slim AS builder

# Use a consistent environment variable for Python
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Install pip-tools for locking dependencies (optional)
RUN apt-get update && \
    apt-get install --no-install-recommends -y gcc build-essential && \
    pip install --upgrade pip setuptools wheel && \
    rm -rf /var/lib/apt/lists/*

# Create working directory
WORKDIR /app

# Copy requirements early to leverage Docker layer caching
COPY requirements.txt .

# Install dependencies in a virtual environment
RUN python -m venv /venv && \
    . /venv/bin/activate && \
    pip install --no-cache-dir -r requirements.txt

# ============================
# 🐳 Stage 2: Runtime Stage
# ============================
FROM python:3.11-alpine AS runtime

# Add security dependencies
RUN apk --no-cache add libgcc libstdc++

# Create a non-root user
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser

# Set workdir and copy venv
WORKDIR /app
COPY --from=builder /venv /venv
ENV PATH="/venv/bin:$PATH"

# Copy your app code
COPY . .

# Change ownership (optional: for stricter file perms)
RUN chown -R appuser:appgroup /app

# Switch to non-root user
USER appuser

# Expose the port (if applicable)
EXPOSE 8000

# Set entrypoint
CMD ["python", "main.py"]

```
### .dockerignore
```
# Python bytecode
__pycache__/
*.pyc
*.pyo
*.pyd

# Virtual environments
venv/
env/
.venv/

# System files
.DS_Store
Thumbs.db

# Environment/config files
*.env
.env.*
secrets/
credentials/

# Git
.git
.gitignore
.gitattributes

# Docker
Dockerfile
.dockerignore

# Editor/IDE configs
.vscode/
.idea/
*.swp

# Tests, cache, and reports
tests/
coverage/
*.cover
*.log
*.tmp
*.bak
.cache/
pytest_cache/
htmlcov/

# Build artifacts
build/
dist/
*.egg-info/

# Jupyter
*.ipynb_checkpoints

```
