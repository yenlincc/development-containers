# The following image should've already been built by GitHub Action
# in an earlier step before attempting to build this Dockerfile
FROM thinkthenrant/development-container-base:for-auto-build

RUN sudo apt-get update \
    # https://www.petefreitag.com/item/877.cfm
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends cmake libclang-dev \
    #
    # Install Rust
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
