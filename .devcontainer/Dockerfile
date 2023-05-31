# Use build arguments for Python version
ARG VARIANT="3.10-bullseye"
ARG NODE_VERSION="none"

# Use specific version of Python
# FROM mcr.microsoft.com/vscode/devcontainers/python:0-${VARIANT}

# Install Python and other dependencies
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    git \
    cmake \
    build-essential \
    jq \
    htop \
    liblua5.2-dev \
    libboost-all-dev \
    libprotobuf-dev \
    libstxxl-dev \
    libbz2-dev \
    wget \
    patch \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /src

RUN git clone --branch v5.24.0 https://github.com/Project-OSRM/osrm-backend.git

WORKDIR /src/osrm-backend

# Apply the TBB patch
RUN wget -O patch-6497-fix-tbbparallelpipeline.patch https://patch-diff.githubusercontent.com/raw/Project-OSRM/osrm-backend/pull/6493.patch && \
    patch -p1 < patch-6497-fix-tbbparallelpipeline.patch && \
    rm patch-6497-fix-tbbparallelpipeline.patch
