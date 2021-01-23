FROM ubuntu:20.04

# Get git, starship shell and vim installed.
# This explains why you should not separate
# the `apt-get update` and
# the remaining `apt-get install commands`:
# http://lenguyenthedat.com/docker-cache/
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    vim git curl ca-certificates
RUN curl -fsSL https://starship.rs/install.sh | bash -s -- --yes
RUN git config --global core.editor "vim" \
    && git config --global user.email "3822365+hencrice@users.noreply.github.com" \
    && git config --global user.name "Yenlin Chen"
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && echo $SNIPPET >> "/root/.bashrc" && echo 'eval "$(starship init bash)"' >> "/root/.bashrc"