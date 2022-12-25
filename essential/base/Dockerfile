FROM ubuntu:22.04

# https://code.visualstudio.com/docs/remote/containers-advanced#_creating-a-nonroot-user
ARG USERNAME=yenlinc
# https://docs.docker.com/engine/reference/builder/#env
# ARG is not persisted in the image so need to set it as ENV so that
# child images built from this can reference it.
ENV USERNAME=${USERNAME}
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    # 
    # Get git, starship shell and vim installed.
    # This explains why you should not separate
    # the `apt-get update` and
    # the remaining `apt-get install commands`:
    # http://lenguyenthedat.com/docker-cache/
    && DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    vim git curl ca-certificates build-essential git-lfs

USER $USERNAME
RUN curl -fsSL https://starship.rs/install.sh | sh -s --yes
RUN git config --global core.editor "vim" \
    && git config --global user.email "3822365+hencrice@users.noreply.github.com" \
    && git config --global user.name "Yenlin Chen"
    #
    # https://code.visualstudio.com/docs/remote/containers-advanced#_persist-bash-history-between-runs
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && sudo mkdir /commandhistory \
    && sudo touch /commandhistory/.bash_history \
    && sudo chown -R $USERNAME /commandhistory \
    && echo $SNIPPET >> "/home/$USERNAME/.bashrc" \
    && echo 'eval "$(starship init bash)"' >> "/home/$USERNAME/.bashrc"