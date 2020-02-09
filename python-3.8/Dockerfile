FROM python:3.8-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED 1

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    && apt-get -y install git openssh-client iproute2 procps lsb-release pipenv curl \
    && curl -fsSL https://starship.rs/install.sh | bash -s -- --yes \
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    # [Optional] Add sudo support for the non-root user
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

COPY --chown=${USERNAME} .bashrc /home/${USERNAME}
COPY --chown=${USERNAME} starship.toml /home/${USERNAME}/.config/

ENV DEBIAN_FRONTEND=dialog
