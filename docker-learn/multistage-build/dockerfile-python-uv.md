## Dockerfile
```
# Use the official Python image as the base
FROM python:3.12-slim-bookworm

# Install curl and certificates required by the installer
RUN apt-get update && apt-get install -y --no-install-recommends curl ca-certificates

# Download the latest UV installer script
ADD https://astral.sh/uv/install.sh /uv-installer.sh

# Run the installer and remove it
RUN sh /uv-installer.sh && rm /uv-installer.sh

# Ensure UV binary is available in the PATH
ENV PATH="/root/.local/bin/:$PATH"

# Set working directory for the app
WORKDIR /app

# Copy application files
COPY pyproject.toml .
COPY main.py .

# Create the lockfile to ensure dependencies are locked
RUN uv lock --no-cache

# Install application dependencies using uv sync
RUN uv sync --frozen --no-cache

# Expose Flask app port (8181 in your case)
EXPOSE 8181

# Run the Flask application using UV
CMD ["uv", "run", "main.py"]

```
```
# Use the official Python 3.12 slim image as base
FROM python:3.12-slim-bookworm

# Install curl and certs for uv installer
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Download and install uv
ADD https://astral.sh/uv/install.sh /uv-installer.sh
RUN sh /uv-installer.sh && rm /uv-installer.sh

# Add uv binary to PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy the project into the image (including pyproject.toml and uv.lock)
ADD . /app

# Set working directory
WORKDIR /app

# Sync the project into a new environment using the lockfile
RUN uv sync --locked

# Expose your app's port
EXPOSE 8181

# Run the application
CMD ["uv", "run", "main.py"]

```
