# The following image should've already been built by GitHub Action
# in an earlier step before attempting to build this Dockerfile
FROM yenlincc/development-container-rust:for-auto-build

# Ref: https://docs.docker.com/engine/reference/builder/#automatic-platform-args-in-the-global-scope
ARG TARGETARCH
# https://rustc-dev-guide.rust-lang.org/building/prerequisites.html
RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    # dependency for Rustlang development
    build-essential \
    llvm \
    python3 \
    pkg-config \
    ninja-build
RUN if [ "${TARGETARCH}" = 'amd64' ]; then \
        # some of Rust language development needs to be verified
        # for 32-bit platform when building on a 64-bit platform.
        # skip installation when target architecture is arm64 because
        # this package is not available
        sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends gcc-multilib; \
    fi
