# Docker Setup
FROM python:3.12-slim

# Install Node.js (Required by Pyright) and curl
RUN apt-get update && apt-get install -y curl && \
    curl -fsSL https://nodesource.com | bash - && \
    apt-get install -y nodejs && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install uv globally inside the container
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

WORKDIR /workspace

# Keep container alive so Emacs TRAMP can connect to it
CMD ["tail", "-f", "/dev/null"]



# docker-compsoe
version: '3.8'

services:
  dev-env:
    build: .
    container_name: python_uv_container
    volumes:
      # Bind mount: Syncs your source files to your local drive
      - .:/workspace
      # Anonymous volume: Keeps Linux-compiled binaries safe inside Docker
      - /workspace/.venv
# pyproject.toml
This defines your project dependencies.
We include fastapi as a sample application package, alongside pyright and ruff so uv manages your development tools.
[project]
name = "emacs-uv-project"
version = "0.1.0"
description = "Perfect Emacs Docker UV Stack"
readme = "README.md"
requires-python = ">=3.12"
dependencies = [
    "fastapi>=0.110.0",
    "uvicorn>=0.28.0",
]

[tool.uv]
dev-dependencies = [
    "pyright>=1.1.350",
    "ruff>=0.3.0",
]


# in Emcs

;;; --- 4. Essential Built-in Tools ---
(use-package eglot
  :ensure nil ; Built-in, no need to install
  :hook ((python-ts-mode . eglot-ensure)
         (rust-ts-mode . eglot-ensure))) ; Modern LSP client
# Step by step workflow
- docker compose up -d --build
- docker exec -it python_uv_container uv sync
- open the project in emacs via tramp c-x c-f
/docker:python_uv_container:/workspace/


