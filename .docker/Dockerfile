# Use an official Ubuntu as base image
FROM ubuntu:22.04

# Avoid prompts from apt
ENV DEBIAN_FRONTEND=noninteractive

# Output the architecture
RUN echo "Architecture: $(uname -m)"

# Install dependencies
RUN apt-get update && apt-get install -y \
    wget \
    curl \
    unzip \
    sqlite3 \
    ca-certificates \
    libc6 \
    && rm -rf /var/lib/apt/lists/*

# Download and install DuckDB CLI
RUN wget https://github.com/duckdb/duckdb/releases/download/v1.1.3/duckdb_cli-linux-amd64.zip \
&& unzip duckdb_cli-linux-amd64.zip\
&& chmod +x duckdb \
&& mv duckdb /usr/local/bin/ \
&& rm duckdb_cli-linux-amd64.zip

# Set working directory
WORKDIR /app

# Copy project files
COPY . .

# Make scripts executable
RUN chmod +x scripts/*.sh

# Default command
CMD ["./scripts/analyze_data.sh"]
