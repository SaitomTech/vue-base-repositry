# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.191.0/containers/javascript-node/.devcontainer/base.Dockerfile

FROM node:12
ENV TZ=Asia/Tokyo
RUN echo $TZ > /etc/timezone

ARG WORKDIR=/project_name
WORKDIR ${WORKDIR}

# Set user/group ID (UID/GID) & USERNAME
ARG USER_UID=1000
ARG USER_GID=${USER_UID}
ARG USERNAME=vscode
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME

# Add sudo support for non-root user
# 「$USERNAMEの人が、rootと同じ行動を、全てパスワード無しで実行できる」の意
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME