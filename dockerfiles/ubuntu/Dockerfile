ARG UBUNTU_VERSION=22.04
FROM ubuntu:${UBUNTU_VERSION}

# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Install packages as root
RUN apt-get update && apt-get install -y \
    build-essential \
    wget \
    curl \
    libffi-dev \
    libsqlite3-dev \
    software-properties-common \
    ca-certificates \
    lsb-release \
    apt-transport-https \
    telnet \
    sudo \
    git \
    && rm -rf /var/lib/apt/lists/*

# Create vscode user with same setup as devcontainer
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

RUN groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} -s /bin/bash \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

# Switch to vscode user
USER vscode
WORKDIR /home/vscode

ENV DEBIAN_FRONTEND=dialog
