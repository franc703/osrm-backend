FROM python:3.10-bullseye

WORKDIR /src

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    git \
    libboost-all-dev \
    liblua5.2-dev \
    libstxxl-dev \
    libtbb-dev \
    libbz2-dev \
    libexpat1-dev \
    libprotobuf-dev \
    protobuf-compiler \
    lua5.2 \
    pkg-config \
    wget \
    patch \
    && rm -rf /var/lib/apt/lists/*

# Clone OSRM-backend
RUN git clone --branch v5.27.1 https://github.com/Project-OSRM/osrm-backend.git

WORKDIR /src/osrm-backend

# Download and apply the TBB patch
RUN wget -O patch-6497-fix-tbbparallelpipeline.patch https://patch-diff.githubusercontent.com/raw/Project-OSRM/osrm-backend/pull/6493.patch && \
    patch -p1 < patch-6497-fix-tbbparallelpipeline.patch && \
    rm patch-6497-fix-tbbparallelpipeline.patch


# Build OSRM-backend
RUN mkdir -p build
WORKDIR /src/osrm-backend/build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release
RUN make
RUN make install
