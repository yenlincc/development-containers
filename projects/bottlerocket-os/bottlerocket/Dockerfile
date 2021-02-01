FROM thinkthenrant/development-container-rust:dev

RUN sudo apt-get update \
    && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install --no-install-recommends \
    build-essential openssl libssl-dev pkg-config liblz4-tool \
    # needed for the installation of AWS CLI
    unzip python3-venv \
    # install Docker
    && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y apt-transport-https \
    gnupg-agent software-properties-common \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add - \
    && sudo add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) \
        stable" \
    && sudo apt-get update && sudo DEBIAN_FRONTEND=noninteractive apt-get install -y docker-ce docker-ce-cli containerd.io \
    # https://docs.docker.com/engine/install/linux-postinstall/
    # ensure $USERNAME (set in the essential/base/Dockerfile)
    # can connect to docker socket
    && sudo usermod -aG docker $USERNAME
# dependencies needed to build Bottlerocket
RUN ${HOME}/.cargo/bin/cargo install cargo-make \
    && ${HOME}/.cargo/bin/cargo install cargo-deny \
    # https://github.com/bottlerocket-os/bottlerocket/blob/develop/QUICKSTART-EKS.md#dependencies
    # dependencies needed to test Bottlerocket with EKS:
    ## install eksctl
    && curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp \
    && sudo mv /tmp/eksctl /usr/local/bin \
    ## Install kubectl
    && cd /tmp \
    && curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" \
    && sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl \
    && rm -r kubectl \
    ## Install awscli
    && curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" \
    && unzip awscli-bundle.zip \
    && sudo ln -s /usr/bin/python3 /usr/bin/python \
    && ./awscli-bundle/install -b ~/bin/aws \
    && rm -r awscli*
