# The following image should've already been built by GitHub Action
# in an earlier step before attempting to build this Dockerfile
FROM yenlincc/development-container-rust:for-auto-build

# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    # dependency for Rustlang development
    build-essential \
    llvm \
    python3 \
    pkg-config \
    ninja-build \
    # some of Rust language development needs to be verified
    # for 32-bit platform when building on a 64-bit platform 
    gcc-multilib
