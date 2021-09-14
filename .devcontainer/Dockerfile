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

# terminal setting (gitコマンドの補完/ブランチ名の表示)
RUN wget --progress=dot:giga https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -O /home/vscode/.git-completion.bash \
    && wget --progress=dot:giga https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh -O /home/vscode/.git-prompt.sh \
    && chmod a+x /home/vscode/.git-completion.bash \
    && chmod a+x /home/vscode/.git-prompt.sh \
    && echo -e "\n\
    source ~/.git-completion.bash\n\
    source ~/.git-prompt.sh\n\
    export PS1='\\[\\e]0;\\u@\\h: \\w\\a\\]\${debian_chroot:+(\$debian_chroot)}\\[\\033[01;32m\\]\\u\\[\\033[00m\\]:\\[\\033[01;34m\\]\\w\\[\\033[00m\\]\\[\\033[1;30m\\]\$(__git_ps1)\\[\\033[0m\\] \\$ '\n\
    " >>  /home/vscode/.bashrc

# install hadolint
RUN wget --progress=dot:giga https://github.com/hadolint/hadolint/releases/download/v2.6.0/hadolint-Linux-x86_64 -O /usr/local/bin/hadolint \
    && chmod +x /usr/local/bin/hadolin
