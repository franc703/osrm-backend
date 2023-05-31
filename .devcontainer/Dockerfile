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
RUN git clone --branch v5.24.0 https://github.com/Project-OSRM/osrm-backend.git

WORKDIR /src/osrm-backend

# Apply the TBB patch
ADD patch-6497-fix-tbbparallelpipeline.patch .
RUN patch -p1 < patch-6497-fix-tbbparallelpipeline.patch && \
    rm patch-6497-fix-tbbparallelpipeline.patch

# Build OSRM-backend
RUN mkdir -p build
WORKDIR /src/osrm-backend/build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release
RUN make
RUN make install
