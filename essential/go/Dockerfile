FROM thinkthenrant/development-container-base:dev

ENV PATH /usr/local/go/bin:$PATH
ARG GO_VERSION=1.16
RUN sudo apt-get update \
    # https://www.petefreitag.com/item/877.cfm
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends wget
RUN sudo wget https://golang.org/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    sudo rm -rf /usr/local/go && \
    sudo tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    sudo rm go${GO_VERSION}.linux-amd64.tar.gz && \
    go install github.com/ramya-rao-a/go-outline && \
    go install github.com/cweill/gotests && \
    go install github.com/fatih/gomodifytags && \
    go install github.com/josharian/impl && \
    go install github.com/josharian/impl && \
    go install github.com/haya14busa/goplay/cmd/goplay && \
    go install github.com/go-delve/delve/cmd/dlv && \
    go install golang.org/x/lint/golint && \
    go install golang.org/x/tools/gopls