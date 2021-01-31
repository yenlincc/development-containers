FROM thinkthenrant/development-container-base:dev

RUN sudo apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && sudo apt-get -y install --no-install-recommends cmake libclang-dev \
    #
    # Install Rust
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
