# The following image should've already been built by GitHub Action
# in an earlier step before attempting to build this Dockerfile
FROM ghcr.io/yenlincc/development-container-base:for-auto-build

ENV PATH /usr/local/go/bin:$PATH
ARG GO_VERSION=1.19.4
ARG MOCKERY_VERSION=2.16.0
# Ref: https://docs.docker.com/engine/reference/builder/#automatic-platform-args-in-the-global-scope
ARG TARGETOS
ARG TARGETARCH
RUN sudo apt-get update \
    # https://www.petefreitag.com/item/877.cfm
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends wget
RUN sudo wget https://golang.org/dl/go${GO_VERSION}.${TARGETOS}-${TARGETARCH}.tar.gz && \
    sudo rm -rf /usr/local/go && \
    sudo tar -C /usr/local -xzf go${GO_VERSION}.${TARGETOS}-${TARGETARCH}.tar.gz && \
    sudo rm go${GO_VERSION}.${TARGETOS}-${TARGETARCH}.tar.gz
RUN if [ "${TARGETARCH}" = 'amd64' ]; then\
        MOCKERY_ARCH='x86_64'\
    else\
        MOCKERY_ARCH="${TARGETARCH}"\
    fi
    # https://stackoverflow.com/questions/12487424/uppercase-first-character-in-a-variable-with-bash
RUN sudo wget https://github.com/vektra/mockery/releases/download/v${MOCKERY_VERSION}/mockery_${MOCKERY_VERSION}_${TARGETOS^}_${MOCKERY_ARCH}.tar.gz && \
    sudo tar -C /usr/local/bin -xzf mockery_${MOCKERY_VERSION}_${TARGETOS^}_${MOCKERY_ARCH}.tar.gz && \
    sudo rm mockery_${MOCKERY_VERSION}_${TARGETOS^}_${MOCKERY_ARCH}.tar.gz && \
    go install github.com/uudashr/gopkgs/cmd/gopkgs@v2 && \
    go install github.com/ramya-rao-a/go-outline@latest && \
    go install github.com/fatih/gomodifytags@v1 && \
    go install github.com/josharian/impl@v1 && \
    go install github.com/haya14busa/goplay/cmd/goplay@v1 && \
    go install github.com/go-delve/delve/cmd/dlv@v1 && \
    go install honnef.co/go/tools/cmd/staticcheck@v0 && \
    go install golang.org/x/tools/gopls@v0
