FROM thinkthenrant/development-container-rust:dev

# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    # dependency for Rustlang development
    build-essential \
    llvm \
    python \
    pkg-config \
    ninja-build \
    # some of Rust language development needs to be verified
    # for 32-bit platform when building on a 64-bit platform 
    gcc-multilib
